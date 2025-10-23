= AI-assisted Audio Distribution Guideline

The below doc contains strategy (long-term) proposals and cut-n-paste instructions to make your AI-assisted audio (AiAA) future-proof, as DDEX proposals on labeling AI-assisted media can help to avoid adverse effects on your AI-assisted audio distributed over streaming or similar services.

== 1. Reference media strategy

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

== 2. Pre-publication processing (loudness, denoise, QA)

**Targets that travel well:** For mainstream DSPs, **−14 LUFS integrated** with **≤ −1.0 dBTP** (true-peak ceiling) works safely. Platforms differ, but this is the common “does no harm” zone. EBU R128/BS.1770 are the underlying standards. 

**Your scripts (fast path):**
- Use your `loudnorm-two-pass.sh` with **two-pass** `loudnorm` (feeds measured values into pass 2). If verify shows LUFS off by ~x LU, re-run with `I = I + target_offset`; if TP ends ≪ −1 dB, optionally relax to **−0.8 dBTP**. This is standard FFmpeg two-pass practice. 
- For batch jobs, **ffmpeg-normalize** wraps the same two-pass method. 

**Why TP may be “much lower” than your ceiling:** `loudnorm` treats **TP as a ceiling**, not a target; it won’t raise peaks to “hit” −1.0 dBTP. Trust the verify pass; it’s normal to end up at −14 LUFS with TP lower than −1 dB when limiting isn’t needed. 

**Optional polish:**
- **Denoise** (light) *before* loudness (e.g., `afftdn`), then two-pass normalize.  
- Re-measure LUFS/LRA/TP and **embed** numbers + hashes in your sidecar and page.

---

== 3. AI disclosure and provenance

**Where the ecosystem is going (and what you can do now):**
- **Spotify (Sept 25, 2025)** announced AI protections (impersonation, spam filtering) and said it’s **supporting DDEX-based AI disclosures** in credits—e.g., noting which parts used AI (vocals, composition, production, mixing/mastering). Multiple outlets reported ~75M spam removals and the new disclosure push. 
- **YouTube** requires creators to **disclose “altered or synthetic media”**; labels are shown to viewers (especially on sensitive topics). For music uploads, put a plain-English disclosure in the description, too. 
- **DDEX**: today’s working specs (ERN/RIN/MEAD/etc.) already carry rich credits/technical metadata; DDEX has active working/ad-hoc groups evolving the standards. Use your sidecar as a **bridge** until ingest pipelines widely accept AI fields. 
- **C2PA Content Credentials**: if/when audio tools support it, C2PA lets you **cryptographically bind provenance** assertions to assets (or via an external manifest). Track-art already benefits; audio support is emerging. Keep an eye on this and be ready to attach manifests to cover art and (when feasible) audio. 

**What to publish now:**
- Your **plain-English AI disclosure** (e.g., “Human lyrics; AI-assisted vocals derived from my voice; AI-assisted instrumentals; no impersonations”), plus **checksums**, **audio stream hash**, **S3 VersionID**, **IPFS CID** (if any), **opus number**, and **absolute provenance URL** in **JSON-LD** (`MusicRecording`) as you’ve done. This aligns with current platform transparency pushes and is future-proof for DDEX/C2PA ingestion. 

---

== 4. Post-publication & "stay safe" guidance for AIAA

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

== Appendix A. Step by step guide

IN PROGRESS
