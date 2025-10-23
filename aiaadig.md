# AI-assisted Audio Distribution Guideline

The below doc contains strategy (long-term) proposals and cut-n-paste instructions to make your AI-assisted audio (AiAA) future-proof, as DDEX proposals on labeling AI-assisted media can help to avoid adverse effects on your AI-assisted audio distributed over streaming or similar services.

## 1. Reference media strategy

**What to keep (and name):**
- A single **master WAV** (48 kHz/24-bit or 44.1/24) as the *source of truth*.  
- **Derived assets**: streaming WAV (if different), MP3 (320k), promo MP4 (static art), stems (optional).  
- **Identifiers** in filenames and sidecar: your **opus number** (internal), **ISRC** (if assigned), catalog/UPC, and version tags (e.g., `_master`, `_mp3`, `_promo`).  
- **Checks**: file SHA-256 **and** an **audio stream hash** (FFmpeg `-f streamhash -hash sha256`) so you can prove “same audio” across containers.

**Immutable storage you can point to:**
- **S3 Object Lock** (Compliance or Governance mode) to make the master **undeletable/unchangeable** for a set retention period (proves non-tampering).
- **IPFS** for public, content-addressed references (publish the **CID v1**; any change yields a new CID).

**What to publish on the provenance page:**
- Links (or opaque IDs) to **S3 Object Lock** object/version, the **IPFS CID** (if used), file/stream hashes, and your internal **opus number**. That gives third parties a verifiable chain later (S3 retention + content addressing).

---

## 2. Pre-publication processing (loudness, denoise, QA)

**Targets that travel well:** For mainstream DSPs, **−14 LUFS integrated** with **≤ −1.0 dBTP** (true-peak ceiling) works safely. Platforms differ, but this is the common “does no harm” zone. EBU R128/BS.1770 are the underlying standards. 

**Your scripts (fast path):**
- Use your `loudnorm-two-pass.sh` with **two-pass** `loudnorm` (feeds measured values into pass 2). If verify shows LUFS off by ~x LU, re-run with `I = I + target_offset`; if TP ends ≪ −1 dB, optionally relax to **−0.8 dBTP**. This is standard FFmpeg two-pass practice. 
- For batch jobs, **ffmpeg-normalize** wraps the same two-pass method. 

**Why TP may be “much lower” than your ceiling:** `loudnorm` treats **TP as a ceiling**, not a target; it won’t raise peaks to “hit” −1.0 dBTP. Trust the verify pass; it’s normal to end up at −14 LUFS with TP lower than −1 dB when limiting isn’t needed. 

**Optional polish:**
- **Denoise** (light) *before* loudness (e.g., `afftdn`), then two-pass normalize.  
- Re-measure LUFS/LRA/TP and **embed** numbers + hashes in your sidecar and page.

---

## 3. AI disclosure and provenance

**Where the ecosystem is going (and what you can do now):**
- **Spotify (Sept 25, 2025)** announced AI protections (impersonation, spam filtering) and said it’s **supporting DDEX-based AI disclosures** in credits—e.g., noting which parts used AI (vocals, composition, production, mixing/mastering). Multiple outlets reported ~75M spam removals and the new disclosure push. 
- **YouTube** requires creators to **disclose “altered or synthetic media”**; labels are shown to viewers (especially on sensitive topics). For music uploads, put a plain-English disclosure in the description, too. 
- **DDEX**: today’s working specs (ERN/RIN/MEAD/etc.) already carry rich credits/technical metadata; DDEX has active working/ad-hoc groups evolving the standards. Use your sidecar as a **bridge** until ingest pipelines widely accept AI fields. 
- **C2PA Content Credentials**: if/when audio tools support it, C2PA lets you **cryptographically bind provenance** assertions to assets (or via an external manifest). Track-art already benefits; audio support is emerging. Keep an eye on this and be ready to attach manifests to cover art and (when feasible) audio. 

**What to publish now:**
- Your **plain-English AI disclosure** (e.g., “Human lyrics; AI-assisted vocals derived from my voice; AI-assisted instrumentals; no impersonations”), plus **checksums**, **audio stream hash**, **S3 VersionID**, **IPFS CID** (if any), **opus number**, and **absolute provenance URL** in **JSON-LD** (`MusicRecording`) as you’ve done. This aligns with current platform transparency pushes and is future-proof for DDEX/C2PA ingestion. 

---

## 4. Post-publication & "stay safe" guidance for AIAA

**Platform realities (2025):**
- **Spotify** normalizes playback around **−14 LUFS**, fights spam, and is rolling out **AI-use disclosures**. Quiet tracks can be turned up at playback within headroom (they consider peaks to avoid encoder overs). Keep **≤ −1 dBTP** to stay safe. 
- **YouTube/YouTube Music**: disclosure labels for synthetic/altered content; normalization primarily **reduces** loud items (don’t count on a boost). Add a human-readable disclosure + provenance link in descriptions. 
- **Bandcamp**: **no LUFS target / no normalization**; they say uploads are **unchanged** (site player is just quieter by default). Master for the sound you want; what you upload is what people hear. 
- **SoundCloud**: public guidance is inconsistent; historically **no consistent loudness normalization**. Either way, assume your uploaded master’s loudness is what listeners hear (subject to transcoding). 

**Risk controls, given the spam crackdown:**
- Avoid **ultra-short, repetitive, or mass-duplicative** uploads; these are flagged by new spam filters. Maintain human-readable notes, **session credits**, and consistent metadata—signals of genuine authorship. 
- Keep **voice model ethics** tight (no impersonations, model/source provenance on file). Consider linking to a short “Creator Policy” page explaining your AI policy.

**Routine post-publish checklist:**
- Verify the track pages show **correct credits** and (where available) **AI disclosure labels**.  
- Archive the exact **delivered assets** (and their hashes) alongside any distributor **ingest receipts/IDs**.  
- Add the track to your **provenance index** (opus number → URL, ISRC, S3 VersionID, IPFS CID).  
- For YouTube, pin a comment with **credits + provenance link**; for SoundCloud/Bandcamp, mirror the disclosure in the description.

---

## Appendix A. Step by step guide

At this point we assume you have prepared the source .wav file (mixed and mastered) to proceed with preparing it for the distribution.

We also assume you have generated track art (still image, at least 1024x1024) and specific other media (such as canvas video for Spotify: 9x16 video no longer than 10sec, with at least 720px in vertical dimension).

The below is assuming on uses latest Ubuntu LTS OS, and the required utilities (bwfmetaedit, jq, ffmpeg, ffmpeg-normalize) are all installed. Generally, that can should work in all Linux and Linux-like environments (including Cygwin).

### A.1 Denoise and normalize loudness

Know your terms when doing this additional mastering.

**LUFS: Loudness Units Full Scale**
- LUFS measures the perceived loudness of your audio, taking into account how the human ear hears sound. Unlike older meters that measure a signal's electrical level (like RMS) or its highest peak, LUFS uses a standardized algorithm that weights certain frequencies to more accurately reflect our hearing. 
- **Integrated LUFS**: This is the average loudness of an entire track from beginning to end. Most streaming platforms (Spotify, Apple Music, YouTube) use this value for loudness normalization, turning down tracks that are too loud to a standardized level (e.g., -14 LUFS).
- **Momentary and Short-Term LUFS**: These measure the loudness of audio over shorter windows (momentary: 400ms; short-term: 3 seconds). They are useful for checking how the loudness of your track varies from one section to another. 

**TP: True Peak**
- TP, or True Peak, measures the actual highest peak level that a waveform will reach during playback. A standard peak meter in your DAW only measures the highest digital sample points, but the process of digital-to-analog conversion can create "inter-sample peaks" that exceed 0 dBFS and cause audible distortion. 
- dBTP: True Peak measurements are displayed in dBTP (decibels True Peak).
- **The Overshoot Problem**: A True Peak meter uses oversampling to accurately predict these hidden peaks, ensuring your audio doesn't clip when played back on a listener's device. 
- In mastering: to avoid distortion from inter-sample peaks, it's standard practice to set your mastering limiter's output ceiling so that the True Peak level never exceeds -1.0 dBTP. Many streaming platforms even have a -1.0 dBTP limit as a standard requirement. 

**LRA: Loudness Range**
- LRA measures the statistical loudness variation within a track, indicating the difference between its quietest and loudest sections. It provides a long-term measure of your track's overall dynamic movement, ignoring the quietest passages. 
- **High vs. Low LRA**: A high LRA value (e.g., 15 LU) indicates a track with a wide dynamic range, like a classical score. A low LRA value (e.g., 3 LU) signifies a track with a very narrow dynamic range, like a heavily compressed pop or electronic track. 
- In mastering: LRA is not a metric with a specific target but rather an indicator of creative intent. A mastering engineer uses LRA to understand the overall dynamic arc of a piece of music and ensure it aligns with the genre and artistic vision. 

Typical values, Spotify-friendly, are: LUFS -14, TP -1.0dB, LRA 11 (LRA defines dynamic range; 15 is the widest - say, for classical pieces; 4-7 mean very narrow range; choose depending on the track type and mood)

#### Using ffmpeg-normalize

##### Denoising: Pick one of these **pre-filter** chains for `-prf`:

*   **General broadband noise (fast):** FFT denoise  
    `-prf "highpass=60,lowpass=16000,afftdn=nr=12:nf=-45"`  
    (`afftdn` is the native FFT denoiser; adjust `nr` strength and `nf` noise-floor as needed.) [Ayosec](https://ayosec.github.io/ffmpeg-filters-docs/5.1/Filters/Audio/afftdn.html)
*   **Music/broadband noise (quality):** Non-Local Means  
    `-prf "highpass=60,lowpass=16000,anlmdn=s=0.0003"`  
    (`anlmdn` trades speed for quality; tune `s`/`patch`/`research` options per material.) [Ayosec](https://ayosec.github.io/ffmpeg-filters-docs/8.0/Filters/Audio/anlmdn.html)
*   **Speech-focused ML denoise:** RNN (needs model file)  
    `-prf "arnndn=model=./arnndn-models/std.rnnn:mix=0.8"`  
    (Clone models from the project and point `model=` to a `.rnnn` file; tweak `mix` to taste.) [GitHub arnndn-models](https://github.com/richardpl/arnndn-models)

> Tip: You can chain filters with commas. Keep the HP/LP filters gentle to avoid tonal damage. [openwebsite.github.io](https://openwebsite.github.io/ffmpeg/ffmpeg-filters.html)

#### Using custom 'loudnorm-two-pass.sh' script

The script:

```bash
#!/usr/bin/env bash
set -euo pipefail

# Loudness normalize WAV (or any audio) to target LUFS and True Peak using FFmpeg loudnorm (two-pass).
# Requirements: ffmpeg, jq
# Example:
#   ./loudnorm-two-pass.sh -i in.wav -o out.wav -I -14 -T -1.0 -L 11

usage() {
  cat <<'USAGE'
Usage:
  loudnorm-two-pass.sh -i INPUT -o OUTPUT [-I LUFS] [-T dBTP] [-L LRA] [--linear true|false] [--dualmono true|false]

Options (defaults in brackets):
  -i, --input     Input audio file (wav/mp3/flac/m4a etc.)
  -o, --output    Output WAV file (pcm_s24le by default)
  -I, --lufs      Target integrated loudness LUFS         [-14]
  -T, --tp        Target true peak (dBTP)                 [-1.0]
  -L, --lra       Target loudness range (LU)              [11]
      --linear    Linear normalization mode               [true]
      --dualmono  Dual-mono correction                    [false]
      --codec     Output audio codec (e.g. pcm_s24le)     [pcm_s24le]
      --verify    After pass 2, run a verify measurement  [on]

Notes:
- Two-pass loudnorm requires measured_* values from pass 1 to be fed into pass 2. (FFmpeg docs)
- Target LRA should not be lower than the source LRA; if constraints are violated, filter may revert to dynamic mode. (FFmpeg docs)
USAGE
}

# --- defaults ---
I_TARGET="-14"
TP_TARGET="-1.0"
LRA_TARGET="11"
LINEAR="true"
DUALMONO="false"
CODEC="pcm_s24le"
VERIFY=1

# --- parse args ---
IN="" ; OUT=""
while [[ $# -gt 0 ]]; do
  case "$1" in
    -i|--input)   IN="$2"; shift 2;;
    -o|--output)  OUT="$2"; shift 2;;
    -I|--lufs)    I_TARGET="$2"; shift 2;;
    -T|--tp)      TP_TARGET="$2"; shift 2;;
    -L|--lra)     LRA_TARGET="$2"; shift 2;;
    --linear)     LINEAR="$2"; shift 2;;
    --dualmono)   DUALMONO="$2"; shift 2;;
    --codec)      CODEC="$2"; shift 2;;
    --verify)     VERIFY=1; shift;;
    -h|--help)    usage; exit 0;;
    *) echo "Unknown arg: $1" >&2; usage; exit 1;;
  esac
done

[[ -n "$IN" && -n "$OUT" ]] || { usage; exit 1; }
command -v ffmpeg >/dev/null || { echo "Missing: ffmpeg" >&2; exit 1; }
command -v jq >/dev/null     || { echo "Missing: jq" >&2; exit 1; }
[[ -f "$IN" ]] || { echo "Input not found: $IN" >&2; exit 1; }

# --- PASS 1: measure ---
echo "[1/3] Measuring loudness on: $IN"
PASS1_LOG="$(mktemp)"
# We capture the JSON block from stderr and keep only the JSON object.
ffmpeg -hide_banner -nostdin -i "$IN" \
  -af "loudnorm=I=${I_TARGET}:TP=${TP_TARGET}:LRA=${LRA_TARGET}:print_format=json" \
  -f null - 2> "$PASS1_LOG" || true

# Extract first JSON object from the log (loudnorm prints one).
MEASURE_JSON="$(awk 'BEGIN{p=0} /^\s*\{/{p=1} p{print} /^\s*\}/{if(p){exit}}' "$PASS1_LOG")"
if [[ -z "$MEASURE_JSON" ]]; then
  echo "ERROR: Could not capture loudnorm JSON from pass 1." >&2
  exit 2
fi

# --- parse pass-1 JSON safely ---
meas_I=$(echo "$MEASURE_JSON"      | jq -r '.measured_I // .input_i')
meas_LRA=$(echo "$MEASURE_JSON"    | jq -r '.measured_LRA // .input_lra')
# FFmpeg prints measured_TP (capital TP); some builds show measured_tp/input_tp
meas_TP=$(echo "$MEASURE_JSON"     | jq -r '.measured_TP // .measured_tp // .input_tp')
meas_thresh=$(echo "$MEASURE_JSON" | jq -r '.measured_thresh // .input_thresh // empty')
meas_offset=$(echo "$MEASURE_JSON" | jq -r '.target_offset // .offset // empty')

echo "  measured_I=$meas_I, measured_LRA=$meas_LRA, measured_TP=$meas_TP, measured_thresh=${meas_thresh:-<none>}, offset=${meas_offset:-<none>}"

# If measured_thresh is missing, dynamic mode is safer than forcing linear=true
EFFECTIVE_LINEAR="$LINEAR"
if [[ -z "$meas_thresh" && "$LINEAR" == "true" ]]; then
  echo "  note: measured_thresh is missing; falling back to linear=false for pass 2."
  EFFECTIVE_LINEAR="false"
fi

# --- build pass-2 filter string (only include present keys) ---
FILTER="loudnorm=I=${I_TARGET}:TP=${TP_TARGET}:LRA=${LRA_TARGET}:linear=${EFFECTIVE_LINEAR}:dual_mono=${DUALMONO}"
FILTER="${FILTER}:measured_I=${meas_I}:measured_LRA=${meas_LRA}:measured_TP=${meas_TP}"
[[ -n "$meas_thresh" ]] && FILTER="${FILTER}:measured_thresh=${meas_thresh}"
[[ -n "$meas_offset" ]] && FILTER="${FILTER}:offset=${meas_offset}"
FILTER="${FILTER}:print_format=summary"

echo "[2/3] Applying normalization to: $OUT"
ffmpeg -hide_banner -y -nostdin -i "$IN" -c:a "$CODEC" -af "$FILTER" "$OUT"

# --- PASS 3: verify (optional) ---
if [[ $VERIFY -eq 1 ]]; then
  echo "[3/3] Verifying result:"
  ffmpeg -hide_banner -nostdin -i "$OUT" \
    -af "loudnorm=I=${I_TARGET}:TP=${TP_TARGET}:LRA=${LRA_TARGET}:print_format=json" \
    -f null - 2>&1 \
    | awk 'BEGIN{p=0} /^\s*\{/{p=1} p{print} /^\s*\}/{if(p){exit}}'
fi

rm -f "$PASS1_LOG"
echo "Done."
```

1) Run **`loudnorm-two-pass.sh`** to hit **I=−14 LUFS, TP≤−1 dBTP**; verify JSON; if LUFS off, iterate by `target_offset`. Save the verify JSON. citeturn0search3  
2) **Render & commit the master** (48k/24 WAV). Export MP3/MP4 from it.  
3) Generate **file SHA-256** and **audio stream hash**; write both into the sidecar + page.  
4) Put master + derivations into **S3 Object Lock** (record **VersionIDs**); optionally pin to **IPFS** and record the **CID**. citeturn0search0turn0search1  
5) Fill the **sidecar**: identities (ISRC/opus), credits, AI disclosure, loudness, hashes, storage IDs.  
6) Update your **provenance page** (JSON-LD + human section).  
7) Upload to **Bandcamp/SoundCloud** (playground, feedback) and to distributor (Spotify/Apple/YouTube Music). Include **plain-English AI disclosure** in descriptions. citeturn1search5turn1search2  
8) After publish: check platform pages, screenshots, archive distributor IDs, and add the entry to your **provenance index**.
