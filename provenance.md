# Provenance basics

Measures to take to make tracks as DDEX compliant (in terms of AI generative audio) as possible.

## Copy-Paste Metadata Blocks

### DistroKid / Spotify credits (short, future-proof)
```
Lyrics: human-written by [Name].
Vocals: human-performed by [Name/Persona].
Instruments/Arrangement: human-performed & programmed; AI-assisted timbre/arrangement ideation; no impersonations.
Production: [DAW/Tools]; Mastering: [Tool/Engineer].
```

### SoundCloud description (tight feedback bait)
```
[1-line concept: e.g., “Ghost-waltz ballad with detuned calliope and twin harmonies.”]
Human lyrics & vocals; AI-assisted sound design (pads/drums); no impersonations.
Q: Cut the bridge 8 bars or keep the organ flourish?
Tags: ghost-pop, ritual-waltz, 3-4, twin-harmonies, calliope, spectral-choir
```

### Bandcamp “Credits” (concise, fan-facing)
```
Lyrics & vocals: human (Lora/Mia).
Arrangement & instruments: human; AI-assisted timbre ideation, re-performed & mixed by K.B.
No voice cloning; no copyrighted samples.
Mastering: [Tool/Engineer]. Personas: Wilds Sisters (Mia lead / Lora harmony).
```

### YouTube description (with site link)
```
A spectral waltz built from live vocals & hand-played MIDI, set in a haunted carousel space.
Credits: human-written lyrics; human vocals; AI-assisted sound design (pads/drums); no impersonations.
More notes + stems preview: https://your-site/post-slug
#ghostpop #ritualwaltz #wildssisters #baroquepop
```

## File naming

### Simple file naming
`2025-09-26_artist-persona_title_v1.0_ISRC.mp3`  
Keeps versions, dates, and IDs obvious when you’re bulk-uploading.

## Where to store provenance data

### WAV / BWF (with BWF MetaEdit)

#### Use these chunks
1) **BWF `bext` chunk** – the core, standardized place  
Fill at least:
- **Description** → short work summary / version (“Ghost-waltz ballad v1.1, human vocals; AI-assisted drums”).  
- **Originator** → your name/artist or production entity.  
- **OriginatorReference** → your internal unique ID (e.g., repo UID, MusicBrainz recording MBID).  
- **OriginationDate / OriginationTime** → UTC date/time of master creation.  
- **TimeReference** → sample count of first sample (leave if N/A).  
- **UMID** if you issue one; otherwise keep blank.  
- **Loudness fields** (LoudnessValue, LoudnessRange, MaxTruePeakLevel, etc.) if you measure EBU R128.  
- **CodingHistory** → human-readable lineage: mics, takes, edits, render toolchain (append lines; newest last).  
These fields are defined by EBU Tech 3285 and the FADGI guidance for BWF bext usage.

2) **iXML chunk** – rich, structured, human-readable XML  
Populate:
- **PROJECT**, **SCENE**, **TAKE**, **NOTE** (you can place a concise *provenance note* here),  
- **FILE_UID** (stable UUID), **SPEED**, **TRACK_LIST** (if multitrack), etc.  
iXML is designed for production metadata and travels well through DAWs/post.

3) **RIFF LIST-INFO** (a.k.a. `INFO`) – for broad app compatibility  
Useful tags:
- **INAM** (Title), **IART** (Artist), **IPRD** (Album/Release), **ICRD** (Creation date),  
- **ICMT** (Comment – short provenance line), **ISFT** (Software), **IENG/ITCH** (Engineer/Technician).  
The US FADGI guidance covers using bext + INFO together.

4) **aXML** – embed an XML record (e.g., **EBUCore/Dublin Core**); perfect for a compact, future-proof provenance block (AI involvement, licenses, links). BWF MetaEdit supports aXML presence/validation.

5) **MD5 of audio essence** – ask BWF MetaEdit to compute/store the MD5 for the audio data chunk; handy for integrity and chain-of-custody.

**Suggested mapping (WAV/BWF)**  
- Provenance (short): `bext.Description` (headline) + `INFO/ICMT` (1–2 lines).  
- Provenance (structured): `iXML` NOTE + `aXML` (EBUCore XML with fields like human/AI roles, tool versions, license URLs).  
- Identity: `bext.Originator` (you), `OriginatorReference` (your UID), optional UMID.  
- Process history: `bext.CodingHistory` (append-only).  
- Technical: loudness fields (if R128), MD5.

---

### MP3 (with ffmpeg → ID3v2.3/2.4)

#### Core ID3 frames to use
- **TIT2** (Title), **TPE1** (Lead artist), **TPE2** (Album artist / ensemble), **TALB** (Album), **TRCK** (Track), **TCON** (Genre), **TDRC/TDOR** (Date/Original date), **TCOM** (Composer), **TEXT** (Lyricist), **TSRC** (ISRC), **TPUB** (Publisher), **TCOP** (Copyright).  
- **TIPL/TMCL** (v2.4) or **IPLS** (v2.3) to credit roles (“Vocal – human”, “Producer”, “Engineer”).  
- **WOAR/WOAF/WCOP/WORS** (official URLs) or **WXXX** (user URL).  
- **COMM** (comment) for a short provenance line.  
These frames are in the ID3 specs; ffmpeg honors a defined subset for MP3 muxing.

#### Custom / provenance fields
For anything beyond the standard set (e.g., “AI_Involvement”, “Provenance_URL”, toolchain), write **TXXX (user text)** frames. ffmpeg maps unknown `-metadata key=value` pairs into TXXX automatically.

> Note: Some ffmpeg builds historically wrote `comment=` to **TXXX** instead of **COMM**; verify your tags after writing (or use eyeD3 for strict COMM if needed).

#### Example ffmpeg write (ID3v2.3)
```bash
ffmpeg -i master.wav -codec:a libmp3lame -b:a 320k \
  -id3v2_version 3 \
  -metadata title="Ritual Waltz / Bone Reflection" \
  -metadata artist="Wilds Sisters" \
  -metadata album_artist="Wilds Sisters" \
  -metadata album="Wilds Collection Vol. 1" \
  -metadata date="2025-09-26" \
  -metadata genre="Ghost Pop" \
  -metadata composer="K. Boyandin" \
  -metadata lyricist="K. Boyandin" \
  -metadata TSRC="US-XXX-25-00001" \
  -metadata publisher="Your Label" \
  -metadata copyright="© 2025 Your Label" \
  -metadata COMM="Provenance: human lyrics & vocals; AI-assisted drums/pads; no impersonations." \
  -metadata AI_Involvement="Vocals/Lyrics human; Arrangement/Sound design AI-assisted; Tools: Suno v5.0, Producer FUZZ-2.0" \
  -metadata Provenance_URL="https://your-site/post-slug" \
  out.mp3
```
- `-id3v2_version 3` forces ID3v2.3 for maximum compatibility; omit or use `4` if you want TIPL/TMCL (v2.4 role frames). ffmpeg’s honored keys list is documented by the community.

**Suggested mapping (MP3)**  
- Provenance (short): **COMM**.  
- Provenance (structured): **TXXX:AI_Involvement**, **TXXX:Provenance_URL**, **TXXX:Tools**.  
- Identity/rights: **TSRC** (ISRC), **TCOP** (copyright), **TPUB** (publisher), **WOAR/WCOP** links.  
- Roles: **TIPL/TMCL** (if using v2.4) or **IPLS** (v2.3) to explicitly credit “Vocals – human”, “Producer”, etc.

---

### “Often-missed but useful” fields to fill

**For both WAV/BWF and MP3:**
- **ISRC** (track-level identifier) – BWF: in iXML/aXML or INFO comment; MP3: **TSRC**.
- **Official URLs** – artist site, release page, provenance page; WAV: aXML/iXML or INFO ICMT; MP3: **WOAR/WXXX**.
- **Sort fields** (ID3v2.4): **TSOP** (performer sort), **TSOA** (album sort), **TSOT** (title sort) – helps libraries keep personas grouped correctly. 
- **Role credits** – use **TIPL/TMCL/IPLS** for granular people/roles (e.g., “Vocal – human”, “Arranger”, “Mastering”).
- **Creation software/version** – WAV: **INFO/ISFT**; MP3: **TSSE** (encoder/settings).
- **Loudness** (if measured) – WAV: bext loudness fields per EBU R128; MP3: store in **TXXX:Loudness_I** etc., or just document in COMM.
- **Unique IDs** – WAV: **UMID** (bext) or **FILE_UID** (iXML) for traceability; MP3: **UFID** (with owner URL, e.g., MusicBrainz).

---

### Minimal EBUCore aXML (drop-in)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ebucore:ebuCoreMain
    xmlns:ebucore="urn:ebu:metadata-schema:ebucore"
    xml:lang="en">
  <ebucore:coreMetadata>
    <!-- Identity -->
    <ebucore:title>Ritual Waltz / Bone Reflection</ebucore:title>
    <ebucore:identifier typeLabel="ISRC">US-XXX-25-00001</ebucore:identifier>
    <ebucore:dateCreated>2025-09-26T14:32:00Z</ebucore:dateCreated>

    <!-- Provenance summary (human vs AI roles) -->
    <ebucore:description typeLabel="Provenance">
      Human-written lyrics; human-performed vocals & hand-played MIDI.
      AI assistance limited to arrangement/timbre ideation (pads/drums).
      No impersonations; no third-party samples.
    </ebucore:description>

    <!-- Contributors & roles -->
    <ebucore:creator>
      <ebucore:person>
        <ebucore:givenName>K.</ebucore:givenName>
        <ebucore:familyName>Boyandin</ebucore:familyName>
        <ebucore:role typeLabel="Composer"/>
        <ebucore:role typeLabel="Lyricist"/>
        <ebucore:role typeLabel="Producer"/>
      </ebucore:person>
    </ebucore:creator>

    <ebucore:contributor>
      <ebucore:person>
        <ebucore:name>Wilds Sisters — Lora</ebucore:name>
        <ebucore:role typeLabel="Vocal (human)"/>
      </ebucore:person>
    </ebucore:contributor>
    <ebucore:contributor>
      <ebucore:person>
        <ebucore:name>Wilds Sisters — Mia</ebucore:name>
        <ebucore:role typeLabel="Vocal (human)"/>
      </ebucore:person>
    </ebucore:contributor>

    <!-- Tools / workflow -->
    <ebucore:comment typeLabel="Tools">
      DAW: Reaper 7.x; Generators: Suno v5.0, Producer FUZZ-2.0;
      Mastering: [tool/chain].
    </ebucore:comment>

    <!-- Rights & links -->
    <ebucore:rights>
      <ebucore:rightsSummary>© 2025 Your Label — All rights reserved.</ebucore:rightsSummary>
      <ebucore:copyright>
        <ebucore:copyrightStatement>
          © 2025 Your Label. Licensed for streaming & download; no model training without consent.
        </ebucore:copyrightStatement>
      </ebucore:copyright>
    </ebucore:rights>
    <ebucore:locator href="https://your-site.tld/post-slug" typeLabel="Provenance URL"/>
  </ebucore:coreMetadata>
</ebucore:ebuCoreMain>
```

**Notes**
- `xmlns:ebucore="urn:ebu:metadata-schema:ebucore"` is a commonly used namespace URI for EBUCore XML. If you validate against a specific XSD version, you can add `xsi:schemaLocation` pointing to the EBU XSD.
- This snippet stays within **coreMetadata** (portable across tools), which EBUCore defines for titles, dates, identifiers, contributors, descriptions, rights, and web locators.
- If you’re using ADM (Audio Definition Model) in EBUCore, you can add an `audioFormatExtended` block alongside `coreMetadata`, but it’s optional for provenance.

---

#### Optional: add ADM loudness/tech notes (if you measure R128)

```xml
<ebucore:technical>
  <ebucore:audioFormat>
    <ebucore:audioFormatExtended>
      <!-- Keep this simple; actual ADM uses detailed elements -->
      <ebucore:comment typeLabel="Loudness">
        Integrated: -14.0 LUFS; LRA: 7.5 LU; Max True Peak: -1.0 dBTP
      </ebucore:comment>
    </ebucore:audioFormatExtended>
  </ebucore:audioFormat>
</ebucore:technical>
```

*(Embed this inside `ebucore:ebuCoreMain` after `coreMetadata` if you like.)* The EBU’s extended audio model is expressed via `audioFormatExtended` in EBUCore; use it lightly unless you’re fully modeling ADM.

---

#### Where this lives in your WAV

- Paste the XML **as-is** into the **aXML** chunk via **BWF MetaEdit**. That chunk is the EBU-specified container for XML metadata in BWF/BW64.
- Keep your short, human-readable headline in `bext:Description` & a one-liner in `INFO/ICMT`; use **aXML** for the richer block above. (BWF MetaEdit supports bext + INFO + aXML workflows.)

---

## Helper scripts/configs

### Prepare artwork as track cover art

```
#!/usr/bin/env bash
# make-cover-baseline.sh
# Create a 600x600 baseline (non-progressive) JPEG for maximum device compatibility.

set -euo pipefail

if ! command -v magick >/dev/null 2>&1 && ! command -v convert >/dev/null 2>&1; then
  echo "Error: ImageMagick (magick/convert) not found." >&2
  exit 1
fi

if [[ $# -lt 2 ]]; then
  echo "Usage: $0 <input-image> <output-jpg> [size=600]"
  exit 1
fi

in="$1"
out="$2"
size="${3:-600}"

# Prefer 'magick' if present; otherwise use legacy 'convert'.
IM_TOOL="magick"
command -v magick >/dev/null 2>&1 || IM_TOOL="convert"

# Make square, center-crop, strip metadata, ensure baseline JPEG.
"$IM_TOOL" "$in" -resize "${size}x${size}^" -gravity center -extent "${size}x${size}" \
  -strip -interlace none -quality 85 "$out"

echo "Wrote baseline JPEG: $out"
```

### MP3: embed a single **Front Cover** (ID3v2.3, clean APICs first)

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

---

### M4A (AAC): embed **covr** artwork with AtomicParsley

```
#!/usr/bin/env bash
# embed-art-m4a.sh
# (Re)embed cover art into M4A/MP4 audio files via AtomicParsley.

set -euo pipefail

if ! command -v AtomicParsley >/dev/null 2>&1; then
  echo "Error: AtomicParsley not found." >&2
  exit 1
fi

if [[ $# -lt 2 ]]; then
  cat <<USAGE
Usage: $0 <cover.jpg> <file-or-glob.m4a> [more.m4a ...]
Note:
  - Prefer a baseline 500–600px JPEG for broad device compatibility.
  - Example: $0 cover_600.jpg *.m4a
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
  # Overwrite in-place, setting the 'covr' atom.
  AtomicParsley "$f" --artwork "$cover" --overWrite >/dev/null
  echo "   OK: embedded artwork (covr)"
done

exit $rc
```

### FLAC: embed picture block cleanly


```
#!/usr/bin/env bash
# embed-art-flac.sh
# Cleanly (re)embed FLAC picture block with a single cover image.

set -euo pipefail

if ! command -v metaflac >/dev/null 2>&1; then
  echo "Error: metaflac not found." >&2
  exit 1
fi

if [[ $# -lt 2 ]]; then
  echo "Usage: $0 <cover.jpg> <file-or-glob.flac> [more.flac ...]"
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
  metaflac --remove --block-type=PICTURE "$f"
  metaflac --import-picture-from="$cover" "$f"
  echo "   OK: embedded METADATA_BLOCK_PICTURE"
done

exit $rc
```

### Extended JSON sidecar

Save as `track.meta.json` (example filled with your style of metadata):

```json
{
  "title": "Ritual Waltz / Bone Reflection",
  "version": "v1.0",
  "date_created_utc": "2025-09-26T14:32:00Z",

  "ids": {
    "isrc": "US-XXX-25-00001",
    "upc": "123456789012",
    "musicbrainz_recording_id": "optional-uuid"
  },

  "participants": {
    "artist": "Wilds Sisters",
    "album_artist": "Wilds Sisters",
    "album": "Wilds Collection Vol. 1",
    "composer": "K. Boyandin",
    "lyricist": "K. Boyandin",
    "producer": "K. Boyandin",
    "label": "Your Label"
  },

  "provenance": {
    "summary": "Human-written lyrics; human vocals & hand-played MIDI. AI assistance limited to drum/pad ideation. No impersonations; no third-party samples.",
    "ai_involvement": {
      "lyrics": "human",
      "vocals": "human",
      "composition_arrangement": "ai_assisted",
      "sound_design": "ai_assisted",
      "mix_master": "human"
    },
    "tools": ["Reaper 7.x", "Suno v5.0", "Producer FUZZ-2.0"],
    "provenance_url": "https://your-site.tld/post-slug"
  },

  "rights": {
    "copyright": "© 2025 Your Label",
    "rights_summary": "All rights reserved. No model training without consent.",
    "publisher": "Your Label"
  },

  "tech": {
    "genre": "Ghost Pop",
    "track_number": "1",
    "disc_number": "1",
    "loudness": {
      "integrated_lufs": -14.0,
      "lra": 7.5,
      "max_true_peak_db": -1.0
    },
    "encoder_note": "320k MP3 target / -1.0 dBTP ceiling"
  },

  "artwork": {
    "path": "art/cover_600.jpg",
    "type": "front",
    "mime": "image/jpeg",
    "pixels": "600x600"
  },

  "bwf": {
    "bext": {
      "Description": "Ghost-waltz ballad v1.0, human vocals; AI-assisted drums/pads",
      "Originator": "Wilds Sisters / Your Label",
      "OriginatorReference": "WS-2025-0001",
      "OriginationDate": "2025-09-26",
      "OriginationTime": "14:32:00",
      "CodingHistory": [
        "A=PCM,F=48000,W=24,M=stereo,T=Reaper7 print",
        "Edit=arrangement polish; Suno/Producer ideation; re-performed",
        "Master=Limiter ceiling -1.0 dBTP"
      ],
      "UMID": ""
    },
    "iXML_note": "Lyrics & vocals human; AI-assisted timbre ideation (pads/drums); tools: Suno v5.0, Producer FUZZ-2.0.",
    "ebucore_axml": "embed" 
  },

  "id3": {
    "prefer_version": "2.3",
    "urls": {
      "work_page": "https://your-site.tld/post-slug",
      "artist_page": "https://your-site.tld"
    },
    "comments": [
      "Provenance: human lyrics & vocals; AI-assisted drums/pads; no impersonations."
    ],
    "custom_txxx": {
      "AI_Involvement": "Vocals/Lyrics human; Arrangement/Sound design AI-assisted; Tools: Suno v5.0, Producer FUZZ-2.0",
      "Provenance_URL": "https://your-site.tld/post-slug",
      "Tools": "Reaper 7.x; Suno v5.0; Producer FUZZ-2.0"
    },
    "sort_fields": {
      "TSOP": "Wilds Sisters",
      "TSOA": "Wilds Collection Vol. 1",
      "TSOT": "Ritual Waltz / Bone Reflection"
    }
  }
}
```

### `json-to-wav.sh` — embed into WAV/BWF (bext + INFO + iXML + aXML)

This script:

- reads the sidecar JSON,
- creates a **CORE CSV** for bext/INFO mapping,
- creates optional **iXML** and **aXML (EBUCore)** snippets,
- calls **BWF MetaEdit** to import & save.

> BWF MetaEdit supports **import/export of CORE CSV/XML** and editing of **iXML/aXML** chunks; FADGI’s docs describe command-line availability and CSV workflows.

```bash
#!/usr/bin/env bash
# json-to-wav.sh
# Usage: json-to-wav.sh <json_sidecar> <in.wav> [out.wav]
set -euo pipefail

JQ=${JQ:-jq}
BWF=${BWF:-bwfmetaedit}

if [[ $# -lt 2 ]]; then
  echo "Usage: $0 <json_sidecar> <in.wav> [out.wav]" >&2
  exit 1
fi

JSON="$1"
IN="$2"
OUT="${3:-$2}"   # in-place by default

command -v "$JQ" >/dev/null || { echo "jq not found"; exit 1; }
command -v "$BWF" >/dev/null || { echo "bwfmetaedit not found"; exit 1; }

# temp files
TMPDIR="$(mktemp -d)"
CORECSV="$TMPDIR/core.csv"
IXML="$TMPDIR/ixml.xml"
AXML="$TMPDIR/axml.xml"

cleanup() { rm -rf "$TMPDIR"; }
trap cleanup EXIT

# Pull BEXT fields from JSON
DESC=$($JQ -r '.bwf.bext.Description // empty' "$JSON")
ORIG=$($JQ -r '.bwf.bext.Originator // empty' "$JSON")
ORIGREF=$($JQ -r '.bwf.bext.OriginatorReference // empty' "$JSON")
ODATE=$($JQ -r '.bwf.bext.OriginationDate // empty' "$JSON")
OTIME=$($JQ -r '.bwf.bext.OriginationTime // empty' "$JSON")
CHIST=$($JQ -r '.bwf.bext.CodingHistory // [] | join("\n")' "$JSON")

# INFO fields
TITLE=$($JQ -r '.title // empty' "$JSON")
ARTIST=$($JQ -r '.participants.artist // empty' "$JSON")
ALBUM=$($JQ -r '.participants.album // empty' "$JSON")
CREATED=$($JQ -r '.date_created_utc // empty' "$JSON")

# Build CORE CSV (headers accepted by BWF MetaEdit for bext/INFO)
# Columns include FileName so import knows which file to target.
{
  echo "FileName,Description,Originator,OriginatorReference,OriginationDate,OriginationTime,CodingHistory,INAM,IART,IPRD,ICRD"
  echo "\"$OUT\",\"$DESC\",\"$ORIG\",\"$ORIGREF\",\"$ODATE\",\"$OTIME\",\"$CHIST\",\"$TITLE\",\"$ARTIST\",\"$ALBUM\",\"$CREATED\""
} > "$CORECSV"

# Optional iXML note
IXML_NOTE=$($JQ -r '.bwf.iXML_note // empty' "$JSON")
if [[ -n "$IXML_NOTE" ]]; then
  cat > "$IXML" <<XML
<?xml version="1.0" encoding="UTF-8"?>
<iXML_VERSION xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">1.5</iXML_VERSION>
<NOTE>$IXML_NOTE</NOTE>
XML
fi

# Optional EBUCore aXML (use your earlier aXML; minimal one here)
EMBED_AXML=$($JQ -r '.bwf.ebucore_axml // empty' "$JSON")
if [[ "$EMBED_AXML" == "embed" ]]; then
  TITLE_ESC=$(printf "%s" "$TITLE" | sed 's/&/&amp;/g; s/</&lt;/g; s/>/&gt;/g')
  ISRC=$($JQ -r '.ids.isrc // empty' "$JSON")
  DATE=$($JQ -r '.date_created_utc // empty' "$JSON")
  SUMM=$($JQ -r '.provenance.summary // empty' "$JSON")
  TOOLS=$($JQ -r '.provenance.tools | join("; ") // empty' "$JSON")
  PURL=$($JQ -r '.provenance.provenance_url // empty' "$JSON")
  RCOPY=$($JQ -r '.rights.copyright // empty' "$JSON")

  cat > "$AXML" <<XML
<?xml version="1.0" encoding="UTF-8"?>
<ebucore:ebuCoreMain xmlns:ebucore="urn:ebu:metadata-schema:ebucore" xml:lang="en">
  <ebucore:coreMetadata>
    <ebucore:title>$TITLE_ESC</ebucore:title>
    <ebucore:identifier typeLabel="ISRC">$ISRC</ebucore:identifier>
    <ebucore:dateCreated>$DATE</ebucore:dateCreated>
    <ebucore:description typeLabel="Provenance">$SUMM</ebucore:description>
    <ebucore:comment typeLabel="Tools">$TOOLS</ebucore:comment>
    <ebucore:rights>
      <ebucore:rightsSummary>$RCOPY</ebucore:rightsSummary>
    </ebucore:rights>
    <ebucore:locator href="$PURL" typeLabel="Provenance URL"/>
  </ebucore:coreMetadata>
</ebucore:ebuCoreMain>
XML
fi

# If OUT different from IN, copy audio first (safe write)
if [[ "$OUT" != "$IN" ]]; then
  cp -p "$IN" "$OUT"
fi

# Import CORE into WAV and save.
# (BWF MetaEdit supports import/export of CORE CSV/XML and saving changes;
# exact CLI flag names vary by build/package, but commonly accept an import of a CORE doc then Save.)
"$BWF" --import-core "$CORECSV" --save "$OUT"

# Inject iXML/aXML if provided (many builds allow XML chunk import via CLI; if not, you can paste via GUI)
if [[ -s "$IXML" ]]; then
  "$BWF" --import-ixml "$IXML" --save "$OUT" || true
fi
if [[ -s "$AXML" ]]; then
  "$BWF" --import-axml "$AXML" --save "$OUT" || true
fi

echo "WAV metadata embedded -> $OUT"
```

### `json-to-mp3.sh` — embed into MP3 (ID3 v2.3 + cover art)

This script:

- maps JSON → standard ID3 frames via **ffmpeg** (`-id3v2_version 3`),
- writes **TXXX** customs (AI_Involvement etc.),
- enforces **v2.3** and **COMM** via **eyeD3**, and
- optionally adds **Front Cover** art (single APIC).

Why these tools?

- ffmpeg can write ID3 v2.3 headers (`-id3v2_version 3`) and honors many standard keys.
- ffmpeg may map `comment` to **TXXX** on some builds; **eyeD3** ensures **COMM** and v2.3 finalization and manages APIC cleanly.

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

### Calculating hashes for audio data

#### What to checksum (and why)

##### A) File-level checksums (for exact-bits verification)
Compute **SHA-256** for each file you distribute or host directly:
- `track.wav` (your final master, with BWF metadata)  
- `track.mp3` (your downloadable/stored MP3)  
- `video.mp4` (your static-art video)

Example:
```bash
sha256sum track.wav track.mp3 video.mp4
# or
openssl dgst -sha256 track.wav track.mp3 video.mp4
```
Use case: anyone who got the file from your Bandcamp/site (or who you sent the file to) can confirm it’s unchanged. This is standard fixity practice.

> Note: The **same audio** inside different containers (MP3 vs MP4) will almost always have **different file hashes** due to different headers/metadata/timestamps. That’s why audio-essence hashes are helpful (next).

##### B) Audio-essence checksums (container-agnostic verification)
1) **WAV/BWF**: embed & publish the **audio-data MD5** (“essence MD5”). You can compute/store it inside the file with **BWF MetaEdit**; later anyone can re-evaluate to confirm the PCM audio data is unchanged even if other chunks changed.  
   - BWF MetaEdit shows stored vs evaluated MD5 for the audio data chunk.

2) **MP3/MP4 (and any container)**: publish a **per-stream hash** computed by FFmpeg so others can verify the audio content independent of container metadata. Two reliable options:
   - **hash/streamhash muxer** (one hash per stream):
     ```bash
     # Hash the audio stream (sha256) regardless of container:
     ffmpeg -i video.mp4 -map 0:a:0 -f hash -hash sha256 -
     # or:
     ffmpeg -i track.mp3 -map 0:a:0 -f streamhash -hash sha256 -
     ```
     (Produces one stable hash for that audio stream.)
   - **framemd5** (hash of decoded frames, timestamps ignored), useful when you need “decoded-audio” equality:
     ```bash
     ffmpeg -i track.mp3 -map 0:a:0 -f framemd5 -
     ```
     (This outputs many lines—store or re-hash the output if you want a single digest.)

Publish the essence hash(es) on the track’s provenance page; anyone can compute the same from any copy (e.g., a re-muxed MP4) to prove it’s the same audio.

#### Script: `make-hashes.sh`

```
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

ARGS=()
while [[ $# -gt 0 ]]; do
  case "$1" in
    -j|--json) JSON="$2"; shift 2;;
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
  # json_put "key.path.like.this" "value"
  local key="$1" value="$2"
  [[ -z "$JSON" ]] && return 0
  command -v jq >/dev/null 2>&1 || return 0
  [[ -f "$JSON" ]] || echo '{}' > "$JSON"
  local tmp
  tmp="$(mktemp)"
  # Set nested keys with jq
  jq --arg v "$value" '
    def setpathstr($p; $v):
      ( $p | split(".") ) as $keys
      | (reduce range(0; $keys|length) as $i
          (.; if $i < $keys|length-1 then .[$keys[$i]] //= {} else . end))
      | .[$keys[-1]] = $v
    ;
    setpathstr("'"$key"'"; $v)
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
            -filter:a loudnorm=I=-23:LRA=7:TP=-1.0:print_format=json \
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

---

## Building provenance URL

### Minimal page outline (copy this structure)

**H1: Track Title (Version, Date)**  
- **Credits**: writer(s), vocalist(s), producer, engineer, label  
- **Identifiers**: ISRC, UPC (if any), MusicBrainz links  
- **AI Disclosure**: concise statement (what was AI-assisted vs. human)  
- **Master Info**: duration, sample rate/bit depth, loudness (LUFS/LRA/TP)  
- **Checksums**: SHA256 for each distributed file (mp3, wav, flac)  
- **Embedded Metadata Snapshot**: key BWF/ID3 fields currently inside files  
- **Links**: canonical release page, platforms, stems/notes, MBID, AcoustID  
- **Changelog**: dated entries describing any change to audio or metadata

---

### Example JSON-LD (drop into the page)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "MusicRecording",
  "name": "Ritual Waltz / Bone Reflection",
  "isrcCode": "US-XXX-25-00001",
  "byArtist": { "@type": "MusicGroup", "name": "Wilds Sisters" },
  "inAlbum": { "@type": "MusicAlbum", "name": "Wilds Collection Vol. 1" },
  "genre": "Ghost Pop",
  "datePublished": "2025-10-06",
  "url": "https://your-site.tld/post-slug",
  "additionalProperty": [{
    "@type": "PropertyValue",
    "name": "AIDisclosure",
    "value": "Lyrics & vocals human; AI-assisted drum/pad ideation; no impersonations."
  },{
    "@type": "PropertyValue",
    "name": "Checksum_SHA256_MP3",
    "value": "…paste hash…"
  }]
}
</script>
```
(Uses **schema.org/MusicRecording** with `isrcCode`; extra details go into `additionalProperty` when there’s no native property.)

---
