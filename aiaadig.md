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

#### A.1.1 Using ffmpeg-normalize

##### A.1.1.1 Denoising: Pick one of these **pre-filter** chains for `-prf`:

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

##### A.1.1.2 Normalize toward −14 / −1.0 / ≤11

“Hit LUFS, keep musical LRA (soft-lock), accept lower TP + denoise”

This favors LUFS and lets true peak float **below** −1 dBTP (which is fine), while **not** forcing LRA under your target.

```bash
ffmpeg-normalize "in.wav" \
  -nt ebu -t -14 -tp -1.0 -lrt 11 --keep-lra-above-loudness-range-target \
  -prf "highpass=60,lowpass=16000,afftdn=nr=12:nf=-45" \
  -c:a pcm_s24le -p -o "out.wav"
```

Why this set?

*   `-t -14` is the LUFS goal; `-tp -1.0` is a ceiling (ending at −2.5 dBTP etc. is _okay_).
*   `--keep-lra-above-loudness-range-target` avoids squashing dynamics below **11 LU** unless truly needed.

**Note**: TP is the cap, not the goal; if it's absolutely required, you could have to use several runs using different parameters.

##### A.1.1.3 Keep LRA locked (strict), still favor LUFS

If you want LRA **held ~at your target** (or the input if already > target), use:

```bash
ffmpeg-normalize "in.wav" \
  -nt ebu -t -14 -tp -1.0 -lrt 11 --keep-loudness-range-target \
  -prf "anlmdn=s=0.0003" \
  -c:a pcm_s24le -p -o "out.wav"
```

*   `--keep-loudness-range-target` tells the tool to preserve the **LRA target** so linear (two-pass) normalization is preferred; it won’t aggressively compress LRA. If the exact LUFS/TP/LRA triangle can’t be satisfied linearly, the tool may switch strategy, but this flag biases it to **keep LRA**. [SLHCK](https://slhck.info/ffmpeg-normalize/usage/options/)

##### A.1.1.4 Batch a folder

```bash
ffmpeg-normalize *.wav -of normalized -ext wav \
  -nt ebu -t -14 -tp -1.0 -lrt 11 --keep-lra-above-loudness-range-target \
  -prf "highpass=60,lowpass=16000,afftdn=nr=10" \
  -c:a pcm_s24le -p
```

Creates `normalized/` with processed files.

---

#### A.1.2 Using custom 'loudnorm-two-pass.sh' script

The script `loudnorm-two-pass.sh`:

```bash
#!/usr/bin/env bash
set -euo pipefail

# FFmpeg two-pass EBU R128 normalization with optional convergence loop.
# Requires: ffmpeg, jq
#
# Why iterate? In linear mode TP is a ceiling, not a target; dynamic mode can land LUFS slightly off.
# We trust verify JSON (pass 3) and nudge by target_offset until LUFS is on point. TP stays ≤ target.
#
# Refs: Two-pass loudnorm & measured_* fields; TP acts as a ceiling. 
# (See docs/guides cited in your notes.)

usage() {
  cat <<'USAGE'
Usage:
  loudnorm-two-pass.sh -i INPUT -o OUTPUT [options]

Options (defaults in brackets):
  -I, --lufs LUFS        Target integrated loudness [ -14 ]
  -T, --tp DBTP          Target true peak (ceiling) [ -1.0 ]
  -L, --lra LU           Target loudness range      [ 11 ]
      --linear true|false   Prefer linear mode when possible [ true ]
      --dualmono true|false Dual-mono correction             [ false ]
      --codec CODEC         Output codec (WAV)               [ pcm_s24le ]
      --verify              Print verify JSON after pass 2   [ on ]
      --converge            Iterate until LUFS within tol    [ off ]
      --tol-lufs N          LUFS tolerance (abs)             [ 0.2 ]
      --max-iters N         Max convergence iterations       [ 4 ]
      --lock-lra            Use source LRA (rounded) instead of -L
      --nudge-tp            If TP ≪ target, relax to -0.8 once
  -i, --input  PATH
  -o, --output PATH
USAGE
}

# defaults
I_TARGET="-14"
TP_TARGET="-1.0"
LRA_TARGET="11"
LINEAR="true"
DUALMONO="false"
CODEC="pcm_s24le"
VERIFY=1
CONVERGE=0
TOL_LUFS="0.2"
MAX_ITERS=4
LOCK_LRA=0
NUDGE_TP=0

IN="" ; OUT=""

# parse args
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
    --converge)   CONVERGE=1; shift;;
    --tol-lufs)   TOL_LUFS="$2"; shift 2;;
    --max-iters)  MAX_ITERS="$2"; shift 2;;
    --lock-lra)   LOCK_LRA=1; shift;;
    --nudge-tp)   NUDGE_TP=1; shift;;
    -h|--help)    usage; exit 0;;
    *) echo "Unknown arg: $1" >&2; usage; exit 1;;
  esac
done

command -v ffmpeg >/dev/null || { echo "Missing: ffmpeg" >&2; exit 1; }
command -v jq >/dev/null     || { echo "Missing: jq" >&2; exit 1; }
[[ -f "${IN:-}" ]] || { usage; echo "Input not found." >&2; exit 1; }
[[ -n "${OUT:-}" ]] || { usage; echo "Output path required." >&2; exit 1; }

# helpers
measure_once() { # prints compact JSON from pass 1 or verify run
  local src="$1"
  ffmpeg -hide_banner -nostdin -i "$src" \
    -af "loudnorm=I=${I_TARGET}:TP=${TP_TARGET}:LRA=${LRA_TARGET}:print_format=json" \
    -f null - 2>&1 \
    | awk 'BEGIN{p=0} /^\s*\{/{p=1} p{print} /^\s*\}/{if(p){exit}}'
}

build_and_apply() {
  local src="$1" dst="$2" mI="$3" mLRA="$4" mTP="$5" mTH="$6" mOFF="$7" linear="$8" lra_run="$9"
  local FILTER="loudnorm=I=${I_TARGET}:TP=${TP_TARGET}:LRA=${lra_run}:linear=${linear}:dual_mono=${DUALMONO}"
  FILTER="${FILTER}:measured_I=${mI}:measured_LRA=${mLRA}:measured_TP=${mTP}"
  [[ -n "$mTH"  ]] && FILTER="${FILTER}:measured_thresh=${mTH}"
  [[ -n "$mOFF" ]] && FILTER="${FILTER}:offset=${mOFF}"
  FILTER="${FILTER}:print_format=summary"
  ffmpeg -hide_banner -y -nostdin -i "$src" -c:a "$CODEC" -af "$FILTER" "$dst"
}

abs() { awk -v x="$1" 'BEGIN{x=(x<0?-x:x); printf("%.6f",x)}'; }
floatle() { awk -v a="$1" -v b="$2" 'BEGIN{exit !(a<=b)}'; }

# PASS 1: measure
echo "[1/3] Measuring: $IN"
P1="$(measure_once "$IN")"
[[ -n "$P1" ]] || { echo "Could not capture pass-1 JSON." >&2; exit 2; }

meas_I=$(echo "$P1"      | jq -r '.measured_I // .input_i')
meas_LRA=$(echo "$P1"    | jq -r '.measured_LRA // .input_lra')
meas_TP=$(echo "$P1"     | jq -r '.measured_TP // .measured_tp // .input_tp')
meas_TH=$(echo "$P1"     | jq -r '.measured_thresh // .input_thresh // empty')
meas_OFF=$(echo "$P1"    | jq -r '.target_offset // .offset // empty')

echo "  pass1: measured_I=$meas_I, LRA=$meas_LRA, TP=$meas_TP, thresh=${meas_TH:-<none>}, offset=${meas_OFF:-<none>}"

# choose mode + LRA
EFFECTIVE_LINEAR="$LINEAR"
[[ -n "$meas_TH" ]] || EFFECTIVE_LINEAR="false"
LRA_RUN="$LRA_TARGET"
[[ $LOCK_LRA -eq 1 && -n "$meas_LRA" ]] && LRA_RUN="$(printf '%.0f\n' "$meas_LRA")"

# PASS 2: apply (first attempt)
echo "[2/3] Applying: I=$I_TARGET TP=$TP_TARGET LRA=$LRA_RUN linear=$EFFECTIVE_LINEAR"
build_and_apply "$IN" "$OUT" "$meas_I" "$meas_LRA" "$meas_TP" "$meas_TH" "$meas_OFF" "$EFFECTIVE_LINEAR" "$LRA_RUN"

# VERIFY & optional convergence
iter=0
while :; do
  echo "[3/3] Verifying ($((iter+1)))…"
  V="$(measure_once "$OUT")"
  echo "$V"
  out_I=$(echo "$V"  | jq -r '.output_i // .input_i')
  out_TP=$(echo "$V" | jq -r '.output_TP // .output_tp // .input_tp')
  t_off=$(echo "$V"  | jq -r '.target_offset // "0"')
  # stop if within tolerance or no convergence requested
  diff_I=$(awk -v a="$out_I" -v b="$I_TARGET" 'BEGIN{print a-b}')
  [[ $CONVERGE -eq 0 ]] && break
  [[ $(abs "$diff_I") = $(abs "$diff_I") ]] # ensure numeric

  if floatle "$(abs "$diff_I")" "$TOL_LUFS"; then
    break
  fi

  # optional TP nudge: if measured TP << target, relax once to -0.8
  if [[ $NUDGE_TP -eq 1 ]]; then
    tp_gap=$(awk -v a="$TP_TARGET" -v b="$out_TP" 'BEGIN{print a - b}') # negative if out_TP < target
    # If TP is more than ~0.7 dB below target and we haven't nudged yet, relax to -0.8
    if awk 'BEGIN{exit !('$tp_gap' > 0.7)}'; then
      echo "  note: output TP well below ceiling; relaxing TP target to -0.8 dBTP once."
      TP_TARGET="-0.8"
    fi
  fi

  # adjust LUFS target by reported target_offset (usually negative when too hot)
  new_I=$(awk -v I="$I_TARGET" -v off="$t_off" 'BEGIN{printf("%.2f", I + off)}')
  echo "  converge: I_target $I_TARGET -> $new_I  (offset $t_off)"
  I_TARGET="$new_I"

  # re-run pass 2 with updated I (& possibly TP)
  echo "[2/3] Re-applying: I=$I_TARGET TP=$TP_TARGET LRA=$LRA_RUN linear=$EFFECTIVE_LINEAR"
  build_and_apply "$IN" "$OUT" "$meas_I" "$meas_LRA" "$meas_TP" "$meas_TH" "$meas_OFF" "$EFFECTIVE_LINEAR" "$LRA_RUN"

  iter=$((iter+1))
  [[ $iter -ge $MAX_ITERS ]] && { echo "Reached max iterations ($MAX_ITERS)."; break; }
done

echo "Done."
```

Typical usage:
`./loudnorm-two-pass.sh -i in.wav -o out.wav -I -14.9 -T -1.0 -L 11`

Pay attention to the final values of the loudness parameters, i.e. those printed like:
```
Input Integrated:    -10.4 LUFS
Input True Peak:      -0.2 dBTP
Input LRA:             3.7 LU
Input Threshold:     -20.4 LUFS

Output Integrated:   -13.9 LUFS
Output True Peak:     -3.8 dBTP
Output LRA:            3.8 LU
Output Threshold:    -24.0 LUFS
```

Most probably "Output True Peak" may be lower if LRA and LUFS are to be met. Use "--converge" for an iterative approach on meeting the target values.

3) Generate **file SHA-256** and **audio stream hash**; write both into the sidecar + page.  
4) Put master + derivations into **S3 Object Lock** (record **VersionIDs**); optionally pin to **IPFS** and record the **CID**. 
5) Fill the **sidecar**: identities (ISRC/opus), credits, AI disclosure, loudness, hashes, storage IDs.  
6) Update your **provenance page** (JSON-LD + human section).  
7) Upload to **Bandcamp/SoundCloud** (playground, feedback) and to distributor (Spotify/Apple/YouTube Music). Include **plain-English AI disclosure** in descriptions. 
8) After publish: check platform pages, screenshots, archive distributor IDs, and add the entry to your **provenance index**.

---

### A.2 Generate .mp3 and .mp4

Use the `convert.sh` script below:

```bash
#!/usr/bin/env bash
set -euo pipefail

#
# Converts .wav to .mp3 and .mp4 with an image used as track art (.mp3) and static background (.m4)
#

if [[ "p$3" == "p" ]]; then
    echo "$0 src_wav dst_prefix image_file"
    exit 0
fi
export SRC_WAV="$1"
export DST_PREFIX="$2"
export IMG_SRC="$3"

if [[ ! -e "$SRC_WAV" || ! -e "$IMG_SRC" ]]; then
    echo "$0: either source WAV ($SRC_WAV) or image file ($IMG_SRC) can't be accessed"
    exit 1
fi

rm -f output.mp3
ffmpeg -i "$SRC_WAV" -vn -ar 44100 -ac 2 -q:a 2 output.mp3
ffmpeg -i output.mp3 -i "$IMG_SRC" -map_metadata 0 -map 0 -map 1 -acodec copy "${DST_PREFIX}.mp3"
rm -f output.mp3
ffmpeg -loop 1 -i "$IMG_SRC" -i "${DST_PREFIX}.mp3" -c:a copy -c:v libx264 -shortest "${DST_PREFIX}.mp4"
```

Where image file should be a square image file, at least 1024x1024 (see also "embed.sh" below). The script produces .mp3 with embedded track art, and a video .mp4 with static background (suitable for YouTube).

### A.3 Generate **file SHA-256** and **audio stream hash**

At this point, prepare a JSON metadata (will be fully filled in further steps), sample `track.meta.json` below.

```json
{
  "title": "Famous Me",
  "version": "v1.0",
  "date_created_utc": "2025-09-29T16:52:41Z",
  "ids": {
    "isrc": "QT3F52558856",
    "upc": "199741081383",
    "musicbrainz_recording_id": ""
  },
  "participants": {
    "artist": "John Doe",
    "album_artist": "John Doe",
    "album": "Famous Me",
    "composer": "Firstname Lastname",
    "lyricist": "Firstname Lastname",
    "producer": "Firstname Lastname",
    "label": "Josh Magnificent"
  },
  "provenance": {
    "summary": "Human-written lyrics; AI assisted vocals derived from human-recorded vocals. AI assisted music generation. No impersonations; no third-party samples.",
    "ai_involvement": {
      "lyrics": "human",
      "vocals": "AI assisted, based upon human vocals records",
      "composition_arrangement": "ai_assisted",
      "sound_design": "ai_assisted",
      "mix_master": "human"
    },
    "tools": [
      "Suno v5.0",
      "Producer FUZZ-2.0",
      "Audacity 3.4.2",
      "ffmpeg"
    ],
    "provenance_url": "https://example.com/tracks/XTZ/"
  },
  "rights": {
    "copyright": "© 2025 John Doe",
    "rights_summary": "All rights reserved. No model training without consent.",
    "publisher": "Josh Magnificent"
  },
  "tech": {
    "genre": "Epic Rock, Aria",
    "track_number": "1",
    "disc_number": "1",
    "duration_iso": "PT3M14S",
    "loudness": {
      "integrated_lufs": -14.0,
      "lra": 11,
      "max_true_peak_db": -1.0,
      "wav": {
        "integrated_lufs": 0.0,
        "lra": 0.00,
        "max_true_peak_db": 0.0
      },
      "mp3": {
        "integrated_lufs": 0.0,
        "lra": 0.00,
        "max_true_peak_db": 0.0
      },
      "mp4": {
        "integrated_lufs": 0.0,
        "lra": 0.00,
        "max_true_peak_db": 0.0
      }
    },
    "encoder_note": "Lavf60.16.100"
  },
  "artwork": {
    "path": "https://media.kamaskera.com/tracks/XTZ-512.jpg",
    "type": "front",
    "mime": "image/jpeg",
    "pixels": "512x512"
  },
  "bwf": {
    "bext": {
      "Description": "Ghost-pop/Indie rap v1.0, AI assisted vocals derived from human vocals records; AI-assisted instrumental",
      "Originator": "Josh Magnificent",
      "OriginatorReference": "XTZ",
      "OriginationDate": "2025-09-29",
      "OriginationTime": "16:52:41",
      "CodingHistory": [
        "A=PCM,F=48000,W=24,M=stereo,T=Audacity print",
        "Edit=arrangement polish; Suno/Producer ideation; re-performed",
        "Master=Limiter ceiling -1.0 dBTP"
      ],
      "UMID": ""
    },
    "iXML_note": "Human-written lyrics; AI assisted vocals derived from human-recorded vocals. AI assisted music generation. No impersonations; no third-party samples.",
    "ebucore_axml": "embed"
  },
  "id3": {
    "prefer_version": "2.3",
    "urls": {
      "work_page": "https://example.com/tracks/XTZ/",
      "artist_page": "https://example.com/"
    },
    "comments": [
      "Provenance: human lyrics; AI assisted vocals derived from human vocals records; AI-assisted instrumentals; no impersonations."
    ],
    "custom_txxx": {
      "AI_Involvement": "Lyrics human; Arrangement/Sound design AI-assisted; Tools: Suno v5.0, Producer FUZZ-2.0, Audacity 3.4.2",
      "Provenance_URL": "https://example.com/tracks/XTZ/",
      "Tools": "Suno v5.0; Producer FUZZ-2.0; Audacity 3.4.2; ffmpeg"
    },
    "sort_fields": {
      "TSOP": "Josh Magnificent",
      "TSOA": "The Bliss",
      "TSOT": "Famous Me"
    }
  },
  "checksums": {
    "file_sha256": {
      "wav": "",
      "mp3": "",
      "mp4": ""
    },
    "audio_stream_sha256": {
      "wav": "",
      "mp3": "",
      "mp4": ""
    },
    "audio_hash_sha256": {
      "wav": "",
      "mp3": "",
      "mp4": ""
    }
  },
  "media" : {
    "versionid": {
      "wav": "",
      "mp3": "",
      "mp4": ""
    }
  }
}
```

#### END
