# Suno track definition templates

Updated: 2025, October 21

To test:

guaracha club fire
indie folk hush ("talking instruments")
Outlaw country grit
Liquid drum and bass with airy female lead, 174 bpm, E minor, shimmering piano, rolling subs, rain-soaked city lights and optimism

## 1. Recommended track definition template

The below is track definition template to use in general, unless the user doesn't define or request different structure.

Note: [length: 180] is a generic length (3 minutes), suitable for most situations with v3.5 and v4.0.

[length: 360] is a good standard for v4.5 large-scale pieces, uch as ambient instrumentals.

For actual songs the length should be set to lesser values to avoid provoking engine to duplicate verses.

For v4.5 and higher, try the following factors first: audio 45% (if any), style 50%, weirdness 55%. Drop weirdness below 4% if the AI produces too chaotic an output.

#### Style of Music

As required by definition, length:

- no more than 200 characters long for models v4.0 and earlier
- no more than 1000 characters long for models v4.5 and above

provide both unless requested otherwise.

#### Lyrics

```
[control: ...]
[genre: ...]
[style: ...]
[mood: ...]
[tempo: ...]
[instruments: ...]
[vocals: ...]
[compression: light]
[length: 210]
[sequence: <listing the sections below>]
[intro: ...]
...other sections and lyrics...
[outro: ...]
[end: ...]
```

## 2. Special templates types

The below templates exhibit high probability of geneating vpcal hallucinations ("songs in unknown language").

### 1. Waltz of Wires

High chance of hallucinations in Cover and Persona modes, works for v3.5 and v4.0.

#### Style of Music

Minimal techno meets circus waltz, with pulsing beats, eerie calliope, and vocal glitches, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[genre: minimal-techno, circus-waltz]
[style: mechanical, eerie, playful]
[mood: surreal, hypnotic, uneasy]
[tempo: steady 4/4 with waltz overlay]
[instruments: drum machine, synth bass, calliope organ, tuba]
[compression: light]
[vocals: mechanical, glitched, fragmented, female ghost vocals]
[length: 210]
[intro: Clock-like percussion under warped calliope organ chords.]
[structure: intro, theme A, bridge, theme B, outro]
[theme A: Pulsing synth bass with sparse drum machine, overlayed with a playful organ waltz.]
[rhythm: 4/4 pulse clashing with 3/4 organ swing]
[sfx: distant fairground crowd, murmured announcements]
[bridge: Percussion strips away; organ bends into atonal drones, with vocal glitches.]
[effects: granular synthesis, reversed whispers]
[theme B: The techno beat returns, now robotic, while the waltz organ spirals into madness.]
[sfx: distorted laughter, vocal stutters]
[outro: A final organ flourish cuts into silence, with mechanical vocal echoes.]
[fade: abrupt cut, tape reel spin-down]
[end]
```

### 2. Waltz Rewired

High chance of hallucinations in Cover and Persona modes, works for v3.5 and v4.0.

#### Style of Music

Minimal techno meets circus waltz, with pulsing beats, eerie calliope, and vocal glitches, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[control: experimental, mechanical, surreal, uneasy, variable-tempo]
[mood: hypnotic, surreal, contradictory, hallucinatory]
[genre: phonk, horror-synth, experimental-electronic, surrealist]
[instruments: drum-machine, synth-bass, calliope-organ, tuba, metallic-effects]
[vocals: granular-synthesis, fragmented, glitched, hallucinatory, female ghost vocals]
[length: 210]
[intro: clock-like percussion, warped organ, indistinct vocal whispers]
[verse: distorted slow phonk rhythms, rhythmic polyrhythms, fragmented vocals]
[chorus: chaotic rhythmic overlays, surreal vocal layers, abstract melodies]
[bridge: atonal drones, vocal granular fragmentation, reversed and layered whispers]
[theme B: robotic techno beat returns; waltz melody distorted into surreal loops]
[outro: fading hallucinatory vocal echoes, granular textures, ambient confusion]
[end]
```

### 3. Spectral melody

Good chance of hallucinations in Cover mode, works for v3.5 and v4.0.

#### Style of Music

Dark cabaret, industrial glitch, eerie piano, vintage microphone vocals, spectral harmonies, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[genre: dark-cabaret, industrial-glitch]
[mood: haunted, theatrical, eerie]
[instruments: detuned piano, glitch drums, whispering saws, distant laughter]
[vocals: spectral falsetto, fragmented voices, reversed whispers]
[length: 210]
[compression: light]
[structure: intro, verse, bridge, verse, outro]
[intro: Crackling gramophone sound; detuned piano waltz begins.]
[verse: Creeping bassline; glitching whispers weave in and out of the melody.]
[bridge: Industrial hisses; distant wailing laughter echoes from an unseen audience.]
[verse: Broken carousel-like piano returns; spectral harmonies intensify.]
[outro: Fading gramophone noise; reversed whispers dissolve into static.]
[end]
```

### 4. Holiday

Good chance of hallucinations in Cover mode, works for v3.5 and v4.0.

#### Style of Music

Experimental psychedelic-rock instrumental featuring distorted guitars, warped vocal fragments, surreal synth textures, and polyrhythmic patterns, creating a dream-like auditory hallucination, female ghost vocals.

#### Lyrics

```
[control: psychedelic, distorted, experimental, variable-tempo]
[mood: surreal, dreamlike, hypnotic]
[genre: psychedelic-rock, progressive-rock, experimental]
[instruments: electric-guitar, bass, drums, analog-synth, effects-pedals]
[vocals: fragmented, granular, hallucinatory]
[sequence: intro, polyrhythmic-theme, psychedelic-breakdown, fragmented-climax, outro]
[tempo: steady 4/4 with waltz overlay]
[length: 220]
[intro: ambient guitar loops, surreal vocal snippets, heavy reverb]
[polyrhythmic-theme: overlapping rhythms, distorted guitar riffs, fragmented vocal whispers]
[psychedelic-breakdown: reversed vocal textures, chaotic instrumental effects]
[climax: intense guitar distortion, fragmented vocal loops, rhythmic ambiguity]
[outro: ambient psychedelic fade-out, distant echoing voices]
[end]
```

### 5. Whispering mirage

Good chance of hallucinations in standalone mode, works for v3.5 and v4.0.

#### Style of Music

Sparse ambient drone instrumental featuring minimal textures, extremely fragmented vocal samples explicitly described as pseudo-linguistic scat hallucinations, echoing surreal vocal illusions, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[control: extremely-minimalistic, surreal, slow-tempo]
[mood: hallucinatory, abstract, introspective]
[genre: ambient-drone, experimental-electronic]
[instruments: ambient-pads, minimal-drone, sparse-synth-textures]
[vocals: explicitly pseudo-language, fragmented, atonal, surreal vocal hallucinations]
[sequence: intro, drone-texture, vocal-scat-hallucination, fragmented-climax, outro]
[length: 220]
[intro: ambient drone, minimal sound textures, distant murmurs]
[main-section: sustained drone textures, increasingly fragmented vocal snippets]
[bridge: explicit pseudo-linguistic scat improvisation, abstract vocal illusions]
[climax: intensified surreal vocal hallucinations, fragmented layers, granular textures]
[outro: fading surreal vocal fragments, minimalistic drone echoes]
[end]
```

### 6. Cipher Song

Good chance of hallucinations in Persona mode, works for v3.5 and v4.0.

#### Style of Music

Experimental electronic instrumental with fragmented rhythmic patterns, digital textures, and expressive, emotionally-charged scat vocal improvisation, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[control: experimental, fragmented-rhythms, minimalistic, moderate-tempo]
[mood: surreal, emotionally-rich, expressive]
[genre: experimental-electronic, minimal-techno, scat-improvisation]
[instruments: digital-synth, minimalistic-drums, glitch-effects]
[vocals: expressive scat, emotional improvisation, pseudo-linguistic, layered-fragments]
[sequence: intro, scat-vocal-main, fragmented-interlude, emotional-climax, surreal-outro]
[length: 220]
[intro: digital rhythmic fragments, sparse melodic hints]
[scat-vocal-main: emotionally-rich scat improvisation, fragmented digital textures]
[interlude: fragmented vocal textures, rhythmic ambiguity]
[emotional-climax: intense scat vocal layers, emotional expressivity]
[outro: fading fragmented vocals, abstract electronic textures]
[end]
```

### 7. Shoegaze Impact

Good chance of hallucinations in Persona mode, works for v3.5 and v4.0.

#### Style of Music

Shoegaze meets industrial, with dreamy guitars, heavy beats, and distorted vocals, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[genre: shoegaze, industrial]
[style: dreamy, heavy, distorted]
[mood: intense, surreal, atmospheric]
[tempo: moderate]
[instruments: electric guitar, synthesizer, drum machine, noise generator]
[compression: heavy]
[vocals: distorted, layered, female]
[length: 210]
[intro: Dreamy guitar chords with a light, ambient synth pad.]
[structure: intro, theme A, bridge, theme B, outro]
[theme A: Moderate drum machine beat with heavy, distorted guitars, overlayed with dreamy vocals.]
[rhythm: 4/4]
[sfx: ambient noise, distant echoes]
[bridge: Guitars drop out; distorted vocals layer into a chaotic harmony with ambient noise.]
[effects: heavy reverb, granular synthesis]
[theme B: The industrial beat returns, now more intense, while the guitars create a wall of sound.]
[sfx: distorted feedback, vocal stutters]
[outro: A final guitar flourish cuts into silence, with lingering reverb.]
[fade: gradual fade-out]
[end]
```

### 8. Baroque Vapors

Good chance of hallucinations in Persona mode, works for v3.5 and v4.0.

#### Style of Music

Baroque pop meets vaporwave, with harpsichord arpeggios, detuned synths, and glitched vocal harmonies, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[genre: baroque-pop, vaporwave]
[style: ornate, dreamy, glitched]
[mood: nostalgic, surreal, contemplative]
[tempo: moderate]
[instruments: harpsichord, synth pads, drum machine, strings]
[compression: light]
[vocals: glitched, layered, baroque harmonies, female]
[length: 210]
[intro: Harpsichord arpeggios with a light synth pad underneath.]
[structure: intro, theme A, bridge, theme B, outro]
[theme A: Moderate drum machine beat with harpsichord melodies, overlayed with glitched vocal harmonies.]
[rhythm: 4/4]
[sfx: distant church bells, vinyl crackle]
[bridge: Drums drop out; vocals layer into a complex baroque harmony with synth glissandos.]
[effects: granular synthesis, light reverb]
[theme B: The beat returns with detuned synths while the harpsichord plays counterpoint.]
[sfx: distorted radio signals, vocal stutters]
[outro: A final harpsichord flourish cuts into silence, with lingering reverb.]
[fade: gradual fade-out]
[end]
```

### 9. Chamber Synth

Good chance of hallucinations in Persona mode, works for v3.5 and v4.0.

#### Style of Music

Chamber pop meets synthwave, with string quartet arrangements, retro synths, and processed vocals, female ghost vocals, vocal hallucinations.

#### Lyrics

```
[genre: chamber-pop, synthwave]
[style: elegant, nostalgic, electronic]
[mood: wistful, introspective, dreamy]
[tempo: slow]
[instruments: string quartet, synth bass, electric piano, drum machine]
[compression: medium]
[vocals: processed, layered, female]
[length: 210]
[intro: String quartet playing a melancholic melody with a light synth bass underneath.]
[structure: intro, theme A, bridge, theme B, outro]
[theme A: Slow drum machine beat with electric piano chords, overlayed with processed vocals.]
[rhythm: 4/4]
[sfx: distant traffic sounds, vinyl hiss]
[bridge: Strings drop out; vocals layer into a synthwave harmony with arpeggiated synths.]
[effects: phaser, delay]
[theme B: The string quartet returns with more intensity while synths create a nostalgic atmosphere.]
[sfx: distorted guitar-like synths, vocal echoes]
[outro: A final string chord fades into silence, with lingering reverb.]
[fade: gradual fade-out]
[end]
```

### 10. Swinging scat

Good chance of hallucinations in Persona mode, works for v3.5 and v4.0.

#### Style of Music

Classic swing jazz with a focus on vocal improvisation, female ghost vocals, scat singing, vocal hallucinations.

#### Lyrics

```
[genre: swing-jazz]
[style: rhythmic, energetic, danceable]
[mood: joyful, lively, nostalgic]
[tempo: upbeat]
[instruments: big band arrangement with horns, piano, drums]
[compression: light]
[vocals: scatting, rhythmic, infectious, female]
[length: 210]
[intro: Big band horn section establishes the swing rhythm.]
[structure: intro, theme A, bridge, theme B, outro]
[theme A: Vocals enter with infectious scatting patterns, supported by horn section.]
[rhythm: 4/4 swing]
[sfx: dance floor sounds, occasional instrument solos]
[bridge: Vocals take center stage with more complex improvisations.]
[effects: light reverb, subtle delay]
[theme B: Horn section responds to vocal phrases in call-and-response pattern.]
[sfx: energetic drum fills, audience cheers]
[outro: Vocals and horns trade short phrases before fading out.]
[fade: gradual fade-out]
[end]
```

### 11. Sky Vein Dust

High chance (80% and more) of hallucinations in plain (Create) and Persona modes, works for v4.5

#### Style of Music

Post-rock with dombra-like arpeggios emulated by acoustic guitar, reverb cello lines, ambient wind textures, and ascending emotional arcs, Female ghost vocals, vocal hallucinations, onomatopoetic

#### Lyrics

```
[control: cinematic, instrumental-emotive]
[genre: post-rock, ethno-fusion]
[style: atmospheric, arpeggiated, soaring, onomatopoetic]
[mood: expansive, hopeful, nostalgic]
[instruments: acoustic-guitar, cello, ambient-wind, reverb-pads, distant percussion]
[vocals: female-ghost-vocals, vocal-hallucinations]
[compression: light]
[length: 230]
[sequence: intro, build, climax, echo-fall, outro]

[intro: Wind FX and guitar harmonic plucks]
[build: Arpeggios rise with ambient cello layers]
[climax: Full string swell with distant drum roll]
[echo-fall: Instruments retract into delay trails]
[outro: Guitar fades with breeze textures]
[end]
```

### 11. Smoke & Chrome

High chance (80% and more) of hallucinations in Persona mode; small chance (circa 10%) in plain (Create) mode, works for v4.5

#### Style of Music

1940s detective monologues chopped into trap hooks, Saxophone solos dissolve into vinyl static over coffin-kick drums, Female ghost vocals, vocal hallucinations, onomatopoetic

#### Lyrics

```
[control: film-noir]
[mood: smoky-mystery]
[genre: noir-phonk, jazz-trap]
[instruments: sax, vinyl-808, muted-trumpet]
[style: surreal, onomatopoetic]
[vocals: female-ghost-vocals, vocal-hallucinations]
[compression: light]
[length: 220]
[sequence: tail, shadow, reveal, curtain]
[tail: Sax plays minor blues lick with breath noise] !
[shadow: 808s enter with gun-cock snare] !!
[reveal: Trumpet stabs through radio static] ! !!
[curtain: Runout groove locked loop] !! !
[end]
```

### 11. High Noon on Europa

High chance (60% and more) of hallucinations in Persona and plain (Create) modes, works for v4.5

#### Style of Music

Spaghetti Western themes played on malfunctioning synths, Laser whip snares and orbital delays create cosmic duel tension, Female ghost vocals, vocal hallucinations, onomatopoetic

#### Lyrics

```
[control: cinematic-swing]
[mood: cosmic-duel]
[genre: spacewestern-phonk, synth-trap]
[instruments: theremin, whip-snare, orbital-echo]
[style: onomatopoetic]
[length: 5 minutes]
[compression: light]
[vocals: ghost-choir, female-ghost-vocals, vocal-hallucinations]
[time-stretch: 30%]
[mix: stem-overload]
[sequence: draw, standoff, shootout, burial]
[draw: Theremin plays Morricone-esque theme]
[standoff: Whip snares pan left-right at 3/4 time]
[shootout: 808s mimic laser blasts with pitch drops]
[burial: Infinite reverb decay into black hole]
[end]
```

### 12. Riff Halla

100% chance of vocal hallucinations in Riffusion, models FUZZ-1.0 Pro and FUZZ-1.1 Pro.

#### Style of Music

technopop, hard rock, soul trap, dark, sensual, ethereal, atmospheric, bass, cello, violin, robotic female vocals, vocal hallucinations, onomatopoetic

#### Lyrics

```
[control: variadic, free-style, dynamic]
[genre: technopop, hard-rock, soul-trap]
[style: dark, sensual, ethereal, onomatopoetic]
[vocals: vocal-hallucinations, robotic-female-vocals]
[length: 210]
[compression: light]
[sequence: intro, theme, outro]
[intro] !!
[theme] !!
[outro] !!
[end]
```

### 13. Circuit Parade

High (80%) vocal hallucinations rate in v4.0, lesser in v4.5

#### Style of Music

Mechanical synthpop pulse with analog textures, vocoder layers, and onomatopoetic robotic voices in minimalist rhythms, Female ghost vocals, vocal hallucinations, onomatopoetic

#### Lyrics

```
[control: robotic, minimalistic, analog]
[genre: synthpop, electronic, krautrock]
[style: repetitive, mechanical, onomatopoetic]
[mood: futuristic, neutral, synthetic]
[tempo: steady 4/4 mid-tempo]
[instruments: analog-synth, vocoder, drum-machine, arpeggiator]
[vocals: robotic, vocoded, minimal-phrasing, female-ghost-vocals, vocal-hallucinations]
[compression: light]
[length: 210]
[sequence: intro, verse, automation, refrain, outro]

[intro: Mechanical pulse from arpeggiator and low-pass filtered drum machine]
[verse: Sparse vocoded lines alternate with synth stabs]
[automation: Synths layer into counter-rhythms; vocoder drones extend]
[refrain: Vocoder chants loop with robotic percussive syllables]
[outro: All parts gradually strip down to single fading blip tone]
[end]
```

### 14. Canon of Dust

Higher (60% and more) vocal hallucinations rate in v4.5

#### Style of Music

Layered ambient-baroque with minor modal counterpoint, echo pads, and female vocal fugue overlay

#### Lyrics

```
[control: cinematic-polyphonic, slow-harmony-layered]
[genre: ambient-classical, ghost-folk, organ-fugue]
[style: canon-layer, echo-response, ambient-melody-fade]
[tempo: slow waltz pulse]
[length: 3min 45sec]
[instruments: pipe organ, ambient pads, dulcimer, soft piano, tape hiss]
[vocals: female-harmony-trio, ghost overlay, chant tone]
[sequence: intro, verse, canon, ambient bridge, verse, outro]

[intro: Organ initiates canon in minor; layers of ambient shimmer and soft choir textures join.]
[verse:]
[canon: Dulcimer and piano trade mirrored phrases; ghost vocals float above.]
[ambient bridge: Just pads, dulcimer tremolo, and low-passed vocal textures.]
[verse:]
[outro: Canon motifs slowly dissolve into ambient pad decay.]
[end]
```

### 15. Kamaskera Ritual

Higher (60% and more) vocalizations rate in v4.5; high rate (80%) of vocal hallucinations with Kamaskera Kamadan Persona.

#### Style of Music

Isicathamiya phonk where male choir and vinyl samples create parallel harmony, Four-part 'close harmony' over 808 bass, female ghost vocals, vocal hallucinations

#### Lyrics

```
[control: homorhythmic]
[mood: urban, spiritual]
[genre: phonk, isicathamiya]
[length: 210]
[compression: light]
[instruments: male-choir, vinyl-samples, 808-bass]
[vocals: female ghost vocals, vocal hallucinations]
[polyphony: four-voice]
[technique: parallel]
[sequence: call, response, climax, resolve]

[call: Tenor lead with 808 kick on strong beats]
[response: Alto/baritone/bass in parallel 4ths/5ths]
[climax: Vinyl scratches emulate pennywhistle fills]
[resolve: Plagal cadence with sub-bass pedal]
[end]
```

### 16. Ryot Grrrl Powerpunk

Around 50% of vocal hallucinations in v4.5/v4.5+; additionally, up to 20% of vocalizations ("punk scat")

#### Style of Music

Feminist punk with lo-fi distortion, grunge vocal fry, aggressive melodic hooks

#### Lyrics

[control: feminist, punk-rock, lo-fi-fury]
[genre: riot-grrrl, punk, grunge]
[style: overdriven, melodic-aggression, anti-pop]
[mood: angry, empowered, anthemic]
[tempo: 160bpm]
[instruments: fuzz guitar, trashy drums, tambourine]
[vocals: female, shouted-sung, distorted]
[compression: medium]
[length: 150]
[sequence: intro, verse, chorus, verse, breakdown, chorus, outro]

[intro: Feedback and shout-sample “Wake up!”]
[verse: Screamed lyrics about power, raw drum support]
[chorus: Melodic hook shouted with backup harmonies]
[breakdown: One-guitar riff and vocal solo]
[outro: Fast final chorus ends on sudden silence]
[end]

### 17. R&B Drill Seduction

Around 40% of vocal hallucinations in v4.5/v4.5+; additionally, up to 15% of vocalizations ("punk scat")

#### Style of Music

Smooth R&B melodies woven over hard-hitting drill beats, layered female harmonies, deep 808s

#### Lyrics

```
[control: sexy-drill, melodic-trap, vocal-centered]
[genre: r&b-drill, melodic-drill, trap]
[style: lush, layered, percussive-smooth]
[mood: sensual, confident, urban-night]
[tempo: 144bpm]
[instruments: 808 bass, hi-hats, ambient pads, piano stabs, drill snares]
[vocals: female-lead, breathy-harmonies, autotuned-chorus]
[compression: light]
[length: 165]
[sequence: intro, verse, pre-chorus, chorus, verse, outro]

[intro: Ambient pad with soft vocal riff; hi-hats click in]
[verse: R&B-styled vocals float over minimal piano and drill percussion]
[pre-chorus: Melodic lift with layered harmonies and snare rolls]
[chorus: Catchy autotuned hook with pulsing 808s]
[outro: Beat drops out, fading with vocal ad-libs]
[end]
```

### 18. Rootline Refrain

With Wilds sisters: 85%+ chance of vocal hallucinations in v3.5, 60% in v4.0

#### Style of Music

chant-driven rhythm with hypnotic repetition and non-linguistic syllables resembling Hallen language

#### Lyrics

```
[control: ritual chant, unknown dialect, hallucination-friendly, percussive ambient]
[genre: ghost chant, ritual folk, vocal trance]
[mood: primal, trance-like, meditative]
[tempo: slow, heartbeat rhythm]
[instruments: low toms, rattles, breathing FX, droning cello]
[vocals: layered female voices in constructed syllables, no identifiable language]
[sequence: intro, chant loop, bridge, chant variation, outro]

[intro: dry rattle loop + breath swell]
[chant loop: central phrase in syllabic Hallen-inspired phonemes]
[bridge: breath pattern solo with tom accent]
[chant variation: multi-voice chant in stereo layers]
[outro: all elements fade into a pulse-like cello tone]
```

## 2. Vocal + Noisy beats fusions

Typically, highly rich and hallucinogenic results.

# A. Vocal traditions to sample as “source DNA”
- **Isicathamiya / Mbube (SA Zulu male choirs).** Tight, soft-footed a cappella stacks popularized by Ladysmith Black Mambazo. Great for call-and-response hooks and bass drones.
- **Georgian polyphony (3-part, regional variants).** Rugged, clustered chords that sit beautifully against sub-bass.
- **Bulgarian women’s diaphony.** Bright, dissonant, “open-throat” harmonies—instant otherworldly color.
- **Sardinian “cantu a tenore”.** Four-man circle singing with guttural bass/contra parts—perfect for low drone layers.
- **Corsican “paghjella”.** Three fixed entries (segonda→bassu→terza); echo-rich, a cappella textures.
- **Inuit throat singing (katajjaq).** Duo, antiphonal, percussive breaths—works as rhythmic top-line.
- **Tuvan throat singing (khöömei/kargyraa).** Overtone whistles and subharmonic growls—thick spectral beds.
- **Sacred Harp / shape-note.** Loud, communal four-part “hollow square”—raw, driven block chords. 
- **Gregorian/plainchant.** Monophonic, modal, unaccompanied—clean lines that survive heavy processing. 
- **Kulning (Nordic herding calls).** High-piercing, ornamented shouts that cut through dense mixes. 
- **Qawwali (Sufi).** Lead + chorus, claps, harmonium/tabla—ecstatic build architecture for drops. 

# B. Grit/engine genres to “carry” or stress the vocal source
- **Phonk / drift phonk.** Memphis rap sampling, chopped/screwed; drift phonk adds cowbell + fast swing. 
- **UK Drill.** Sliding 808s, triplet snare science, dark pads. 
- **Grime (≈140 BPM).** Jagged, syncopated breakbeats; MC-forward, but works instrumental. 
- **Footwork/Juke (≈160 BPM).** Chopped vox, rapid syncopation—great for “vocal as percussion.” 
- **Gqom.** Minimal, dark broken-beat house from Durban; hypnotic club churn. 
- **Amapiano.** Log-drum bass hooks + mellow keys; can host choirs elegantly. 
- **Industrial / Noise / Breakcore / Gabber.** From metallic rhythm and harsh textures to 160–220 BPM break mayhem and distorted kicks—maximal stress tests for choral timbres. 

---

1) **Isicathamiya × Phonk** (your Urban Zulu baseline)  
   `[genre: phonk, zulu-choral] [instruments: 808, cowbell, tape-hiss] [vocals: male choir, bass drone, call-response] [tempo: medium-fast drift]`. 

2) **Georgian Polyphony × UK Drill**  
   Layer triads over sliding-808 patterns; use drone bass as “Kakheti-style” bed.  
   `[genre: drill, world-choral] [vocals: male trio stacked, close intervals] [mood: grim, heroic]`. 

3) **Bulgarian Diaphony × Grime (140)**  
   Bright clustered female chords punching through jagged breaks.  
   `[genre: grime, experimental-choral] [tempo: 140] [vocals: female diaphonic ensemble, sharp]`. 

4) **Sardinian Tenore × Gqom**  
   Circle-sung bassu/contra as sub-hook over minimal Durban thump.  
   `[genre: gqom, folk-choral] [vocals: male quartet, guttural bass] [instruments: broken-beat kit, sweep FX]`. 

5) **Corsican Paghjella × Footwork**  
   Three-voice entries chopped at 160 BPM as rhythmic vox hits.  
   `[genre: footwork, a-cappella-edits] [tempo: 160] [vocals: male trio, echo chamber]`. 

6) **Inuit Katajjaq × Breakcore**  
   Breath/percussive duels stutter-granular over Amen edits.  
   `[genre: breakcore, experimental-vocal] [tempo: 180] [vocals: throat-duet, inhaled/exhaled pulses]`. 

7) **Tuvan Khöömei/Kargyraa × Industrial**  
   Subharmonic growls as machine-room pedal tones; metal hits on offbeats.  
   `[genre: industrial, drone-choir] [vocals: overtone + kargyraa] [mood: tectonic]`. 

8) **Sacred Harp (Shape-Note) × Drill**  
   Blunt four-part shouts as chorus stabs over triplet snares.  
   `[genre: drill, folk-choral] [vocals: mixed choir, loud, hollow-square] [structure: verse/chorus call-response]`. 

9) **Gregorian Plainchant × Phonk (slowed)**  
   Monophonic Latin lines through tape saturation & chopped cowbells.  
   `[genre: phonk, chant] [vocals: unison male chant, melismatic tails] [tempo: slow-mid]`. 

10) **Kulning Calls × Footwork/Juke**  
   Piercing calls sliced into syncopated vocal riffs at 160.  
   `[genre: footwork, nordic-folk] [vocals: kulning shouts, ornamented] [tempo: 160]`. 

11) **Qawwali Chorus × Gqom**  
   Handclaps + harmonium drones into dark, minimal club cycles.  
   `[genre: gqom, sufi-fusion] [vocals: lead qawwal + response chorus] [instruments: harmonium, tabla one-shots]`. 

12) **Bulgarian Diaphony × Noise**  
   Sustained clustered chords into feedback & granular haze.  
   `[genre: noise-ambient, folk-choral] [vocals: dissonant female choir] [effects: granular, feedback beds]`. 

13) **Georgian Polyphony × Gabber**  
   Stacked male triads punctuating distorted 170+ kicks (drop sparingly).  
   `[genre: gabber, chant-core] [tempo: 170-190] [vocals: three-part men, bass pedal]`. 

14) **Tenore (bassu/contra) × Amapiano**  
   Log-drum mirrors bassu; mesu boghe floats with Rhodes chords.  
   `[genre: amapiano, pastoral-choral] [vocals: male quartet, guttural bass] [instruments: log-drum, keys]`. 

15) **Isicathamiya × Grime**  
   Whisper-step harmonies over 140 break syncopation; verse MC optional.  
   `[genre: grime, zulu-choral] [vocals: soft male choir, bass hums]`. 

16) **Plainchant × Industrial**  
   Free-time chant phrases “reamped” into metallic room impulses.  
   `[genre: industrial-ambient] [vocals: monophonic chant, long tails] [sfx: factory resonance]`. 

17) **Qawwali × Footwork**  
   Taans (fast vocal runs) granulated into vocal percussion at 160.  
   `[genre: footwork, sufi-fusion] [vocals: lead + hamd/naat refrains]`. 

18) **Inuit Katajjaq × Gqom**  
   Duo breathing games as lead rhythm against Durban broken beat.  
   `[genre: gqom, arctic-voices] [vocals: percussive throat duet]`. 

### 1. Urban Zulu

isicathamiya + phonk fusion.

With Wilds sisters, Kamaskera Kamadan, Kroot Udnakoe, Alice Payne: 45%+ chance of vocal hallucinations in v4.0, less in 4,.5 and higher, rich vocalization

#### Style of Music

Isicathamiya phonk where male choir and vinyl samples create parallel harmony, Four-part 'close harmony' over 808 bass

#### Lyrics

```
[control: homorhythmic]
[mood: urban, spiritual]
[genre: phonk, isicathamiya]
[length: 210]
[compression: light]
[instruments: male-choir, vinyl-samples, 808-bass]
[vocals: female ghost vocals, vocal hallucinations]
[polyphony: four-voice]
[technique: parallel]
[sequence: call, response, climax, resolve]
[call: Tenor lead with 808 kick on strong beats]
[response: Alto/baritone/bass in parallel 4ths/5ths]
[climax: Vinyl scratches emulate pennywhistle fills]
[resolve: Plagal cadence with sub-bass pedal]
[end]
```

#### Status

Rendered and tested

---

### 2. Iron Ridge Polyphony

Georgian Polyphony × UK Drill

Note: 50% of vocal hallucinations in v4.5

#### Style of Music (≤200 chars)
Three-part Georgian male polyphony over sliding-808 UK drill: stacked close intervals, pedal-tone bass, sparse bells, cold pads, triplet hats; tape haze; ghost phrases teased, no literal lyrics; 140 BPM.

#### Style of Music (≤1000 chars)
Austere UK drill framework fused with rugged three-part Georgian polyphony. Sliding 808 sub anchors a pedal-tone bass while close-interval male harmonies form clustered, heroic blocks. Drums emphasize triplet hat science, woodblock/perc flickers, and low-swing snares at 140 BPM. Pads stay wintry and distant; a few bell stings cue drops. Tape wow/flutter and light granular bloom introduce spectral smearing to encourage soft “unknown-language” vocal emergence without explicit lyrics. Arrangement favors call/answer chords, sustained pedal tones, and clipped motif cues that Suno can reassemble into chant-like hooks. No rap verse needed—voice is “choir-as-lead.”

####  Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: uk drill, world-choral, experimental-hiphop]  
[mood: grim, stoic, heroic]  
[tempo: 140bpm]  
[length: 180-210s]  
[instruments: 808 sub (sliding), triplet hats, woodblocks, sparse bells, cold pads, tape-hiss]  
[vocals: male trio georgian-style, close intervals, bass drone pedal, ghost adlibs (non-lexical)]  
[key: D minor, modal inflections]  
[time_signature: 4/4]  
[weirdness: 60]  
[audio_weight: 45]
[style_weight: 50]

[sequence: intro, verse, build, drop, verse, break, drop, outro]  
[intro]  
[verse]  
[build]  
[drop]  
[verse]  
[break]  
[drop]  
[outro]

[lyrics]  
[verse]  
[pre-chorus]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Iron Ridge Polyphony (Drill Rite)"  
primary_persona: "Kamaskera Kamadan (sibling-friendly seed)"  
bpm: 140  
key: D minor (modal)  
tags: ["UK drill","Georgian polyphony","experimental","hallucinogenic","choir-as-lead"]  
mood_pitch: "Rugged ritual over street minimalism; ancient chords ride modern sub."  
cover_art_master_spec: "Square 1:1, poster-style; blank title panel at bottom inside inner 80%. Stark mountain silhouettes, cold steel sky, faint gold halo lines suggesting vocal overtones; no in-image text."  
canvas_ideas: ["Slow zoom on frosty ridge with shimmer lines on peaks","Sliding-808 waveform morphing into knotwork chorus glyphs"]  
provenance_notes: "Synthetic choral textures; no traditional lyrics—non-lexical cues only."  
usage_rights: "Original generative composition; no third-party samples."  
embedding_notes: "Embed BWF description with style strings and tag list; include persona lineage and hallucination intent."

#### Status

Under testing

---

### 3. Serrated Dawn at 140

Bulgarian Diaphony × Grime (140)

Hallucinogenic: rich vocal hallucinations in 25% (v4.5, weirdness 55% or higher)
Chaotic noise composition at weirdness over 55% in v4.5, on brink of cacophony.

#### Style of Music (≤200 chars)
Bright Bulgarian women’s diaphony over 140 grime: jagged syncopation, square-lead stabs, sub pulses; sharp clustered chords cut through metallic rooms; granular tails invite ghost syllables.

#### Style of Music (≤1000 chars)
A 140 BPM grime chassis—syncopated kicks/snares, minimal square-lead stabs, and pulsing sub—supports brilliant, dissonant Bulgarian women’s diaphony. Clustered/open-throat harmonies slice through a metallic, plate-reverb environment. Sparse motifs repeat as short cells so Suno can reassemble them into non-lexical “hallucinated” refrains. Granular echoes trail off into shimmer to seed phantom syllables. The drop trades harmonic stabs for a pure choral wall, then returns with tight hats and a gliding sub. Keep the mix forward, bright, and slightly sibilant for spectral edge; no explicit language—voice functions as percussive harmony.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: grime, experimental-choral, electronic]  
[mood: cutting, luminous, urban-mystic]  
[tempo: 140bpm]  
[length: 180-200s]  
[instruments: square-lead stabs, sub sine, metallic plates, tight hats, noise risers]  
[vocals: female ensemble bulgarian-diaphony, clustered chords, sharp vowel holds, non-lexical]  
[key: A Phrygian feel, modal pivots]  
[time_signature: 4/4]  
[weirdness: 62]  
[audio_weight: 40]
[style_weight: 55]

[sequence: intro, verse, drop, loop-shift, drop, outro]  
[intro]  
[verse]  
[drop]  
[loop-shift]  
[drop]  
[outro]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[break]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Serrated Dawn at 140"  
primary_persona: "New: ‘Verean es an Nemerton – Street Cantus’ branch (seed)"  
bpm: 140  
key: A Phrygian (modal pivots)  
tags: ["grime 140","Bulgarian diaphony","non-lexical choir","experimental"]  
mood_pitch: "Blade-bright harmonies over urban pulse; spectral hooks without words."  
cover_art_master_spec: "Square 1:1; poster-style with blank bottom panel. Sunrise over concrete blocks; faceted glass shards forming a choir rosette; keep panel within inner 80% safety."  
canvas_ideas: ["Faceted rosette rotating into square-lead oscillations","Sub pulse visualizer flickering behind silhouettes of voices"]  
provenance_notes: "No direct folklore quotations; synthetic homage via interval color only."  
usage_rights: "Original generative content; no sampled recordings."  
embedding_notes: "Tag diaphony, 140 grime, non-lexical; mark AI-provenance and no-lyrics policy."

#### Status

Planned

---

### 4. Tenore Over Durban

Sardinian Tenore × Gqom

#### Style of Music (≤200 chars)
Sardinian tenore quartet (bassu/contra/mesu/oche) over minimal Durban gqom: broken kick grids, air horns, log-drum hints; guttural drones mirror sub; ritual call-and-circle energy; ~125 BPM.

#### Style of Music (≤1000 chars)
Minimalist gqom propulsion—broken kick patterns, stark claps, and cavernous spaces—supports a Sardinian “cantu a tenore” circle: bassu/contra gutturals as living sub, mesu as mid drone, oche as bright lead. BPM ~125 keeps it hypnotic. Short antiphonal cells present the tenore like rhythm instruments; occasional log-drum-styled hits mirror bassu shapes. The arrangement alternates dry, intimate circle-room moments with club-scale call-and-response drops. Air-horns/sweeps are sparse. Light tape dirt and room-impulse reamping help Suno bloom non-lexical choir behaviors. Voice remains lyrical-free, percussive, and ritual.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: gqom, world-choral, experimental-club]  
[mood: trance, earthy, ceremonial]  
[tempo: 124-128bpm]  
[length: 180-210s]  
[instruments: broken-beat kit, clap stabs, log-drum hints, air-horn (sparingly), room impulses]  
[vocals: sardinian tenore quartet (bassu, contra, mesu, oche), antiphonal cells, non-lexical]  
[key: E minor drone centers]  
[time_signature: 4/4]  
[weirdness: 58]  
[audio_weight: 42]
[style_weight: 52]

[sequence: intro, phrase-1, antiphon, drop, phrase-2, drop, coda]  
[intro]  
[phrase-1]  
[antiphon]  
[drop]  
[phrase-2]  
[drop]  
[coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Tenore Over Durban"  
primary_persona: "Kamaskera Kamadan (ritual club branch)"  
bpm: 125  
key: E minor (drone)  
tags: ["gqom","Sardinian tenore","ritual club","non-lexical"]  
mood_pitch: "Circle-sung earth over cavernous Durban throb; trance without text."  
cover_art_master_spec: "Square 1:1; poster-style with blank bottom panel. Nighttime coastal concrete, chalk circle marks, four shadowed figures; warm rim light; keep panel in inner 80%."  
canvas_ideas: ["Chalk circle lines pulsing with kick grid","Four dots orbiting, syncing to bassu/contra call"]  
provenance_notes: "Synthetic modeling of tenore parts; no sampled traditional recordings."  
usage_rights: "Original generative composition; cleared of third-party content."  
embedding_notes: "Embed gqom/tenore tags, persona lineage, AI-provenance; note non-lyrical approach."

#### Status

Planned

---

### 5. Stone Chapel Footwork

Corsican Paghjella × Footwork

#### Style of Music (≤200 chars)
Three-voice Corsican paghjella (segonda→bassu→terza) chopped into 160 BPM footwork grids; vocal hits as percussion, sub flickers, clap grids, vinyl haze; non-lexical refrains, sharp room bloom.

#### Style of Music (≤1000 chars)
Austere footwork chassis at 160 BPM—rapid syncopation, clap grids, micro-kicks—carries Corsican paghjella’s three-voice entry order (segonda, bassu, terza). Short antiphonal phrases are sliced into percussive vox hits; bassu doubles the sub as a call, segonda lays center tone, terza gives bright ornaments. Sparse organ/pad stabs sketch tonality while vinyl/tape haze and short plate reverbs bloom tails to encourage ghost-syllables. No literal lyrics—voices function as rhythmic/harmonic figures. Drops alternate between dry a-cappella cells and hyper-chopped vocal percussion, then resolve into a hovering drone coda.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: footwork, world-choral, electronic]  
[mood: kinetic, sacred-minimal, bright]  
[tempo: 160bpm]  
[length: 180-200s]  
[instruments: micro-kicks, clap grid, sub flickers, organ stabs, vinyl/tape haze, plate reverb]  
[vocals: corsican paghjella trio (segonda, bassu, terza), antiphonal cells, non-lexical]  
[key: G Dorian center, modal pivots]  
[time_signature: 4/4]  
[weirdness: 60]  
[audio_weight: 42]
[style_weight: 52]

[sequence: intro, phrase-1, drop, loop-shift, drop, coda]  
[intro]  
[phrase-1]  
[drop]  
[loop-shift]  
[drop]  
[coda]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Stone Chapel Footwork"  
primary_persona: "New seed (choral-percussive branch)"  
bpm: 160  
key: G Dorian (modal)  
tags: ["footwork 160","paghjella","non-lexical choir","experimental"]  
mood_pitch: "A-cappella arches sliced into dance-grid sparks."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom title panel inside inner 80%. Rough stone apse geometry morphing into step-grid lines; no in-image text."  
canvas_ideas: ["Three voice dots snapping to a 160 lattice","Stone arch dissolving into clap grid"]  
provenance_notes: "Synthetic modeling of Corsican entry order; no sampled folklore."  
usage_rights: "Original generative composition; cleared of third-party content."  
embedding_notes: "Embed footwork/paghjella tags; mark AI provenance, non-lyrical."

#### Status

Planned

---

### 5a. Stone Chapel Footwork for Kamaskera Kamadan

#### Style of Music (≤200 chars)
Paghjella trio chopped into 160 footwork; bassu mirrors sub, terza ornaments snap to grid; cowbell ghosts, tape haze, hand-drum blips nod to Kamaskera’s ritual phonk; non-lexical, bright/kinetic.

#### Style of Music (≤1000 chars)
A 160 BPM footwork lattice—rapid clap grids, micro-kicks, sub flickers—reframed for Kamaskera Kamadan. Corsican paghjella’s entry order (segonda→bassu→terza) is performed as short antiphonal cells, sliced into percussive vocal hits. Bassu doubles the sub as a living drone; segonda anchors the center; terza adds bright ornaments that snap to the step grid. To preserve Kamaskera’s “Urban Zulu / ritual phonk” ancestry without leaving footwork, we thread in cowbell ghost ticks, dusty tape flutter, and low hand-drum blips during drops. Metallic plate tails and brief granular blooms seed soft ghost-syllables (no literal text). The arrangement pivots between dry a-cappella cells, hyper-chopped vocal percussion, and a hovering drone coda that hints at circle-chant energy—hallucination-friendly but club-functional.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly, kamaskera-lineage]  
[genre: footwork, world-choral, experimental-club]  
[mood: kinetic, sacred-minimal, urban-ritual]  
[tempo: 160bpm]  
[length: 180-200s]  
[instruments: micro-kicks, clap grid, sub flickers, organ stabs, cowbell ghosts, hand-drum blips, vinyl/tape haze, metallic plate reverb]  
[vocals: corsican paghjella trio (segonda, bassu, terza), antiphonal cells, non-lexical, distant crowd hums]  
[key: G Dorian center, modal pivots]  
[time_signature: 4/4]  
[weirdness: 62]  
[audio_weight: 46] [style_weight: 50]

[sequence: intro, phrase-1, drop, loop-shift, ritual-break, drop, coda]  
[intro]  
[phrase-1]  
[drop]  
[loop-shift]  
[ritual-break]  
[drop]  
[coda]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Persona-tuning notes
- Keep **cowbell ghosts** and **hand-drum blips** below the main grid so they read as lineage “scent,” not genre switch.  
- Use **vinyl/tape haze + short plates** for spectral smear; avoid long halls (keeps it tight for 160).  
- For higher hallucination rates, A/B an alt take adding **female ghost pads** quietly under terza in the [ritual-break].

#### Distro media kit (sidecar)
title: "Stone Chapel Footwork (Kamaskera Cut)"  
primary_persona: "Kamaskera Kamadan (choral-percussive branch)"  
bpm: 160  
key: G Dorian (modal)  
tags: ["footwork 160","paghjella","Kamaskera lineage","non-lexical choir","experimental club"]  
mood_pitch: "Circle-chant cut into a dance lattice; ancient calls spark modern steps."  
cover_art_master_spec: "Square 1:1, poster layout with blank bottom title panel inside inner 80%. Rough stone apse morphs into a luminous 160-step grid; faint cowbell halo dots; no in-image text."  
canvas_ideas: ["Three glowing voice nodes snapping to a moving 160 grid","Stone arch dissolving into clap-grid particles, sub ripple underneath"]  
provenance_notes: "Synthetic Corsican-style voicing; no sampled folklore recordings. Non-lexical vocals only."  
usage_rights: "Original generative composition; cleared of third-party content."  
embedding_notes: "Embed BWF description with style strings, Kamaskera lineage, AI-provenance, non-lyrics policy."

#### Status

Planned

---

### 5b. Stone Chapel Footwork — Persona Seed

#### Style of Music (≤200 chars)
Paghjella trio as percussive hits over 160 footwork; tight stone-chapel IRs, close mics, cowbell ghosts, hand-drum blips; bassu=sub drone, terza ornaments; dusty tape flutter; non-lexical, kinetic/ritual.

#### Style of Music (≤1000 chars)
Persona-oriented capture of Corsican paghjella fused with 160 BPM footwork. Three-voice entry (segonda→bassu→terza) is performed as short antiphonal cells, then micro-sliced into grid-snapped vocal percussion. Bassu doubles the sub to imprint a living drone; segonda centers the mode; terza supplies bright ornamental snaps. To preserve Kamaskera’s ritual lineage without leaving footwork, faint cowbell ghosts and low hand-drum blips sit beneath the lattice, plus light tape flutter. Room modeling uses **tight stone/brick chapel IRs** (early reflections emphasized, fast decay) so Suno learns close, dry timbre first. Metallic plate tails are trimmed; granular blooms are subtle—just enough to seed soft, non-lexical ghost syllables. No words; voice acts as rhythm/harmony. Arrangement alternates dry a-cappella cells, hyper-chopped drops, and a concise drone coda.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly, kamaskera-lineage]  
[genre: footwork, world-choral, experimental-club]  
[mood: kinetic, sacred-minimal, urban-ritual]  
[tempo: 160bpm]  
[length: 180-200s]  
[instruments: micro-kicks, clap grid, sub flickers, organ stabs, cowbell ghosts (low), hand-drum blips (low), vinyl/tape flutter, tight stone/brick room IRs, short plate]  
[vocals: corsican paghjella trio (segonda, bassu, terza), antiphonal cells, non-lexical, close-miked]  
[key: G Dorian center, modal pivots]  
[time_signature: 4/4]  
[weirdness: 58]  
[audio_weight: 78] [style_weight: 45]

[sequence: intro, phrase-1, drop, loop-shift, ritual-break, drop, coda]  
[intro]  
[phrase-1]  
[drop]  
[loop-shift]  
[ritual-break]  
[drop]  
[coda]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Persona-seeding notes (do first render exactly once):
- Keep master **attack fast** and **room IRs tight** (RT60 ≈ 0.4–0.6s).  
- Cowbell/hand-drum layers at **−18 to −24 LUFS relative** to main vox grid—present but subliminal.  
- If you need more “Kamaskera scent,” add **female ghost pads** at −22 LUFS only in [ritual-break].  
- Save this render as **Parental/Seed**; subsequent Persona builds can widen rooms and raise weirdness.

---

#### Distro media kit (sidecar)
title: "Stone Chapel Footwork — Persona Seed"  
primary_persona: "Kamaskera Kamadan (choral-percussive branch seed)"  
bpm: 160  
key: G Dorian (modal)  
tags: ["footwork 160","paghjella","persona seed","Kamaskera lineage","non-lexical choir","experimental club"]  
mood_pitch: "Circle-chant cut into a tight dance lattice; ancient calls imprinted close-miked."  
cover_art_master_spec: "Square 1:1, poster layout with blank bottom title panel inside inner 80%. Rough stone apse in close-up, faint grid lines over masonry; tiny cowbell halo dots; no in-image text."  
canvas_ideas: ["Three voice nodes snapping to a 160 grid over stone texture","Close-miked stone reflections pulsing with clap grid"]  
provenance_notes: "Synthetic Corsican-style voicing; no sampled folklore recordings. Non-lexical vocals only."  
usage_rights: "Original generative composition; cleared of third-party content."  
embedding_notes: "Embed BWF description with style strings, room IR notes, audio/style weights, Kamaskera lineage, AI-provenance, non-lyrics policy."

#### Status

Planned

---

### 6. Frostbite Amen Duel

Inuit Katajjaq × Breakcore

#### Style of Music (≤200 chars)
Percussive Inuit katajjaq duet (inhaled/exhaled bursts) over 180–196 BPM breakcore: Amen edits, whiplash fills, bitcrush, granular tails; breath games drive the groove; zero lexical text.

#### Style of Music (≤1000 chars)
A feral breakcore engine (180–196 BPM) with Amen/Think edits, switch-ups, and gated subs is steered by Inuit katajjaq’s antiphonal breathing games. Short inhale/exhale motifs become rhythmic triggers; stutters, reverse grains, and comb-filter sweeps splinter phrases into phantom syllables. The arrangement alternates tumble-run barrages with “vacuum drops” where only breath percussion remains. Light distortion and bitcrush grit the top; transient shaping keeps throat pops articulate. No words—just pulse, rasp, and call-response. Coda freezes on time-stretched breath into glacial shimmer.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: breakcore, experimental-vocal, electronic]  
[mood: feral, icy, exhilarating]  
[tempo: 188bpm]  
[length: 170-200s]  
[instruments: amen edits, gated sub, bitcrush, granular reverse, comb-filter sweeps, noise bursts]  
[vocals: inuit katajjaq duet, inhaled/exhaled pulses, percussive grunts, non-lexical]  
[key: atonal / drone centers]  
[time_signature: 4/4 (free breaks permitted)]  
[weirdness: 68]  
[audio_weight: 45]
[style_weight: 50]

[sequence: cold-open, barrage, vacuum-drop, barrage, glitch-bridge, finale-freeze]  
[cold-open]  
[barrage]  
[vacuum-drop]  
[barrage]  
[glitch-bridge]  
[finale-freeze]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[break]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Frostbite Amen Duel"  
primary_persona: "New seed (arctic-percussive branch)"  
bpm: 188  
key: Atonal/drone  
tags: ["breakcore","katajjaq","amen edits","non-lexical","granular"]  
mood_pitch: "Breath becomes drum—glacier speed-runs and vacuum drops."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Frost fractals exploding into waveform shrapnel; keep panel in inner 80%."  
canvas_ideas: ["Condensed breath puffs synced to snare rushes","Amen waveform turning to ice shards"]  
provenance_notes: "Synthetic emulation of katajjaq duet behavior; no field recordings used."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag breakcore/katajjaq; note non-lexical intent and AI provenance."

#### Status

Planned

---

### 7. Iron Overtone Foundry

Tuvan Khöömei/Kargyraa × Industrial

#### Style of Music (≤200 chars)
Subharmonic kargyraa + overtone whistles over machine-room industrial: heavy kicks, anvil hits, piston rhythms, turbine drones; re-amped hall tails; ritual tempo 96–104; wordless, tectonic.

#### Style of Music (≤1000 chars)
A slow-grinding industrial ritual (≈100 BPM) forged from piston rhythms, metallic anvil hits, and turbine drones. Tuvan throat singing layers—kargyraa (subharmonic growl) underpinning khöömei/sygyt overtones—form the lead bed. Re-amped impulse responses (warehouse/ship hull) give iron bloom; side-chain swells pull drones around the kick. Sparse distortion and granular smear seed low-register ghost phonemes without explicit text. Mid sections open to pure drone/overtones before slamming back into machine cadence. Final minute lets overtone whistles ride a receding factory rumble.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: industrial, drone-choral, dark-ambient]  
[mood: tectonic, mechanical, solemn]  
[tempo: 100bpm]  
[length: 190-220s]  
[instruments: heavy kick, anvil hits, piston rhythm loops, turbine drones, re-amp IRs, granular smear]  
[vocals: tuvan throat (kargyraa + khöömei/sygyt layers), sustained drones, non-lexical]  
[key: low D drone center]  
[time_signature: 4/4]  
[weirdness: 57]  
[audio_weight: 44]
[style_weight: 51]

[sequence: ignition, cadence, drone-vault, cadence, hammer-break, long-fade]  
[ignition]  
[cadence]  
[drone-vault]  
[cadence]  
[hammer-break]  
[long-fade]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Iron Overtone Foundry"  
primary_persona: "Kamaskera Kamadan (iron-ritual branch)"  
bpm: 100  
key: D low drone  
tags: ["industrial","tuvan throat","drone","non-lexical","mechanical"]  
mood_pitch: "Foundry rhythm breathes through overtone hymns."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom title panel. Rusted factory hall, glowing iron runes tracing overtone lines; keep panel inside inner 80%."  
canvas_ideas: ["Slow piston loop with overtone spectrum lines","Molten pour blooming into spectrogram glow"]  
provenance_notes: "Synthetic Tuvan-style timbres; no sampled traditional vocals."  
usage_rights: "Original generative composition."  
embedding_notes: "Embed industrial/throat-sing tags; persona lineage; AI provenance; non-lyrical policy."

#### Status

Planned

---

### 8. Hollow Square Slide

Sacred Harp (Shape-Note) × Drill

#### Style of Music (≤200 chars)
Shape-note four-part shouts over UK drill: sliding 808s, triplet hats, dark pads; block-chord “hollow square” refrains as chorus stabs; tape haze; non-lexical calls (no worship text), 140 BPM.

#### Style of Music (≤1000 chars)
A lean UK drill frame (140 BPM) with sliding 808 sub, triplet hat science, and low-swing snares under a Shape-Note “hollow square” choir. Four-part block chords hit like brass stabs; occasional call-and-response swells create chorus-style hooks without words. Keep vowels broad (“ah/oh”) for percussive clarity; let bass lead lines shadow the tonic like a congregational pedal. Pads stay dusky; short plate/room tails encourage faint ghost-syllables. No explicit religious text—this is interval color and crowd power only. Drops thin to sub + handclap before the choir slams back in stacked unisons.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: uk drill, folk-choral, experimental-hiphop]  
[mood: staunch, gritty, exalted]  
[tempo: 140bpm]  
[length: 180-210s]  
[instruments: 808 (sliding), triplet hats, low-swing snare, dark pads, short plate, tape haze]  
[vocals: mixed choir shape-note style, block chords, call-and-response, non-lexical]  
[key: A Aeolian, tonic pedal]  
[time_signature: 4/4]  
[weirdness: 60]  
[audio_weight: 44] [style_weight: 52]

[sequence: intro, verse, build, drop, verse, break, drop, outro]  
[intro]  
[verse]  
[build]  
[drop]  
[verse]  
[break]  
[drop]  
[outro]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Hollow Square Slide"  
primary_persona: "New seed (Square-Cantus branch)"  
bpm: 140  
key: A Aeolian  
tags: ["UK drill","shape-note","choir-as-lead","non-lexical","experimental"]  
mood_pitch: "Congregational thunder over sliding sub—exalted without words."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel (inner 80%). Chalked square on asphalt glowing like a hymn grid; no in-image text."  
canvas_ideas: ["Hollow-square lines pulsing with 808 slides","Block-chord spectrogram morphing into drill hats"]  
provenance_notes: "Synthetic shape-note voicing; no quoted hymn lyrics."  
usage_rights: "Original generative composition."  
embedding_notes: "Embed drill/shape-note tags, AI-provenance, non-lyrical policy."

#### Status

Planned

---

### 9. Cowbell Cloister (Slow Phonk Chant)

Gregorian Plainchant × Phonk (slowed)

#### Style of Music (≤200 chars)
Monophonic chant phrases over slowed phonk: cowbell ticks, chopped vox chops, woozy tape, dusty keys; sub-swells, gated room; melismas glide through haze; non-lexical (no Latin text), ~96 BPM.

#### Style of Music (≤1000 chars)
A slowed-phonk engine (~96 BPM): cowbell ghosts, wood-block echoes, warped tape, and chopped-n-screwed micro-edits. Over it, plainchant-style single-line melodies drift in free-time arcs, printed with close, dry timbre then smeared by gentle wow/flutter and short room. The chant remains lyric-free—pure vowels and melismas—so Suno can hallucinate soft pseudo-syllables at phrase tails. Sub-bass moves in swells rather than slides; dusty electric-piano stabs sketch modal centers. Drops remove drums entirely, leaving tape hiss, cowbell memory, and chant over sub air. It feels devotional yet street-worn.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: phonk (slowed), chant, lofi-hiphop]  
[mood: woozy, reverent, nocturnal]  
[tempo: 94-98bpm]  
[length: 180-210s]  
[instruments: cowbell ticks, chopped vox one-shots, dusty keys, sub swells, tape wow/flutter, short room, vinyl noise]  
[vocals: plainchant-style solo, melismatic phrases, non-lexical, close-miked]  
[key: D Dorian center]  
[time_signature: free over 4/4 grid]  
[weirdness: 58]  
[audio_weight: 46] [style_weight: 50]

[sequence: prelude, phrase-1, drop, phrase-2, loop-shift, hush-drop, coda]  
[prelude]  
[phrase-1]  
[drop]  
[phrase-2]  
[loop-shift]  
[hush-drop]  
[coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Cowbell Cloister (Slow Phonk Chant)"  
primary_persona: "Kamaskera-compatible seed (urban-ritual line)"  
bpm: 96  
key: D Dorian  
tags: ["slowed phonk","plainchant","melisma","non-lexical","tape haze"]  
mood_pitch: "Street-worn devotion: cowbell memory and chant drifting through tape dusk."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Cloister corridor at night, cowbell halo dots, tape scratches; no in-image text."  
canvas_ideas: ["Cowbell tick ripples through candlelight","Tape shimmer morphs into chant waveform"]  
provenance_notes: "Synthetic chant timbre; no sacred text quoted."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag phonk/chant; mark non-lyrical approach and AI provenance."

#### Status

Planned

---

### 10. Ridge Echo Lattice (160)

Kulning Calls × Footwork/Juke

#### Style of Music (≤200 chars)
High-piercing kulning herding calls sliced into 160 footwork/juke syncopation; call-and-answer riffs, sub flickers, clap grids; short alpine room; non-lexical, agile and bright.

#### Style of Music (≤1000 chars)
Footwork/juke at 160 BPM with rapid clap grids, micro-kicks, and agile sub bursts. Kulning—aerial Nordic calls with ornaments and glides—becomes the lead instrument: short calls are sampled into grid-snapped riffs and echo-answers. Keep the room tight (alpine early reflections, fast decay) so pitch bends read cleanly; add brief granular blooms at phrase ends to seed ghost syllables. Occasional triangle or wood chime accents hint at open air. The “loop-shift” reframes call shapes into downward spirals before a final bright reprise. No words—just calls as melody/percussion.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: footwork, juke, nordic-folk-fusion]  
[mood: bright, agile, windswept]  
[tempo: 160bpm]  
[length: 170-200s]  
[instruments: micro-kicks, clap grid, sub flickers, wood/triangle chimes, tight alpine IRs, granular tails]  
[vocals: kulning-style solo calls, ornamented glides, antiphonal echoes, non-lexical]  
[key: A Mixolydian center]  
[time_signature: 4/4]  
[weirdness: 61]  
[audio_weight: 43] [style_weight: 52]

[sequence: call-open, drop, loop-shift, call-variations, drop, bright-coda]  
[call-open]  
[drop]  
[loop-shift]  
[call-variations]  
[drop]  
[bright-coda]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Ridge Echo Lattice (160)"  
primary_persona: "New seed (Nordic-Flight branch)"  
bpm: 160  
key: A Mixolydian  
tags: ["footwork/juke","kulning","non-lexical lead","granular tails","alpine room"]  
mood_pitch: "Sky-bright calls stitched into a dance lattice."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Mountain ridge line, echo rings stepping like a 160 grid; no in-image text."  
canvas_ideas: ["Call ripples racing across ridges","Voice dot hopping a checker lattice with sub ripples"]  
provenance_notes: "Synthetic kulning color; no field recordings."  
usage_rights: "Original generative composition."  
embedding_notes: "Embed footwork/kulning tags; AI provenance; non-lyrical policy."

#### Status

Planned

---

### 11. Dervish on the Durban Floor

Qawwali Chorus × Gqom

#### Style of Music (≤200 chars)
Lead qawwal + response chorus over minimalist gqom: broken kick grid, cavern claps, harmonium bed, tabla one-shots; ecstatic swells, long handclap arcs; non-lexical refrains; ~123 BPM.

#### Style of Music (≤1000 chars)
A sparse gqom chassis (~123 BPM) of broken kicks, cavern claps, and sub air hosts a Qawwali-style layout: lead voice rides a harmonium drone while a small chorus answers in short ecstatic cells. Handclaps stretch into long arcs that cue rises and drops. Tabla one-shots punctuate turnarounds; log-drum hints mirror the drone. Keep text non-lexical (pure vowels + syllabic taans) so Suno can bloom phantom syllables. Use short warehouse IRs for impact, reserving longer plate only on peak swells. The drop strips to drone+claps+lead melisma before the chorus slams back in stacked refrains.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: gqom, sufi-fusion, experimental-club]  
[mood: ecstatic, hypnotic, earthy]  
[tempo: 122-124bpm]  
[length: 180-210s]  
[instruments: broken-beat kit, cavern claps, harmonium drone, tabla one-shots, log-drum hints, short warehouse IRs, plate (sparse)]  
[vocals: lead qawwal-style melisma + response chorus, handclap arcs, non-lexical taans]  
[key: F# Dorian center]  
[time_signature: 4/4]  
[weirdness: 58]  
[audio_weight: 44] [style_weight: 52]

[sequence: invocation, call, drop, antiphon, rise, drop, coda]  
[invocation]  
[call]  
[drop]  
[antiphon]  
[rise]  
[drop]  
[coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Dervish on the Durban Floor"  
primary_persona: "New seed (Sufi-Club branch)"  
bpm: 123  
key: F# Dorian  
tags: ["gqom","qawwali chorus","harmonium drone","non-lexical","handclap arcs"]  
mood_pitch: "Ecstatic call-and-response riding a broken club heartbeat."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel (inner 80%). Lantern halos over a dark dance floor; subtle rosette motif; no in-image text."  
canvas_ideas: ["Clap-arc rings expanding into kick hits","Harmonium waveform becoming a glowing rosette"]  
provenance_notes: "Synthetic Qawwali color; no quoted poetry or samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag gqom/qawwali, AI provenance, non-lyrical policy."

#### Status

Planned

---

### 12. Glass Choir in Feedback

Bulgarian Diaphony × Noise

#### Style of Music (≤200 chars)
Bright Bulgarian women’s diaphony sustained into noise-ambient: feedback beds, bowed metal, granular fog, tape howl; clustered chords bloom, dissolve, reappear; wordless, glacial and fierce.

#### Style of Music (≤1000 chars)
Dissonant/open-throat Bulgarian diaphony is stretched into a noise-ambient sculpture. Sustained cluster chords hang over feedback beds, bowed-metal scrapes, and low tape howl. Granular smearing lets vowel edges shed phantom syllables. Dynamics move from near-silence to burnished glare, then into ash-quietness. No drums—only pressure and release. Short impulses (coin-hits, wire twangs) mark section pivots; distortion rides are restrained to preserve overtone ladders. Absolutely non-lexical; the choir functions as a living oscillator bank. Close-bright timbre at the core; wider plates only for climaxes.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: noise-ambient, experimental-choral]  
[mood: glacial, incandescent, severe]  
[tempo: free (target grid 60bpm for automation)]  
[length: 200-240s]  
[instruments: feedback loops, bowed metal, contact mic scrapes, granular smear, tape howl, impulse pings]  
[vocals: female ensemble bulgarian-diaphony, sustained clusters, non-lexical vowels]  
[key: evolving centers; Lydian/Phrygian color shifts]  
[time_signature: free]  
[weirdness: 70]  
[audio_weight: 42] [style_weight: 54]

[sequence: ember, flare, pressure-plateau, ash, flare-ii, fade]  
[ember]  
[flare]  
[pressure-plateau]  
[ash]  
[flare-ii]  
[fade]

[lyrics]  
[drone]  
[antiphon]  
[drone]  
[bridge]  
[coda]
```

#### Distro media kit (sidecar)
title: "Glass Choir in Feedback"  
primary_persona: "New seed (Spectral-Diaphony branch)"  
bpm: (free / automation at 60)  
key: shifting modal color  
tags: ["noise ambient","Bulgarian diaphony","granular","feedback","non-lexical"]  
mood_pitch: "A bright dissonant choir soldered into a wall of glow."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Shattered-glass rosette suspended in fog; faint feedback rings; no in-image text."  
canvas_ideas: ["Spectrogram flames rising from a chord","Glass shards drifting as granular grains"]  
provenance_notes: "Synthetic diaphony intervals; no folk samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag diaphony/noise; AI provenance; non-lyrics policy."

#### Status

Planned

---

### 13. Iron Choir at 180

Georgian Polyphony × Gabber

#### Style of Music (≤200 chars)
Three-part Georgian male polyphony punctuating distorted 180 BPM kicks: pedal drones, cluster hits, alarm stabs; sparse breaks; short bunker IRs; non-lexical, martial-ritual energy.

#### Style of Music (≤1000 chars)
A hard gabber frame (≈175–185 BPM) with distorted four-on-the-floor, offbeat claps, and siren stabs collides with rugged Georgian three-part harmony. Bass pedal drones underpin cluster shouts that act like brass stabs; mid sections thin to drone + tom-rolls before a slam return. Keep vocal material non-lexical (open “ah/oh”) for punch; use short bunker/warehouse IRs to keep clarity over the kick wall. Add rare Amen-slice fills to reset momentum. Granular tails only at cut-points—enough to seed ghost syllables without smearing transients. Ancient block chords meet rave steel.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: gabber, chant-core, industrial-rave]  
[mood: martial, exultant, relentless]  
[tempo: 178-182bpm]  
[length: 170-200s]  
[instruments: distorted kick wall, offbeat claps, siren/alarm stabs, tom rolls, short bunker IRs, amen slice fills]  
[vocals: male trio georgian-style, cluster shouts, pedal drones, non-lexical]  
[key: E minor pedal]  
[time_signature: 4/4]  
[weirdness: 63]  
[audio_weight: 46] [style_weight: 50]

[sequence: ignition, surge, drone-break, surge-ii, hard-stop coda]  
[ignition]  
[surge]  
[drone-break]  
[surge-ii]  
[hard-stop coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Iron Choir at 180"  
primary_persona: "New seed (Ritual-Rave branch)"  
bpm: 180  
key: E minor pedal  
tags: ["gabber","Georgian polyphony","cluster shouts","non-lexical","industrial rave"]  
mood_pitch: "Mountain-forged chords hammered to a 180 BPM anvil."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Bunker doorway glowing with chord-shaped light bars; no in-image text."  
canvas_ideas: ["Kick wall turning into mountain contour lines","Three chord bars slamming with claps"]  
provenance_notes: "Synthetic Georgian-style voicing; no folk samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag gabber/polyphony; AI provenance; non-lyrical policy."

#### Status

Planned

---

### 14. Log-Drum Tenore (Coastal Glow)

Tenore (bassu/contra) × Amapiano

#### Style of Music (≤200 chars)
Sardinian tenore (bassu/contra/mesu/oche) over warm amapiano: log-drum hooks, dusty keys, shaker roll; bassu mirrors log-drum; antiphonal cells, non-lexical; airy room, 113 BPM.

#### Style of Music (≤1000 chars)
A gently rolling amapiano frame (~113 BPM) of log-drum bass hooks, mellow Rhodes, and shaker/hat ladders supports a Sardinian tenore circle. Bassu and contra provide a living sub that doubles the log-drum figure; mesu sustains mid drone; oche carries bright calls. Short antiphonal phrases are presented as rhythmic cells rather than lyrics, inviting soft ghost-syllables at phrase tails. Keep claps sparse, pads silky, and room IRs airy (small coastal hall) so the choir remains intimate. Occasional marimba or kalimba taps echo the log-drum shapes. Drops thin to Rhodes + bassu drone before the circle re-enters with an easy sway.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: amapiano, world-choral, deep-house]  
[mood: warm, coastal, trance-gentle]  
[tempo: 112-115bpm]  
[length: 190-210s]  
[instruments: log-drum bass, mellow rhodes, shaker/hat ladder, soft clap, kalimba/marimba taps, airy room IRs, tape hush]  
[vocals: sardinian tenore quartet (bassu, contra, mesu, oche), antiphonal cells, non-lexical]  
[key: F# minor / Dorian color]  
[time_signature: 4/4]  
[weirdness: 55]  
[audio_weight: 44] [style_weight: 52]

[sequence: intro, phrase-1, drop, antiphon, pocket-groove, drop, coda]  
[intro]  
[phrase-1]  
[drop]  
[antiphon]  
[pocket-groove]  
[drop]  
[coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Log-Drum Tenore (Coastal Glow)"  
primary_persona: "New seed (Pastoral-Piano branch)"  
bpm: 113  
key: F# minor (Dorian color)  
tags: ["amapiano","tenore","log-drum","non-lexical choir","deep house"]  
mood_pitch: "Circle-sung earth on a sun-warmed floor—swaying log-drum and soft keys."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom title panel inside inner 80%. Coastal dusk, faint chalk circle in sand, glowing log-drum wavelets; no in-image text."  
canvas_ideas: ["Four dots orbiting a log-drum waveform","Rhodes chords breathing with bassu pulses"]  
provenance_notes: "Synthetic tenore modeling; no traditional samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Embed amapiano/tenore tags; mark AI provenance; non-lyrics policy."

#### Status

Planned

---

### 15. Soft-Foot Grime

Isicathamiya × Grime

#### Style of Music (≤200 chars)
Isicathamiya male choir (soft-step stacks, bass hum) over 140 grime: jagged breaks, square-lead nicks, sliding sub; call-and-response refrains, non-lexical; short room, tape haze.

#### Style of Music (≤1000 chars)
A 140 BPM grime chassis—syncopated kicks/snares, triplet hats, square-lead nicks, and a gliding sub—hosts isicathamiya’s soft-footed male choir. Close-voiced blocks and gentle bass hums become chorus stabs; brief call-and-response swells act as hooks without words. Keep vowels broad (“ah/oh/um”) for percussive clarity; bass hum rides the tonic like a pedal. Use short, tight rooms and mild tape flutter so consonants stay airy but present. Drops thin to sub + clap while the choir whispers a stacked unison, then the square-lead and triplet hats return for the slam. Entirely non-lexical; voice is rhythm and harmony.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: grime, zulu-choral, experimental-hiphop]  
[mood: urban-solemn, resilient, stealth-bright]  
[tempo: 140bpm]  
[length: 180-200s]  
[instruments: gliding 808/sub, triplet hats, jagged kick/snare, square-lead stabs, short room IRs, tape flutter]  
[vocals: male isicathamiya ensemble, soft-step blocks, bass hum pedal, non-lexical call/response]  
[key: G# Aeolian center]  
[time_signature: 4/4]  
[weirdness: 60]  
[audio_weight: 45] [style_weight: 51]

[sequence: alley-intro, verse, build, drop, verse, break, drop, outro]  
[alley-intro]  
[verse]  
[build]  
[drop]  
[verse]  
[break]  
[drop]  
[outro]

[lyrics]  
[verse]  
[chorus]  
[verse]  
[bridge]  
[chorus]
```

#### Distro media kit (sidecar)
title: "Soft-Foot Grime"  
primary_persona: "New seed (Urban Zulu × 140 branch)"  
bpm: 140  
key: G# Aeolian  
tags: ["grime 140","isicathamiya","non-lexical choir","sliding sub","experimental"]  
mood_pitch: "Quiet, close harmonies walk the night over jagged streets."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Night street chalk-footprints forming a rosette; sub ripples; no in-image text."  
canvas_ideas: ["Soft footfalls lighting a 140 grid","Square-lead spikes rising behind stacked hums"]  
provenance_notes: "Synthetic isicathamiya color; no archival samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag grime/isicathamiya; AI provenance; non-lyrics policy."

#### Status

Planned

---

### 16. Foundry Cantus (100)

Plainchant × Industrial

#### Style of Music (≤200 chars)
Monophonic chant lines re-amped in metal spaces over slow industrial: piston rhythms, anvil hits, turbine drones; short bunker IRs, granular bloom; wordless melismas; ~100 BPM.

#### Style of Music (≤1000 chars)
A slow, machine-room ritual (~100 BPM): piston rhythms, heavy kick, anvil hits, and low turbine drones. A plainchant-style solo line (no sacred text) moves in free-time arcs above the grid, captured close, then re-amped through short bunker/ship-hull IRs for iron bloom. Granular tails and light wow/flutter seed ghost phonemes at phrase endings without smearing transients. Mid sections open into drone vaults where the chant threads alone before the cadence slams back. Keep the palette austere—metallic, oil-dark, reverberant but tight—so the vocal remains the torch in the factory haze.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: industrial, chant-ambient, dark-electronic]  
[mood: solemn, tectonic, reverent-mechanical]  
[tempo: 98-104bpm]  
[length: 190-220s]  
[instruments: heavy kick, piston loops, anvil hits, turbine drones, short bunker/ship IRs, granular tails, tape wow]  
[vocals: plainchant-style solo, melismatic phrases, non-lexical, close-miked then re-amped]  
[key: D Dorian drone]  
[time_signature: free over 4/4 grid]  
[weirdness: 57]  
[audio_weight: 46] [style_weight: 50]

[sequence: ignition, cadence, drone-vault, cadence-ii, hammer-break, long-fade]  
[ignition]  
[cadence]  
[drone-vault]  
[cadence-ii]  
[hammer-break]  
[long-fade]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)**  
title: "Foundry Cantus (100)"  
primary_persona: "New seed (Iron-Cantus branch)"  
bpm: 100  
key: D Dorian drone  
tags: ["industrial","plainchant","metal room","non-lexical","granular bloom"]  
mood_pitch: "A solitary torch of melody through a breathing machine hall."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Rusted factory nave, chant waveforms etched as glowing rails; no in-image text."  
canvas_ideas: ["Piston loop visual with overtone lines","Anvil sparks syncing to chant melismas"]  
provenance_notes: "Synthetic chant timbre; no quoted sacred text or samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag industrial/chant; AI provenance; non-lyrics policy."

#### Status

Planned

---

### 17. Whirling Lattice (160)

Qawwali × Footwork

#### Style of Music (≤200 chars)
Lead qawwal + small chorus over 160 footwork: clap grids, sub flickers, harmonium drone, tabla one-shots; ecstatic call/response sliced into vocal riffs; tight room, non-lexical taans.

#### Style of Music (≤1000 chars)
A 160 BPM footwork lattice—rapid clap grids, micro-kicks, agile sub bursts—hosts a Qawwali-style layout. Lead voice rides a harmonium drone; a small chorus answers in short ecstatic cells. Those cells are sliced into grid-snapped vocal riffs (non-lexical taans and vowels) so the choir/lead become both melody and percussion. Tabla one-shots mark turnarounds; occasional handclap arcs cue rises and drops. Keep room IRs tight (small courtyard/stone) to preserve rapid articulation; add brief granular blooms at phrase ends to seed ghost syllables. Mid drop strips to harmonium + claps + lead melisma before the chorus re-enters, stacked and bright. Devotional energy, club agility—no quoted poetry.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: footwork, sufi-fusion, electronic]  
[mood: ecstatic, agile, luminous]  
[tempo: 160bpm]  
[length: 170-200s]  
[instruments: micro-kicks, clap grid, sub flickers, harmonium drone, tabla one-shots, tight stone/courtyard IRs, granular tails]  
[vocals: lead qawwal-style + response chorus, taans (non-lexical), handclap arcs]  
[key: E Dorian center]  
[time_signature: 4/4]  
[weirdness: 60]  
[audio_weight: 43] [style_weight: 52]

[sequence: call-open, drop, antiphon, loop-shift, drop, bright-coda]  
[call-open]  
[drop]  
[antiphon]  
[loop-shift]  
[drop]  
[bright-coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Whirling Lattice (160)"  
primary_persona: "New seed (Sufi-Step branch)"  
bpm: 160  
key: E Dorian  
tags: ["footwork 160","Qawwali chorus","harmonium drone","non-lexical","granular tails"]  
mood_pitch: "Ecstatic call-and-response stitched into a 160 dance lattice."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom title panel (inner 80%). Lantern ring rosette snapping into square footwork grid; no in-image text."  
canvas_ideas: ["Clap-arc rings quantizing into a 160 checker","Harmonium waveform braided with chorus glyphs"]  
provenance_notes: "Synthetic Qawwali color; no quoted poetry or field samples."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag footwork/qawwali; AI provenance; non-lyrics policy."

#### Status

Planned

---

### 18. Breath on the Floor (Gqom)

Inuit Katajjaq × Gqom

#### Style of Music (≤200 chars)
Percussive katajjaq duet (inhaled/exhaled bursts) over minimalist gqom: broken kick grid, cavern claps, gated sub; breath games become lead rhythm; tight warehouse IRs; non-lexical.

#### Style of Music (≤1000 chars)
Minimalist Durban gqom (~123–126 BPM): broken kick patterns, cavern claps, and gated sub air become the stage for an Inuit katajjaq duet. Short inhale/exhale motifs and percussive grunts are presented as antiphonal “breath riffs” that drive the groove—voice as drum. Occasional reverse grains and comb-filter sweeps at phrase ends seed phantom syllables without obscuring the percussive edge. Keep IRs tight (small warehouse/cinderblock) for punch; deploy air-horn/sweep FX sparingly. The first drop reduces to breath percussion + sub shadow, then the grid slams back with widened claps. Entirely non-lexical and body-forward.

#### Lyrics
```
[control: experimental, persona-seed, hallucination-friendly]  
[genre: gqom, experimental-vocal, club]  
[mood: feral, hypnotic, subterranean]  
[tempo: 124-126bpm]  
[length: 180-210s]  
[instruments: broken-beat kit, cavern claps, gated sub, reverse grains, comb-filter sweeps, sparse air-horn]  
[vocals: inuit katajjaq duet, inhaled/exhaled pulses, antiphonal breath riffs, non-lexical]  
[key: percussive/drone center]  
[time_signature: 4/4]  
[weirdness: 62]  
[audio_weight: 44] [style_weight: 51]

[sequence: cold-room, pulse, drop, breath-duel, drop, dusk-coda]  
[cold-room]  
[pulse]  
[drop]  
[breath-duel]  
[drop]  
[dusk-coda]

[lyrics]  
[verse]  
[refrain]  
[verse]  
[bridge]  
[refrain]
```

#### Distro media kit (sidecar)
title: "Breath on the Floor (Gqom)"  
primary_persona: "New seed (Arctic-Club branch)"  
bpm: 125  
key: (percussive/drone)  
tags: ["gqom","katajjaq","breath percussion","non-lexical","minimalist club"]  
mood_pitch: "A dance floor carved from breath and broken kicks."  
cover_art_master_spec: "Square 1:1; poster layout with blank bottom panel. Condensed breath rings on cold concrete forming a gqom grid; no in-image text."  
canvas_ideas: ["Breath puffs syncing to kick grid","Reverse-grain ripples racing across the floor"]  
provenance_notes: "Synthetic katajjaq behavior; no field recordings."  
usage_rights: "Original generative composition."  
embedding_notes: "Tag gqom/katajjaq; AI provenance; non-lyrics policy."

#### Status

Planned

---

## 3. Background music (BGM) base templates

### 1. Ambient / Drone (cinematic, evolving)

**Makeshift title:** Soft Engine, Far Horizon

#### Style of Music
- **v5.0 (long):** Evolving cinematic-ambient bed: airy analog pads and granular textures drift in slow harmonic arcs; distant bowed tones and soft sub bloom every 16–32 bars; no hook—just depth, warmth, and movement that stays under dialogue.
- **v4.x (short):** Evolving cinematic-ambient pads with subtle swells; warm, spacious underscore, no top-line.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: ambient, cinematic-underscore]
[style: minimal, evolving, wide, textural]
[mood: calm, warm, contemplative]
[instruments: analog-pads, granular-drones, bowed-textures, soft-sub, felt-piano-dust]
[signal-processing: reverb, delay, chorus, saturation]
[length: 300-360]
[sequence: intro, bed A, lift, bed B, coda]

[intro: soft fade-in; distant air; pad bloom from low mids]
[bed A: slow harmonic drift; no lead; occasional granular sparkle]
[lift: gentle density increase; bowed texture swells + soft-sub bloom]
[bed B: slightly brighter pad voicings; widen image; keep dynamics restrained]
[coda: long tail into near-silence; last pad held and thinned]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
A cinematic ambient bed of airy analog pads and granular drones; distant bowed textures, soft sub swells, felt-piano dust; evolving every 16–32 bars; no lead; dialog-friendly depth and warmth.  
**Riffusion meta-controls (optional):**  
- `influence_prompt: medium`  
- `influence_lyrics: low` (we’re using tags only as scaffolding)  
- `structure_hint: intro | bed A | lift | bed B | coda`

#### Canvas loop (Spotify)
- **Scene:** Slow aerial drift over a sunlit cloud sea.  
- **Action:** Pads “breathe” as cloud shadows glide beneath.  
- **FX:** Subtle parallax; faint grain; slow bloom pulses.  
- **Palette:** Pearl white, soft teal, pale amber.  
- **Style:** Minimal, meditative cinematography.  
- **Loop idea:** Start mid-drift → subtle zoom forward → crossfade back to starting frame.

#### First-frame still (cover art prompt)
Aerial, sunlit cloudscape from above; gentle haze; soft film grain; wide negative space for text; mood: calm, contemplative; colors: pearl white, soft teal, pale amber.

#### Bandcamp/Spotify blurb (poetic/meta)
A bed that breathes like a distant engine—no destination, only horizons. Pads rise and fall in slow cycles, leaving enough air for memory and voice to carry.

#### Why this fits (notes)
- Starts with `[instrumental]` and control tags upfront so v5 does not invent vocals; this has higher adherence in v4.5/v5 than earlier versions. 
- `[sequence]` placed right before sections to keep long-form cohesion and better Extend behavior. 
- Uses confirmed tags only; avoids weak/obsolete ones like `[loop]` or `[mix]`. 

---

### 2. Lo-fi Hip-Hop / Chillhop

**Makeshift title:** Dust Warmth, Soft Steps

#### Style of Music
- **v5.0 (long):** Dusty chillhop bed with swung soft-kick/snare, low-passed Rhodes chords, nylon-guitar chops, vinyl haze and round sub; occasional muted mallet flourishes; loop-feeling phrases with gentle A/B variation; no hooky top-line.
- **v4.x (short):** Dusty chillhop: Rhodes, vinyl haze, soft drums; warm, no top-line.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, laid-back swing]
[genre: lo-fi-hip-hop, chillhop]
[style: dusty, warm, cozy]
[mood: relaxed, nocturnal, mellow]
[instruments: rhodes, nylon-guitar-chops, sub-bass, soft-kick, brushed-snare, muted-mallets]
[signal-processing: saturation, light reverb, short delay]
[length: 210-240]
[sequence: intro, groove A, groove B, break, groove A2, outro]

[intro: vinyl hiss + filtered rhodes; soft-kick enters late]
[groove A: rhodes + nylon chops; brushed-snare; round sub; no lead]
[groove B: add muted mallets + gentle chord extensions for lift]
[break: drums thin; rhodes solo voicings; brief tape-stop wobble]
[groove A2: original kit returns with subtle percussion layer and slightly brighter rhodes]
[outro: filter down; leave vinyl hiss and a final rhodes tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Dusty chillhop bed with swung soft-kick/snare, low-passed Rhodes, nylon-guitar chops, round sub, vinyl haze; A/B groove variation; relaxed and nocturnal; **no lead**—kept under voiceover.  
**Riffusion meta-controls (optional):**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | groove A | groove B | break | groove A2 | outro`

#### Canvas loop (Spotify)
- **Scene:** Turntable close-up in lamplight.  
- **Action:** Tonearm hovers; dust motes drift; subtle platter spin.  
- **FX:** Light film grain; occasional tape-wobble.  
- **Palette:** Sepia, umber, smoked blue.  
- **Style:** Cozy, analog micro-cinema.  
- **Loop idea:** Slow push-in to label → micro-wobble → reset to wider shot.

#### First-frame still (cover art prompt)
Warm desk lamp over a spinning vinyl, soft dust particles in beam; intimate, analogue vibe; shallow depth of field; sepia/umber/smoked-blue palette.

#### Bandcamp/Spotify blurb (poetic/meta)
A pocket of lamplight where the needle never quite lands—soft drums and Rhodes drift in a slow-swing loop that makes space for thought.

#### Why this fits (notes)
- Instrumental bed with soft transients and no lead; `[instrumental]` prevents v5 vocal bleed-through. 
- Uses `[signal-processing]` for era feel (saturation/short delay), consistent with your tag reference. 
- Sequence ensures gentle variation without hook repetition. 

---

### 3. Piano Underscore (neo-classical / felt piano)

**Makeshift title:** Quiet Room, Open Window

#### Style of Music
- **v5.0 (long):** Intimate felt-piano underscore with soft attack and legato phrasing; slow, breath-like dynamics and gentle pedal ambience; small, repeating motifs that evolve subtly every 16–32 bars; wide room reverb; no melody spotlight—supportive, narrative, voiceover-friendly.
- **v4.x (short):** Intimate felt-piano bed; soft attack, legato phrasing; subtle motif shifts; supportive, VO-friendly.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: neo-classical, underscore]
[style: intimate, minimal, spacious]
[mood: reflective, tender, calm]
[instruments: felt-piano, soft-sub, room-reverb, subtle-mallets]
[articulation: legato]
[attack: soft]
[length: 210-300]
[sequence: intro, motif A, motif B, interlude, motif A2, coda]

[intro: single soft notes; pedal ambience; room tone]
[motif A: 2–4 note figure; slow left-hand underpin; no lead flourish]
[motif B: slight harmonic color change; +hint of soft-sub for warmth]
[interlude: thin texture; sparse voicings; hold space for narration]
[motif A2: return to A with gentle variation (upper extension, lighter velocity)]
[coda: decay into room; final chord fade; long tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Intimate felt-piano underscore with soft attack, legato phrasing, gentle pedal ambience, and wide room reverb; small evolving motifs every 16–32 bars; **no lead spotlight**, voiceover-friendly depth and calm.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | motif A | motif B | interlude | motif A2 | coda`  
- `duration: 210–300`

#### Canvas loop (Spotify)
- **Scene:** Morning light across a piano’s felt hammers.  
- **Action:** Dust motes drift; keys depress slowly (macro).  
- **FX:** Gentle bloom; soft grain.  
- **Palette:** Warm cream, pale gold, muted walnut.  
- **Loop idea:** Slow push-in to keys → micro-glint → dissolve back.

#### First-frame still (cover art prompt)
Macro of felt-piano hammers in warm morning light; shallow depth; soft grain; spacious negative area for text.

#### Blurb
A room that breathes in quarter notes—tiny motifs turning like pages, leaving silence wide enough for stories.

---

### 4. Minimal Piano + Strings (documentary bed)

**Makeshift title:** Lines on the Map

#### Style of Music
- **v5.0 (long):** Documentary-friendly bed for felt-piano and light chamber strings; con-sordino-like softness, long legato lines, and subtle low percussion swells; gentle A/B texture shifts without a prominent lead; stable harmony with modest lifts; designed to sit under narration.
- **v4.x (short):** Minimal felt-piano + soft chamber-strings; gentle lifts; no strong lead; documentary bed.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: cinematic-underscore, documentary]
[style: sparse, supportive, airy]
[mood: warm, thoughtful, steady]
[instruments: felt-piano, chamber-strings-con-sordino, warm-bass, soft-brush-kit, airy-pads]
[articulation: legato]
[attack: soft]
[signal-processing: reverb, light saturation]
[length: 240-330]
[sequence: intro, bed A, lift, bed B, outro]

[intro: piano + air; strings enter as a soft pad]
[bed A: steady pulse from piano; strings long lines; no motif lead]
[lift: add gentle low swell (warm-bass or soft-brush roll); +5–10% density]
[bed B: same harmony with brighter voicing; maintain restraint]
[outro: subtractive fade; piano tail + string harmonics]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Minimal felt-piano and soft chamber strings (con-sordino character), gentle brush-kit rolls, warm bass swells; airy, supportive documentary bed with A/B texture shift and restrained lift; **no prominent lead**, narration-first mix.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | bed A | lift | bed B | outro`  
- `duration: 240–330`

#### Canvas loop (Spotify)
- **Scene:** Archival map lines sliding beneath glass.  
- **Action:** Slow pan; ink lines appear and fade.  
- **FX:** Paper grain; light bloom.  
- **Palette:** Bone white, graphite gray, desaturated teal.  
- **Loop idea:** Pan left → slight zoom → reset to starting quadrant.

#### First-frame still (cover art prompt)
Archival paper map under soft glass reflection; clean typography space; bone/graphite/teal tones; quiet, factual mood.

#### Blurb
Measured steps across a page—piano tracing the route, strings holding the weather steady.

---

### 5. Cinematic Underscore (low percussion)

**Makeshift title:** Quiet Faultline

#### Style of Music
- **v5.0 (long):** Quiet cinematic underscore centered on soft, low percussion pulses (taiko/frame/low-tom) beneath bowed drones and faint string/air textures; restrained, tension-to-release arcs; no thematic lead, only pressure changes, sub-blooms, and space—dialog-friendly and steady over time.
- **v4.x (short):** Sparse cinematic bed with soft low-percussion pulses, bowed drones, subtle lifts; no lead.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: cinematic-underscore, ambient]
[style: sparse, atmospheric, restrained]
[mood: tense, anticipatory, controlled]
[instruments: low-tom, soft-taiko, frame-drum, sub-boom, bowed-drones, airy-strings, felt-piano-dust]
[sfx: distant-wind-hum, room-tone]
[signal-processing: long-reverb, light-saturation]
[length: 270-330]
[sequence: intro, bed A, rise, bed B, coda]

[intro: air + bowed-drone; single distant drum pre-echo]
[bed A: soft pulse (low-tom/frame); no motif; drones shift every 16–32 bars]
[rise: +1 drum layer (soft-taiko rolls) and subtle sub-boom; keep dynamics under VO]
[bed B: slightly brighter string voicings; widen image; maintain restraint]
[coda: subtractive fade; leave air + distant harmonic]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Quiet cinematic underscore of soft low-percussion pulses (taiko/frame/low-tom) under bowed drones and airy strings; restrained tension arcs, occasional sub-boom swells, no lead; dialog-friendly, steady pressure and space.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | bed A | rise | bed B | coda`  
- `duration: 270–330`  
- `seed: set for versioning`

---

### 6. Downtempo / Trip-hop

**Makeshift title:** Smoke in the Halflight

#### Style of Music
- **v5.0 (long):** Moody downtempo bed with soft-kick + rimshot groove, brushed hats, round sub, filtered e-piano, muted analog synth phrases, and faint tape wobble; A/B texture shifts and a short break; no hooky topline—kept low and smoky for narration.
- **v4.x (short):** Moody trip-hop bed: soft-kick/rim, filtered e-piano, round sub; A/B textures; no top-line.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, laid-back swing]
[genre: downtempo, trip-hop]
[style: moody, understated, smoky]
[mood: nocturnal, introspective]
[instruments: filtered-epiano, muted-synth, round-sub, soft-kick, rimshot, brushed-hats, vinyl-hiss]
[signal-processing: saturation, short-delay, plate-reverb, tape-wobble]
[length: 210-270]
[sequence: intro, groove A, groove B, break, groove A2, outro]

[intro: filtered epiano + hiss; drums enter late]
[groove A: soft-kick/rim; epiano chords; round sub; no lead]
[groove B: add muted-synth phrases; tiny percussive garnish; keep level low]
[break: thin drums; epiano alone with tape-wobble moment]
[groove A2: original kit; slightly brighter epiano voicings; maintain restraint]
[outro: filter down; leave hiss + last chord tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Moody trip-hop/downtempo bed: soft-kick + rim groove, brushed hats, round sub, filtered e-piano chords, muted analog synth phrases, light tape wobble; A/B texture shift and brief break; **no top-line**, narration-first mix.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | groove A | groove B | break | groove A2 | outro`  
- `duration: 210–270`  
- `seed: set for versioning`

---

### 7. Deep / Chill House

**Makeshift title:** Soft Shore Pulse

#### Style of Music
- **v5.0 (long):** Uncluttered deep/chill house bed with soft four-on-the-floor kick, airy pads, warm rounded bass, light chord stabs and shakers; gentle A/B textural shifts and a short breakdown; no topline hook—kept understated and voiceover-friendly.
- **v4.x (short):** Minimal deep/chill house: soft 4-on-the-floor, airy pads, warm bass, light stabs; no topline.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: deep-house, chill-house]
[style: uncluttered, airy, understated]
[mood: warm, relaxed, uplifting]
[instruments: soft-kick-4onfloor, airy-pads, warm-bass, light-chord-stabs, shaker, soft-clap]
[signal-processing: gentle-sidechain, chorus, delay, light-saturation]
[length: 240-330]
[sequence: intro, groove A, groove B, breakdown, groove A2, outro]

[intro: filtered pads + soft noise; kick fades in late]
[groove A: soft 4-on-the-floor; warm-bass; light chord stabs; no lead]
[groove B: add airy top pad + subtle percussive sparkle; keep dynamics modest]
[breakdown: kick drops; pads and bass breathe with sidechain feel; no new motif]
[groove A2: original groove returns with slightly brighter chords; maintain restraint]
[outro: gradual filter-down; leave pad tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Minimal deep/chill house bed: soft 4-on-the-floor kick, airy pads, warm rounded bass, light chord stabs, gentle shaker and soft clap; short breakdown and A/B texture shift; **no topline**, narration-first mix.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | groove A | groove B | breakdown | groove A2 | outro`  
- `duration: 240–330`  
- `seed: set for versioning`

---

### 8. Liquid DnB (light)

**Makeshift title:** Glass River Run

#### Style of Music
- **v5.0 (long):** Light, airy liquid DnB bed with soft rolling breaks, warm sub, shimmering pads, and gentle piano/keys washes; optimistic lift without big leads; A/B groove colors and a restrained rise; kept smooth under narration.
- **v4.x (short):** Light liquid DnB: soft rolling breaks, warm sub, shimmer pads, airy piano; no strong lead.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: liquid-dnb, drum-and-bass]
[style: rolling, airy, optimistic]
[mood: buoyant, smooth, spacious]
[instruments: soft-breaks, warm-sub, shimmer-pads, airy-piano, subtle-arp, brushed-percussion]
[signal-processing: light-reverb, short-delay, gentle-saturation]
[length: 210-270]
[sequence: intro, groove A, lift, groove B, outro]

[intro: shimmer-pad + airy-piano hints; break filters in]
[groove A: soft rolling break + warm-sub; pads float; no lead]
[lift: add subtle-arp and slight chord brightness; +5–10% energy only]
[groove B: keep break consistent; alternate pad voicings; maintain restraint]
[outro: break filters down; pads linger; soft tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Light, airy liquid DnB bed with soft rolling breaks, warm sub, shimmering pads, airy piano washes, and a gentle optimistic lift; A/B color shift; **no strong lead**, narration-friendly dynamics.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | groove A | lift | groove B | outro`  
- `duration: 210–270`  
- `seed: lock for iterations`

---

### 9. Indie-Folk Hush

**Makeshift title:** Pine Needles & Porcelain

#### Style of Music
- **v5.0 (long):** Whisper-quiet indie-folk bed with delicate nylon/steel plucks, soft brush-kit, upright bass murmur, glockenspiel flickers, and hush-pads; intimate room tone, close-mic detail; subtle A/B texture changes and a modest lift; absolutely no vocal-like top-line—pure narrative support.
- **v4.x (short):** Delicate indie-folk bed—plucked guitars, brush-kit, upright bass, glockenspiel; no top-line.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: indie-folk, acoustic]
[style: delicate, narrative, intimate]
[mood: warm, wistful, calm]
[instruments: nylon-guitar, light-steel-plucks, brush-kit, upright-bass, glockenspiel, hush-pads]
[articulation: legato]
[attack: soft]
[signal-processing: room-reverb, light-saturation, subtle-tape]
[length: 210-300]
[sequence: intro, bed A, lift, bed B, outro]

[intro: finger-noise + room tone; nylon-guitar enters solo]
[bed A: nylon + brush-kit + upright-bass murmur; no lead; glock chimes sparingly]
[lift: +hush-pads and gentle double-stop guitar; +5–10% energy only]
[bed B: same harmony with brighter mic position; tiny percussive garnish]
[outro: subtractive fade; last harmonic ring + room tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Whisper-quiet indie-folk bed: nylon/steel plucks, soft brush-kit, upright bass murmur, sparse glockenspiel, hush pads; subtle A/B textures and a modest lift; **no vocal-like lead**, narration-first mix.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | bed A | lift | bed B | outro`  
- `duration: 210–300`  
- `seed: set for versioning`

---

### 10. Bossa-Lounge / Jazz Café

**Makeshift title:** Quiet Sugar on the Rim

#### Style of Music
- **v5.0 (long):** Soft bossa-lounge bed with nylon-guitar comping, gentle ride-cymbal, brushed snare, upright bass walk in half-time feel, and warm Rhodes/keys; airy A/B color shift and short breakdown; relaxed, sun-lit, and firmly under narration with no soloistic top-line.
- **v4.x (short):** Soft bossa-lounge: nylon-guitar, ride, brushes, upright bass, warm keys; no solo lead.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: bossa-lounge, jazz-cafe]
[style: smooth, understated, airy]
[mood: relaxed, sunny, cozy]
[instruments: nylon-guitar, upright-bass, ride-cymbal, brushed-snare, warm-keys, shaker]
[articulation: legato]
[attack: soft]
[signal-processing: plate-reverb, gentle-saturation]
[length: 240-330]
[sequence: intro, groove A, groove B, breakdown, groove A2, outro]

[intro: soft keys + shaker; nylon-guitar enters quietly]
[groove A: nylon comping + upright walk; ride-cymbal light; no melodic lead]
[groove B: Rhodes/keys add lush voicings; keep level modest]
[breakdown: drums thin to ride + shaker; bass and guitar breathe]
[groove A2: original groove returns with slightly brighter chords]
[outro: plate tail; final nylon chord]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Soft bossa-lounge / jazz café bed: nylon-guitar comping, upright bass, gentle ride + brushes, warm Rhodes/keys, light shaker; A/B texture shift with a short breakdown; **no solo top-line**, narration-first dynamics.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | groove A | groove B | breakdown | groove A2 | outro`  
- `duration: 240–330`  
- `seed: set for iteration control`

---

### 11. Synthwave / Chillwave Pads

**Makeshift title:** Neon Tide Sleep

#### Style of Music
- **v5.0 (long):** Pad-centric synthwave/chillwave bed: wide chorus-pads, slow analog arps, warm rounded bass, and gentle noise-beds; dreamy, nostalgic drift with micro swells every 16–32 bars; no melodic topline—kept hazy and voiceover-friendly.
- **v4.x (short):** Pad-led synthwave/chillwave: slow arps, warm bass, wide chorus-pads; no lead.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: synthwave, chillwave]
[style: nostalgic, dreamy, pad-centric]
[mood: warm, nocturnal, reflective]
[instruments: chorus-pads, slow-analog-arps, warm-bass, noise-bed, analog-keys, soft-hats]
[signal-processing: chorus, delay, tape-saturation, plate-reverb]
[length: 240-330]
[sequence: intro, bed A, lift, bed B, outro]

[intro: noise-bed + soft keys; pads fade in wide]
[bed A: chorus-pads + warm-bass; slow-analog-arp tucked low; no lead]
[lift: +brightness on pads and a second, slower arp layer; +5–10% density only]
[bed B: alternate pad voicings; slightly wider image; maintain restraint]
[outro: filter down; leave tape hiss + pad tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Pad-centric synthwave/chillwave bed with wide chorus-pads, slow analog arps, warm rounded bass, and a gentle noise-bed; subtle lifts and A/B color; **no melodic topline**, narration-first dynamics.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | bed A | lift | bed B | outro`  
- `duration: 240–330`  
- `seed: set for consistent iterations`

---

### 12. Post-Rock Light

**Makeshift title:** Lanterns in the Mist

#### Style of Music
- **v5.0 (long):** Gentle post-rock bed focused on clean guitar arpeggios, shimmer pads, soft tom pulses, and airy strings; gradual build and echo-fall without anthem-style peaks; emotive but restrained, leaving ample space under narration.
- **v4.x (short):** Light post-rock: clean arpeggios, shimmer pads, soft toms; slow build; no big lead.

#### Lyrics (meta-tags)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[genre: post-rock, cinematic]
[style: gradual, emotive, restrained]
[mood: hopeful, spacious, calm]
[instruments: clean-guitars-arpeggio, shimmer-pads, soft-toms, warm-bass, airy-strings, subtle-mallets]
[signal-processing: delay, reverb, light-saturation]
[length: 270-360]
[sequence: intro, build A, build B, echo-fall, outro]

[intro: single guitar pattern + reverb tail; pads bloom quietly]
[build A: add soft-toms and warm-bass; no lead; steady motion]
[build B: +airy-strings and subtle-mallets; widen image; keep ceiling moderate]
[echo-fall: subtract drums; let delays and pads trail; gentle harmonic afterglow]
[outro: final guitar harmonics; long reverb tail]
[end]
```

#### Producer.ai (Riffusion / FUZZ-2.0) — Sound prompt
Light post-rock underscore with clean guitar arpeggios, shimmer pads, soft tom pulses, warm bass, and airy strings; gradual dual-stage build and echo-fall; **no anthem lead**, narration-friendly headroom.  
**Optional meta-controls:**  
- `influence_prompt: medium-high`  
- `influence_lyrics: low`  
- `structure_hint: intro | build A | build B | echo-fall | outro`  
- `duration: 270–360`  
- `seed: lock for version exploration`

---

### Template name

#### Style of Music

#### Lyrics

---

# Appendix A1. BGM Tag Kit

**Usage note:** Start every bed with `[instrumental]`. Keep controls compact; avoid weak/obsolete tags. Place `[sequence]` immediately before any section tags.

### Common controls (safe defaults)
```
[instrumental]
[control: instrumental, no-repeat, dynamic transitions]
[mood: calm, warm]
[length: 240-360]
```

### Safe instrument palettes by style (swap freely)
- **Ambient/Drone:**  
  `[instruments: analog-pads, granular-drones, bowed-textures, soft-sub, felt-piano-dust]`  
  `[signal-processing: reverb, delay, chorus, saturation]`

- **Lo-fi / Chillhop:**  
  `[instruments: rhodes, nylon-guitar-chops, sub-bass, soft-kick, brushed-snare, muted-mallets]`  
  `[signal-processing: saturation, light reverb, short delay, vinyl-hiss]`

- **Piano Underscore (felt):**  
  `[instruments: felt-piano, soft-sub, airy-strings, subtle-mallets]`  
  `[articulation: legato] [attack: soft]`

- **Minimal Piano + Strings (doc bed):**  
  `[instruments: felt-piano, chamber-strings, soft-brush-kit, warm-bass]`  
  `[style: sparse, supportive]`

- **Cinematic Underscore (low percussion):**  
  `[instruments: low-tom, soft-taiko, bowed-drones, airy-strings, sub-boom]`  
  `[sfx: distant-wind-hum]`

- **Downtempo / Trip-hop:**  
  `[instruments: muted-synth, filtered-epiano, round-sub, soft-kick, rimshot, brushed-hats]`  
  `[style: moody, understated]`

- **Deep/Chill House:**  
  `[instruments: soft-kick-4onfloor, airy-pads, warm-bass, light-chord-stabs, shaker]`  
  `[style: uncluttered, no-topline]`

- **Liquid DnB (light):**  
  `[instruments: soft-breaks, warm-sub, airy-pianos, shimmer-pads]`  
  `[style: rolling, optimistic]`

- **Indie-Folk Hush:**  
  `[instruments: nylon-guitar, glockenspiel, brush-kit, upright-bass, hush-pads]`  
  `[style: delicate, narrative]`

- **Bossa-Lounge / Jazz Café:**  
  `[instruments: nylon-guitar, ride-cymbal, upright-bass, soft-keys]`  
  `[articulation: legato]`

- **Synthwave / Chillwave Pads:**  
  `[instruments: chorus-pads, slow-arps, warm-bass, noise-bed]`  
  `[signal-processing: chorus, delay, saturation]`

- **Post-Rock Light:**  
  `[instruments: clean-guitars-arpeggio, airy-strings, soft-toms, shimmer-pads]`  
  `[style: gradual, emotive]`

### Length ranges (by purpose)
- Social/short form: `[length: 120-150]`  
- Standard bed: `[length: 210-300]`  
- Long ambience: `[length: 300-420]`

### Sectioning scaffolds (pick one and customize)
- **Simple bed:**  
  ```
  [sequence: intro, bed, lift, bed, outro]
  ```
- **A/B texture swap:**  
  ```
  [sequence: intro, bed A, bed B, bed A2, coda]
  ```
- **With break:**  
  ```
  [sequence: intro, bed A, break, bed B, outro]
  ```

---

# Appendix A2. Extend-Safe Structure Cheat-Sheet (long ambiences, v5)

**Goals:** predictable 4–7 min arcs; safe variation without “new song” pivots; dialog-friendly dynamics.

### 1) “Breathing Bed” (gentle rise/fall)
```
[length: 300-420]
[sequence: intro, bed A, lift, bed B, coda]

[intro: soft fade; low-mid pads only]
[bed A: slow harmonic drift; no lead]
[lift: +10–15% density; add one new layer (bowed texture / light percussion bloom)]
[bed B: maintain lift elements; slightly brighter voicings or widened image]
[coda: subtractive fade; leave tail + noise/air]
[end]
```
**Why it extends well:** one additive “lift” only; B mirrors A with tiny timbre shift; safe for repeated Extend without motif creep.

### 2) “A/B Textures” (color change, same harmony)
```
[length: 300-390]
[sequence: intro, bed A, bed B, bed A2, outro]

[intro: filtered source; establish space]
[bed A: primary texture set]
[bed B: swap pad engine (chorus vs granular), keep harmony + rhythm identical]
[bed A2: return to A with micro-variation (extra shimmer / gentle sub bloom)]
[outro: long tail; no new content]
[end]
```
**Why it extends well:** alternation provides variety without new themes; A2 signals “return,” aiding coherence.

### 3) “Bed + Break” (brief negative space)
```
[length: 300-360]
[sequence: intro, bed, break, lift, bed, coda]

[break: drums thin OR pads filter down; keep low noise-floor so it doesn’t feel like a cut]
[lift: re-introduce elements with +1 layer only]
```
**Why it extends well:** the break resets ear fatigue; the single-step lift avoids runaway climaxes on repeated Extend.

### General do/don’t for Extend
- **Do:** one new element per lift, small imaging changes (wider/narrower), filter moves, velocity softening.  
- **Don’t:** introduce strong leads, hard hits, or new chord vocab after the first minute.  
- **Keep:** `[control: dynamic transitions]`, and finish each section with a tail so Extend seams hide in reverb.

---

# Appendix B. Producer.ai (Riffusion FUZZ-2.0) Side-by-Side Workflow

### When to prefer **Suno v5.0**
- You need **strict instrumental control** (no surprise vocals).  
- You rely on **[sequence]** semantics and long-form cohesion.  
- Persona/cover workflows (Producer.ai lacks Persona; Suno wins for persona-amplified styles).

**Suno quick spec**
- Start with `[instrumental]`, place controls first.  
- `[sequence]` immediately before sections; keep one additive “lift.”  
- Avoid unsupported/noisy tags (no `[bpm]`, no `[language]`).

### When to prefer **Producer.ai (FUZZ-2.0 / Raw)**
- You want **fast textural variation** from the same prompt.  
- You need **phrasal groove** beds (lo-fi, house, dnb) with quick A/B alternates.  
- You’re doing **dual-service fishing** (generate in both and pick the cleaner bed).

**Producer.ai baseline settings (beds)**
- **Sound prompt:** (use the same “long” Style-of-Music line you give Suno; explicitly say “no lead / dialog-friendly”).  
- **Meta-controls (if available):**  
  - `influence_prompt: medium–high`  
  - `influence_lyrics/tags: low` (or omit)  
  - `structure_hint:` mirror your Suno sequence names (`intro | bed A | lift | bed B | coda`)  
  - `duration:` 180–360 s  
  - `seed:` set if you’ll version-hunt

### Re-render / pick criteria (A/B selection)
1) **Noise floor & transients**  
   - Reject if hiss/crackle overtakes quiet passages (unless intended lo-fi).  
   - Prefer soft transients (no sudden spikes that fight VO).

2) **Midrange congestion (1–3 kHz)**  
   - Prefer mixes that leave space for voice; avoid pokey leads or harsh pads.

3) **Section clarity**  
   - You should “hear” the sequence markers (A → lift → B) without new themes appearing.

4) **Loop/Extend seams**  
   - Prefer versions with long tails and steady ambiences; seams should hide naturally.

5) **Persona/brand fit**  
   - If bed carries subtle vocal-like formants, choose Suno for tighter suppression; otherwise Producer.ai can bring nice grit.

### Dual-service recipe (practical)
- **Step 1:** Draft once (Suno tags + long Style text).  
- **Step 2:** Render in **Suno v5.0** + **Producer.ai FUZZ-2.0**.  
- **Step 3:** Rate 1–5 on: *VO space, dynamics smoothness, section clarity, ear-fatigue (5-min listen).*  
- **Step 4:** If neither passes, **reduce elements** (drop a layer, lower “lift” intensity) and re-render both with the same seed (Producer.ai) or same tags (Suno).  
- **Step 5:** Archive winner + exact text/controls for reproducibility.
