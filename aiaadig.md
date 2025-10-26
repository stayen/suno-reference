# AI-assisted Audio Distribution Guideline

The below doc contains strategy (long-term) proposals and cut-n-paste instructions to make your AI-assisted audio (AiAA) future-proof, as DDEX proposals on labeling AI-assisted media can help to avoid adverse effects on your AI-assisted audio distributed over streaming or similar services.

## 1. Reference media strategy

**Keep and name:**
- One **golden master WAV** (44.1/48 kHz, 24-bit). Derive everything (MP3, promo MP4, streaming WAV) from this master.
- File names: include your internal **opus number** (e.g., `opus_2570`), plus `_master`, `_mp3`, `_promo`, and external IDs (ISRC/UPC) when assigned.
- Publish both a **file hash** and an **audio-stream hash** (verifies “same audio across containers”).

```bash
# file SHA-256
sha256sum master.wav

# audio-stream hash (content of the first audio stream only)
ffmpeg -v error -nostdin -i master.wav -f streamhash -hash sha256 -
```

**Immutable references:**
- Store masters in **S3 with Object Lock** (WORM) and record each object’s **VersionID** on your provenance page; Object Lock prevents overwrite/delete for a set retention period. 
- Optionally mirror to **IPFS** and publish the **CID (v1)** (content-addressed; any content change = new CID). 

---

## 2. Pre-publication processing (loudness, denoise, QA)

**Targets that travel well:** deliver around **−14 LUFS (integrated)** and **≤ −1.0 dBTP (true-peak ceiling)** — common, safe “do-no-harm” targets aligned with EBU R128/BS.1770 metering used by modern pipelines. 

**Two-pass loudness (deterministic, reproducible):**  
Use your `loudnorm-two-pass.sh` (or `ffmpeg-normalize`) to **measure → apply with measured_* → verify**. The FFmpeg `loudnorm` filter’s recommended two-pass flow feeds back **measured_I/LRA/TP/threshold/offset** from pass-1 into pass-2; **TP acts as a ceiling** (the filter won’t “aim” for −1 dBTP if you’re already below it). 

```bash
# example (yours): converge near I=-14 LUFS, TP ceiling -1.0 dBTP
./loudnorm-two-pass.sh -i master_in.wav -o master_out.wav -I -14 -T -1.0 --lock-lra --converge
# tip: if verify shows LUFS off by ~x LU, rerun with I += target_offset (script can do this)
```

**Batch option:** `ffmpeg-normalize` wraps the same two-pass method and writes back the normalized file. 

**Light cleanup (optional):** do denoise *before* loudness; then re-measure LUFS/LRA/TP and record the numbers for provenance.

---

## 3. AI disclosure and provenance

**What platforms expect (2025 highlights):**
- **YouTube / YouTube Music** requires creators to **disclose “meaningfully altered or synthetic” content** when it appears realistic; labels are shown to viewers. Add a short disclosure in the description linking your provenance URL. 
- **Spotify (Sept 25, 2025)**: new AI safeguards (anti-impersonation, spam filtering) and **support for DDEX-based AI disclosures in credits**; the company disclosed **~75M spammy tracks removed** in the past year. Your plain-English disclosure + structured fields keeps you onside. 

**Sidecar → page → JSON-LD:**
- Keep a **JSON sidecar** per track (opus number, ISRC/UPC, creators/roles, tools, hashes, streamhash, S3 VersionIDs, optional IPFS CID, loudness metrics, AI disclosure).
- Publish a **provenance page** per opus with a **JSON-LD `MusicRecording`** block for discoverability (include your internal opus number in `identifier`, and add `additionalProperty` for checksums and storage IDs).

```json
{
  "@context": "https://schema.org",
  "@type": "MusicRecording",
  "name": "Gravel of Time",
  "identifier": "opus 2570",
  "byArtist": {"@type": "MusicGroup", "name": "Daniel Kamaskera"},
  "url": "https://kamaskera.com/tracks/2570/",
  "datePublished": "2025-09-29",
  "isrcCode": "QT3F52558856",
  "inAlbum": {"@type": "MusicAlbum", "name": "Wilds Collection"},
  "genre": "Ghost Pop / Indie",
  "duration": "PT2M59S",
  "image": "https://media.kamaskera.com/tracks/2/5/2570/gravel-of-time-512.jpg",
  "additionalProperty": [
    {"@type":"PropertyValue","name":"AIDisclosure","value":"Human lyrics; AI-assisted vocals from my recordings; AI-assisted instrumentals; no impersonations."},
    {"@type":"PropertyValue","name":"SHA256_WAV","value":"<file sha256>"},
    {"@type":"PropertyValue","name":"AudioStream_SHA256","value":"<streamhash sha256>"},
    {"@type":"PropertyValue","name":"S3_VersionID_WAV","value":"<version-id>"},
    {"@type":"PropertyValue","name":"IPFS_CID_v1","value":"<cid-if-used>"}
  ]
}
```

**Copy block — short disclosure (paste into descriptions/credits):**  
“Lyrics/vocals: human. AI assistance: arrangement & sound design (no impersonations). Full provenance, hashes, and loudness metrics: <your provenance URL>.”

---

## 4. Post-publication & "stay safe" guidance for AIAA

**Platform realities (2025):**
- **Spotify** normalizes playback around **−14 LUFS**, fights spam, and is rolling out **AI-use disclosures**. Quiet tracks can be turned up at playback within headroom (they consider peaks to avoid encoder overs). Keep **≤ −1 dBTP** to stay safe. 
- **YouTube/YouTube Music**: disclosure labels for synthetic/altered content; normalization primarily **reduces** loud items (don’t count on a boost). Add a human-readable disclosure + provenance link in descriptions. 
- **Bandcamp**: **no LUFS target / no normalization**; they say uploads are **unchanged** (site player is just quieter by default). Master for the sound you want; what you upload is what people hear. 
- **SoundCloud**: public guidance is inconsistent; historically **no consistent loudness normalization**. Either way, assume your uploaded master’s loudness is what listeners hear (subject to transcoding). 
- Anti-spam hygiene: avoid mass low-effort uploads; keep session credits, hashes, and provenance visible—those are strong “real artist” signals that align with current enforcement. 

**Risk controls, given the spam crackdown:**
- Avoid **ultra-short, repetitive, or mass-duplicative** uploads; these are flagged by new spam filters. Maintain human-readable notes, **session credits**, and consistent metadata—signals of genuine authorship. 
- Keep **voice model ethics** tight (no impersonations, model/source provenance on file). Consider linking to a short “Creator Policy” page explaining your AI policy.

**Routine post-publish checklist:**
- Verify the track pages show **correct credits** and (where available) **AI disclosure labels**.  
- Archive the exact **delivered assets** (and their hashes) alongside any distributor **ingest receipts/IDs**.  
- Add the track to your **provenance index** (opus number → URL, ISRC, S3 VersionID, IPFS CID).  
- For YouTube, pin a comment with **credits + provenance link**; for SoundCloud/Bandcamp, mirror the disclosure in the description.

### Summary

**Spotify:** applies **loudness normalization** around ~−14 LUFS at playback (adds/subtracts gain while respecting headroom), and is actively filtering spam + supporting AI disclosures in credits; keeping **TP ≤ −1.0 dBTP** helps avoid encoder overs. Publish a clear disclosure. 
**YouTube / YouTube Music:** disclosure labels for synthetic/altered media are rolling out; include your human-readable disclosure and provenance link in the description. Don’t count on the platform to “boost” quieter masters; master to how you want it heard. 
**Bandcamp / SoundCloud:** public, stable loudness policies are sparse; assume **what you upload is what listeners hear** subject to their transcodes. Keep your disclosure in descriptions and point to the provenance URL.
**Anti-spam hygiene:** avoid mass low-effort uploads and near-duplicates; keep **session credits**, hashes, and provenance public — these are strong “real-artist” signals aligned with current enforcement. 

## 5. 90-seconds check (do that every time)

1) **Render master** (44.1/48 kHz, 24-bit WAV).  
2) **Normalize (two-pass)** to **I≈−14 LUFS / TP≤−1 dBTP**; verify and save the JSON results. (Use your `loudnorm-two-pass.sh` or `ffmpeg-normalize`.) 
3) Compute **SHA-256** (file) + **AudioStream SHA-256**; record both.  
4) Store master + derivations in **S3 Object Lock**; record **VersionIDs**. Optionally pin to **IPFS** (record **CID v1**). 
5) Fill sidecar (IDs/credits/disclosure/loudness/hashes/storage IDs) and publish/update the **provenance page** with `MusicRecording` JSON-LD.  
6) When uploading (Spotify via distributor / YouTube / Bandcamp / SoundCloud), paste the **short disclosure** and **provenance link** into descriptions.

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
    "isrc": "QT-XX-VV-RR-12345",
    "upc": "NONE-SO-FAR",
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

Enter the AI assistance comments (see above for the sample). Store the above "sidecar file" for further use.

Now use the below `make-hashes.sh` script to store the media files checksums into the sidecar. Note: the streaming hash is related to the actual audio stream. It is usually not changed if the file changes metadata (unlike the hash checksum for the entire media file).

```bash
#!/usr/bin/env bash
set -euo pipefail

# Fuses: file SHA-256 + FFmpeg audio essence hashes + EBU R128 loudness +
# encoder note (MP3). Optionally embeds BWF audio-data MD5 in WAV.

usage() {
  cat <<'USAGE'
Usage:
  make-hashes.sh [options] FILE [FILE2 ...]
Options:
  -j, --json PATH     Update (or create) sidecar JSON with results
  -I, --lufs          Expected integrated loudness LUFS   [-14]
  -T, --tp            Expected true peak (dBTP)           [-1.0]
  -L, --lra           Expected loudness range (LU)        [11]
  --bwf-embed         For .wav: embed BWF audio-data MD5 (<MD5 > chunk)
  -q, --quiet         Less console output
  -h, --help          This help

Examples:
  make-hashes.sh track.wav track.mp3 video.mp4
  make-hashes.sh -j track.meta.json track.wav track.mp3 video.mp4
  make-hashes.sh --bwf-embed -j track.meta.json track.wav
USAGE
}

JSON=""
BWF_EMBED=0
QUIET=0
I_TARGET="-14"
TP_TARGET="-1.0"
LRA_TARGET="11"

ARGS=()
while [[ $# -gt 0 ]]; do
  case "$1" in
    -j|--json) JSON="$2"; shift 2;;
    -I|--lufs) I_TARGET="$2"; shift 2;;
    -T|--tp)   TP_TARGET="$2"; shift 2;;
    -L|--lra)  LRA_TARGET="$2"; shift 2;;
    --bwf-embed) BWF_EMBED=1; shift;;
    -q|--quiet) QUIET=1; shift;;
    -h|--help) usage; exit 0;;
    --) shift; break;;
    -*) echo "Unknown option: $1" >&2; usage; exit 1;;
    *) ARGS+=("$1"); shift;;
  esac
done
FILES=("${ARGS[@]}")
[[ ${#FILES[@]} -eq 0 ]] && { usage; exit 1; }

need() { command -v "$1" >/dev/null 2>&1 || { echo "Missing: $1" >&2; exit 1; }; }
need sha256sum
need ffmpeg
command -v jq >/dev/null 2>&1 || echo "Note: jq not found; JSON sidecar updates will be disabled." >&2
command -v ffprobe >/dev/null 2>&1 || echo "Note: ffprobe not found; encoder tag may be unavailable." >&2

json_put() {
  # json_put "dot.path.like.this" "value"
  local key="$1" value="$2"
  [[ -z "$JSON" ]] && return 0
  command -v jq >/dev/null 2>&1 || return 0
  [[ -f "$JSON" ]] || echo '{}' > "$JSON"
  local tmp; tmp="$(mktemp)"

  # Use setpath() with a path-array, and parse JSON values when possible.
  jq --arg p "$key" --arg v "$value" '
    def tokeys: split(".");
    def maybe: (try ($v|fromjson) catch $v);
    setpath( ($p|tokeys); maybe )
  ' "$JSON" > "$tmp" && mv "$tmp" "$JSON"
}

extract_hash_value() { sed -E 's/.*=([0-9A-Fa-f]+).*/\1/'; }
extract_streamhash_value() { awk -F= '{print $NF}' | tr -d '\r\n'; }

get_loudness_json() {
  # Prints a compact JSON with integrated_lufs, lra, max_true_peak_db
  local f="$1"
  # Run loudnorm once; capture the JSON block from stderr
  local block
  block="$( ffmpeg -hide_banner -i "$f" \
            -filter:a loudnorm=I=${I_TARGET}:LRA=${LRA_TARGET}:TP=${TP_TARGET}:print_format=json \
            -f null - 2>&1 \
            | awk 'BEGIN{p=0} /^ *\{/{p=1} {if(p)print} /^ *\}/{if(p){exit}}' )" || true
  if [[ -n "$block" ]]; then
    # loudnorm outputs measured_* OR input_* fields depending on pass; prefer measured_*
    echo "$block" | jq -c '{
      integrated_lufs: ( .measured_I // .input_i ) | tonumber,
      lra:             ( .measured_LRA // .input_lra ) | tonumber,
      max_true_peak_db:( .measured_tp // .input_tp ) | tonumber
    }' 2>/dev/null || true
  fi
}

get_encoder_tag() {
  local f="$1"
  local enc=""
  if command -v ffprobe >/dev/null 2>&1; then
    enc="$( ffprobe -v error -show_entries format_tags=encoder \
            -of default=nw=1:nk=1 "$f" 2>/dev/null || true )"
  fi
  if [[ -z "$enc" ]] && command -v mediainfo >/dev/null 2>&1; then
    enc="$( mediainfo --Inform="General;%Encoded_Library%" "$f" 2>/dev/null || true )"
    [[ -z "$enc" ]] && enc="$( mediainfo --Inform="Audio;%Encoded_Library%" "$f" 2>/dev/null || true )"
  fi
  echo "$enc"
}

if [[ $BWF_EMBED -eq 1 ]]; then
  need bwfmetaedit
fi

for f in "${FILES[@]}"; do
  [[ -f "$f" ]] || { echo "Not a file: $f" >&2; continue; }
  base="$(basename "$f")"; ext="${f##*.}"; ext="${ext,,}"

  # A) File-level SHA-256
  sha256="$(sha256sum "$f" | awk '{print $1}')"
  (( QUIET == 0 )) && echo "[${base}] file_sha256: $sha256"
  case "$ext" in
    wav) json_put "checksums.file_sha256.wav" "$sha256" ;;
    mp3) json_put "checksums.file_sha256.mp3" "$sha256" ;;
    mp4|m4v|mov) json_put "checksums.file_sha256.mp4" "$sha256" ;;
    *)   json_put "checksums.file_sha256.$ext" "$sha256" ;;
  esac

  # B) Audio-essence hashes (per-stream + combined)
  stream_sha256="$(
    ffmpeg -v error -i "$f" -map 0:a:0 -f streamhash -hash sha256 - 2>/dev/null \
      | tail -n1 | extract_streamhash_value
  )"
  if [[ -n "$stream_sha256" ]]; then
    (( QUIET == 0 )) && echo "[${base}] audio_stream_sha256: $stream_sha256"
    json_put "checksums.audio_stream_sha256.$ext" "$stream_sha256"
  fi

  combined="$(
    ffmpeg -v error -i "$f" -map 0:a:0 -f hash -hash sha256 - 2>/dev/null \
      | tail -n1 | extract_hash_value
  )"
  if [[ -n "$combined" ]]; then
    (( QUIET == 0 )) && echo "[${base}] audio_hash_sha256:   $combined"
    json_put "checksums.audio_hash_sha256.$ext" "$combined"
  fi

  # C) Optional BWF audio-data MD5 embed (WAV only)
  if [[ $BWF_EMBED -eq 1 && "$ext" == "wav" ]]; then
    if bwfmetaedit --MD5-Embed --reject-overwrite "$f" >/dev/null 2>&1; then
      (( QUIET == 0 )) && echo "[${base}] BWF MD5 embedded (<MD5 > chunk)"
      json_put "checksums.bwf_audio_md5.note" "Embedded in WAV <MD5 > chunk (view via BWF MetaEdit Tech export)."
    else
      echo "[${base}] WARN: Could not embed BWF MD5" >&2
    fi
  fi

  # D) Loudness (Integrated LUFS, LRA, Max True Peak)
  if [[ "$ext" == "wav" || "$ext" == "mp3" || "$ext" == "flac" || "$ext" == "mp4" || "$ext" == "m4a" ]]; then
    lj="$( get_loudness_json "$f" )"
    if [[ -n "$lj" ]]; then
      (( QUIET == 0 )) && echo "[${base}] loudness: $lj"
      # Write under tech.loudness.<ext> in the sidecar
      json_put "tech.loudness.$ext" "$lj"
    fi
  fi

  # E) Encoder note (MP3 focus)
  if [[ "$ext" == "mp3" ]]; then
    enc="$( get_encoder_tag "$f" )"
    if [[ -n "$enc" ]]; then
      note="$enc"
      # If you keep a fixed ceiling in mastering, append it here or downstream.
      json_put "tech.encoder_note" "$note"
      (( QUIET == 0 )) && echo "[${base}] encoder_note: $note"
    fi
  fi

done

[[ -n "$JSON" && $QUIET -eq 0 ]] && echo "Updated sidecar JSON: $JSON"
```

Like this: `./make-hashes.sh -j track.meta.json track.wav track.mp3 video.mp4`

### A.4 Conclude filling the sidecar AND embed metadata into audio files

Check the sidecar file; if there are still missing records, fill them properly.

Use `json-to-mp3.sh` script below to embed the .mp3 with metadata, including provenance records.

```bash
#!/usr/bin/env bash
# json-to-mp3.sh
# Usage: json-to-mp3.sh <json_sidecar> <in.mp3> [out.mp3]
set -euo pipefail

JQ=${JQ:-jq}
FFMPEG=${FFMPEG:-ffmpeg}
EYED3=${EYED3:-eyeD3}

if [[ $# -lt 2 ]]; then
  echo "Usage: $0 <json_sidecar> <in.mp3> [out.mp3]" >&2
  exit 1
fi

JSON="$1"
IN="$2"
OUT="${3:-$2}"

command -v "$JQ" >/dev/null || { echo "jq not found"; exit 1; }
command -v "$FFMPEG" >/dev/null || { echo "ffmpeg not found"; exit 1; }
command -v "$EYED3" >/dev/null || { echo "eyeD3 not found"; exit 1; }

TITLE=$($JQ -r '.title // empty' "$JSON")
ARTIST=$($JQ -r '.participants.artist // empty' "$JSON")
ALBUM_ARTIST=$($JQ -r '.participants.album_artist // empty' "$JSON")
ALBUM=$($JQ -r '.participants.album // empty' "$JSON")
GENRE=$($JQ -r '.tech.genre // empty' "$JSON")
DATE=$($JQ -r '.date_created_utc // empty' "$JSON")
COMPOSER=$($JQ -r '.participants.composer // empty' "$JSON")
LYRICIST=$($JQ -r '.participants.lyricist // empty' "$JSON")
PUBLISHER=$($JQ -r '.rights.publisher // empty' "$JSON")
COPYRIGHT=$($JQ -r '.rights.copyright // empty' "$JSON")
ISRC=$($JQ -r '.ids.isrc // empty' "$JSON")

COMM=$($JQ -r '.id3.comments[0] // empty' "$JSON")
URL_WORK=$($JQ -r '.id3.urls.work_page // empty' "$JSON")
URL_ARTIST=$($JQ -r '.id3.urls.artist_page // empty' "$JSON")

TXXX_AI=$($JQ -r '.id3.custom_txxx.AI_Involvement // empty' "$JSON")
TXXX_URL=$($JQ -r '.id3.custom_txxx.Provenance_URL // empty' "$JSON")
TXXX_TOOLS=$($JQ -r '.id3.custom_txxx.Tools // empty' "$JSON")

TSOP=$($JQ -r '.id3.sort_fields.TSOP // empty' "$JSON")
TSOA=$($JQ -r '.id3.sort_fields.TSOA // empty' "$JSON")
TSOT=$($JQ -r '.id3.sort_fields.TSOT // empty' "$JSON")

ART_PATH=$($JQ -r '.artwork.path // empty' "$JSON")

# If OUT differs, start from a fresh copy
if [[ "$OUT" != "$IN" ]]; then
  cp -p "$IN" "$OUT"
fi

# First pass: ffmpeg writes standard frames (v2.3)
TMP="$OUT.tmp.mp3"
$FFMPEG -y -i "$OUT" -id3v2_version 3 -codec copy \
  -metadata title="$TITLE" \
  -metadata artist="$ARTIST" \
  -metadata album_artist="$ALBUM_ARTIST" \
  -metadata album="$ALBUM" \
  -metadata genre="$GENRE" \
  -metadata date="$DATE" \
  -metadata composer="$COMPOSER" \
  -metadata lyricist="$LYRICIST" \
  -metadata publisher="$PUBLISHER" \
  -metadata copyright="$COPYRIGHT" \
  -metadata TSRC="$ISRC" \
  -metadata AI_Involvement="$TXXX_AI" \
  -metadata Provenance_URL="$TXXX_URL" \
  -metadata Tools="$TXXX_TOOLS" \
  -metadata TSOP="$TSOP" \
  -metadata TSOA="$TSOA" \
  -metadata TSOT="$TSOT" \
  "$TMP"

mv "$TMP" "$OUT"

# Second pass: ensure COMM and v2.3; clean/add art in a single APIC
# Remove any existing images (avoid multiple APICs)
$EYED3 --remove-all-images "$OUT" >/dev/null

# Add Front Cover if provided
if [[ -n "$ART_PATH" && -f "$ART_PATH" ]]; then
  $EYED3 --add-image "$ART_PATH:FRONT_COVER" "$OUT" >/dev/null
fi

# Add comment explicitly as COMM
if [[ -n "$COMM" ]]; then
  $EYED3 --comment "$COMM" "$OUT" >/dev/null
fi

# Force ID3 v2.3 final tag flavor for broad compatibility
$EYED3 --to-v2.3 "$OUT" >/dev/null

echo "MP3 metadata embedded -> $OUT"
```

Like this: `./json-to-mp3 .sh track.meta.json in.mp3 out.mp3`

In case the art is greater than 600x600px, it can have issues when the track is played on legacy devices; use the below script to  embed a lesser image than a typical track art.

The script `embed-art-to-mp3.sh`:

```bash
#!/usr/bin/env bash
# embed-art-mp3.sh
# Cleanly (re)embed a single Front Cover image into MP3 files as ID3v2.3.

set -euo pipefail

if ! command -v eyeD3 >/dev/null 2>&1; then
  echo "Error: eyeD3 not found." >&2
  exit 1
fi

if [[ $# -lt 2 ]]; then
  cat <<USAGE
Usage: $0 <cover.jpg> <file-or-glob.mp3> [more.mp3 ...]
Tips:
  - Use a baseline 500–600px JPEG for best car/tablet compatibility.
  - Example: $0 cover_600.jpg *.mp3
USAGE
  exit 1
fi

cover="$1"; shift
if [[ ! -f "$cover" ]]; then
  echo "Error: cover image not found: $cover" >&2
  exit 1
fi

rc=0
for f in "$@"; do
  if [[ ! -f "$f" ]]; then
    echo "Skip (not a file): $f" >&2
    rc=1
    continue
  fi

  echo ">> Processing: $f"
  # Remove all existing images / APIC frames (avoid duplicate/secondary types).
  eyeD3 --remove-all-images "$f" >/dev/null

  # Ensure ID3v2 tag exists (some files might be missing it).
  eyeD3 --v2 "$f" >/dev/null

  # Add exactly one Front Cover. (APIC type: FRONT_COVER)
  eyeD3 --add-image "$cover:FRONT_COVER" "$f" >/dev/null

  # Convert tag flavor to v2.3 for older devices.
  eyeD3 --to-v2.3 "$f" >/dev/null

  echo "   OK: embedded Front Cover (ID3v2.3)"
done

exit $rc
```

Like this: `./embed-art-to-mp3.sh newart.jpg in.mp3 out.mp3`

### A.5 Put master + derivations into **S3 Object Lock** (record **VersionIDs**); optionally pin to **IPFS** and record the **CID**

For any future inquiries, it's a good idea to keep the original files (mastered and normalized .wav and the derived tracks, such as .mp3 and .mp4) into an immutable and reliable storage, such as S3 Object Lock  buckets, or IPFS.

Detailed instructions on that are still to be written. It's a good idea to also keep a backup copy of all the media files, art and projects created by Audacity or your audio editor of choice, as well.

### A.6 Update your **provenance page** (JSON-LD + human section)

Creating a provenance page template for your favorite CMS can be a challenge, this set of topics to be covered later.

An example of real-life provenance page: [Wilds Collection - Gravel Of Time](https://kamaskera.com/tracks/2570/).

### A.7 Upload to distribution services and similar platforms.

Upload to **Bandcamp/SoundCloud** (playground, feedback) and to distributor (Spotify/Apple/YouTube Music). Include **plain-English AI disclosure** in descriptions. 

### A.8 Post-publishing

Check platform pages, screenshots, archive distributor IDs, and add the entry to your **provenance index** (you do keep one, don't you?).
