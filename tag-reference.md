# Suno meta-tags

Last modified: 2025, November 19.

## Suno service news (updated: September 24, 2025): model v5.0

Starting from September, Suno began deploying version 5.0 of their model.

The model is richer in polyphony, in vocals implementations and better implements the in-tag instructions.
 
**New v5.0 capabilities (confirmed November 2025):**
**Genre mashups** now work reliably (e.g., `[genre: midwest emo + neosoul]`)
**Natural language tempo descriptors** (e.g., `[tempo: mid-tempo 90s hip-hop swing]`)
**Enhanced prompt parsing** for embedded tags in conversational text

## Suno service news (updated: July 18, 2025): model v4.5+

On 18-th of July Suno has released for paid subscriptions, access to a new model, "v4.5+"

The initial tests showed that v4.5+ generated more variable, richer tracks with better polyphony and overall quality. Typical restrictions are the same as for v4.5. It's not yet known if there are changes in how v4.5+ interprets meta-tags.

Also, the "Inspo" tool has been added to tracks generation UI. That, according to the UI hint, uses songs from specified playlist as "source for inspiration" In practice, Suno blends the "inspiring" tracks, making kind of pot pourri  in the output. No formal definitions for "Inspo" was officially done yet.

## Riffusion relation

Since April 27, 2025 Riffusion.com audio tracks generation service (very much like Suno) introduced paid levels of membership and a new model FUZZ-1.0 Pro.

After 400+ generations that were first tested in Suno and then in Riffusion ("Style of Music" at Suno going to "Sound" prompt at Riffusion; "Lyrics" going to "Lyrics") it was discovered that Riffusion  generally follows the same set of official and user-tested meta-tags known for Suno.

## Known misbehaving tags/tags values (consider obsolete)

| Tag | Status | Notes |
|-----|--------|-------|
| `[autotune: ...]` | ❌ Unsupported |  |
| `[filter: ...]` | ❌  Inefficient |  |
| `[loop: ...]` | ❌ Unsupported |  |
| `[mix, mixing: ...]` | ❌ Inefficient |  |
| `[master: ...]` | ❌ Inefficient |  |
| `[pan, panning: ...]` | ❌ Inefficient |  |
| `[style: none]` | ❌ Invalid | "none" is not interpreted as a meaningful style. Will confuse output. |
| `[section: ...]` | ❌ Redundant | Rejected or misread; use `[intro: ...]`, `[verse: ...]` etc. |
| `[theme: ...]` | ❌ Invalid | unlabelled  theme tag is ignored or causes parsing errors, use [theme A: ...] etc. |
| `[volume: ...]` | ❌  Inefficient |  |

## Tips on using meta-tags

1. **Use only known or confirmed tags.**
2. **Avoid alias or ambiguous tags** like `bpm`, `key`, `language`.
3. **Test in Standalone mode first** — many tags that break in Extend or Cover work fine solo.
4. If in doubt, **use "[style: experimental]"** or "[control: hallucinatory]" to encourage flexible output instead of forcing 

## Parsing Note for Suno v4.0+

- Any **unrecognized tag** (e.g. `[emotion build]`, `[tense development]`) is treated as a generic **[section X: ...]** tag.

- Use colon syntax to embed directives safely:
  ```
  [tense development: Style and mood of the theme gets more tense until a climactic counterpoint is reached]
  ```
- Avoid placing instruction text **outside** the tag, as it will be **sung/spoken**:
  ```
  [tense development]
  Style and mood... ← ❌ becomes lyrics
  ```
- Avoid inserting lyrics/text to sing as [verse] colon notation: the engine will only sing that text if doesn't  find obvious rendering directives; place the verse lyrics immediately below its [verse] tag

- To prevent looping: do not repeat identical lyrics or tag sections verbatim; add variation or split across multiple [verse A], [verse B] etc.

- For structure: always include [sequence: ...] to control order when extending or building long-form compositions.

## Version-Dependent Differences in Tag Behavior (v4.0 vs v4.5)  

Suno v4.0 and v4.5 share the same meta-tag system in spirit, but **there are notable differences in how tags are interpreted and how reliably they influence the music** between these two versions. Key version-dependent differences include:

- **Natural Language Prompting**: Suno **v4.5 is significantly better at understanding descriptive, sentence-form prompts with embedded tags**, whereas v4.0 tended to respond mostly to more rigid, shorthand tags. In v4.0, users often listed a sequence of tags or keywords (e.g. `[Intro]`, `[Verse]`, `[Chorus]`, or `Mood: energetic | Genre: Pop | Vocals: Female` etc.) and kept instructions terse. With v4.5, the model can parse richer language around tags. The Suno v4.5 update was tuned to *"understand and translate your descriptions"* of mood, instruments, and style with more nuance. An official guide notes that *v4.5 still supports the old bracket tags format, **"but now responds better when those tags are embedded into natural, full-sentence instructions."***. In short, **v4.0 required more prompt "keyword telegraphing," while v4.5 allows a more conversational prompt with tags inside it**. For example: instead of just writing `[Chorus: anthemic]`, a v4.5 user might write a full line like "The **[chorus]** should hit with **[anthemic]** vocal harmonies and huge drums," and v4.5 will follow that more accurately than v4.0 would. This reflects improved prompt adherence in v4.5. Users have found they can be more verbose and specific in v4.5 without confusing the model. 

- **Prompt Adherence and Reliability**: Overall **v4.5 is more reliable in obeying meta-tags than v4.0 was**. Suno v4 sometimes ignored or only loosely followed tags (especially complex style directives), leading to user frustration. In fact, some early v4.0 users complained that *"I can’t get Suno to obey the style tags, it’s as if they are not used at all..."*. By contrast, v4.5’s improved prompt fidelity means tags like `[Intro]`, `[Bridge]`, `[Mood: X]`, etc., *more consistently shape the output*. A Redditor noted that *"steering the final product with style tags is a lot better now [in 4.5]"* and that they can even use more natural phrasing instead of hunting for the perfect v4-era keyword. In summary, where v4.0 might *gloss over* a bracket tag or require multiple re-rolls to get the effect, v4.5 more often gets it right on the first try (especially for genre and mood tags, thanks to prompt adherence improvements).

- **Structural Tags and Song Length**: Both versions support tags like `[Verse]`, `[Chorus]`, etc., but **v4.5 can handle longer structures**. Suno v4.0 was limited to about ~4 minutes of song, often requiring an *Extend* feature to continue. In v4.5 the max length doubled to 8 minutes, and the model maintains coherence over that length. This means tags delineating multiple verses and choruses (or multiple `[Theme A]`, `[Theme B]` sections in a long piece) are more feasible in v4.5. The tags themselves didn’t change, but the *behavior* is that v4.0 sometimes truncated or ignored later structural tags if the song was too long, whereas v4.5 can actually execute a full structure from intro to extended outro with all tags accounted for. Additionally, v4.5 introduced an **improved "Cover+Persona" mode** and better *Extend*, but those are features beyond the lyric meta-tags (except that `[extend-style]` tag from the doc is less needed now since v4.5 can natively go long).

- **Deprecated vs Replacement Tags**: The transition from earlier versions to v4 introduced some tag deprecations. For example, as noted above, **`[sing-style]` was used in Suno’s early alpha** but by v4.0 it was replaced by `[vocal-style]`. Similarly, **`[song-type]` was an early tag** to indicate if the piece should be a song, rap, instrumental, etc., but by v4.0 it was rendered inert. Another subtle change: older prompts sometimes used `[style]` for genre/style, but in v4.0+ it became more effective to use `[genre:]` and specific style qualifiers (because "[style: none]" had proven invalid and you needed to actually name a style). These differences were captured in the documentation’s errata, but it’s worth noting they specifically affect **v3-era vs v4-era usage**. By the time of v4.0, those older tags were already phased out, and v4.5 continued to ignore them. In practical terms, a user coming from Suno v3.5 to v4.0 had to unlearn a tag like `[bpm]` or `[section]`. But between v4.0 and v4.5, there were *not* many new deprecations - mostly improvements in understanding rather than removal of tags (the major tag removals happened earlier, in the jump to v4).  

- **Parameter Interpretation**: Some tags retained the same name but **improved their parameter handling in v4.5**. For instance, the `[tempo:]` tag in v4.0 could accept broad terms like "slow" or "fast." Suno v4.5 still doesn’t take exact BPM numbers, but it got *smarter about tempo descriptors* - it will pick up on more nuanced phrases like "mid-tempo 90s hip-hop swing" within a tag or prompt. Another example is the `[vocal-style:]` or `[vocal-tone:]` parameters: v4.0 might understand basic values (whispered, raspy, etc.), but v4.5 has a greater range of vocal texture it recognizes (you can specify things like "nasal, twangy" or "smooth crooning" in v4.5 and it more likely yields a difference, whereas v4.0 would often ignore such fine detail unless it was a preset tag). The underlying model upgrade in v4.5 *"captures subtle musical elements"* better, which extends to tag parameters for subtle dynamics (like the difference between a "soft" and "intense" whisper in `[whisper:]`). The documentation’s tag definitions didn’t change, but the *outcome* of using certain parameters (like `[chorus: soft]` vs `[chorus: anthemic]`) is more distinct in v4.5 than it was in v4.0, thanks to the model’s improved fidelity.

- **Genre Tag Expansion**: As mentioned, v4.5 expanded genre support. This isn’t a syntax change but a behavior change: a tag like `[genre: jazz-house]` or `[genre: midwest emo]` might have confused v4.0 (or defaulted to one genre, ignoring the hybrid), whereas **v4.5 handles multi-genre combinations much more gracefully**. The result is that **some meta-tags that v4.0 would effectively not honor suddenly became meaningful in v4.5**. For example, if you put `[genre: punk rock meets classical]` in v4.0, you’d likely get something incoherent or just one genre dominating. In v4.5, the same tag prompt can actually yield a convincing punk/classical crossover because the model learned genre blending. Therefore, users in v4.5 can utilize *more imaginative genre tags or mashups*, which is a new capability not reflected in the older documentation of tags.  

In essence, **Suno v4.0 and v4.5 use the *same set of meta-tags* for the most part, but v4.5 interprets them more accurately and with a broader palette.** V4.5 encourages more descriptive usage of tags (embedding them in sentences, stacking multiple attributes) whereas v4.0 required a more minimal, list-based approach. This means certain tags that were technically available in v4.0 only truly became *useful* in v4.5. A concrete example: `[Mood: Uplifting] [Genre: Gospel] [Style: Lo-fi]` might yield something muddled in v4.0, but in v4.5 one could write, "Create an *uplifting lo-fi gospel* piece - **[Mood: uplifting] [Genre: gospel] [Style: lo-fi]**, with a choir and dusty vinyl crackle," and it will surprisingly adhere to that vision. The tag names didn’t change, but the *behavior and fidelity did* from v4.0 to v4.5. Users should note these improvements when crafting prompts for the respective versions.

## Instrumental vs. Song (Vocal) Tag Usage  

Suno’s meta-tag system covers both purely instrumental music and songs with vocals, and **some tags are more relevant to one or the other**. It’s important to distinguish how tags apply in instrumental tracks versus vocal tracks, and note any differences in v4.0/v4.5 behavior for each category:

- **Instrumental Tracks**: To generate an instrumental (no vocals) piece, the key tag is **`[instrumental]`**. This tag explicitly tells Suno *not to produce vocals*, focusing on instruments only. The documentation defines `[instrumental]` as *"ensures the track contains no vocals"*. In both v4.0 and v4.5, placing `[instrumental]` at the start of the lyrics prompt is the recommended way to get a music bed with zero singing. V4.5 seems to honor this even better (v4.0 sometimes would slip a faint vocal hum or oh’s, but v4.5 is more strict about it, likely due to improved prompt adherence). When using `[instrumental]`, you can also specify a style parameter (e.g. `[instrumental: orchestral cinematic composition]`) to guide the flavor. 

  For instrumental pieces, **structure tags like** `[Intro]`, `[Verse]`, `[Chorus]` still can apply - they will just denote purely instrumental sections. For example, you might do:  
  ```
  [instrumental]  
  [intro: Slowly building strings and piano]  
  [verse: Main melody introduced on guitar]  
  [chorus: Full band enters with drums and bass]  
  ```  
  This is valid in both v4.0 and v4.5. The difference is, v4.5 will likely produce a more coherent instrumental "song" with those sections (taking care to change up the instrumentation per tag), whereas v4.0 might have been more repetitive without vocals to lead. The documentation even gave *track structure recommendations* for instrumentals using normal section tags (intro, verse, etc.) but no vocals, illustrating that structural tags are not exclusively for sung lyrics.

  Additionally, instrumental tracks often use **solo and instrument tags** extensively. Tags like `[Instrument: Piano]` or `[Guitar Solo]` become the "lead voice" in absence of vocals. Suno v4.5 can follow these well - e.g. `[Instrument: Violin (Lead)]` would likely make violin carry the melody. In v4.0 it also works, but perhaps with less nuance. The user doc defines a generic `[instrument]` tag to highlight a particular instrument in the arrangement, and an `[instruments]` tag to list multiple instruments for the whole track setup. Both of these are quite useful for instrumentals. For instance, one could prompt: `[instruments: acoustic guitar, cajón, handclaps]` to set the timbre palette of an instrumental. Suno v4.0 and v4.5 both pay attention to these lists, though v4.5 is better at correctly blending unusual combinations.

  It’s also worth noting the **`[solo]` tag** (or instrument-specific solos) are primarily instrumental in nature. The doc provides `[solo: ...]` as a tag meaning an improvised instrumental solo section. In a song with vocals, a `[solo]` usually means an instrumental break (guitar solo, etc.). In a purely instrumental track, a `[solo]` might simply mean a single instrument is spotlighted. Both versions support it, but again v4.5 tends to produce more convincing solos (e.g. an electric guitar solo that actually sounds distinct and lead-like, whereas v4.0 solos might sound more like a continuation of the backing track). Community tags like `[Drum Solo]` or `[Instrumental Break]` are effectively specialized cases and work similarly across versions. 

- **Songs with Vocals**: For tracks that include singing or rapping, there are many *vocal-related tags* which wouldn’t apply to instrumentals. Basic structural tags like `[Verse]`, `[Chorus]`, `[Bridge]`, `[Outro]` are chiefly used in vocal songs to organize lyrics and musical sections. Suno v4.0 and v4.5 both rely on these to know where to generate verses vs choruses. Typically, *verses have new lyrics, choruses repeat the hook*. If you use these tags in an instrumental track, the model might still create contrasting sections instrumentally (for example, a "chorus" section could bring in a fuller arrangement even if no words). But their primary purpose is for lyrical structure. V4.5 showed improvement in handling these - e.g. it produces **more dynamic, distinct choruses and bridges** than v4.0 did. The user comparison of v4 vs v4.5 noted *"more varied sections and transitions"* in v4.5’s instrumental output as well, meaning it followed the intended structure better.

  For vocals specifically, tags like **`[Male]`, `[Female]`, `[Choir]`, `[Duet]`** (and their v4.5 variants `[Male Vocal]`, etc.) are crucial. They tell Suno what kind of voice to use. In a song context, you might start your lyrics with `[female:]` or simply tag the chorus with `[choir]` to add choral backing. Suno v4.0 did allow this, but v4.5 expanded the realism and range. For example, **v4.5 can produce richer choir harmonies** when given `[Choir]` - it understands parameters like "angelic" or "powerful" on that tag - whereas v4.0’s choir might have been more muted. The documentation lists detailed parameters for `[choir]` (layered, gospel, dissonant, etc.) which presumably apply to both versions, but v4.5 has the edge in executing those styles convincingly. 

  Another vocal-centric tag is **`[harmonies]` / `[background-vocals]`**, which instructs adding harmony vocals behind the lead. In songs, this is widely used for choruses or to thicken important lines. The doc’s `[background-vocals]` tag (with parameters like harmonic, layered) is clearly for vocal tracks. Suno v4.0 could add background "oohs" or harmonies, but sometimes it struggled to keep them musically aligned. V4.5 does a better job - for instance, if you specify `[background-vocals: layered harmonies in the chorus]`, v4.5 is more likely to produce a satisfying result (stacked harmonies on the chorus lines) than v4.0 was. This aligns with v4.5’s improved *"richer vocals"* claim. 

  **Spoken segments and effects**: In vocal songs, tags like `[Spoken Word]`, `[Rap]` (if used) or things like `[laugh]`, `[sigh]` (sound effect tags for vocals) come into play. The documentation included `[laughter]` as a tag for adding laughter SFX, which is obviously only relevant if vocals are present. Both v4.0 and v4.5 can inject these vocal effects if prompted (though these are more for fun - a well-placed evil laugh in a metal song, etc.). There is also a `[whisper]` tag in the doc, denoting a whispered vocal style. This is clearly vocal-oriented; you’d use it in a lyric line or section to get a whispery delivery. Notably, v4.5 handles whispered and spoken vocals more deftly - earlier versions sometimes *sang* the words anyway or made them too loud. V4.5, if given `[whisper: ...]` at the intro or verse, will often produce actual whispering voices, which adds a creepy or intimate effect as intended. This is another area where the tag’s *behavior* improved with the version.

  Finally, **persona/voice tags**: In vocal songs, controlling the character of the voice is key. We discussed how `[personae:]` tag was a user-documented attempt to lock a voice persona (gritty male, etc.), but it’s not officially supported due to the Persona feature being separate. Instead, users achieve consistent voice by tagging the first verse or chorus with gender/range and tone (e.g. `[Male: gritty baritone]`). Both v4.0 and v4.5 allow that kind of description. V4.5 introduced the official *Personas* UI where you can simply select a voice profile (which was separate from the text prompt). If a Persona is selected, it essentially overrides what a meta-tag might try to do. So one could say a *version-dependent behavior* is: in v4.5, if you have a Persona chosen, tags like `[Male Vocal]` or `[Female Vocal]` might be redundant or ignored (because the model is already locked to a specific voice). In v4.0 (which had no Personas feature), those tags were the only way to specify voice gender. So usage shifts: **v4.0 relied on meta-tags for voice selection, while v4.5’s UI offers Personas that achieve the same without tags** - though you can still use tags if you want to *mix* multiple voices in one song (like a duet). 

In summary, **instrumental tracks tend to use tags focusing on instruments, solos, and overall structure**, whereas **vocal tracks use an additional layer of tags for voice type, lyrics structuring, and vocal effects/harmonies**. Both v4.0 and v4.5 share the tag set, but v4.5 executes these with more fidelity (e.g. better separation of an instrumental break, more realistic backing vocals, clearer distinction between a verse and chorus as per tags). When crafting prompts, one should include tags appropriate to the content: for an instrumental, you’d definitely include `[instrumental]` and instrument tags; for a song, you’d use section and vocal tags (and *not* include `[instrumental]`, since that would suppress vocals entirely). The good news is Suno v4.5 is versatile enough that you can even combine them - for example, some advanced prompts have a song with an instrumental intro: they literally write something like:  
```
[Instrumental intro]  
(guitar chords play, no vocals)  
[Verse 1]  
Lyrics start here...  
``` 
And it works (the model starts with an instrumental intro then brings in vocals). This kind of nuanced control is exactly what meta-tags enable, and v4.5 handles it more "intelligently" than earlier versions.

## Newly Confirmed or User-Tested Meta-Tags (v4.0 / v4.5)

- announcer
- build
- duet
- era: <decade or stylistic period>
- hook
- female vocal
- harmonies: <description>
- male vocal
- no-repeat
- polyphony
- spoken word
- technique
- vocalist: <name or descriptor>
- vulnerable vocals: <description>
- whisper
- whispering

### Instrument Solo Tags
- Usable as structural tags, often treated like `[section]` but with strong instrument focus:
    - `[guitar solo: blues-style run with wah FX]`
    - `[sax solo: late-night echo sax with heavy reverb]`
    - `[violin solo: baroque trills and glissando]`
    - `[synth solo: retro wave arpeggios rise into high delay]`
    - `[flute solo: airy modal runs]`

### Expanded [style:] Values (freeform, observed functional)
- `retro-horror`
- `psychedelic-swing`
- `neo-folk-electronica`
- `horror-synth-cabaret`
- `trap-fugue`
- `sacred-jazz-chant`
- `industrial-surf`
- `musique-concrète-pop`

### Confirmed Free-Form [style] or [genre] Examples
- `horror-synth`, `ghost-folk`, `spacewestern-phonk`, `ambient-baroque`, `baroque-opera`
- `glitch-jazz`, `vaporwave-trap`, `noir-hip-hop`, `musique-concrète`, `hauntology`
- `enka-minimal-techno`, `dub-clockpunk`, `phonk-noir`, `echo-chamber-pop`

---

## Update for v4.5, v4.5+ and upcoming v4.6 (added: August 25, 2025)

Starting with v4.5, the maximal "Style of Music" field length has been increased from 200 characters to 1000.

### New/confirmed tags

**New tags confirmed for v4.5+:**
 
- announcer
- aria-rise
- build
- chant-loop
- hook
- inversion
- lament
- polyphony
- scat break
- subject

**New for v4.5 and later:**

- hook
- rapped verse
- distorted vocals
- quiet arrangement

**New tags confirmed for v5.0 (November 2025):**

- aria-rise (enhanced operatic implementation)
- build (improved polyphonic builds)
- chant-loop (expanded ritualistic parameters)
- inversion (fugal technique support)
- lament (sorrowful motif generation)
- polyphony (richer vocal polyphony)
- scat break (jazz improvisation sections)
- subject (primary theme marking)
- technique (compositional method specification)

### Tags with expanded v5.0 behavior

- **[control]**: Now supports `hallucinatory`, `no-repeat`, `dynamic transitions` parameters
- **[genre]**: Hybrid genres (e.g., "midwest emo + neosoul") now reliably produce blended styles
- **[tempo]**: Natural language phrases like "mid-tempo 90s hip-hop swing" are parsed effectively
- **[vocalist]**: More consistent voice locking across sections
- **[whisper]/[whispering]**: Improved whisper detection and rendering

### Tags obsoleted or changing the behavior

Meta-tags related to audio engineering (e.g. [mix], [master], [filter], [panning], [volume]) are considered ineffective in current Suno versions.

Several early meta-tags have been deprecated in favor of newer equivalents. For example, **`[sing-style]`** (from Suno v3) was replaced by `[vocal-style]` and is ignored in v4. **`[song-type]`** (intended to denote song vs. rap vs. instrumental) was an experiment that became inert by v4.0. Likewise, an unlabeled `[theme]` tag (without a letter or description) no longer works – users must use specific section labels like `[Theme A]`, `[Theme B]` etc. or it will be ignored. In summary, many v3-era tags were phased out and **v4.5 will simply ignore** any of these obsolete tags if used.

The catch-all `[section: ...]` tag has been rendered redundant. Instead of using `[section]` as a placeholder, the model expects explicit structural tags (intro, verse, chorus, etc.). In fact, any unrecognized tag word is now parsed as a section label by default. Users have found that using the actual section names yields better results, whereas a raw `[section: X]` might be ignored or misinterpreted. Suno’s documentation explicitly lists **`section`** as removed/redundant.

There is no supported `[loop]` meta-tag to force looping playback. Earlier guides suggested tags like `[loop]` or `[loop chorus]`, but these do not function in v4.5. Indeed, “loop” is on the removed-tags list. To create a loop or repeated section, users must manually copy structures (or use the _Extend_ feature); a single tag will not make the song endlessly loop.

The autotune effect tag is effectively **deprecated** in v4.5. While some community guides still mention using `[Autotune]` for a pitch-corrected vocal style, the official word is that **`autotune`** was removed as an unstable tag. Users confirm that simply adding `[Autotune]` in lyrics has little to no effect now – you may get an “auto-tuned” feel only by describing it in the style text or using a persona that implies it.

The tag **`[end]`** (intended to mark the song’s conclusion) exists, but community feedback indicates it’s not very reliable. One user noted that _“\[end\] frequently does not work… even `[5 second fade out][end]` doesn’t seem to stop the music”_, though it **does** tend to prevent any new vocals after that point. In practice, Suno might ignore an end tag and continue the instrumental to the full length. As a workaround, some creators include an outro section description (and sometimes silence) to encourage a proper ending, since the `[end]` tag alone is hit-or-miss.

### Tags with new behavior

**Genre Mashups in `[genre:]`** – Suno v4.5 dramatically improved its handling of combined genres. The genre tag now accepts **hybrid values** and actually produces blended styles, which older versions often failed to do. For example, a prompt with **`[genre: midwest emo + neosoul]`** will yield a coherent mix of those genres in v4.5, whereas v4.0 might have defaulted to one genre or produced a muddled result. The model was expanded to recognize **1,200+ genres/styles** and interpret “X + Y” combinations smoothly. This means users can get creative with genre tags (even inventing combos like _“jazz-house,” “folk EDM,” “punk meets classical”_) and expect v4.5 to honor both elements more faithfully than before.

**Richer Tempo Descriptors** – The **`[tempo:...]`** tag became more nuanced in v4.5. While it still doesn’t support exact BPM numbers, it now understands descriptive tempo phrases much better. In v4.0 one might only use simple terms (`[tempo: slow]` or `fast`), but v4.5 can parse complex inputs like _“mid-tempo 90s hip-hop swing”_ or _“steady 4/4, 120bpm feel”_ embedded in a tempo tag. The engine won’t lock to an exact BPM, but it will interpret **relative tempo and rhythmic feel** from natural language. Essentially, v4.5’s broader language comprehension lets you be more specific in tempo/mood tags (e.g. “slow-burning waltz tempo”) and get a correspondingly specific output, which was less true in earlier versions.

**More Expressive Vocal Tags** – Tags controlling vocal style/timbre respond more deeply in v4.5. The model now differentiates subtle vocal instructions: for instance, `[vocal-style: whispered, airy]` or `[vocals: nasal, twangy tone]` will noticeably affect the performance. In v4.0, many such modifiers were ignored unless they were very common adjectives. Now, however, v4.5 was tuned for emotional and tonal nuance – users report that specifying a singer’s tone (raspy, operatic, whispered, etc.) yields a clear change in the output. Even without a dedicated tag, putting a descriptor in brackets (e.g. `[whisper voice]`) can work, but the recommended approach is to use the proper tag syntax (like `vocal-style` or include it in a `[vocals: ...]` list). **Result:** a richer palette of vocal textures – from smooth crooning to rough growls – can be invoked via tags in v4.5, whereas previously the model often defaulted to a generic voice.

**Strict Instrumental Tag Adherence** – The `[instrumental]` tag (to generate music with **no vocals**) is honored more reliably post-v4.5. In v4.0 the “instrumental” tag sometimes wasn’t 100% respected (users occasionally heard stray humming or ooohs). In v4.5, by contrast, if you start your lyrics with **`[instrumental]`**, the model will produce a purely instrumental track almost every time. The upgrade in prompt fidelity means the system correctly silences vocals when asked. Users have also learned they can combine this tag with a brief style hint (e.g. `[instrumental: lo-fi hip hop beat]`) to guide the instrumental’s genre. This stricter obedience to the instrumental directive is a quality-of-life improvement noted by many after the v4.5 update.

**Longer Structures Now Possible** – With v4.5’s extended max song length (~8 minutes), the classic structure tags like `[Verse]`, `[Chorus]`, `[Bridge]`, etc., can be used in _more repeated sections_ without being dropped. Previously, a very long prompt with many sections might see later tags get ignored as the model ran out of time/attention (v4.0 often wouldn’t reliably include a 3rd or 4th verse). Now, **v4.5 can execute a full song structure end-to-end** with multiple verses, choruses, a bridge, even multiple themes, and an outro. Community feedback around the v4.5+ release confirmed that the model maintains coherence over longer sequences, so tags defining, say, Verse 4 or a second Bridge actually produce those sections. Essentially, _the tags themselves haven’t changed_, but the **song-length limit increase and better coherence** mean you can structure a song with many tagged sections (intro through outro) and expect v4.5 to follow through. (As a side note, the formerly used `[extend-style]` tag for continuing songs is less needed now, since the base model can generate extended compositions without a separate extend prompt.)

**Improved Tag Prompt Parsing** – Suno v4.5 introduced a smarter prompt parser, which affects how tags are interpreted within more natural sentences. Users have noticed that they can **embed tags in a descriptive sentence** and v4.5 still gets it – something v4.0 struggled with. For example: _“The \[chorus\] should explode with \[anthemic\] harmonies and big drums.”_ In v4.0, that may have confused the model or caused it to sing the words, but v4.5 correctly reads those as tags (Chorus section; anthemic style). The outcome is that you don’t have to list tags stiffly on separate lines; you can mix them into a narrative prompt. The model’s better natural-language understanding means **tags can carry more context**. A Reddit user noted that steering the song with style tags _“is a lot better now \[in 4.5\]”_ and you can use more natural phrasing around them. This update doesn’t introduce new tags per se, but it _expands the way existing tags can be used_, allowing for creative prompt-writing that still yields the desired structured result.

**“Control” Meta-Tag Enhancements** – The special `[control: ...]` tag (which sets high-level guidance) gained new community uses in v4.5. It’s not a new tag, but users started leveraging it for things like preventing repetition or encouraging experimental outputs. For example, Suno experts suggest using **`[control: hallucinatory]`** to coax the model into more free-form, improvised vocals/instrumentation (useful for ambient or avant-garde pieces where _“vocal hallucinations”_ and non-lexical vocals are desired). Another trick is **`[control: no-repeat]`**, which some have placed at the top of a prompt to tell v4.5 not to repeat sections or lines excessively. Similarly, values like _“dynamic transitions”_ or _“instrumental”_ can be put in the control tag to influence the overall composition (e.g. `[control: instrumental, no-repeat, dynamic transitions]`). These were not documented in older reference material, but after v4.5 users discovered the model does respond to certain keywords in a control tag. In short, **v4.5 expanded the _impact_ of the `[control:]` tag**, making it a catch-all for high-level directives (from structure handling to creative “weirdness”). This goes hand-in-hand with using descriptive style tags – v4.5’s tolerance for abstract or compound instructions opened up new possibilities to guide the AI with tags like **hallucinatory, surreal, cinematic, no-repeat**, etc., under the `[control]` umbrella.

---

# Style of Music/Lyrics restrictions

Suno would refuse to render a track definition, if it finds, within "Style of Music" strings the service considers a protected trademarks, such as

- "kraftwerk": use "krautrock" / "old school EDM" etc when describing the style/technique
- "Orbis Mundi"
- "skank": when defining the guitar play style, use "ska stroke" instead

etc.

---

# Meta-tags definitions: frequently used meta-tags

## [announcer]

**Category:** Vocal / narrative role tag  
**Primary use:** To request a spoken or semi-spoken “host” or “presenter” voice that introduces, comments on, or frames parts of the track.

**Behavior and intent**  
`[announcer]` suggests a clear, articulate delivery similar to a radio DJ, podcast host, sports commentator, or event MC. It works best when you briefly describe the tone and context you want:

- Radio-style intros: “late-night FM host”, “upbeat morning radio DJ”  
- Retro aesthetics: “1950s newsreel announcer”, “old vinyl commercial announcer”  
- In‑universe narration: “mystery show host”, “horror anthology narrator”

**Placement and syntax**  

- *Lyrics field:*  
  - As a section header or inline role cue:  
    - `[announcer: retro radio DJ, warm, friendly tone]`  
    - `[announcer: horror show host, ominous, slow delivery]`  
- *Style of Music field:*  
  - As part of the description if the announcer role is central to the track:  
    - “lofi hip-hop with a warm late-night radio announcer introducing each section”

**Typical use-cases**  

- “Radio show” or “podcast” framing around songs or instrumental beds  
- Story intros and outros that explain the scene or episode  
- Fake commercials, station IDs, or interludes inside concept albums  

Use short, concrete adjectives for voice color (warm, crisp, vintage, serious, playful) rather than long prose to keep this tag effective.

**Example**
```
[announcer: horror show host, ominous, slow delivery]
"The mystery comes over the cursed land, as dusk approaches..."
```

---

## [aria-rise]
*   **Meaning**: A section marked by an **operatic, rising vocal phrase**, often dramatic and soaring.
*   **Placement**: Within `[vocals]` or `[structure]`.
*   **Accepted Parameters**:
    *   **solo** – single dramatic vocal.
    *   **choral** – choir rising together.
    *   **orchestral** – orchestration builds with vocal rise.
*   **Sample Usage**:
    ```
    [aria-rise: Soprano vocals rise into climax, strings swell]  
    ```
*   **Genre-Based Usage**:
    *   **Opera/Classical**: Traditional aria-style build.
    *   **Symphonic Metal**: Operatic vocals with band.
    *   **Cinematic Pop**: Ballad climax.
### **Track Structure Recommendation**:
    *   `[verse: restrained delivery]`
    *   `[aria-rise: dramatic operatic build]`
    *   `[chorus: full orchestration + vocals]`

---

## [break]
- **Meaning**: A **brief pause or stripped-down section** in the song, often used for tension or transition.
- **Placement**: Typically used within `[structure]`, `[rhythm]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **instrumental** - A solo instrumental section.
  - **percussive** - A drum break with no melody.
  - **silence** - A moment of complete pause.
  - **glitch** - A digitally processed stutter effect.
  - **acapella** - Vocals only, no instrumentation.
- **Sample Usage**:
  ```
  [break: Silence before the final chorus drop.]
  ```
- **Genre-Based Usage**:
  - **Hip-Hop & Breakbeat**: Percussive breaks for **sampling and scratching**.
  - **Jazz & Funk**: Drum breaks set up **improvised solos**.
  - **Electronic & Trap**: **Glitch or silence breaks** before a drop.
  - **Rock & Metal**: **Instrumental breakdowns** add intensity.

### **Track Structure Recommendation**
- **[intro: Full-band intro leading into break]**
- **[verse: Steady groove with instrumental build]**
- **[chorus: Strong energy before break]**
- **[bridge: Sudden percussive break leading to climax]**
- **[outro: Soft acapella break before fade-out]**

---

## [breakdown]
- **Meaning**: A section where the **instrumentation is stripped down**, usually reducing intensity before building back up.
- **Placement**: Typically used within `[structure]`, `[rhythm]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **percussive** - Emphasis on drums or rhythmic elements.
  - **instrumental** - Focused on instruments with minimal vocals.
  - **electronic** - Filtered or chopped electronic elements.
  - **syncopated** - A more rhythmically complex breakdown.
  - **minimal** - Only a few instruments, creating an intimate moment.
- **Sample Usage**:
  ```
  [breakdown: Percussive break with syncopated drum fills before the final chorus.]
  ```
- **Genre-Based Usage**:
  - **Electronic & EDM**: Often used before a **drop**, with **filtered synths**.
  - **Rock & Metal**: Stripped-down **guitar and bass sections** before a climax.
  - **Hip-Hop & Trap**: Beat-only sections for **rapping emphasis**.
  - **Jazz & Funk**: Instrumental solo breaks for **improvisation**.

### **Track Structure Recommendation**
- **[intro: Soft ambient pads leading into verse]**
- **[verse: Full instrumentation with vocal delivery]**
- **[chorus: Energetic, layered section]**
- **[breakdown: Stripped percussion and bass, creating anticipation]**
- **[bridge: Gradual build-up leading back into chorus]**
- **[outro: Fading synths with percussion elements]**

---

## [bridge]
- **Meaning**: A contrasting section that **connects different parts of a song**, often providing harmonic or melodic variation.
- **Placement**: Typically used within `[structure]` or `[harmony]`.
- **Accepted Parameters**:
  - **melodic** - Focus on a new melody line.
  - **harmonic** - Introduces a new chord progression.
  - **instrumental** - No vocals, only instrumental contrast.
  - **climactic** - Builds intensity leading into the final chorus.
  - **stripped-down** - Softer than other sections, creating contrast.
- **Sample Usage**:
  ```
  [bridge: Stripped-down vocals with subtle guitar arpeggios before the climax.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: A **melodic shift** before returning to the chorus.
  - **Jazz & Soul**: Modulations to **new harmonic territories**.
  - **Metal & Prog Rock**: Dynamic **tempo or key changes**.
  - **Electronic & House**: **Filter sweeps** and instrumental shifts.

### **Track Structure Recommendation**
- **[intro: Instrumental fade-in]**
- **[verse: Primary melody and lyrics]**
- **[chorus: Energetic, memorable hook]**
- **[bridge: Harmonic variation leading into tension]**
- **[chorus: Final, climactic return]**
- **[outro: Slow fade-out with ambient textures]**

---

## [build]

**Category:** Structural / dynamic progression tag  
**Primary use:** To mark a section that gradually increases intensity, usually leading into a chorus, drop, or climax.

**Behavior and intent**  
`[build]` tells Suno that this section should feel like a ramp: layers come in, drums grow more energetic, harmony thickens, and tension rises before a payoff. It often pairs with tags like `[drop]`, `[chorus]`, or `[hook]`.

**Placement and syntax**  

- *Lyrics field:*  
  - As a section start tag, often combined with descriptive modifiers:  
    - `[build | rising tension, more drums, more synth layers]`  
    - `[pre-chorus | build | bigger rhythm, lifted melody]`  
- *Style of Music field:*  
  - “epic electronic track with long cinematic builds and impactful drops”

**Typical use-cases**  

- EDM / pop: pre‑chorus builds into a big chorus or drop  
- Post-rock / cinematic: long atmospheric builds into climactic peaks  
- Rock / metal: drum and guitar swells before a shout‑along chorus

Keep your scene short but specific: describe what increases (drums, distortion, choir, tempo feel, etc.) rather than just saying “more intense”.

---

## [chant-loop]
*   **Meaning**: Specifies a **repeated vocal or instrumental chant**, looped for trance-like or ritualistic effect.
*   **Placement**: Often within `[vocals]`, `[structure]`, or `[texture]`.
*   **Accepted Parameters**:
    *   **ritual** – repetitive, tribal-like chants.
    *   **layered** – multiple voices stacked in loop.
    *   **percussive** – chant delivered rhythmically.
    *   **ambient** – soft, mantra-like background chant.
*   **Sample Usage**:
    ```
    [chant-loop: Layered ghost voices repeating mantra phrase]  
    ```
*   **Genre-Based Usage**:
    *   **World & Folk**: Ritual or traditional chant forms.
    *   **Ambient & Drone**: Mantra textures as sound bed.
    *   **Hip-Hop & Trap**: Chanted loops as rhythmic backing.
    *   **Industrial/Experimental**: Distorted, mechanical chant.
### **Track Structure Recommendation**:
    *   `[intro: chant-loop begins quietly]`
    *   `[chorus: chant grows in volume]`
    *   `[outro: chant fades to silence]`

---

## [coda]
- **Meaning**: Specifies the **concluding section of a piece**, often distinct from the main body, used for closure or reinforcement of themes.
- **Placement**: Typically used within `[structure]` or `[harmony]`.
- **Accepted Parameters**:
  - **recapitulative** - Revisits earlier themes before resolving.
  - **unexpected** - Provides a twist at the end.
  - **fading** - Gradually reduces in volume and texture.
  - **dramatic** - A sudden, strong ending.
  - **layered** - Multiple instrument groups resolving together.
- **Sample Usage**:
  ```
  [coda: Soft piano outro echoing the main melody.]
  ```
- **Genre-Based Usage**:
  - **Classical & Symphonic**: **Recapitulation of themes** for structural unity.
  - **Rock & Progressive**: **Extended guitar-driven codas** for epic conclusions.
  - **Electronic & Ambient**: **Fading textures** to leave an open-ended feel.
  - **Pop & Jazz**: **Reharmonized final phrases** for a smooth exit.

### **Track Structure Recommendation**
- **[intro: Gentle motif introduction]**
- **[verse: Expands on the theme with dynamic variations]**
- **[chorus: Peak energy with full harmonization]**
- **[bridge: A contrasting section to heighten emotional impact]**
- **[coda: Slow, resolving melody fading into silence]**

---

## [chorus]
- **Meaning**: Defines the **main repeated hook** of the song, often the most memorable part.
- **Placement**: Typically used within `[structure]` or `[vocals]`.
- **Accepted Parameters**:
  - **anthemic** - Big, singalong chorus.
  - **soft** - Gentle, contrasting chorus.
  - **harmonic** - Focus on vocal harmonies.
  - **dynamic** - Instrumentation builds in the chorus.
  - **stripped** - Minimal arrangement for emotional impact.
- **Sample Usage**:
  ```
  [chorus: Anthemic vocal-driven hook with layered harmonies.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **Catchy, energetic chorus** hooks.
  - **Ballads & Folk**: **Soft, emotionally driven choruses**.
  - **Metal & Punk**: **Aggressive, high-energy choruses**.
  - **Electronic & Dance**: **Instrumentally rich choruses** that peak dynamically.

### **Track Structure Recommendation**
- **[intro: Instrumental buildup]**
- **[verse: Lead-in to the hook]**
- **[chorus: High-energy, anthem-like section]**
- **[bridge: Dynamic contrast leading into final chorus]**
- **[outro: Stripped-down reprise of the chorus]**

---

## [compression]
- **Meaning**: Defines **dynamic range processing**, used to balance loud and soft parts in a track.
- **Placement**: Typically used within `[mixing]`, `[dynamics]`, or `[effects]`.
- **Accepted Parameters**:
  - **light** - Soft compression, retaining dynamic variation.
  - **heavy** - Strong compression, flattening peaks.
  - **pumping** - Rhythmic compression, common in EDM.
  - **transparent** - Subtle compression that smooths dynamics without altering tone.
  - **aggressive** - High-ratio compression for a punchy sound.
- **Sample Usage**:
  ```
  [compression: Transparent vocal compression for clarity.]
  ```
- **Genre-Based Usage**:
  - **Pop & Vocal Music**: Light compression ensures **consistent vocals**.
  - **EDM & Trap**: Pumping compression creates **rhythmic breathing effects**.
  - **Rock & Metal**: Aggressive compression **enhances impact**.
  - **Jazz & Acoustic**: Transparent compression **maintains dynamics**.

### **Track Structure Recommendation**
- **[intro: No compression, natural ambiance]**
- **[verse: Light compression to keep vocal dynamics intact]**
- **[chorus: Heavier compression to emphasize power]**
- **[bridge: Subtle compression to create contrast]**
- **[outro: Gradual release of compression for a more organic fade-out]**

---

## [control]
- **Meaning**: Specifies **how certain elements of the composition are structured, processed, or restricted**.
- **Placement**: Typically used at the **beginning of the definition**, as it applies to **global track parameters**.
- **Accepted Parameters**:
  - **instrumental** - No vocals in the track.
  - **acapella** - Vocals only, no instrumentation.
  - **looped** - The structure is cyclic or repetitive.
  - **no-repeat** - Ensures no section is repeated.
  - **dynamic** - Allows variation in tempo, intensity, and texture.
- **Sample Usage**:
  ```
  [control: Instrumental, no-repeat, dynamic transitions.]
  ```
- **Genre-Based Usage**:
  - **Ambient & Minimalist**: **Looped structures** maintain atmosphere.
  - **Jazz & Improvised Music**: **Dynamic control** allows live feel.
  - **Electronic & Dance**: **No-repeat variations** create continuous evolution.
  - **Symphonic & Cinematic**: **Instrumental focus** supports narrative flow.

### **Track Structure Recommendation**
- **[intro: Loop-based rhythmic foundation]**
- **[verse: Dynamic texture variations]**
- **[chorus: Expanding soundscape with thematic growth]**
- **[bridge: Contrast through modulation]**
- **[outro: Instrumental fade-out, sustaining tension]**

---

## [drop]
- **Meaning**: Defines a **sudden shift in intensity**, often a key element in EDM and modern music styles.
- **Placement**: Typically used within `[structure]`, `[dynamics]`, or `[effects]`.
- **Accepted Parameters**:
  - **bass-heavy** - A deep, sub-bass-driven drop.
  - **melodic** - A drop that introduces a powerful melody.
  - **glitchy** - The drop is fragmented and unpredictable.
  - **orchestral** - A cinematic drop into high-energy themes.
  - **minimalist** - A subtle yet effective drop with reduced elements.
- **Sample Usage**:
  ```
  [drop: Bass-heavy synth explosion after the build-up.]
  ```
- **Genre-Based Usage**:
  - **EDM & Dubstep**: Central to **massive beat drops**.
  - **Hip-Hop & Trap**: **808-driven drops** enhance groove.
  - **Rock & Metal**: **Drum-heavy and guitar-driven breakdowns**.
  - **Cinematic & Experimental**: **Tension-building orchestral drops**.

### **Track Structure Recommendation**
- **[intro: Minimal build-up with rising tension]**
- **[verse: Establishing groove and melody]**
- **[chorus: Expanding harmonic textures]**
- **[build-up: Crescendo leading into drop]**
- **[drop: Heavy bass and dynamic shift]**
- **[outro: Soft landing with reverb decay]**

---

## [genre]
- **Meaning**: Defines the **overall stylistic category** of the composition.
- **Placement**: Typically **at the start of the definition**, as it determines how the track is structured.
- **Accepted Parameters**:
  - **single-genre** - A single, well-defined musical genre (e.g., `[genre: jazz]`).
  - **hybrid-genre** - A fusion of two or more genres (e.g., `[genre: jazz-electronic-fusion]`).
  - **subgenre** - A more specific style within a genre (e.g., `[genre: dark-ambient]`).
- **Sample Usage**:
  ```
  [genre: cinematic-orchestral hybrid with electronic textures.]
  ```
- **Genre-Based Usage**:
  - **Rock & Pop**: `[genre: classic-rock]`, `[genre: indie-pop]`
  - **Electronic & Dance**: `[genre: deep-house]`, `[genre: industrial-techno]`
  - **Hip-Hop & R&B**: `[genre: trap-soul]`, `[genre: boom-bap]`
  - **Experimental & Soundscape**: `[genre: musique-concrete]`, `[genre: noise-drone]`

### **Track Structure Recommendation**
- **[intro: Atmospheric textures setting the tone]**
- **[verse: Genre-defining elements introduced]**
- **[chorus: Fully developed style with layered instruments]**
- **[bridge: A contrasting section that reinterprets genre tropes]**
- **[outro: Genre's characteristic resolution or fade-out]**

---

## [hook]

**Category:** Structural / key element tag  
**Primary use:** To highlight the most memorable musical / lyrical idea in the track.

**Behavior and intent**  
`[hook]` marks a phrase or line meant to “stick in the ear”. It can be a micro‑section within a chorus, a short melodic motif, or a repeated line that carries the song’s identity. Unlike `[chorus]`, which defines a whole section, `[hook]` often focuses on a compact, repeatable idea.

**Placement and syntax**  

- *Lyrics field:*  
  - As a section label or inline cue:  
    - `[hook] Wherever we go, the record spins slow.`  
    - `[chorus | catchy hook, simple repeating phrase]`  
- *Style of Music field:*  
  - “warm old‑vinyl hip‑hop with a simple, nostalgic hook in the chorus”

**Typical use-cases**  

- Emphasizing one key line in the chorus that should stand out  
- Creating a short vocal motif for instrumental‑heavy tracks  
- Tagging call‑and‑response lines or slogans in rap / pop

For best results, keep the hook text very short, rhythmically clear, and easy to repeat.

---

## [intro]
- **Meaning**: Defines the **opening section of a track**, setting the mood, instrumentation, and rhythm before transitioning into structured sections.
- **Placement**: Typically **at the beginning of the track definition**.
- **Accepted Parameters**:
  - **soft** - Gentle, understated opening.
  - **dramatic** - Strong, impactful beginning.
  - **percussive** - Driven by rhythmic elements.
  - **atmospheric** - Textural, ambient soundscapes.
  - **synth-driven** - Electronic intro using pads, arpeggios.
- **Sample Usage**:
  ```
  [intro: Soft choral voices fading in with ambient pads.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **Guitar intros leading into heavy riffs**.
  - **Electronic & Synthwave**: **Filtered synths and arpeggios**.
  - **Jazz & Fusion**: **Solo saxophone or piano introduction**.
  - **Cinematic & Classical**: **Grand orchestral swells**.

### **Track Structure Recommendation**
- **[intro: Low strings rumbling beneath ethereal choral voices]**
- **[verse: Vocal melody enters with soft piano accompaniment]**
- **[chorus: Full orchestration with percussion layers]**
- **[bridge: Drop in intensity, shifting to solo violin]**
- **[outro: Gentle fade-out with harp and flute]**

---

## [instruments]
- **Meaning**: Specifies the **instruments used in the composition**, helping define the timbre and orchestration of the track.
- **Placement**: Typically placed **before structure tags** to establish instrumentation at the beginning of the track definition.
- **Accepted Parameters**:
  - **Specific instruments** - e.g., **piano, violin, electric guitar, synthesizer, brass, flute, harp**.
  - **Ensembles** - e.g., **string quartet, symphonic orchestra, jazz trio**.
  - **Electronic elements** - e.g., **808 bass, modular synth, vocoder, pads**.
- **Sample Usage**:
  ```
  [instruments: Acoustic guitar, soft synth pads, subtle piano accompaniment.]
  ```
- **Genre-Based Usage**:
  - **Rock & Pop**: **Electric guitar, bass, drums, synths**.
  - **Classical & Cinematic**: **Orchestral strings, brass, harp**.
  - **Electronic & Ambient**: **Synth pads, drones, digital bells**.
  - **Jazz & Blues**: **Saxophone, upright bass, electric piano**.

### **Track Structure Recommendation**
- **[instruments: Piano, cello, atmospheric synths]**
- **[intro: Solo piano melody introducing the theme]**
- **[verse: Cello enters with deep harmonies]**
- **[chorus: Synth pads build a cinematic atmosphere]**
- **[outro: Instruments fade out into soft reverberation]**

---

## [inversion]
*   **Meaning**: States that a **theme or motif should be inverted** (played upside-down in melodic contour).
*   **Placement**: Paired with `[subject]` or `[motif]`.
*   **Accepted Parameters**:
    *   **strict** – precise inversion.
    *   **free** – partial inversion with modification.
    *   **stretched** – inversion with augmented rhythm.
*   **Sample Usage**:
    ```
    [inversion: Subject theme inverted on strings]  
    ```
*   **Genre-Based Usage**:
    *   **Fugue/Classical**: Canonical inversion technique.
    *   **Jazz Fusion**: Inverted melodic riffs.
    *   **Electronic/Experimental**: Inverted synth motif loops.
### **Track Structure Recommendation**:
    *   `[subject: original theme]`
    *   `[inversion: mirror of subject]`
    *   `[coda: combine both for resolution]`

---

## [lament]
*   **Meaning**: Defines a **sorrowful, descending motif or expressive passage**.
*   **Placement**: Within `[melody]`, `[harmony]`, or `[vocals]`.
*   **Accepted Parameters**:
    *   **descending** – typical lament bass line (e.g. minor descending tetrachord).
    *   **vocal** – sorrowful vocal delivery.
    *   **instrumental** – plaintive strings or winds.
    *   **choral** – choir in lament style.
*   **Sample Usage**:
    ```
    [lament: Descending strings in minor mode]  
    ```
*   **Genre-Based Usage**:
    *   **Baroque/Classical**: Lament bass line.
    *   **Gothic/Metal**: Sorrowful motifs.
    *   **Folk/Choral**: Funeral lament style.
### **Track Structure Recommendation**:
    *   `[verse: narrative lyrics]`
    *   `[lament: sorrowful instrumental descent]`
    *   `[chorus: emotional climax]`

---

## [length]
- **Meaning**: Specifies the **desired duration of the track**, controlling overall runtime.
- **Placement**: Typically placed **before `[structure]`** to ensure Suno processes it before structuring the composition.
- **Accepted Parameters**:
  - **short** - 30-60 seconds.
  - **standard** - 2-3 minutes (default).
  - **extended** - 4-5 minutes.
  - **loopable** - Designed to seamlessly loop.
  - **epic** - 5+ minutes with grand arrangements.
- **Sample Usage**:
  ```
  [length: Extended, with a cinematic build-up]
  ```
- **Genre-Based Usage**:
  - **Pop & Mainstream**: **Standard radio-friendly lengths (2-3 min)**.
  - **Electronic & Dance**: **Extended club mixes (5+ min)**.
  - **Classical & Film Score**: **Epic storytelling (5+ min orchestral)**.
  - **Game Music & Ambient**: **Loopable background tracks**.

### **Track Structure Recommendation**
- **[length: Loopable]**
- **[intro: Smooth ambient pad fade-in]**
- **[verse: Subtle arpeggiated melodies drifting through]**
- **[chorus: Slightly intensified layering for dynamic movement]**
- **[outro: Seamless transition to start again]**

---

## [mood]
- **Meaning**: Defines the **emotional atmosphere** of the track.
- **Placement**: Typically used at the **start of the track definition** to guide composition style.
- **Accepted Parameters**:
  - **dark** - Brooding, mysterious, or ominous.
  - **uplifting** - Positive, energizing.
  - **melancholic** - Sad, introspective.
  - **mystical** - Ethereal, otherworldly.
  - **playful** - Lighthearted and fun.
- **Sample Usage**:
  ```
  [mood: Dark, atmospheric tension with deep drones.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **Dark and aggressive moods**.
  - **Electronic & Chill**: **Uplifting or melancholic textures**.
  - **Cinematic & Orchestral**: **Mystical and grand moods**.
  - **Jazz & Soul**: **Playful and laid-back vibes**.

### **Track Structure Recommendation**
- **[mood: Melancholic, soft and reflective]**
- **[intro: Gentle strings and atmospheric pads]**
- **[verse: Emotional, expressive melody on piano]**
- **[chorus: Expansive orchestration with rising intensity]**
- **[outro: Soft, fading resolution in minor tonality]**

---

## [pre-chorus]
- **Meaning**: Defines the **section leading from the verse into the chorus**, building tension and anticipation.
- **Placement**: Typically placed **between `[verse]` and `[chorus]`** in `[structure]`.
- **Accepted Parameters**:
  - **rising** - Gradual build-up into the chorus.
  - **syncopated** - Off-beat rhythms to create anticipation.
  - **minimal** - Stripped-down before a strong chorus impact.
  - **harmonized** - Vocally layered to enhance tension.
- **Sample Usage**:
  ```
  [pre-chorus: Rising vocal harmonies with increasing synth layers.]
  ```
- **Genre-Based Usage**:
  - **Pop & R&B**: **Melodic pre-choruses setting up catchy hooks**.
  - **Rock & Alternative**: **Guitar-driven pre-choruses for tension**.
  - **Hip-Hop & Trap**: **Minimalist, beat-only pre-choruses**.
  - **Cinematic & Epic**: **Orchestral swells leading into grand moments**.

### **Track Structure Recommendation**
- **[verse: Soft piano melody with subdued vocals]**
- **[pre-chorus: Gradual rise in vocal intensity and instrumentation]**
- **[chorus: Full orchestral and vocal explosion]**
- **[outro: Smooth transition back to soft textures]**

---

## [polyphony]

**Category:** Arrangement / vocal-choir / harmony tag  
**Primary use:** To request multiple independent melodic lines or layered voices rather than a single simple melody with block chords.

**Behavior and intent**  
`[polyphony]` encourages overlapping melodies and counterpoint. In vocal music, it suggests several simultaneous lines (choir parts interweaving rather than moving in lockstep). In instrumental music, it can yield more complex interacting parts instead of one dominant lead with static backing.

**Placement and syntax**  

- *Lyrics field:*  
  - As a section descriptor, especially for choirs or group singing:  
    - `[chorus | polyphony, overlapping choir lines, call-and-response]`  
    - `[bridge | polyphony in strings and woodwinds, slowly unfolding]`  
- *Style of Music field:*  
  - “sacred-style polyphony with interweaving vocal lines and gentle organ support”

**Typical use-cases**  

- Choral / sacred / renaissance‑inspired pieces  
- Complex climactic choruses with several melody fragments at once  
- Orchestral or post‑rock textures where many lines move semi-independently

For best results, pair `[polyphony]` with clear section roles (verse, chorus, coda) and maybe indicate which instruments or voices participate.

---

## [refrain]
- **Meaning**: Defines a **repeated phrase or musical passage**, typically appearing in multiple sections of the track.
- **Placement**: Typically placed **within `[structure]`, `[chorus]`, or `[vocals]`**.
- **Accepted Parameters**:
  - **melodic** - A tune repeated throughout.
  - **lyrical** - A repeated vocal phrase.
  - **instrumental** - A motif repeated by instruments.
  - **harmonic** - A chord progression appearing multiple times.
- **Sample Usage**:
  ```
  [refrain: Repeated vocal phrase that echoes at the end of each chorus.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **"Melodic" refrains for earworms**.
  - **Hip-Hop & R&B**: **"Lyrical" refrains for hook-based tracks**.
  - **Electronic & House**: **"Instrumental" refrains for looping textures**.
  - **Orchestral & Jazz**: **"Harmonic" refrains for theme consistency**.

### **Track Structure Recommendation**
- **[intro: Refrain introduced as an instrumental hook]**
- **[verse: New melody leading toward the refrain]**
- **[chorus: Full refrain, sung with layered harmonies]**
- **[bridge: A break before the refrain returns]**
- **[outro: Fading refrain, gradually repeating into silence]**

---

## [scat break]
*   **Meaning**: Denotes a **scatting vocal improvisation section**, usually jazz-influenced.
*   **Placement**: Within `[vocals]` or `[structure]`.
*   **Accepted Parameters**:
    *   **solo** – single vocalist scat improvisation.
    *   **duet** – multiple voices scatting in call-and-response.
    *   **layered** – overlapping scat vocals for texture.
*   **Sample Usage**:
    ```
    [scat break: Playful jazz-style scat improvisation, no lyrics]  
    ```
*   **Genre-Based Usage**:
    *   **Jazz & Swing**: Classic scat solos.
    *   **Experimental & Avant-pop**: Vocal improvisation as texture.
    *   **Hip-Hop Fusion**: Rhythmic scatting between verses.
### **Track Structure Recommendation**:
    *   `[verse: lyrical section]`
    *   `[scat break: vocalist improvises syllables]`
    *   `[chorus: return to main hook]`

---

## [sequence]
- **Meaning**: Specifies **the order and repetition of musical sections**, helping structure the track dynamically.
- **Placement**: Typically used **within [structure]**, ensuring that segments appear in a defined order.
- **Accepted Parameters**:
  - **linear** - A straightforward progression of sections.
  - **cyclical** - Repeating sections in a structured manner.
  - **reversed** - Themes appear in the opposite order.
  - **mirrored** - The second half of the track reflects the first.
- **Sample Usage**:
  ```
  [sequence: Linear with a mirrored return in the final section.]
  ```
- **Genre-Based Usage**:
  - **Classical & Film Score**: **"Mirrored" for symmetrical compositions.**
  - **Dance & Electronic**: **"Cyclical" for repeating, looping sections.**
  - **Rock & Pop**: **"Linear" for conventional storytelling structures.**
  - **Progressive & Jazz**: **"Reversed" for unconventional arrangements.**

### **Track Structure Recommendation**
- **[sequence: Cyclical, alternating between verse and instrumental interludes]**
- **[intro: Soft pad textures leading into rhythm]**
- **[section: Thematic section introducing melody]**
- **[section: Repeated development with slight variation]**
- **[outro: Return of the theme in a mirrored resolution]**

---

## [style]
- **Meaning**: Defines the **musical style or aesthetic** of the track, influencing genre fusion and overall production approach.
- **Placement**: **Before [genre] or [mood]**, specifying artistic direction.
- **Accepted Parameters**:
  - **minimalist** - Sparse instrumentation, subtle textures.
  - **cinematic** - Large-scale, soundtrack-like arrangements.
  - **lo-fi** - Vintage, tape-saturated, and degraded sound.
  - **high-energy** - Intense, fast-paced composition.
  - **experimental** - Non-traditional elements and unpredictable shifts.
- **Sample Usage**:
  ```
  [style: Cinematic with sweeping orchestral arrangements.]
  ```
- **Genre-Based Usage**:
  - **Ambient & Minimalist**: **"Minimalist" for delicate, sparse textures.**
  - **Film Score & Symphonic**: **"Cinematic" for dramatic orchestrations.**
  - **Lo-Fi & Vintage Hip-Hop**: **"Lo-fi" for nostalgic sound.**
  - **Electronic & Industrial**: **"Experimental" for glitch and non-traditional structures.**

### **Track Structure Recommendation**
- **[style: Minimalist, focusing on space and subtle dynamics]**
- **[intro: Soft ambient pads and distant reverberations]**
- **[verse: Sparse instrumentation with delayed plucks]**
- **[chorus: Slow chordal swells creating depth]**
- **[outro: Fading echoes and cinematic strings]**

---

## [subject]
*   **Meaning**: Marks the **primary musical theme or motif**, especially in fugues or structured classical/jazz works.
*   **Placement**: Within `[harmony]`, `[melody]`, or `[structure]`.
*   **Accepted Parameters**:
    *   **main** – introduces the principal theme.
    *   **counter** – secondary theme against the main subject.
    *   **stretto** – overlapping entries of the subject.
*   **Sample Usage**:
    ```
    [subject: Main fugue theme on organ]  
    ```
*   **Genre-Based Usage**:
    *   **Classical**: Core fugue subject.
    *   **Jazz**: Head motif before improvisation.
    *   **Experimental/Phonk-Classical**: Subject line woven into hybrid styles.
### **Track Structure Recommendation**:
    *   `[intro: subject introduced]`
    *   `[inversion: theme restated in reverse]`
    *   `[bridge: new harmonic counterpoint]`

---

## [technique]

**Category:** Instrumental / performance detail tag  
**Primary use:** To specify how an instrument or voice is played or treated (e.g., picking style, bowing, extended techniques), not just *what* instrument is used.

**Behavior and intent**  
`[technique]` is a general label you can pair with a short description of performance style. Instead of simply saying “[guitar]”, you can indicate “[guitar | technique: muted funky strums]”. This helps shape rhythmic feel and timbre.

**Placement and syntax**  

- *Lyrics field:*  
  - As part of a section descriptor for arrangement:  
    - `[intro | guitar, technique: tremolo picking over reverb]`  
    - `[bridge | cello, technique: harmonics and glissando]`  
- *Style of Music field:*  
  - “neo-folk with detailed acoustic techniques: fingerstyle arpeggios, soft slides, and harmonics”

**Typical use-cases**  

- Guitar, strings, winds: fingerstyle, bowing, staccato, legato, muted, slapped, etc.  
- Vocal techniques: “technique: belting”, “technique: soft head voice”, “technique: spoken rhythmically”  
- Experimental sounds: “technique: prepared piano”, “technique: tape‑style pitch warble”

Keep technique descriptions short, focusing on physical action (“plucked,” “bowed long,” “muted,” “sliding”) rather than abstract mood words.

---

## [tempo]
- **Meaning**: Defines the **speed (BPM) and pacing** of the track.
- **Placement**: Typically **before [rhythm] or [mood]**, influencing groove and feel.
- **Accepted Parameters**:
  - **slow** - Relaxed, chill pacing (BPM 60-90).
  - **moderate** - Balanced, mid-tempo energy (BPM 90-120).
  - **fast** - High-energy, upbeat (BPM 120-160).
  - **variable** - Tempo changes dynamically.
- **Sample Usage**:
  ```
  [tempo: Fast, high-energy BPM with driving percussion.]
  ```
- **Genre-Based Usage**:
  - **Ballads & Lo-Fi**: **"Slow" for relaxed pacing.**
  - **Pop & Rock**: **"Moderate" for steady song flow.**
  - **EDM & Metal**: **"Fast" for energetic, danceable beats.**
  - **Prog Rock & Experimental**: **"Variable" for tempo shifts.**

### **Track Structure Recommendation**
- **[tempo: Moderate with a slight increase in the chorus]**
- **[intro: Smooth tempo introduction with light percussion]**
- **[verse: Consistent mid-tempo groove]**
- **[chorus: Slightly faster tempo for added intensity]**
- **[outro: Gradual slow-down leading into a soft fade]**

---

## [verse]
- **Meaning**: Defines a **repeated song section with evolving lyrics or instrumentation**, typically alternating with a chorus.
- **Placement**: Typically used **within [structure]**, indicating lyrical or instrumental sections.
- **Accepted Parameters**:
  - **soft** - Gentle and subdued verse dynamics.
  - **powerful** - Intense, full-sounding verse.
  - **instrumental** - A non-vocal variation of the verse.
  - **spoken-word** - A recited rather than sung verse.
- **Sample Usage**:
  ```
  [verse: Soft, intimate vocal lines over acoustic guitar.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **"Powerful" for high-energy vocal passages.**
  - **Hip-Hop & Spoken Word**: **"Spoken-word" for rhythmic delivery.**
  - **Folk & Acoustic**: **"Soft" for storytelling lyrical verses.**
  - **Electronic & Synthwave**: **"Instrumental" for evolving textures.**

### **Track Structure Recommendation**
- **[verse: Soft, whispery vocals over minimalist piano]**
- **[chorus: Full-band explosion with layered harmonies]**
- **[verse: Powerfully sung variation with rising energy]**
- **[outro: Verse returns in a stripped-down, fading arrangement]**

---

## [vocals]
- **Meaning**: Defines **the presence, type, and characteristics of vocal performances** in the track.  
- **Placement**: Typically used **before [structure] or [style]**, guiding the vocal performance and its prominence.  
- **Accepted Parameters**:
  - **lead** - Primary vocal line leading the melody.  
  - **background** - Secondary harmonized or atmospheric vocals.  
  - **choir** - Layered choral voices, often used for dramatic effect.  
  - **spoken-word** - Rhythmically spoken lyrics instead of singing.  
  - **a cappella** - Only vocal performances, no instrumental accompaniment.  
  - **filtered** - Vocals processed with special effects (e.g., robotic, distorted).  
- **Sample Usage**:
  ```
  [vocals: Lead female vocals with ethereal background harmonies.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **"Lead" for a strong melodic presence.**  
  - **Gospel & Orchestral**: **"Choir" for layered, harmonic vocals.**  
  - **Hip-Hop & Spoken Word**: **"Spoken-word" for rhythmic vocal phrasing.**  
  - **Electronic & Experimental**: **"Filtered" for robotic or distorted effects.**  

### **Track Structure Recommendation**
- **[vocals: Lead female voice, with ethereal harmonies]**  
- **[intro: Atmospheric pad swells introducing whispered background vocals]**  
- **[verse: Soft, expressive lead vocals with light reverberation]**  
- **[chorus: Choir-like harmonies creating a soaring effect]**  
- **[bridge: Spoken-word transition with distant echoes]**  
- **[outro: Vocals fading into layered ambient whispers]**

---

# Meta-tags definitions: less frequently used meta-tags

Below is the list of meta-tags recognized by Suno audio tracks generation service (as confirmed by user tests and official Suno documentation).

## [accelerando]
- **Meaning**: Specifies a **gradual increase in tempo**, creating a sense of urgency, excitement, or transition.
- **Placement**: Typically used within `[tempo]`, `[structure]`, or `[rhythm]`.
- **Accepted Parameters**:
  - **gradual** - Slow, steady increase in speed.
  - **sudden** - Sharp, quick tempo increase.
  - **layered** - Different instruments accelerating at different rates.
  - **intensified** - Accompanied by increased dynamics or harmonic tension.
  - **syncopated** - Rhythmic acceleration with offbeat emphasis.
- **Sample Usage**:
  ```
  [accelerando: Gradual tempo increase leading into the climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: Used in **symphonic works and fugues** for momentum.
  - **Jazz & Latin**: Accelerando builds **swing and groove** over a solo section.
  - **Rock & Metal**: Driving guitar riffs increase tempo for **intensity**.
  - **EDM & Trance**: Used in buildups before a **drop**.

### **Track Structure Recommendation**
- **[intro: Steady tempo with calm instrumentation]**
- **[verse: Gradual accelerando with layering synths]**
- **[chorus: Full-speed section with high energy]**
- **[bridge: Slowdown before another accelerando]**
- **[outro: Return to a slower tempo]**

---

## [ad-lib]
- **Meaning**: Specifies a **freely improvised vocal or instrumental phrase**, often used in **solos or embellishments**.
- **Placement**: Typically used within `[vocals]` or `[structure]`.
- **Accepted Parameters**:
  - **vocal** - Spontaneous, expressive singing.
  - **instrumental** - Improvised instrumental fills.
  - **rhythmic** - Ad-libbed drum patterns.
  - **melodic** - Improvised melody variations.
  - **harmonic** - Free chordal movement.
- **Sample Usage**:
  ```
  [ad-lib: Vocal runs in the final chorus for emotional impact.]
  ```
- **Genre-Based Usage**:
  - **Jazz & Blues**: Essential for **improvised solos**.
  - **Hip-Hop & R&B**: Vocal **ad-libs enhance** expressiveness.
  - **Rock & Metal**: Guitar ad-libs add **raw energy**.
  - **Latin & Afrobeat**: Percussion ad-libs for **dance groove**.

### **Track Structure Recommendation**
- **[intro: Sparse vocals with ad-lib whispers]**
- **[verse: Structured melody with ad-libbed embellishments]**
- **[chorus: Powerful vocal ad-libs on key lines]**
- **[bridge: Improvised guitar or sax solo]**
- **[outro: Soft, fading ad-lib phrases]**

---

## [ambient]
- **Meaning**: Defines a track as **atmospheric, textural, and non-rhythmic**, often using **drones, pads, or environmental sounds**.
- **Placement**: Typically used within `[style]`, `[mixing]`, or `[structure]`.
- **Accepted Parameters**:
  - **textural** - Emphasizes layered sound textures.
  - **minimal** - Sparse and open sound design.
  - **dark** - Mysterious, eerie ambient tones.
  - **bright** - Ethereal, uplifting ambiance.
  - **dissonant** - Subtle or strong unresolved tension.
- **Sample Usage**:
  ```
  [ambient: Dark, textural drones fading in and out.]
  ```
- **Genre-Based Usage**:
  - **Cinematic & Soundtrack**: Enhances **scene-setting and emotion**.
  - **Electronic & Drone**: Builds **slow-moving soundscapes**.
  - **Experimental & Avant-Garde**: Creates **abstract sonic experiences**.
  - **Lo-Fi & Chill**: **Soft ambient pads** provide a relaxing background.

### **Track Structure Recommendation**
- **[intro: Faint, layered ambient textures]**
- **[verse: Soft ambient swells and deep bass pads]**
- **[chorus: Expanding textures with shimmering synths]**
- **[bridge: Minimalist moment with evolving drones]**
- **[outro: Fading ambient echoes]**

---

## [arpeggio]
- **Meaning**: Defines a **broken chord sequence**, where notes are played individually instead of simultaneously.
- **Placement**: Typically used within `[harmony]` or `[rhythm]`.
- **Accepted Parameters**:
  - **rising** - Arpeggio pattern ascends.
  - **falling** - Arpeggio pattern descends.
  - **circular** - Continuously repeating patterns.
  - **syncopated** - Offbeat rhythmic arpeggios.
  - **randomized** - Variations in note sequence.
- **Sample Usage**:
  ```
  [arpeggio: Syncopated synth arpeggios driving the groove.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: Harpsichord and piano **arpeggios** provide intricate motion.
  - **Rock & Progressive**: Guitar arpeggios **enhance melody flow**.
  - **Electronic & Synthwave**: Rapid, repeating **synth arpeggios** create movement.
  - **Jazz & Blues**: Improvised arpeggios add harmonic **fluidity**.

### **Track Structure Recommendation**
- **[intro: Soft, rising piano arpeggios]**
- **[verse: Low arpeggios supporting the melody]**
- **[chorus: Faster, syncopated arpeggio patterns]**
- **[bridge: Swirling synth arpeggios layered over bass]**
- **[outro: Descending, fading arpeggios]**

---

## [arrangement]
- **Meaning**: Defines the **organization of musical elements**, including **instrumentation, section order, and layering**.
- **Placement**: Typically used within `[structure]`, `[orchestration]`, or `[mixing]`.
- **Accepted Parameters**:
  - **dense** - Full, layered orchestration.
  - **minimal** - Sparse, delicate textures.
  - **layered** - Different instrumental layers building over time.
  - **dynamic** - Varying section energy throughout.
  - **orchestral** - Classical-style arrangement.
- **Sample Usage**:
  ```
  [arrangement: Layered instrumentation building towards climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Symphonic**: **Dense orchestral arrangements** for cinematic pieces.
  - **Jazz & Big Band**: **Dynamic arrangements** with brass and woodwinds.
  - **Electronic & Pop**: **Layered synth arrangements** create depth.
  - **Minimalist & Experimental**: **Sparse arrangements** leave room for textures.

### **Track Structure Recommendation**
- **[intro: Minimal arrangement with only a piano and soft pads]**
- **[verse: Gradually introducing more instruments]**
- **[chorus: Full, layered arrangement with harmonies]**
- **[bridge: Stripped-down section before a build-up]**
- **[outro: Gradual removal of instruments for a soft fade-out]**

---

## [articulation]
- **Meaning**: Specifies how notes are played in terms of attack, transition, and connection between them.
- **Placement**: Typically placed within `[instruments]` or `[style]`.
- **Accepted Parameters**:
  - **staccato** - Short, detached notes.
  - **legato** - Smooth, connected notes.
  - **marcato** - Strongly accented notes.
  - **tenuto** - Notes played at full duration.
  - **accented** - Notes emphasized with additional force.
  - **spiccato** - Lightly bouncing bow strokes (for strings).
  - **sustained** - Notes held for extended durations.
- **Sample Usage**:
  ```
  [articulation: Staccato strings and legato woodwinds for contrast.]
  ```
- **Advice**:
  - **Use "staccato"** for punchy, rhythmic compositions.
  - **Use "legato"** for smooth and flowing melodies.
  - **Combine articulations** to create **dynamic contrasts**.

---

## [attack]
- **Meaning**: Defines how quickly a note reaches its full volume after being played.
- **Placement**: Typically placed within `[dynamics]`, `[instruments]`, or `[mixing]`.
- **Accepted Parameters**:
  - **sharp** - A quick, percussive attack (good for plucked strings, electronic leads).
  - **soft** - A gentle, gradual attack (suitable for pads, ambient textures).
  - **gradual** - Slow attack leading to full volume (useful for swells and cinematic soundscapes).
  - **percussive** - Extremely sharp attack for rhythmic impact.
- **Sample Usage**:
  ```
  [attack: Soft attack on synth pads for smooth transitions.]
  ```
- **Advice**:
  - Use **sharp attack** for **rhythmic punch** (percussion, electric bass).
  - Use **gradual attack** for **build-ups and orchestral swells**.
  - Combine with `[sustain]` to shape the **envelope** of a sound.

---

## [background-vocals]
- **Meaning**: Specifies **harmonized or complementary vocals** that support the lead vocal.
- **Placement**: Typically used within `[vocals]`, `[harmony]`, or `[structure]`.
- **Accepted Parameters**:
  - **harmonic** - Background vocals provide harmonic support.
  - **call-response** - Background vocals interact with the lead.
  - **layered** - Multiple vocal tracks stacked for richness.
  - **ethereal** - Distant, reverb-heavy vocals for ambiance.
  - **chant** - Repeated, rhythmic background phrases.
- **Sample Usage**:
  ```
  [background-vocals: Layered harmonies in the chorus for depth.]
  ```
- **Genre-Based Usage**:
  - **Pop & R&B**: Rich **harmonic background vocals** enhance melodies.
  - **Gospel & Soul**: **Call-and-response** vocals create intensity.
  - **Electronic & Dream Pop**: **Ethereal vocals** blend into atmospheric textures.
  - **Rock & Metal**: **Chanted or shouted background vocals** add energy.

### **Track Structure Recommendation**
- **[intro: Sparse, whispered background vocals]**
- **[verse: Subtle harmonies supporting the melody]**
- **[chorus: Layered, full background harmonies]**
- **[bridge: Call-and-response vocals adding drama]**
- **[outro: Ethereal fade-out with reverb on background vocals]**

---

## [bass]
- **Meaning**: Defines the **bassline characteristics**, its prominence, and style.
- **Placement**: Typically placed within `[instruments]`, `[mixing]`, or `[rhythm]`.
- **Accepted Parameters**:
  - **deep** - Low, rumbling bass frequencies.
  - **sub-bass** - Focus on **low-end frequencies** under 60Hz.
  - **pulsing** - Repetitive bass rhythm, often in electronic music.
  - **saturated** - Heavy, distorted bass (common in **phonk, industrial, metal**).
  - **modulated** - Bass with frequency or amplitude variations.
  - **syncopated** - Offbeat or groove-heavy bass patterns.
- **Sample Usage**:
  ```
  [bass: Deep, pulsating sub-bass driving the rhythm.]
  ```
- **Advice**:
  - **Deep/sub-bass** works best for **electronic, trap, and cinematic** music.
  - **Syncopated bass** is ideal for **funk, jazz, and reggae**.
  - Use **saturation or distortion** to create a **gritty, aggressive tone**.

---

## [bass-slide]
- **Meaning**: Specifies a **sliding bass note**, often used for groove or tension.
- **Placement**: Typically used within `[bass]`, `[rhythm]`, or `[effects]`.
- **Accepted Parameters**:
  - **upward** - Slide from a lower pitch to a higher note.
  - **downward** - Slide from a higher pitch to a lower note.
  - **glissando** - A smooth, continuous slide.
  - **percussive** - Short, quick slides for rhythmic emphasis.
  - **synth** - A bass slide effect generated on a synthesizer.
- **Sample Usage**:
  ```
  [bass-slide: Downward glissando before the chorus drop.]
  ```
- **Genre-Based Usage**:
  - **Funk & Jazz**: Upward **bass slides add groove**.
  - **Hip-Hop & Trap**: **808 sub-bass slides** create deep movement.
  - **Rock & Metal**: **Aggressive bass slides** introduce breakdowns.
  - **Electronic & House**: **Synth bass slides** add energy to drops.

### **Track Structure Recommendation**
- **[intro: Deep, slow bass slide into the groove]**
- **[verse: Subtle slides in the bassline for fluidity]**
- **[chorus: Upward bass-slide leading into the drop]**
- **[bridge: Dramatic downward slide transitioning to tension]**
- **[outro: Fading bass-slide resolving into silence]**

---

## [beat-switch]
- **Meaning**: Indicates a **sudden or gradual change in rhythm**, often altering tempo, groove, or drum patterns.
- **Placement**: Typically used within `[rhythm]`, `[structure]`, or `[break]`.
- **Accepted Parameters**:
  - **sudden** - A sharp, unexpected change in beat.
  - **gradual** - A slow transition from one beat to another.
  - **double-time** - The beat shifts to twice the original speed.
  - **half-time** - The beat slows to half speed.
  - **syncopated** - The rhythm becomes more unpredictable.
- **Sample Usage**:
  ```
  [beat-switch: Sudden double-time transition into the drop.]
  ```
- **Genre-Based Usage**:
  - **Hip-Hop & Phonk**: **Beat-switches** create contrast between sections.
  - **Trap & EDM**: **Half-time switches** slow the groove for tension.
  - **Jazz & Funk**: **Syncopated beat-switches** add complexity.
  - **Rock & Metal**: **Double-time sections** increase intensity.

### **Track Structure Recommendation**
- **[intro: Slow, steady beat]**
- **[verse: Syncopated groove with tension]**
- **[chorus: Sudden beat-switch to double-time]**
- **[bridge: Half-time breakdown for contrast]**
- **[outro: Gradual fade into the original groove]**

---

## [big finish]
- **Meaning**: Defines a **grand, climactic ending**, often with **increased volume, instrumentation, or dramatic buildup**.
- **Placement**: Typically used within `[structure]`, `[dynamics]`, or `[orchestration]`.
- **Accepted Parameters**:
  - **orchestral** - Full symphonic ending.
  - **rock** - Extended guitar and drum finale.
  - **electronic** - Massive synth drop or explosion.
  - **fade-out** - Grand but gradually diminishing.
  - **percussive** - Intense drum fills leading to the end.
- **Sample Usage**:
  ```
  [big finish: Orchestral swells and cymbal crashes building to a dramatic ending.]
  ```
- **Genre-Based Usage**:
  - **Cinematic & Classical**: **Orchestral swells** for epic finales.
  - **Rock & Metal**: **Explosive guitar solos and drum fills**.
  - **EDM & House**: **Huge synth climax** followed by silence.
  - **Pop & Ballads**: **Gradual fade-out with layered vocals**.

### **Track Structure Recommendation**
- **[intro: Soft, minimal entry]**
- **[verse: Building intensity with each phrase]**
- **[chorus: Expanding into rich harmonies]**
- **[bridge: Peak of emotional tension]**
- **[outro: Big finish with all instruments at full power]**

---


- **Meaning**: Indicates a section where **energy gradually increases**, leading into a climax or drop.
- **Placement**: Typically placed within `[structure]`, `[dynamics]`, or `[arrangement]`.
- **Accepted Parameters**:
  - **orchestral swell** - Gradual increase in volume using orchestral instruments.
  - **percussive rise** - Increasing drum intensity.
  - **synth riser** - Electronic sound increasing in pitch and volume.
  - **filtered buildup** - Progressive removal of **low/high frequencies** to create anticipation.
  - **crescendo** - General increase in intensity.
- **Sample Usage**:
  ```
  [buildup: Synth risers and filtered drums lead into the drop.]
  ```
- **Advice**:
  - **Layer different instruments** (e.g., drums, synths, strings) for more dramatic buildups.
  - Use **filtered buildups** to emphasize **tension and release**.
  - Keep buildups **consistent with genre norms** (orchestral in cinematic, risers in EDM).

---

## [cadence]
- **Meaning**: Defines how a **musical phrase ends** in terms of **chord progression** or **resolution**.
- **Placement**: Typically placed within `[harmony]`, `[structure]`, or `[theme]`.
- **Accepted Parameters**:
  - **perfect cadence** - Strong resolution (V-I progression).
  - **plagal cadence** - "Amen" sound, softer resolution (IV-I progression).
  - **deceptive cadence** - Leads to an unexpected chord (V-vi progression).
  - **suspended cadence** - Leaves the resolution hanging (V-IV or unresolved progressions).
  - **chromatic cadence** - Ending involving **non-diatonic** movement.
- **Sample Usage**:
  ```
  [cadence: Deceptive cadence keeps the suspense before resolution.]
  ```
- **Advice**:
  - **Perfect cadences** create **strong closures** in **classical and pop**.
  - **Deceptive cadences** are useful for **suspenseful or dramatic effects**.
  - Use **suspended cadences** to create **open-ended, atmospheric conclusions**.

---

## [cadential]
- **Meaning**: Specifies the type of harmonic progression leading into a **cadence** (the ending of a musical phrase or section).
- **Placement**: Typically used within `[harmony]`, `[structure]`, or `[theme]`.
- **Accepted Parameters**:
  - **strong** - A definitive cadence, often **V-I** (dominant to tonic).
  - **weak** - Less conclusive, often ending on a **subdominant or supertonic**.
  - **suspended** - An unresolved cadence, leaving harmonic tension.
  - **interrupted** - A deceptive cadence, leading to an unexpected chord.
  - **chromatic** - Cadences involving non-diatonic notes for added color.
- **Sample Usage**:
  ```
  [cadential: Strong V-I resolution at the end of the chorus.]
  ```
- **Advice**:
  - **Use strong cadences** to create a **sense of closure**.
  - **Weak or suspended cadences** are great for building anticipation.
  - **Chromatic cadences** can add emotional or exotic harmonic effects.

---

## [call-and-response]
- **Meaning**: Defines a musical interaction where a phrase (the "call") is followed by a responding phrase (the "response"), commonly used in **blues, gospel, jazz, and African music**.
- **Placement**: Typically placed within `[structure]` or `[vocals]`.
- **Accepted Parameters**:
  - **instrumental** - The response is played by instruments.
  - **vocal** - The response is sung by another voice or choir.
  - **echoed** - The response mimics the original call.
  - **contrapuntal** - The response creates a **counterpoint** rather than direct imitation.
  - **syncopated** - The response shifts the rhythmic pattern.
- **Sample Usage**:
  ```
  [call-and-response: Saxophone calls with trumpet responses.]
  ```
- **Advice**:
  - **Use instrumental call-and-response** for **jazz and funk**.
  - **Use vocal responses** for **choir and gospel**.
  - **Contrapuntal responses** work well for **baroque or jazz improvisation**.

---

## [chant]
- **Meaning**: Specifies a **repetitive, rhythmic vocal phrase**, often used for emphasis or ritualistic effect.
- **Placement**: Typically used within `[vocals]`, `[structure]`, or `[harmony]`.
- **Accepted Parameters**:
  - **repetitive** - The phrase is looped multiple times.
  - **monotone** - A single note chant without melody variation.
  - **harmonic** - Layered chanting with harmonies.
  - **tribal** - Percussion-driven, earthy rhythmic chants.
  - **ritualistic** - Dark or mystical chanting style.
- **Sample Usage**:
  ```
  [chant: Deep, monotone chanting layered over bass drones.]
  ```
- **Genre-Based Usage**:
  - **Gothic & Darkwave**: **Ritualistic chants** add eerie depth.
  - **Hip-Hop & Trap**: **Repetitive chants** provide rhythmic hooks.
  - **Folk & World Music**: **Tribal-style chants** for cultural influence.
  - **Electronic & Psytrance**: **Layered chant loops** create hypnotic vibes.

### **Track Structure Recommendation**
- **[intro: Distant chants fading in]**
- **[verse: Lead vocals with rhythmic chant backing]**
- **[chorus: Full harmonic chanting with layered vocals]**
- **[bridge: Stripped-down percussion with solo chanting]**
- **[outro: Chanting fading into silence]**

---

## [choir]
- **Meaning**: Specifies **group vocal harmonization**, often for a grand, emotional effect.
- **Placement**: Typically used within `[vocals]`, `[harmony]`, or `[structure]`.
- **Accepted Parameters**:
  - **layered** - Thick, multi-part harmony.
  - **angelic** - Light, ethereal vocal blending.
  - **powerful** - Strong, dominant choir presence.
  - **dissonant** - Slight harmonic tension in the choral arrangement.
  - **gospel** - Energetic, uplifting choir harmonies.
- **Sample Usage**:
  ```
  [choir: Angelic high-pitched harmonies in the background of the chorus.]
  ```
- **Genre-Based Usage**:
  - **Gospel & Soul**: **Full, harmonic choir sections** drive emotional power.
  - **Classical & Cinematic**: **Layered choral voices** for grandeur.
  - **Metal & Symphonic Rock**: **Dark choirs** create drama and tension.
  - **Electronic & Ambient**: **Reverb-heavy ethereal choirs** add texture.

### **Track Structure Recommendation**
- **[intro: Soft choir hums with pads]**
- **[verse: Subtle choral harmonies under lead vocals]**
- **[chorus: Full choir harmonization]**
- **[bridge: Choir-only interlude with layered harmonies]**
- **[outro: Angelic choir fading into silence]**

---

## [chromatic]
- **Meaning**: Refers to the use of notes **outside the diatonic scale**, creating richer harmonic movement and tension.
- **Placement**: Typically used within `[harmony]` or `[structure]`.
- **Accepted Parameters**:
  - **ascending** - A chromatic passage moving upwards.
  - **descending** - A chromatic passage moving downwards.
  - **full** - A passage that uses **every semitone** within an octave.
  - **partial** - Chromaticism used sparingly.
  - **ornamental** - Used for embellishment rather than harmonic movement.
- **Sample Usage**:
  ```
  [chromatic: Descending chromatic scale in the bridge section.]
  ```
- **Advice**:
  - **Chromatic melodies** create a **jazzy or dramatic** effect.
  - **Partial chromaticism** is great for adding **melodic color**.
  - **Descending chromatic movement** often conveys **melancholy or tension**.

---

## [climax]
- **Meaning**: Defines the **peak moment of intensity** in the composition, usually involving **increased dynamics, energy, or harmonic tension**.
- **Placement**: Typically used within `[structure]`, `[dynamics]`, or `[harmony]`.
- **Accepted Parameters**:
  - **sudden** - A sharp, unexpected burst of intensity.
  - **gradual** - A slow build-up leading to the climax.
  - **instrumental** - The peak is led by instruments rather than vocals.
  - **vocal-driven** - The climax is focused on an expressive vocal moment.
  - **layered** - Various instruments stack up to build the intensity.
- **Sample Usage**:
  ```
  [climax: Gradual build with layered strings and a powerful vocal peak.]
  ```
- **Genre-Based Usage**:
  - **Classical & Cinematic**: Strings and brass **swelling into an orchestral explosion**.
  - **Rock & Metal**: **Guitar solos and drum intensity** heighten energy.
  - **EDM & Trance**: **Big synth rises** leading into a massive drop.
  - **Pop & Ballads**: A **vocal belt moment** paired with orchestral backing.

### **Track Structure Recommendation**
- **[intro: Soft, slow instrumental opening]**
- **[verse: Gradual increase in energy with layered melodies]**
- **[chorus: Expanded arrangement with stronger vocals]**
- **[climax: Full intensity with drums, vocals, and orchestral backing]**
- **[outro: Gradual descent back into soft textures]**

---

## [cluster]
- **Meaning**: Specifies the use of **tone clusters**—closely spaced notes played together to create a **dissonant or textured** sound.
- **Placement**: Typically used within `[harmony]` or `[structure]`.
- **Accepted Parameters**:
  - **soft** - Gentle, ambient clusters (e.g., softly played piano or synth pads).
  - **harsh** - Dissonant, aggressive clusters used for tension.
  - **chaotic** - Unpredictable, heavily layered tone clusters.
  - **orchestral** - Clusters played by **string sections, woodwinds, or brass**.
  - **electronic** - Synth-based clusters with modulated frequencies.
- **Sample Usage**:
  ```
  [cluster: Harsh orchestral brass clusters in the climax.]
  ```
- **Advice**:
  - **Soft clusters** work well for **ambient and impressionistic music**.
  - **Harsh clusters** are used in **horror scores, avant-garde, and industrial**.
  - **Electronic clusters** can create **textural drone effects**.

---

## [consonance]
- **Meaning**: Specifies harmonies that **sound stable, resolved, and pleasant**, in contrast to **dissonance**.
- **Placement**: Typically used within `[harmony]`, `[chords]`, or `[theme]`.
- **Accepted Parameters**:
  - **soft** - Warm, gentle consonance (e.g., major 3rds, perfect 5ths).
  - **bright** - Open, ringing consonance (e.g., high-frequency harmonics).
  - **rich** - Full, extended consonance (e.g., added 6th or 9th chords).
  - **ethereal** - Light, floating consonance (e.g., unresolved 7th chords).
- **Sample Usage**:
  ```
  [consonance: Rich harmonies with open voicings.]
  ```
- **Advice**:
  - **Bright consonance** works well for **orchestral and cinematic music**.
  - **Soft consonance** is ideal for **lullabies, ambient music, and smooth jazz**.
  - **Rich consonance** creates a **fuller, emotional harmonic structure**.

---

## [content]
- **Meaning**: Specifies the **lyrical or thematic focus** of the composition.
- **Placement**: Typically used within `[lyrics]`, `[theme]`, or `[mood]`.
- **Accepted Parameters**:
  - **narrative** - A storytelling-driven approach.
  - **abstract** - Non-linear or impressionistic themes.
  - **emotional** - Focused on deep emotional expression.
  - **philosophical** - Reflective, thought-provoking themes.
  - **surreal** - Dreamlike, otherworldly imagery.
- **Sample Usage**:
  ```
  [content: Abstract reflections on dreams and memories.]
  ```
- **Genre-Based Usage**:
  - **Singer-Songwriter & Folk**: **Narrative lyrics** tell stories.
  - **Experimental & Psychedelic**: **Surreal and abstract** imagery dominates.
  - **Hip-Hop & Rap**: **Philosophical and personal themes** drive lyricism.
  - **Rock & Metal**: **Emotional intensity** leads storytelling.

### **Track Structure Recommendation**
- **[intro: Setting the theme with instrumental tone]**
- **[verse: Lyrical exposition developing the story]**
- **[chorus: Emotional peak with expressive delivery]**
- **[bridge: A contrasting lyrical idea or realization]**
- **[outro: Poetic resolution or lingering question]**

---

## [counterpoint]
- **Meaning**: Specifies the **interweaving of multiple independent melodic lines**, often used in classical and complex compositions.
- **Placement**: Typically used within `[harmony]` or `[structure]`.
- **Accepted Parameters**:
  - **simple** - Light counterpoint with two melodies.
  - **complex** - Multiple layers of melodic interplay.
  - **fugue-like** - A strict contrapuntal structure with variations.
  - **imitative** - One melodic line repeats or mimics another.
  - **contrasting** - The counter-melodies are highly distinct from each other.
- **Sample Usage**:
  ```
  [counterpoint: Imitative string lines weaving around the main theme.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: Used in **fugues and choral compositions**.
  - **Progressive Rock & Jazz**: **Contrapuntal guitar and keyboard interplay**.
  - **Electronic & Synthwave**: **Layered arpeggios acting as counter-melodies**.
  - **Film Scores & Orchestral**: **Rich, multi-voiced textures** create drama.

### **Track Structure Recommendation**
- **[intro: Soft piano motif introduced]**
- **[verse: Simple counterpoint between strings and woodwinds]**
- **[chorus: Richer layers, adding brass and backing vocals]**
- **[bridge: Complex fugue-like variations of the main melody]**
- **[outro: Counterpoint gradually fading out into resolution]**

---

## [crescendo]
- **Meaning**: Specifies a **gradual increase in volume and intensity**, building anticipation and emotional impact.
- **Placement**: Typically used within `[dynamics]`, `[structure]`, or `[orchestration]`.
- **Accepted Parameters**:
  - **slow** - A long, drawn-out build-up.
  - **fast** - A rapid dynamic swell.
  - **layered** - Instruments gradually enter to increase intensity.
  - **orchestral** - A full-bodied cinematic swell.
  - **electronic** - Synth and effect-based crescendo leading to a drop.
- **Sample Usage**:
  ```
  [crescendo: Slow orchestral build leading into a dramatic climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Cinematic**: Used for **dramatic moments in symphonic music**.
  - **Rock & Metal**: Builds into **guitar solos or intense chorus entries**.
  - **EDM & Dance**: Leads into **drops using risers and FX**.
  - **Ambient & Post-Rock**: **Layered textures swelling into climaxes**.

### **Track Structure Recommendation**
- **[intro: Soft pad textures with slow crescendo]**
- **[verse: Gradual instrumental layering]**
- **[chorus: Full orchestration at peak intensity]**
- **[bridge: Lower dynamic, preparing for another crescendo]**
- **[outro: Slow fade, diminishing in volume]**

---

## [development]
- **Meaning**: Defines the **evolution of a theme**, whether through variations, new harmonies, or instrumental shifts.
- **Placement**: Typically used within `[structure]` or `[theme]`.
- **Accepted Parameters**:
  - **thematic** - The original theme evolves over time.
  - **harmonic** - Chord progressions gradually transform.
  - **orchestral** - Increasing instrumental complexity.
  - **electronic** - Gradual modulation of synth textures.
  - **minimalist** - Subtle, repeated transformations.
- **Sample Usage**:
  ```
  [development: Harmonic shifts and layered instrumentation evolving throughout.]
  ```
- **Genre-Based Usage**:
  - **Classical & Romantic**: Central to **sonatas and symphonies**.
  - **Jazz & Blues**: **Improvised solos** develop the core theme.
  - **Electronic & Progressive Rock**: **Gradual synth or guitar evolution**.
  - **Soundtrack & Ambient**: **Slow-moving changes in texture and harmony**.

### **Track Structure Recommendation**
- **[intro: Simple motif introduced]**
- **[verse: Thematic variation with subtle instrumentation shifts]**
- **[chorus: Expanded version with harmonic changes]**
- **[bridge: Completely transformed theme with contrasting elements]**
- **[outro: Final statement of theme with subtle alterations]**

---

## [diminuendo]
- **Meaning**: Specifies a **gradual decrease in volume and intensity**, opposite of a crescendo.
- **Placement**: Typically used within `[dynamics]`, `[structure]`, or `[orchestration]`.
- **Accepted Parameters**:
  - **slow** - A long, gradual decrease.
  - **fast** - A sudden reduction in intensity.
  - **layered** - Elements fade one by one.
  - **orchestral** - Strings and brass fading into softer instruments.
  - **electronic** - Filters and reverb reducing volume dynamically.
- **Sample Usage**:
  ```
  [diminuendo: Orchestral swell fading into a solo violin melody.]
  ```
- **Genre-Based Usage**:
  - **Classical & Opera**: Used to **end pieces with elegance**.
  - **Rock & Pop**: Applied to **chorus fade-outs**.
  - **Electronic & Ambient**: **Gradual filters and reverb reductions**.
  - **Jazz & Funk**: **Soft brass and piano fade-outs**.

### **Track Structure Recommendation**
- **[intro: Building harmonies with dynamic intensity]**
- **[verse: Strong, rhythmic presence]**
- **[chorus: Peak volume and instrumentation]**
- **[bridge: Gradual dimming of layers]**
- **[outro: Soft resolution with fading notes]**

---

## [dissonance]
- **Meaning**: Refers to harmonic tension created by **unstable or clashing note combinations**. Often used to create drama, tension, and emotional intensity.
- **Placement**: Typically used within `[harmony]`, `[chords]`, or `[theme]`.
- **Accepted Parameters**:
  - **mild** - Subtle tension, often used in jazz or cinematic music.
  - **harsh** - Strong, aggressive dissonance (common in horror, avant-garde).
  - **clashing** - Extreme dissonance, used for unsettling effects.
  - **resolved** - Temporary dissonance that moves toward consonance.
  - **sustained** - A prolonged dissonant harmony for atmospheric effect.
- **Sample Usage**:
  ```
  [dissonance: Harsh sustained strings for eerie suspense.]
  ```
- **Advice**:
  - **Use mild dissonance** for **jazz, blues, and orchestral compositions**.
  - **Harsh dissonance** is great for **horror, experimental, and industrial music**.
  - **Resolved dissonance** creates a balance between tension and relief.

---

## [distorted vocals]
*   **Meaning**: Applies a **gritty, overdriven, or processed effect** to the voice. Produces a raw or industrial tone.
*   **Placement**: Within `[vocals]` or `[effects]`.
*   **Accepted Parameters**:
    *   **harsh** – strong distortion, almost screamed.
    *   **gritty** – rough, rock-style overdrive.
    *   **industrial** – digital, metallic distortion.
    *   **subtle** – light saturation for texture.
*   **Sample Usage**:
    ```
    [distorted vocals: Gritty, overdriven delivery in chorus]  
    ```
*   **Genre-Based Usage**:
    *   **Rock/Metal**: Aggressive vocal edge.
    *   **Industrial/Experimental**: Metallic or glitchy vocal treatment.
    *   **EDM/Trap**: Distorted hooks or vocal chops.
### **Track Structure Recommendation**:
    *   `[verse: clean vocals]`
    *   `[chorus: distorted vocals layered with harmonies]`
    *   `[bridge: instrumental break, return to clean]`

---

## [distortion]
- **Meaning**: Specifies **audio processing** that **adds harmonic saturation, clipping, or fuzz** to an instrument or sound.
- **Placement**: Typically used within `[instruments]`, `[mixing]`, or `[effects]`.
- **Accepted Parameters**:
  - **light** - Gentle distortion for warmth (often in blues, rock).
  - **heavy** - Strong, aggressive distortion (common in metal, industrial).
  - **overdrive** - Mild saturation (used in classic rock and blues).
  - **fuzz** - Extreme distortion with a rough edge.
  - **crushed** - Digital bit-crushing for lo-fi and glitch effects.
- **Sample Usage**:
  ```
  [distortion: Heavy electric guitar in the chorus.]
  ```
- **Advice**:
  - **Overdrive works well** for **blues, funk, and vintage rock**.
  - **Heavy distortion is essential** in **metal, industrial, and punk**.
  - **Crushed distortion** is perfect for **lo-fi, glitch, and experimental tracks**.

---

## [drum-fill]
- **Meaning**: Specifies **a short percussive passage** that serves as a transition between sections.
- **Placement**: Typically used within `[rhythm]`, `[structure]`, or `[effects]`.
- **Accepted Parameters**:
  - **simple** - A short, clean drum fill.
  - **complex** - A fast, multi-layered fill.
  - **syncopated** - A rhythmically offbeat drum fill.
  - **rolling** - A continuous roll into the next section.
  - **heavy** - A powerful drum fill with toms and cymbals.
- **Sample Usage**:
  ```
  [drum-fill: Heavy rolling toms leading into the chorus.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **Powerful tom fills** drive intensity.
  - **Jazz & Funk**: **Syncopated snare and hi-hat fills**.
  - **Electronic & House**: **Quick snare builds leading into a drop**.
  - **Pop & R&B**: **Smooth transition fills** for polished production.

### **Track Structure Recommendation**
- **[intro: Soft beat introduction]**
- **[verse: Groove with subtle fills]**
- **[chorus: Heavy rolling toms leading into the next section]**
- **[bridge: Syncopated drum fill increasing tension]**
- **[outro: Final drum hit fade-out]**

---

## [duet]

**Category:** Vocal configuration tag  
**Primary use:** To request two distinct lead voices sharing the spotlight: trading lines, harmonizing, or answering each other.

**Behavior and intent**  
`[duet]` suggests a conversation or partnership between two singers. Suno may interpret this as contrasting timbres (e.g., one higher, one lower) or different phrasing styles.

**Placement and syntax**  

- *Lyrics field:*  
  - At the start of the track or specific sections:  
    - `[duet | female lead + male lead, alternating lines]`  
    - `[chorus | duet, both voices sing together in harmony]`  
  - You can add inline cues like “(Voice A)” / “(Voice B)” if you want the text to imply who sings what, even though it’s a soft hint.
- *Style of Music field:*  
  - “romantic ballad duet with intertwined vocals and gentle piano”

**Typical use-cases**  

- Dialog-based love songs or narrative conversations  
- Call‑and‑response choruses in pop, gospel, or folk  
- Two‑character story tracks (e.g., Wilds Sisters, two Personas, etc.)

Keep the language around the duet simple (“two voices”, “trading lines”, “singing together”) to avoid confusing the model with too much detail.

---

## [dynamics]
- **Meaning**: Defines **how volume and intensity change** over the course of the track.
- **Placement**: Typically used within `[mixing]`, `[structure]`, or `[harmony]`.
- **Accepted Parameters**:
  - **soft-loud** - Gradual build from quiet to intense.
  - **loud-soft** - A sudden drop in intensity.
  - **balanced** - Evenly maintained dynamics throughout.
  - **layered** - Different instruments fade in and out dynamically.
  - **swelling** - Gradual increases and decreases over time.
- **Sample Usage**:
  ```
  [dynamics: Soft-loud progression, building toward the climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Cinematic**: **Swelling orchestral sections**.
  - **Rock & Metal**: **Loud-soft contrasts for dramatic effect**.
  - **Electronic & House**: **Gradual builds leading into drops**.
  - **Jazz & Blues**: **Dynamic phrasing in solos and vocals**.

### **Track Structure Recommendation**
- **[intro: Soft ambient tones]**
- **[verse: Gradual increase in instrumentation]**
- **[chorus: Full dynamic intensity]**
- **[bridge: Drop in intensity for contrast]**
- **[outro: Fading, quiet textures]**

---

## [echo]
- **Meaning**: Defines **delayed repetitions** of a sound, creating a sense of **space and depth**.
- **Placement**: Typically used within `[effects]`, `[mixing]`, or `[sfx]`.
- **Accepted Parameters**:
  - **short** - Quick, tight echo (adds rhythmic texture).
  - **long** - Extended echoes, used for atmospheric effects.
  - **delayed** - A noticeable delay before repetition.
  - **stereo** - Echo panned to different sides of the stereo field.
  - **reversed** - Echoes played in reverse for surreal effects.
- **Sample Usage**:
  ```
  [echo: Long stereo vocal echoes for a spacious feel.]
  ```
- **Advice**:
  - **Short echo** is useful for **adding presence to vocals**.
  - **Long or stereo echoes** create **dreamy or cinematic atmospheres**.
  - **Reversed echoes** can be used for **psychedelic and experimental tracks**.

---

## [effects]
- **Meaning**: Specifies **additional sound effects** applied to instruments, vocals, or the overall track.
- **Placement**: Typically used within `[mixing]`, `[sfx]`, or `[instruments]`.
- **Accepted Parameters**:
  - **reverb** - Adds spaciousness to the sound.
  - **delay** - Repeats the sound with a slight time gap.
  - **flanger** - Creates a swirling, modulated effect.
  - **chorus** - Slightly detuned copies of the sound for a richer tone.
  - **phaser** - Phase-shifted sound creating a sweeping effect.
  - **compression** - Balances volume dynamics.
  - **glitch** - Adds unpredictable distortions and pitch shifts.
- **Sample Usage**:
  ```
  [effects: Reverb and chorus on electric piano for a lush feel.]
  ```
- **Advice**:
  - **Reverb is essential** for **natural space and ambiance**.
  - **Use flanger and phaser** for **psychedelic and electronic textures**.
  - **Glitch effects** are great for **experimental and electronic genres**.

---

## [element]
- **Meaning**: Specifies **a specific musical component** to emphasize in the mix.
- **Placement**: Typically used within `[mixing]`, `[focus]`, or `[structure]`.
- **Accepted Parameters**:
  - **melody** - Focus on lead melodic instruments.
  - **harmony** - Chordal structure is prominent.
  - **bass** - Emphasis on low-end frequencies.
  - **percussion** - Drums and rhythmic textures take priority.
  - **synth** - Electronic textures and pads are featured.
- **Sample Usage**:
  ```
  [element: Melody-focused orchestration with soaring violin leads.]
  ```
- **Genre-Based Usage**:
  - **Orchestral & Cinematic**: **Emphasizing melody and harmony**.
  - **Electronic & Ambient**: **Focused on synth and bass layers**.
  - **Jazz & Blues**: **Highlighting improvisational elements**.
  - **Rock & Metal**: **Balancing bass, drums, and melody**.

### **Track Structure Recommendation**
- **[intro: Bass-heavy foundation]**
- **[verse: Melody-driven section with harmonic support]**
- **[chorus: Synth elements becoming more prominent]**
- **[bridge: Emphasis on percussion and bass]**
- **[outro: Melody fading into silence]**

---

## [emotional]
- **Meaning**: Defines the **emotional tone** of the composition.
- **Placement**: Typically used within `[mood]`, `[style]`, or `[vocals]`.
- **Accepted Parameters**:
  - **melancholic** - Sad, reflective tone.
  - **uplifting** - Positive, energetic mood.
  - **dramatic** - High emotional stakes.
  - **nostalgic** - Reminiscent of past themes.
  - **ethereal** - Dreamlike, otherworldly quality.
- **Sample Usage**:
  ```
  [emotional: Dramatic, swelling orchestration building into a powerful finale.]
  ```
- **Genre-Based Usage**:
  - **Cinematic & Orchestral**: **Grand, emotive compositions**.
  - **Indie & Alternative**: **Melancholic storytelling**.
  - **Electronic & Ambient**: **Ethereal and nostalgic moods**.
  - **Pop & R&B**: **Uplifting, emotional vocals**.

### **Track Structure Recommendation**
- **[intro: Soft piano intro setting a melancholic tone]**
- **[verse: Nostalgic vocal delivery with swelling strings]**
- **[chorus: Dramatic peak with layered harmonies]**
- **[bridge: Soft breakdown emphasizing emotion]**
- **[outro: Ethereal fade-out with lingering vocals]**

---

## [end]
- **Meaning**: Defines the **final section or conclusion** of a piece.
- **Placement**: Typically used within `[structure]`, `[coda]`, or `[outro]`.
- **Accepted Parameters**:
  - **sudden** - An abrupt stop.
  - **fade-out** - Gradual volume reduction.
  - **orchestral** - A grand, full-bodied closing.
  - **acoustic** - A stripped-down, intimate ending.
  - **reprise** - A final return to the main theme.
- **Sample Usage**:
  ```
  [end: Soft piano outro fading into silence.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **Sudden or crashing finales**.
  - **Pop & R&B**: **Smooth fade-out endings**.
  - **Jazz & Blues**: **Soft, improvisational finishes**.
  - **Classical & Film Score**: **Grand orchestral closings**.

### **Track Structure Recommendation**
- **[intro: Thematic motif introduced]**
- **[verse: Expands on theme]**
- **[chorus: Peak intensity with full instrumentation]**
- **[bridge: Contrast in tone or harmony]**
- **[end: Reprise of main theme with fading dynamics]**

---

## [ensemble]
- **Meaning**: Specifies the **type and size of musical group performing the piece**, ranging from small acoustic duos to full orchestras.
- **Placement**: Typically used within `[instruments]`, `[orchestration]`, or `[structure]`.
- **Accepted Parameters**:
  - **duo** - Two performers or instruments.
  - **quartet** - A four-instrument or vocal ensemble.
  - **chamber** - Small classical ensemble (e.g., strings, woodwinds).
  - **symphonic** - Full symphony orchestra.
  - **big-band** - Jazz-oriented large ensemble.
  - **electronic** - Synth-heavy layered instrumentals.
- **Sample Usage**:
  ```
  [ensemble: Chamber strings with light percussive support.]
  ```
- **Genre-Based Usage**:
  - **Classical & Cinematic**: **Chamber and symphonic ensembles**.
  - **Jazz & Swing**: **Big-band brass sections**.
  - **Folk & Acoustic**: **Duo or quartet-style arrangements**.
  - **Electronic & Synthwave**: **Layered digital ensembles**.

### **Track Structure Recommendation**
- **[intro: Sparse strings setting a contemplative tone]**
- **[verse: Expanding ensemble with additional harmonies]**
- **[chorus: Full symphonic sound with layered brass and percussion]**
- **[bridge: Stripped-down quartet section for contrast]**
- **[outro: Gentle fade-out with only a piano duo]**

---

## [epic]
- **Meaning**: Defines a **grand, large-scale, and dramatic quality** in the composition.
- **Placement**: Typically used within `[style]`, `[orchestration]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **cinematic** - Large orchestral arrangements, often used in film scoring.
  - **battle** - High-energy, intense rhythmic focus.
  - **triumphant** - Builds toward a heroic climax.
  - **dark** - Mysterious and heavy, with tension.
  - **ethereal** - Grand but with an airy, floating quality.
- **Sample Usage**:
  ```
  [epic: Triumphant orchestral buildup with heavy percussion and brass.]
  ```
- **Genre-Based Usage**:
  - **Film Score & Classical**: **Cinematic, orchestral crescendos**.
  - **Metal & Symphonic Rock**: **Heavy, dramatic instrumentation**.
  - **Electronic & Hybrid**: **Synth-driven epic buildups**.
  - **World & Folk Fusion**: **Large-scale, battle-march compositions**.

### **Track Structure Recommendation**
- **[intro: Slow, brooding strings with distant percussion]**
- **[verse: Rising tension with low brass and deep drums]**
- **[chorus: Full explosion of sound with choirs and heavy percussion]**
- **[bridge: Soft, ethereal section leading into the final push]**
- **[outro: Grand, fading orchestral finale with triumphant tones]**

---

## [episode]
- **Meaning**: Defines a **self-contained musical section**, often functioning as a contrasting or transitional moment.
- **Placement**: Typically used within `[structure]`, `[form]`, or `[development]`.
- **Accepted Parameters**:
  - **melodic** - The episode introduces a new melody.
  - **harmonic** - A shift in chordal structure.
  - **percussive** - A drum-heavy interlude.
  - **instrumental** - Features only instruments, no vocals.
  - **syncopated** - Rhythmically complex, often jazz- or funk-based.
- **Sample Usage**:
  ```
  [episode: Syncopated piano-driven section before returning to the main theme.]
  ```
- **Genre-Based Usage**:
  - **Classical & Fugue**: **Melodic development episodes**.
  - **Progressive Rock & Jazz**: **Instrumental solos and rhythmic variations**.
  - **Electronic & Dance**: **Breakbeat episodes in house or techno**.
  - **Hip-Hop & Trap**: **Beat switches creating contrast**.

### **Track Structure Recommendation**
- **[intro: Establishing the main theme]**
- **[verse: Developing the first melodic phrase]**
- **[episode: Harmonic shift with new instrumentation]**
- **[chorus: Returning to the primary hook]**
- **[outro: Reintroducing elements from the episode for a final twist]**

---

## [eq]
- **Meaning**: Defines **equalization settings**, adjusting frequency balance for clarity or effect.
- **Placement**: Typically used within `[mixing]`, `[effects]`, or `[instrument]`.
- **Accepted Parameters**:
  - **bass-heavy** - Emphasizes low-end frequencies.
  - **bright** - Boosts high frequencies.
  - **warm** - A smooth, midrange-heavy mix.
  - **punchy** - Emphasized mid-bass for impact.
  - **lo-fi** - Reduced high frequencies for a vintage feel.
- **Sample Usage**:
  ```
  [eq: Bright, airy vocals with deep, warm bass.]
  ```
- **Genre-Based Usage**:
  - **Hip-Hop & Trap**: **Bass-heavy EQ for deep kicks**.
  - **Lo-Fi & Chillwave**: **Mellow, soft EQ filtering**.
  - **Rock & Punk**: **Punchy midrange guitar presence**.
  - **Orchestral & Film Score**: **Balanced, bright EQ for clarity**.

### **Track Structure Recommendation**
- **[intro: Filtered low-end build-up]**
- **[verse: Bright EQ on vocals, deep bass support]**
- **[chorus: Full-spectrum EQ for dynamic impact]**
- **[bridge: Warm, reduced treble section for contrast]**
- **[outro: High-frequency fade-out, reducing to bass elements]**

---

## [era]
- **Purpose**: Suggests historical or cultural period affecting style.
- **Syntax**: `[era: 1990s Memphis underground]`
- **Usage Tips**: Often paired with `[genre]` or `[style]`.
- **Accepted Parameters**: freeform definition marking the epoch
- **Version Info**: Soft-supported in v4.0+
- **Sample Usage**:
  ```
  [era: retro-futurist 1980s cyberpunk club]
  [era: 1980s neon synthwave]
  [era: 1940s noir jazz ballad]
  [era: 1830s romantic piano prelude]
  ```

---

## [exposition]
- **Meaning**: The **first introduction of the main musical theme**, often recurring in various forms throughout the track.
- **Placement**: Typically used within `[structure]` or `[theme]`.
- **Accepted Parameters**:
  - **thematic** - Clearly introduces the song's main theme.
  - **contrapuntal** - Introduces multiple independent voices.
  - **layered** - Builds up gradually with textures.
  - **stripped-down** - A minimal, soft exposition.
  - **dramatic** - Begins with strong impact.
- **Sample Usage**:
  ```
  [exposition: A quiet, ethereal solo piano introduces the primary theme.]
  ```
- **Genre-Based Usage**:
  - **Classical & Sonata Form**: **Expositions are crucial in symphonies**.
  - **Film & Theatrical Scores**: **Opening motifs return in different variations**.
  - **Jazz & Improvisational Music**: **Thematic statements set up solos**.
  - **Electronic & Progressive Rock**: **Layered build-up of primary elements**.

### **Track Structure Recommendation**
- **[intro: Gentle soundscape preparing for exposition]**
- **[exposition: Main theme introduced with minimal accompaniment]**
- **[development: Variation of the theme with additional instruments]**
- **[recapitulation: Return to the exposition theme with a fuller sound]**
- **[outro: Soft restatement of the exposition, fading out]**

---

## [extend-style]
- **Meaning**: Defines the **way an extension of the track is handled**, particularly in Suno's extension feature.
- **Placement**: Typically used **at the beginning of the "Lyrics" input**, as it applies to how the track is extended beyond its original length.
- **Accepted Parameters**:
  - **seamless** - The extension continues smoothly from the original.
  - **contrasting** - The extension introduces new elements for variety.
  - **thematic** - The extension builds upon the main theme.
  - **instrumental** - The extension focuses on instrumental variations.
  - **looped** - The extension repeats existing material with minor changes.
- **Sample Usage**:
  ```
  [extend-style: Seamless continuation of the theme with evolving synth textures.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Ambient**: Seamless looping for **continuous atmospheres**.
  - **Jazz & Classical**: Thematic extensions for **long-form improvisation**.
  - **EDM & House**: Extended **instrumental builds before a drop**.
  - **Rock & Progressive**: Contrasting sections for **dynamic variation**.

### **Track Structure Recommendation**
- **[intro: Establishing theme with soft pads]**
- **[verse: Smooth transition into rhythmic elements]**
- **[chorus: Strong melodic hook with harmonic backing]**
- **[bridge: Gradual development, leading to an extension]**
- **[extend-style: Thematic expansion with orchestral layering]**
- **[outro: Gentle fade-out with sustained reverb]**

---

## [fade]
- **Meaning**: Specifies **how the track gradually reduces volume**, often at the end or between sections.
- **Placement**: Typically used within `[structure]`, `[dynamics]`, or `[outro]`.
- **Accepted Parameters**:
  - **slow** - Gradual volume decrease over an extended period.
  - **fast** - Quick, abrupt fade.
  - **layered** - Different instruments fade at different times.
  - **filtering** - Frequencies fade gradually rather than pure volume.
  - **reverb-tail** - The fade relies on **reverb decay**.
- **Sample Usage**:
  ```
  [fade: Slow orchestral fade-out with lingering string harmonics.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **Classic fade-outs on repeated chorus**.
  - **Ambient & Chillout**: **Long reverb-based fades**.
  - **Jazz & Blues**: **Instrumental fades with solo improvisations**.
  - **Electronic & Dance**: **Filtered high-end fades** for club mixes.

### **Track Structure Recommendation**
- **[intro: Gentle fade-in of ambient textures]**
- **[verse: Gradual build in energy]**
- **[chorus: Full intensity, sustained instrumentation]**
- **[bridge: Reducing elements, preparing for fade-out]**
- **[fade: Slow disappearance of melodic elements, leaving soft pads]**

---

## [female]
- **Meaning**: Specifies **that the lead or backing vocals should be female**.
- **Placement**: Typically used within `[vocals]`, `[harmony]`, or `[structure]`.
- **Accepted Parameters**:
  - **high** - Soprano or high-pitched female vocals.
  - **mid** - Mezzo-soprano or natural female vocals.
  - **low** - Alto or lower-pitched female voice.
  - **ethereal** - Soft, airy female voice with reverb.
  - **powerful** - Strong, belting female vocals.
- **Sample Usage**:
  ```
  [female: Ethereal soprano voice leading the chorus with reverb.]
  ```
- **Genre-Based Usage**:
  - **Pop & R&B**: **Powerful female lead vocals** for emotional impact.
  - **Classical & Opera**: **High-pitched soprano arias**.
  - **Electronic & Dream Pop**: **Airy female vocals blending into textures**.
  - **Jazz & Soul**: **Smooth, rich alto tones for expressive delivery**.

### **Track Structure Recommendation**
- **[intro: Soft high-pitched female vocal humming]**
- **[verse: Mid-range female vocals over light instrumentation]**
- **[chorus: Powerful belting vocals with rich harmonies]**
- **[bridge: Ethereal, reverb-drenched vocal echoes]**
- **[outro: Gentle soprano whispers fading into silence]**

---

## [fermata]
- **Meaning**: Indicates that a **note or chord is held longer than its usual duration**, creating a moment of emphasis or suspense.
- **Placement**: Typically used within `[harmony]` or `[structure]`.
- **Accepted Parameters**:
  - **sustained** - A long hold on a note.
  - **dramatic** - A fermata that creates tension before resolving.
  - **subtle** - A small pause, slightly extending the note duration.
  - **orchestral** - Fermata used in orchestral settings to highlight a phrase.
- **Sample Usage**:
  ```
  [fermata: Dramatic hold on final chord before resolution.]
  ```
- **Advice**:
  - **Use fermatas sparingly** to maintain pacing.
  - **Dramatic fermatas** work well for **cinematic, orchestral, and classical music**.
  - **Subtle fermatas** add expressiveness to **jazz and ballads**.

---

## [finale]
- **Meaning**: Defines the **grand, concluding section** of a composition, often marked by increased intensity or a resolution.
- **Placement**: Typically used within `[structure]`, `[coda]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **grand** - A strong, full-orchestra or multi-instrument climax.
  - **sparse** - A minimal, intimate closing section.
  - **thematic** - A return to the main theme for final resolution.
  - **dramatic** - A sudden, unexpected conclusion.
  - **fade** - A closing that gradually diminishes in sound.
- **Sample Usage**:
  ```
  [finale: Grand orchestral climax with full choir and cymbal crashes.]
  ```
- **Genre-Based Usage**:
  - **Classical & Opera**: **Large-scale orchestral conclusions**.
  - **Rock & Metal**: **Heavy, sustained guitar and drum finales**.
  - **Electronic & EDM**: **Layered synth peaks leading to silence**.
  - **Film Score & Symphonic**: **Thematic resolution with emotional payoff**.

### **Track Structure Recommendation**
- **[intro: Soft thematic motif]**
- **[verse: Expanding instrumentation and harmonic depth]**
- **[chorus: Peak intensity with layered melodies]**
- **[bridge: A soft contrast before the final build-up]**
- **[finale: Grand orchestral resolution with full instrumentation]**

---

## [focus]
- **Meaning**: Specifies which **instrumental, rhythmic, or harmonic elements** should be most prominent in the track.
- **Placement**: Typically used within `[mixing]`, `[dynamics]`, or `[structure]`.
- **Accepted Parameters**:
  - **melody** - Emphasis on the lead melodic line.
  - **harmony** - The focus is on chord progression and harmonization.
  - **bass** - The low-end frequencies and bassline are the most prominent.
  - **percussion** - The beat and rhythm take precedence.
  - **vocals** - The voice is the central element in the mix.
- **Sample Usage**:
  ```
  [focus: Deep bass and layered harmonies driving the composition.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Dance**: **Bass-focused tracks** for groove-heavy compositions.
  - **Orchestral & Classical**: **Melody-focused with prominent lead instruments**.
  - **Rock & Metal**: **Guitar riffs and harmonic progressions in focus**.
  - **Hip-Hop & Trap**: **Emphasis on vocals and heavy 808 bass**.

### **Track Structure Recommendation**
- **[intro: Subtle pads setting the mood]**
- **[verse: Bass-focused groove with minimal chords]**
- **[chorus: Expanding harmonies to create fullness]**
- **[bridge: Stripped-down percussion focus]**
- **[outro: Melody fades into a soft reverb tail]**

---

## [fragmentation]
- **Meaning**: Refers to breaking down a **melodic, harmonic, or rhythmic theme** into smaller motifs or segments, which are then repeated, altered, or developed.
- **Placement**: Typically used within `[theme]` or `[variation]`.
- **Accepted Parameters**:
  - **melodic** - A fragmented version of the main melody.
  - **rhythmic** - The main rhythm is split into smaller units.
  - **counterpoint** - Fragmented elements are layered for complexity.
  - **staggered** - The fragments enter at different time intervals.
  - **randomized** - Unpredictable fragmentation for an avant-garde feel.
- **Sample Usage**:
  ```
  [fragmentation: Staggered melodic fragments echo across different instruments.]
  ```
- **Advice**:
  - **Use melodic fragmentation** to create **variation and interest**.
  - **Rhythmic fragmentation** adds a **complex groove**.
  - **Counterpoint fragmentation** is great for **fugues and orchestral works**.

---

## [fugue]
- **Meaning**: Defines a **counterpoint-based composition** where a theme is introduced and then developed through layered entries.
- **Placement**: Typically used within `[structure]` or `[theme]`.
- **Accepted Parameters**:
  - **subject** - The main theme, stated clearly at the beginning.
  - **answer** - The second entry of the theme, either in the dominant or another voice.
  - **counterpoint** - Additional lines interacting with the main theme.
  - **development** - Harmonic and rhythmic expansion of the theme.
  - **stretto** - Overlapping and condensed theme entries.
- **Sample Usage**:
  ```
  [fugue: Staggered theme entries in strings, building into a layered climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: **Organ fugues and contrapuntal choral works**.
  - **Jazz & Improvisation**: **Interwoven melodic lines between instruments**.
  - **Progressive Rock & Metal**: **Complex multi-guitar or keyboard fugue structures**.
  - **Electronic & Experimental**: **Synth fugues with automated counterpoint**.

### **Track Structure Recommendation**
- **[intro: Single voice introducing the subject]**
- **[fugue: Additional voices enter, answering the main theme]**
- **[development: Expanding the harmonic complexity]**
- **[stretto: Overlapping faster-paced theme entries]**
- **[outro: Soft resolution with fading counterpoint lines]**

---

## [gain]
- **Meaning**: Adjusts **relative loudness/emphasis** of a section or instrument layer.
- **Placement**: Section-based; best in `[intro:]`, `[climax:]`, or `[bridge:]`.
- **Accepted Parameters**:
  - **`low`, `medium`, `high`** - Relative section gain.
  - **`fade-in`, `fade-out`, `surge`** - Dynamic behavior.
  - **`compressed`, `peaking`** - Useful for distortion or emotional exaggeraton.
- **Sample Usage**:
  ```
  [climax: Vocals rise above a wall of distorted guitars, reaching emotional peak.]
  [gain: high, peaking, compressed]
  ```
- **Genre-Based Usage**:
  - **Post-rock, cinematic scores**: long gain surges.
  - **EDM, glitch-hop**: peaking beats, fade-in bass.
  - **Ballads, soft-pop**: fade-in vocals in intro, rising chorus.

---

## [glissando]
- **Meaning**: Specifies a **continuous slide** from one pitch to another, often associated with string instruments, trombones, synths, or harps.
- **Placement**: Typically used within `[instruments]` or `[harmony]`.
- **Accepted Parameters**:
  - **ascending** - The pitch slides upwards.
  - **descending** - The pitch slides downwards.
  - **slow** - A gradual slide between pitches.
  - **fast** - A rapid slide between notes.
  - **chromatic** - A glissando that includes all chromatic steps.
- **Sample Usage**:
  ```
  [glissando: Fast ascending synth glissando for a futuristic feel.]
  ```
- **Advice**:
  - **Slow glissandos** create a dreamy or eerie atmosphere.
  - **Fast glissandos** add excitement, especially before a **climax**.
  - **Descending glissandos** are often used for **melancholy or fading effects**.

---

## [glitch]
- **Meaning**: Specifies **artificial, digital-style distortions** that contribute to a fractured or unpredictable sound.
- **Placement**: Typically used within `[effects]`, `[structure]`, or `[rhythm]`.
- **Accepted Parameters**:
  - **stutter** - Repetitive chopping of audio.
  - **bit-crush** - Lower-resolution sound for a pixelated effect.
  - **tape-stop** - Sudden halting of sound as if stopping playback.
  - **granular** - Fragmented, layered playback of the sound.
  - **randomized** - Unpredictable glitches throughout.
- **Sample Usage**:
  ```
  [glitch: Randomized stutters and granular synthesis applied to drums.]
  ```
- **Genre-Based Usage**:
  - **IDM & Glitchcore**: **Highly processed and manipulated electronic beats**.
  - **Industrial & Cyberpunk**: **Harsh, mechanical distortions**.
  - **Hip-Hop & Phonk**: **Chopped vocals with stutter effects**.
  - **Experimental & Noise**: **Extreme sound degradation for atmospheric effect**.

### **Track Structure Recommendation**
- **[intro: Filtered pads with occasional glitch artifacts]**
- **[verse: Glitchy percussion and vocal chops]**
- **[chorus: Stuttering synths and bit-crushed drums]**
- **[bridge: Tape-stop effect leading into a drop]**
- **[outro: Fading granular effects into silence]**

---

## [grind]
- **Meaning**: Defines **aggressive, fast-paced, or heavily distorted instrumentation**, often used in extreme genres.
- **Placement**: Typically used within `[rhythm]`, `[dynamics]`, or `[mixing]`.
- **Accepted Parameters**:
  - **metallic** - Sharp, industrial-style distortion.
  - **low-end** - Heavy, bass-driven grinding.
  - **machine-like** - Mechanized repetition and intensity.
  - **dissonant** - Unpleasant, abrasive tonalities.
  - **chaotic** - Unstructured, frenetic arrangement.
- **Sample Usage**:
  ```
  [grind: Low-end distorted bass and machine-like rhythmic intensity.]
  ```
- **Genre-Based Usage**:
  - **Grindcore & Metal**: **Fast, aggressive guitars and blast beats**.
  - **Industrial & Cyberpunk**: **Machine-driven rhythms and harsh noise**.
  - **Noise & Experimental**: **Chaotic, dissonant soundscapes**.
  - **Electronic & Breakcore**: **Distorted synths and fractured beats**.

### **Track Structure Recommendation**
- **[intro: Dark, grinding bass drone]**
- **[verse: Heavy distorted guitars with fast drumming]**
- **[chorus: Full power, chaotic grind elements]**
- **[bridge: Industrial machine-like breakdown]**
- **[outro: Sudden stop with high-pitched feedback]**

---

## [happy]
- **Meaning**: Defines the **emotional tone** of the track, ensuring that the composition conveys joy, positivity, and energy.
- **Placement**: Typically used within `[mood]`, `[style]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **bright** - A cheerful, lighthearted mood.
  - **upbeat** - Energetic and lively.
  - **playful** - Fun, quirky, and whimsical.
  - **joyful** - Warm and emotionally uplifting.
  - **danceable** - Optimized for rhythmic movement.
- **Sample Usage**:
  ```
  [happy: Upbeat and bright chord progressions with playful melodies.]
  ```
- **Genre-Based Usage**:
  - **Pop & Funk**: **Bright, danceable rhythms**.
  - **Jazz & Swing**: **Bouncy, uplifting harmonies**.
  - **Electronic & House**: **Fast tempos and feel-good synth leads**.
  - **Orchestral & Classical**: **Light, staccato string sections**.

### **Track Structure Recommendation**
- **[intro: Light piano motif with uplifting string swells]**
- **[verse: Playful syncopated rhythms]**
- **[chorus: Full instrumentation with soaring melody]**
- **[bridge: Soft breakdown, preparing for a final joyful chorus]**
- **[outro: Bright, sustained chords fading out]**

---

## [harmonics]
- **Meaning**: Refers to **overtones** produced above a fundamental pitch, common in **strings, brass, and woodwinds**. They create an **airy or shimmering sound**.
- **Placement**: Typically used within `[instruments]`, `[harmony]`, or `[style]`.
- **Accepted Parameters**:
  - **natural** - Harmonics produced by lightly touching a string.
  - **artificial** - Forced harmonics, often used on guitar.
  - **bell-like** - High, ringing harmonics.
  - **ethereal** - Soft, floating harmonic tones.
  - **sustained** - Long-lasting harmonic sounds.
- **Sample Usage**:
  ```
  [harmonics: Ethereal violin harmonics for a mysterious atmosphere.]
  ```
- **Advice**:
  - **Natural harmonics** work well in **orchestral and ambient compositions**.
  - **Bell-like harmonics** are perfect for **fantasy and cinematic scores**.
  - **Sustained harmonics** blend well with **pads and ambient textures**.

---

## [harmonies]
- **Purpose**: Signals multi-part harmonization.
- **Syntax**: `[harmonies: three-part choral blending with delay]`
- **Usage Tips**: Can be used alone or with `[vocals]`, `[polyphony]`.
- **Accepted Parameters**: freeform description
- **Version Info**: Active in v4.0+, may be ignored in v3.5.
- **Sample Usage**: `[harmonies: layered soprano and alto ghost vocals over pad shimmer]`

---

## [harmony]
- **Meaning**: Defines how **chords and multiple voices interact**, emphasizing harmony-driven elements in the track.
- **Placement**: Typically used within `[vocals]`, `[structure]`, or `[arrangement]`.
- **Accepted Parameters**:
  - **simple** - Basic, diatonic harmonies.
  - **rich** - Complex, layered chord structures.
  - **choral** - Choir-like vocal harmonization.
  - **jazz-influenced** - Extended and colorful harmonies.
  - **barbershop** - Tight, four-part vocal harmonies.
- **Sample Usage**:
  ```
  [harmony: Rich, layered choral harmonization with sustained voicings.]
  ```
- **Genre-Based Usage**:
  - **Classical & Choral**: **Polyphonic vocal harmonization**.
  - **Jazz & Soul**: **Complex harmonic textures**.
  - **Rock & Pop**: **Layered vocal harmonies in choruses**.
  - **Folk & World**: **Natural, acoustic harmony blending**.

### **Track Structure Recommendation**
- **[intro: Gentle piano chords introducing harmonic motif]**
- **[verse: Simple harmonized vocals over guitar]**
- **[chorus: Rich vocal harmonies layered for intensity]**
- **[bridge: Jazz-influenced modulations]**
- **[outro: Soft fading harmonies resolving into silence]**

---

## [improvisation]
- **Meaning**: Allows performers to **freely create melodic, harmonic, or rhythmic variations** during performance.
- **Placement**: Typically used within `[harmony]`, `[style]`, or `[theme]`.
- **Accepted Parameters**:
  - **freeform** - Fully spontaneous improvisation.
  - **jazzy** - Improvised elements in a jazz style.
  - **ornamental** - Embellishments added to the main melody.
  - **structured** - Improvisation within a set harmonic framework.
  - **call-and-response** - Improvised phrases between instruments or voices.
- **Sample Usage**:
  ```
  [improvisation: Jazzy trumpet solo over a soft piano accompaniment.]
  ```
- **Advice**:
  - **Freeform improvisation** works well for **ambient and experimental music**.
  - **Structured improvisation** is ideal for **jazz, blues, and classical variations**.
  - **Ornamental improvisation** can enhance **baroque, romantic, and cinematic styles**.

---

## [inflection]
- **Meaning**: Refers to **subtle tonal or dynamic variations** that **alter expressiveness**.
- **Placement**: Typically used within `[vocals]`, `[dynamics]`, or `[harmony]`.
- **Accepted Parameters**:
  - **subtle** - Gentle variations in pitch or dynamics.
  - **dramatic** - Strong inflections for emotional impact.
  - **vocal** - Inflection in singing or spoken words.
  - **instrumental** - Expressive changes in phrasing for instruments.
  - **crescendo-inflection** - Gradual intensity increase.
- **Sample Usage**:
  ```
  [inflection: Subtle vocal inflection for expressive storytelling.]
  ```
- **Advice**:
  - **Use vocal inflection** for **expressive singing and spoken word delivery**.
  - **Dramatic inflection** is great for **orchestral and cinematic builds**.
  - **Subtle inflection** can **enhance emotion without overpowering the mix**.

---

## [instrument]
- **Meaning**: Specifies **a particular instrument that is prominent** in the track.
- **Placement**: Typically used within `[instruments]`, `[arrangement]`, or `[focus]`.
- **Accepted Parameters**:
  - **piano** - Emphasizes piano as a lead instrument.
  - **guitar** - Focus on electric or acoustic guitar.
  - **violin** - Strings take the lead.
  - **synth** - Synth-heavy composition.
  - **brass** - Horns and brass section as a central element.
- **Sample Usage**:
  ```
  [instrument: Acoustic guitar fingerpicking leading the melody.]
  ```
- **Genre-Based Usage**:
  - **Folk & Country**: **Guitar and banjo prominence**.
  - **Jazz & Blues**: **Saxophone and brass-led arrangements**.
  - **Electronic & Synthwave**: **Heavy use of analog synthesizers**.
  - **Classical & Orchestral**: **Rich string sections**.

### **Track Structure Recommendation**
- **[intro: Solo violin melody establishing the theme]**
- **[verse: Piano accompaniment supporting the main melody]**
- **[chorus: Strings swell alongside brass accents]**
- **[bridge: Guitar interlude providing contrast]**
- **[outro: Gentle harp plucking fading into silence]**

---

## [instrumental]
- **Meaning**: Ensures that **the track contains no vocals**, focusing entirely on instrumentation.
- **Placement**: Typically used at the **beginning of the "Lyrics" section** to indicate that no lyrics should be generated.
- **Accepted Parameters**:
  - **orchestral** - Fully symphonic arrangement.
  - **electronic** - Focused on synths and digital instruments.
  - **acoustic** - Natural, unplugged instrumental piece.
  - **cinematic** - Score-like, narrative-driven instrumental.
  - **jazz-improvised** - Live, free-form instrumental sections.
- **Sample Usage**:
  ```
  [instrumental: Cinematic orchestral composition with no vocals.]
  ```
- **Genre-Based Usage**:
  - **Film Scores & Soundtracks**: **Fully orchestral compositions**.
  - **Electronic & Ambient**: **Synth-heavy soundscapes with no voice**.
  - **Classical & Chamber Music**: **Solo or ensemble instrumentals**.
  - **Progressive Rock & Metal**: **Extended instrumental solos**.

### **Track Structure Recommendation**
- **[intro: Slowly building orchestral strings]**
- **[verse: Main melody introduced on piano]**
- **[chorus: Full arrangement swells with brass]**
- **[bridge: Percussion-driven section with dynamic shifts]**
- **[outro: Soft fade-out with distant reverberations]**

---

## [intensity]
- **Meaning**: Controls **emotional/musical tension** and **arc of energy** throughout the song.
- **Placement**: 
  - Can be placed **globally** or **per section**.
  - Highly effective in `[control:]` or `[sequence:]` aligned use.
- **Accepted Parameters**:
  - **`low`, `medium`, `high`** - Base level of emotional delivery
  - **`rising`, `falling`, `fluctuating`** - Movement of energy
  - **`flat`, `plateau`, `explosive`, `collapsing`** - Specialized arc patterns
  - **`low → high → collapse`** - Composite form (good for dramatic forms)
- **Sample Usage**:
  ```
  [control: cinematic, emotional, slow-build]
  [intensity: low → medium → explosive → collapse]
  ```
- **Genre-Based Usage**:
  - **Post-metal, cinematic orchestral**: extreme rise-to-collapse.
  - **Synthwave, vaportrap**: plateau with sudden spike.
  - **Indie folk, lo-fi pop**: subtle rising arcs.

---

## [interlude]
- **Meaning**: Defines a **short instrumental break between sections**, often used to provide contrast or transition between verses and choruses.
- **Placement**: Typically placed **between structured sections** such as `[verse]`, `[chorus]`, and `[bridge]`.
- **Accepted Parameters**:
  - **instrumental** - Purely instrumental passage.
  - **melodic** - A recurring theme or motif.
  - **rhythmic** - A percussive, groove-based break.
  - **ambient** - A textural or atmospheric transition.
  - **minimal** - A sparse, stripped-down moment before the next section.
- **Sample Usage**:
  ```
  [interlude: Soft guitar arpeggios transitioning into the next verse.]
  ```
- **Genre-Based Usage**:
  - **Rock & Alternative**: **Guitar solo-based interludes**.
  - **Electronic & House**: **Synth builds and filter sweeps**.
  - **Orchestral & Classical**: **Short instrumental cadenzas**.
  - **Hip-Hop & R&B**: **Beat-driven breaks before the next verse**.

### **Track Structure Recommendation**
- **[intro: Dreamy piano chords]**
- **[verse: Soft vocals over light synth textures]**
- **[interlude: Atmospheric pad swells before the chorus]**
- **[chorus: Full arrangement kicks in with deep bass]**
- **[outro: Minimal fade-out of synth echoes]**

---

## [intermezzo]
- **Meaning**: Specifies a **self-contained musical passage** that may be unrelated to the main sections but serves as a brief contrast.
- **Placement**: Typically placed **between primary musical sections** like `[movement]`, `[theme]`, or `[structure]`.
- **Accepted Parameters**:
  - **contrasting** - A section that differs from the main theme.
  - **reflective** - A slow, introspective segment.
  - **dramatic** - A sudden, intense moment before resolving.
  - **ornamental** - A decorative or virtuosic passage.
- **Sample Usage**:
  ```
  [intermezzo: Dramatic orchestral swell before returning to the main theme.]
  ```
- **Genre-Based Usage**:
  - **Classical & Opera**: **Orchestral interludes in multi-movement pieces**.
  - **Progressive Rock & Metal**: **Sudden changes in dynamics or tempo**.
  - **Jazz & Fusion**: **Improvised instrumental detours**.
  - **Cinematic & Score**: **Dramatic moments before action sequences**.

### **Track Structure Recommendation**
- **[intro: Solo piano introduction]**
- **[theme: Strings carry the main melody]**
- **[intermezzo: Sudden timpani rolls and brass swells]**
- **[development: Main theme modulated into a darker key]**
- **[outro: Soft flute reprise of the melody]**

---

## [language]
- **Meaning**: Specifies the **language of the lyrics or vocal performance** in the generated track.
- **Placement**: Typically placed **at the beginning of the track definition** or before `[vocals]`.
- **Accepted Parameters**:
  - **English** - Standard default setting.
  - **Spanish** - Latin-inspired phonetics.
  - **French** - Romantic and flowing vocal tone.
  - **Japanese** - Suitable for J-Pop, anime-style vocals.
  - **Italian** - Often used in opera and classical pieces.
  - **Multilingual** - A mix of different languages in the song.
- **Sample Usage**:
  ```
  [language: French]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **English, Spanish, Japanese**.
  - **Classical & Opera**: **Italian, German, French**.
  - **World & Folk**: **Multilingual, Arabic, Mandarin**.
  - **Hip-Hop & R&B**: **English, Spanish, African dialects**.

### **Track Structure Recommendation**
- **[language: Italian]**
- **[intro: Operatic soprano melody with light piano accompaniment]**
- **[verse: Dramatic vocal lines with orchestral backing]**
- **[chorus: Emotional crescendo, fully harmonized vocals]**
- **[outro: Fading choral resolution in Latin]**

---

## [laughter]
- **Meaning**: Adds **laughter as a sound effect or vocal element** in the track.
- **Placement**: Typically used within `[sfx]`, `[vocals]`, or `[effects]`.
- **Accepted Parameters**:
  - **subtle** - Light chuckles, background effect.
  - **maniacal** - Evil, exaggerated laughter.
  - **nervous** - Uneasy or trembling chuckles.
  - **group** - Multiple voices laughing together.
  - **looped** - Continuous, rhythmic laughter.
- **Sample Usage**:
  ```
  [laughter: Maniacal, distorted laughter echoing in the background.]
  ```
- **Genre-Based Usage**:
  - **Horror & Darkwave**: **Evil, unsettling vocal effects**.
  - **Jazz & Theatrical**: **Playful, vaudeville-style laughing breaks**.
  - **Hip-Hop & Phonk**: **Dark, menacing laugh samples**.
  - **Experimental & Avant-Garde**: **Layered, manipulated laughter textures**.

### **Track Structure Recommendation**
- **[intro: Low synth hum with distant, eerie laughter]**
- **[verse: Tension-building piano progression]**
- **[laughter: Maniacal chuckles creeping in the background]**
- **[chorus: Full instrumental impact, layered horror effects]**
- **[outro: Echoing laughter fading into silence]**

---

## [layering]
- **Meaning**: Defines the use of multiple **sounds, instruments, or textures** stacked together to create a **thicker or more dynamic sound**.
- **Placement**: Typically used within `[mixing]`, `[orchestration]`, or `[structure]`.
- **Accepted Parameters**:
  - **dense** - A full, rich arrangement with multiple instruments layered.
  - **thin** - A minimal arrangement with subtle layers.
  - **gradual** - Layers that slowly build up over time.
  - **dynamic** - Layers that shift and evolve throughout the track.
  - **textural** - Subtle atmospheric layering for ambiance.
- **Sample Usage**:
  ```
  [layering: Dense synth pads supporting dynamic brass and strings.]
  ```
- **Advice**:
  - **Dense layering** is useful for **cinematic, symphonic, and electronic builds**.
  - **Gradual layering** works well for **progressive music or ambient styles**.
  - **Textural layering** enhances **atmosphere and depth**.

---

## [legato]
- **Meaning**: Specifies **smooth, connected note transitions** in melodies and harmonies.
- **Placement**: Typically used within `[harmony]` or `[vocals]`.
- **Accepted Parameters**:
  - **soft** - Gentle legato phrasing.
  - **flowing** - Constantly connected and expressive.
  - **orchestral** - String and wind instruments blending seamlessly.
  - **electronic** - Synth-based legato glide effects.
  - **intense** - Dramatic, film-score-like smooth phrasing.
- **Sample Usage**:
  ```
  [legato: Flowing, cinematic string movements blending with choir.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: **Smooth violin and wind melodies**.
  - **Jazz & Blues**: **Expressive, slurred saxophone phrasing**.
  - **Electronic & Synthwave**: **Gliding synth leads**.
  - **Ambient & Soundtrack**: **Ethereal, evolving soundscapes**.

### **Track Structure Recommendation**
- **[intro: Slow, legato string swells fading in]**
- **[verse: Flowing vocal line with smooth piano accompaniment]**
- **[chorus: Expansive, cinematic orchestration with legato phrasing]**
- **[bridge: Soft legato violin solo transitioning back to vocals]**
- **[outro: Gentle legato fade-out of choir and strings]**

---

## [male]
- **Meaning**: Specifies that the **lead or backing vocals should be performed by a male voice**.
- **Placement**: Typically used within `[vocals]`, `[harmony]`, or `[structure]`.
- **Accepted Parameters**:
  - **low** - Deep bass or baritone male vocals.
  - **mid** - Natural tenor range.
  - **high** - Falsetto or high tenor vocals.
  - **gritty** - Rough, textured male vocals.
  - **operatic** - Classical, dramatic male vocals.
- **Sample Usage**:
  ```
  [male: Deep, rich baritone leading the verse.]
  ```
- **Genre-Based Usage**:
  - **Rock & Blues**: **Gritty, raspy male vocals**.
  - **Pop & R&B**: **Smooth tenor male leads**.
  - **Classical & Opera**: **Operatic bass or tenor voices**.
  - **Jazz & Soul**: **Expressive male vocals with vibrato**.

### **Track Structure Recommendation**
- **[intro: Soft spoken male intro with ambient backing]**
- **[verse: Deep baritone vocals over piano]**
- **[chorus: Powerful mid-range male harmonies]**
- **[bridge: Falsetto rise into emotional climax]**
- **[outro: Whispered male harmonics fading into silence]**

---

## [male vocal], [female vocal]
- **Meaning**: Specify dominant vocal gender identity.
- **Syntax**: `[male vocal]`, `[female vocal]`
- **Usage Tips**: Use **with** `[vocals]` or `[vocalist]` tags; does not require colon.
- **Known Parameters**: N/A
- **Version Info**: Confirmed since v3.5, reliably parsed in v4.0+
- **Sample Usage**: `[female vocal]`

---

## [marcato]
- **Meaning**: Indicates that **notes should be played in a forceful, accented manner**.
- **Placement**: Typically used within `[rhythm]` or `[dynamics]`.
- **Accepted Parameters**:
  - **sharp** - Sudden, pronounced attack on each note.
  - **percussive** - Rhythmically strong articulation.
  - **orchestral** - Bold, dynamic orchestral accents.
  - **syncopated** - Accents placed off the beat.
- **Sample Usage**:
  ```
  [marcato: Orchestral brass accents, sharp and dramatic.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: **String sections playing in sharp articulation**.
  - **Jazz & Big Band**: **Bold brass accents**.
  - **Rock & Metal**: **Aggressive, percussive riffing**.
  - **Electronic & Industrial**: **Heavily accented synth stabs**.

### **Track Structure Recommendation**
- **[intro: Percussive piano intro with marcato strings]**
- **[verse: Syncopated marcato brass hits]**
- **[chorus: Full orchestra with pronounced articulation]**
- **[bridge: Short, staccato motifs developing tension]**
- **[outro: Dramatic brass ending with accented closure]**

---

## [minuet]
- **Meaning**: Specifies a **dance-like, triple-meter (3/4 or 6/8) structure** reminiscent of classical minuets.
- **Placement**: Typically used within `[style]`, `[rhythm]`, or `[tempo]`.
- **Accepted Parameters**:
  - **baroque** - Authentic minuet style from the 17th-18th century.
  - **waltz-like** - Flowing, romantic interpretation.
  - **modernized** - Updated for contemporary instruments.
  - **chamber** - Designed for small ensembles.
- **Sample Usage**:
  ```
  [minuet: Baroque-style string minuet in 3/4 time.]
  ```
- **Genre-Based Usage**:
  - **Classical & Renaissance**: **Authentic minuet structures**.
  - **Jazz & Fusion**: **Swing-infused minuet adaptations**.
  - **Folk & Acoustic**: **Waltz-like guitar arrangements**.
  - **Electronic & Experimental**: **Synth-based minuets with arpeggiated lines**.

### **Track Structure Recommendation**
- **[intro: Light harpsichord motif introducing the minuet]**
- **[theme: Baroque-inspired strings in 3/4 time]**
- **[variation: Flute melody complementing the minuet rhythm]**
- **[outro: Soft piano closing in minuet style]**

---

## [modulation]
- **Meaning**: Specifies a **change in key** or **tonal shift** within the composition.
- **Placement**: Typically used within `[harmony]`, `[structure]`, or `[theme]`.
- **Accepted Parameters**:
  - **`sudden`, `abrupt`** - An abrupt key change for dramatic effect.
  - **`ascending`, `rising`** - Moves up in pitch (e.g., C major to D major).
  - **`descending`, `falling`** - Moves down in pitch (e.g., G major to F major).
  - **`gradual`, `smooth`, `subtle`** - Slow harmonic drift.
  - **`minor-shift`, `major-shift`** - Mood-altering key changes.
  - **`chromatic`, `modal`, `atonal`** - Modulation using non-diatonic steps.
- **Sample Usage**:
  ```
  [modulation: Sudden shift from A minor to C major in the bridge.]
  ```
- **Advice**:
  - **Subtle modulations** create a **flowing progression** in pop and classical music.
  - **Sudden modulations** enhance **dramatic or surprise elements**.
  - **Chromatic modulations** work well for **film scores and jazz**.

---

## [mutation]
- **Meaning**: Refers to the **transformation** of a melody, harmony, or rhythm into a new variation over time.
- **Placement**: Typically used within `[structure]`, `[theme]`, or `[variation]`.
- **Accepted Parameters**:
  - **gradual** - The transformation happens slowly.
  - **abrupt** - Sudden shifts in melody or harmony.
  - **textural** - Changes in sound design rather than pitch.
  - **harmonic** - The harmonic foundation shifts over time.
  - **rhythmic** - The rhythm gradually evolves.
- **Sample Usage**:
  ```
  [mutation: Gradual harmonic shift from major to minor.]
  ```
- **Advice**:
  - **Gradual mutation** works well for **ambient and electronic music**.
  - **Abrupt mutation** is useful for **avant-garde and progressive rock**.
  - **Textural mutation** is great for **experimental and cinematic music**.

---

## [no]  
- **Meaning**: **Negates or disables** a particular feature or characteristic in the track. It is used to explicitly prevent the inclusion of certain musical elements.  
- **Placement**: Typically placed **before structure or vocal tags** to ensure exclusions are processed early.  
- **Accepted Parameters**:  
  - **no-vocals** - Ensures the track is fully instrumental.  
  - **no-drums** - Removes percussion elements.  
  - **no-bass** - Prevents the presence of bass frequencies or instruments.  
  - **no-reverb** - Avoids reverb effects.  
  - **no-fade** - Disables fade-in or fade-out.  
- **Sample Usage**:  
  ```
  [no: no-vocals, no-drums]
  ```
- **Genre-Based Usage**:  
  - **Ambient & Soundscape**: **"No-drums" for pure atmospheric textures.**  
  - **Classical & Cinematic**: **"No-reverb" for a dry, raw recording feel.**  
  - **Electronic & House**: **"No-bass" to create a floating, ethereal quality.**  
  - **Minimalist & Acoustic**: **"No-fade" for sharp track endings.**  

### **Track Structure Recommendation**  
- **[no: no-vocals, no-reverb]**  
- **[intro: Soft piano with dry orchestration]**  
- **[verse: Subtle string backing, no atmospheric effects]**  
- **[chorus: Main melody played without reverberation]**  
- **[outro: Quick, abrupt stop on the final note]**  

---

## [no-repeat]

**Category:** Control / structural behavior tag  
**Primary use:** To discourage the model from automatically repeating lines, verses, or full sections when you do not want extra duplication.

**Behavior and intent**  
Suno sometimes repeats text fragments to fill a section. The `[no-repeat]` tag is a soft instruction that you want fresh material or a single occurrence of the given lines, rather than extended repetition. It is *not* guaranteed, but it can reduce unplanned looping.

**Placement and syntax**  

- *Lyrics field:*  
  - At the start of a section or directly before important lines:  
    - `[no-repeat | verse with simple, one-time images]`  
    - `[verse | no-repeat]`  
- *Style of Music field:*  
  - Rare; usually unnecessary. This tag is most useful embedded in lyrics.

**Typical use-cases**  

- Narrative verses where each line advances the story  
- Spoken word or rap sections where repetition would muddy the meaning  
- Short epigrams or punchlines you only want once

Combine `[no-repeat]` with *deliberately non-repetitive* text: if your words are already highly repetitive, the model has less room to vary them.

---

## [orchestra]
- **Meaning**: Specifies the **type of orchestral arrangement** used in the track.  
- **Placement**: Typically placed **before `[instruments]` or `[structure]`** to define the orchestration.  
- **Accepted Parameters**:  
  - **symphonic** - Full orchestra with all sections.  
  - **chamber** - Small ensemble, often with strings and winds.  
  - **brass-heavy** - Focus on bold brass sections.  
  - **string-dominant** - Emphasizes violins, cellos, and other stringed instruments.  
  - **percussion-driven** - Strong orchestral percussion presence.  
- **Sample Usage**:  
  ```
  [orchestra: chamber, string-dominant]
  ```
- **Genre-Based Usage**:  
  - **Classical & Romantic**: **"Symphonic" for grand compositions.**  
  - **Jazz & Big Band**: **"Brass-heavy" for powerful sound.**  
  - **Cinematic & Soundtrack**: **"Percussion-driven" for dramatic scoring.**  
  - **Electronic & Hybrid**: **"Chamber" for intimate, modern fusion.**  

### **Track Structure Recommendation**  
- **[orchestra: symphonic, brass-heavy]**  
- **[intro: Slow strings swelling into a majestic brass fanfare]**  
- **[theme: Heroic brass melody over rich orchestration]**  
- **[development: Expanding harmonic complexity with woodwinds]**  
- **[outro: Gentle string diminuendo fading into silence]**  

---

## [orchestration]
- **Meaning**: Defines how instruments are **arranged and distributed** in the composition.
- **Placement**: Typically used within `[ensemble]`, `[structure]`, or `[style]`.
- **Accepted Parameters**:
  - **dense** - A rich, full orchestral arrangement.
  - **transparent** - A light and airy arrangement with space.
  - **layered** - Different instrumental groups are stacked in layers.
  - **chamber** - A small ensemble with intimate textures.
  - **cinematic** - A dramatic, film-score-like orchestration.
- **Sample Usage**:
  ```
  [orchestration: Layered strings and brass for a cinematic build-up.]
  ```
- **Advice**:
  - **Dense orchestration** is great for **epic scores and symphonic metal**.
  - **Transparent orchestration** works for **baroque, jazz, and folk music**.
  - **Layered orchestration** adds **depth and richness to any genre**.

---

## [outro]
- **Meaning**: Defines the **final section of the track**, specifying how it concludes.  
- **Placement**: Typically placed **after `[structure]`**, indicating the closing style.  
- **Accepted Parameters**:  
  - **fade-out** - Gradually decreasing volume to silence.  
  - **sudden-stop** - A sharp, abrupt end.  
  - **reverb-tail** - Ending with a long reverberation.  
  - **soft-landing** - A gentle, resolving finish.  
  - **climactic** - A dramatic final section.  
- **Sample Usage**:  
  ```
  [outro: Climactic brass swell with a sudden-stop ending.]
  ```
- **Genre-Based Usage**:  
  - **Rock & Pop**: **"Fade-out" for classic endings.**  
  - **Classical & Jazz**: **"Soft-landing" for smooth resolutions.**  
  - **EDM & Dance**: **"Reverb-tail" for atmospheric club endings.**  
  - **Cinematic & Epic**: **"Climactic" for impactful finishes.**  

### **Track Structure Recommendation**  
- **[intro: Delicate harp melody building into orchestral swells]**  
- **[verse: Expanding dynamic range with layered vocals]**  
- **[chorus: Powerful string and brass crescendos]**  
- **[outro: Sudden-stop ending for dramatic effect]**  

---

## [pad]
- **Meaning**: Defines **the type of sustained, atmospheric background sound layers** used to enhance depth.  
- **Placement**: Typically used within `[instruments]`, `[structure]`, or `[effects]`.  
- **Accepted Parameters**:  
  - **warm** - Soft, analog-style pads.  
  - **bright** - High-frequency shimmering pads.  
  - **evolving** - Slowly shifting, morphing pads.  
  - **dark** - Low, ominous textures.  
  - **orchestral** - Simulated string ensemble pads.  
- **Sample Usage**:  
  ```
  [pad: Warm, evolving synth textures filling the background.]
  ```
- **Genre-Based Usage**:  
  - **Ambient & Drone**: **"Evolving" pads for immersive atmospheres.**  
  - **Cinematic & Soundtrack**: **"Orchestral" pads for emotional weight.**  
  - **Electronic & Chillout**: **"Warm" pads for relaxed textures.**  
  - **Industrial & Experimental**: **"Dark" pads for unsettling tension.**  

### **Track Structure Recommendation**  
- **[pad: Evolving orchestral strings with warm synth undertones]**  
- **[intro: Deep synth pads fading in]**  
- **[verse: Soft piano melody supported by atmospheric pads]**  
- **[chorus: Full orchestral pad swell behind lead vocals]**  
- **[outro: Dark, haunting pad fading into silence]**  

---

## [pedal-point]
- **Meaning**: A **sustained or repeated note**, typically in the bass, that remains constant while harmonies above it change.
- **Placement**: Typically used within `[harmony]`, `[bass]`, or `[structure]`.
- **Accepted Parameters**:
  - **low** - A deep, rumbling pedal note in the bass.
  - **high** - A sustained note in the treble register.
  - **suspended** - A pedal point that delays resolution.
  - **dissonant** - A pedal tone that clashes with the chords above it.
  - **resolved** - A pedal point that smoothly transitions into a cadence.
- **Sample Usage**:
  ```
  [pedal-point: Low sustained organ note for a gothic atmosphere.]
  ```
- **Genre-Based Usage**:
  - **Classical**: Used in **Bach’s fugues and organ compositions** for harmonic grounding.
  - **Jazz**: Walking bass lines often contain pedal points for harmonic **tension and release**.
  - **Cinematic**: Low drone-like pedal points in **horror or thriller soundtracks** enhance unease.
  - **Metal/Rock**: Guitar pedal tones sustain **dissonance** before heavy riffing.

---

## [personae]
- **Meaning**: Specifies the **vocal character or persona** performing the track, ensuring consistency across verses, harmonies, and vocal layers.
- **Placement**: Typically placed **before `[vocals]` or `[harmony]`**, defining a character or vocal identity early in the track.
- **Accepted Parameters**:
  - **gritty-male** - A deep, textured male voice.
  - **ethereal-female** - Light, airy female vocals.
  - **robotic** - Artificial, vocoder-like singing.
  - **opera-tenor** - Classical, operatic male tenor.
  - **soft-whisper** - Gentle, whispered tones.
- **Sample Usage**:
  ```
  [personae: Robotic male voice with synthetic textures.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Cyberpunk**: **"Robotic" for digital, AI-like vocals**.
  - **Rock & Metal**: **"Gritty-male" for powerful lead vocals**.
  - **Classical & Operatic**: **"Opera-tenor" for dramatic arias**.
  - **Ambient & Experimental**: **"Soft-whisper" for eerie textures**.

### **Track Structure Recommendation**
- **[personae: Ethereal female voice leading into soft whispers]**
- **[intro: Solo vocal phrase floating over atmospheric synths]**
- **[verse: Expressive lines carried by delicate vocal textures]**
- **[chorus: Full harmonization expanding the character’s voice]**
- **[outro: Whispered phrases fading into echoes]**

---

## [pizzicato]
- **Meaning**: Defines **plucked string articulations** for a more rhythmic and staccato effect in string instruments.
- **Placement**: Typically used **within `[instruments]` or `[harmony]`**.
- **Accepted Parameters**:
  - **light** - Subtle, delicate pizzicato.
  - **sharp** - Pronounced, dynamic plucks.
  - **bouncy** - Playful, rhythmic feel.
  - **dark** - Ominous, low-register pizzicato.
- **Sample Usage**:
  ```
  [pizzicato: Bouncy, rhythmic plucked strings over a jazz groove.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: **Light pizzicato passages in string quartets**.
  - **Jazz & Swing**: **Bouncy plucks in basslines and violin accents**.
  - **Cinematic & Horror**: **Dark, eerie pizzicato used for suspense**.
  - **Electronic & Pop**: **Pizzicato-like synth plucks for texture**.

### **Track Structure Recommendation**
- **[pizzicato: Light, playful plucks introducing the theme]**
- **[verse: Delicate pizzicato string backing under lead melody]**
- **[chorus: Expanding harmonies with layered pizzicato texture]**
- **[bridge: Deep, dramatic low-string plucks]**
- **[outro: Soft pizzicato fading into silence]**

---

## [power-off drop]
- **Meaning**: Defines a **dramatic, abrupt silence effect**, simulating an electronic system suddenly turning off.
- **Placement**: Typically used **within `[structure]`, `[drop]`, or `[effects]`**.
- **Accepted Parameters**:
  - **sudden** - Instant drop with no reverb tail.
  - **glitchy** - Stuttering before the cut-off.
  - **resonant** - A slight echo before silence.
  - **percussive** - Accompanied by a bass thump or impact.
- **Sample Usage**:
  ```
  [power-off drop: Sudden, glitchy silence after the beat build-up.]
  ```
- **Genre-Based Usage**:
  - **Electronic & EDM**: **Used for suspense before beat drops**.
  - **Hip-Hop & Trap**: **Tactical silence before 808 kicks return**.
  - **Industrial & Experimental**: **Creates eerie interruptions in rhythm**.
  - **Cinematic & Sci-Fi**: **Futuristic breakdowns with simulated glitches**.

### **Track Structure Recommendation**
- **[intro: Rising synth arpeggios building tension]**
- **[verse: Heavy bass and beat-driven groove]**
- **[power-off drop: Abrupt silence before the chorus]**
- **[chorus: Full re-entry with dramatic percussion]**
- **[outro: Distant echoes fading into silence]**

---

## [prelude]
- **Meaning**: Specifies an **introductory musical passage**, often setting the mood for the entire composition.
- **Placement**: Typically used **before `[structure]`, `[intro]`, or `[theme]`**.
- **Accepted Parameters**:
  - **solo** - A single instrument introduction.
  - **orchestral** - Full symphonic opening.
  - **ambient** - Atmospheric, pad-driven textures.
  - **rhythmic** - Percussion-driven thematic intro.
- **Sample Usage**:
  ```
  [prelude: Orchestral string overture with a cinematic buildup.]
  ```
- **Genre-Based Usage**:
  - **Classical & Romantic**: **Grand, symphonic preludes before themes**.
  - **Electronic & Synthwave**: **Slow ambient buildups into beats**.
  - **Cinematic & Epic**: **Huge orchestral introductions before action**.
  - **Jazz & Blues**: **Piano-based preludes before main motifs**.

### **Track Structure Recommendation**
- **[prelude: Solo piano opening with emotional phrasing]**
- **[theme: Full string orchestra carrying the melody]**
- **[development: Expansion into a cinematic arrangement]**
- **[outro: Soft fade-out with distant echoes]**

---

## [pronunciation]
- **Meaning**: Specifies **how words should be enunciated** in the vocal performance, which can be useful for ensuring clarity or stylization.
- **Placement**: Typically placed **within `[vocals]` or `[language]`** to ensure it is applied correctly.
- **Accepted Parameters**:
  - **clear** - Words are pronounced distinctly.
  - **soft** - Slightly subdued, gentle enunciation.
  - **accented** - Adds a specific accent (e.g., French, British, Southern).
  - **slurred** - Lazy or smooth pronunciation.
  - **robotic** - AI-style, flat vocal articulation.
- **Sample Usage**:
  ```
  [pronunciation: Clear and crisp, ensuring every word is understood.]
  ```
- **Genre-Based Usage**:
  - **Pop & R&B**: **"Soft" for emotional delivery**.
  - **Hip-Hop & Trap**: **"Accented" for stylized flow**.
  - **Jazz & Blues**: **"Slurred" for relaxed phrasing**.
  - **Electronic & Experimental**: **"Robotic" for synthetic vocals**.

### **Track Structure Recommendation**
- **[pronunciation: Clear, with a slightly accented delivery]**
- **[verse: Precise articulation with moderate pacing]**
- **[chorus: Expressive, slightly exaggerated vowels]**
- **[bridge: Whispered delivery, intimate phrasing]**
- **[outro: Words fading into a breathy whisper]**

---

## [pulse]
- **Meaning**: Defines **the rhythmic foundation or heartbeat** of the track.
- **Placement**: Typically used **within `[rhythm]`, `[tempo]`, or `[structure]`** to guide the groove.
- **Accepted Parameters**:
  - **steady** - A constant, unchanging pulse.
  - **driving** - Strong, forceful rhythmic push.
  - **syncopated** - Off-beat or complex rhythmic emphasis.
  - **irregular** - Changing tempo patterns.
  - **subtle** - Light, minimal rhythmic presence.
- **Sample Usage**:
  ```
  [pulse: Driving and syncopated, creating a hypnotic groove.]
  ```
- **Genre-Based Usage**:
  - **House & Techno**: **"Steady" for dance beats**.
  - **Jazz & Funk**: **"Syncopated" for groove**.
  - **Progressive Rock & Metal**: **"Irregular" for time changes**.
  - **Orchestral & Cinematic**: **"Subtle" for gradual builds**.

### **Track Structure Recommendation**
- **[pulse: Steady with slight acceleration in the chorus]**
- **[verse: Rhythmic guitar pattern anchoring the beat]**
- **[chorus: Full percussion section emphasizing pulse]**
- **[bridge: Pulse breaks down into irregular phrasing]**
- **[outro: Slow rhythmic fade into silence]**

---

## [quiet arrangement]
*   **Meaning**: Defines a section with **minimal instrumentation and reduced dynamics**, emphasizing sparseness or intimacy.
*   **Placement**: Within `[arrangement]` or `[structure]`.
*   **Accepted Parameters**:
    *   **ambient** – airy pads, little motion.
    *   **acoustic** – stripped to guitar/piano only.
    *   **intimate** – focus on voice with minimal backing.
    *   **fade-down** – arrangement reduces gradually.
*   **Sample Usage**:
    ```
    [quiet arrangement: Sparse piano and soft strings, no percussion]  
    ```
*   **Genre-Based Usage**:
    *   **Pop/Ballad**: Stripped sections before chorus return.
    *   **Jazz/Soul**: Soft interlude with light comping.
    *   **Ambient/Drone**: Entire piece may be a quiet arrangement.
### **Track Structure Recommendation**:
    *   `[intro: quiet arrangement with piano only]`
    *   `[verse: soft vocals over sparse texture]`
    *   `[chorus: full arrangement returns]`

---

## [rapped verse]
*   **Meaning**: Specifies a **rap-delivered verse**, rhythmically spoken instead of sung.
*   **Placement**: Within `[vocals]` or `[structure]` for verses.
*   **Accepted Parameters**:
    *   **fast-flow** – quick delivery.
    *   **slow-flow** – laid-back cadence.
    *   **aggressive** – intense, sharp delivery.
    *   **melodic** – rap with pitched inflection.
*   **Sample Usage**:
    ```
    [rapped verse: Rhythm-heavy delivery with minimal backing]  
    ```
*   **Genre-Based Usage**:
    *   **Hip-Hop/Trap**: Primary rap verses.
    *   **Pop/R&B Fusion**: Rap interludes between sung sections.
    *   **Experimental/Alt**: Spoken-word hybrid rap flows.
### **Track Structure Recommendation**:
    *   `[intro: instrumental]`
    *   `[rapped verse: first verse with rhythmic delivery]`
    *   `[chorus: sung refrain]`

---

## [recapitulation]
- **Meaning**: Refers to **the return of the main theme**, often after a development section, commonly used in classical and cinematic compositions.
- **Placement**: Typically used **within `[structure]` or `[theme]`**.
- **Accepted Parameters**:
  - **exact** - Identical to the original theme.
  - **varied** - Altered slightly with new harmonies.
  - **orchestral** - Expanded for a larger arrangement.
  - **minimal** - Stripped-down return of the theme.
- **Sample Usage**:
  ```
  [recapitulation: Orchestral reprise of the opening theme with added brass.]
  ```
- **Genre-Based Usage**:
  - **Classical & Symphonic**: **"Exact" for structured returns**.
  - **Jazz & Improvisation**: **"Varied" for theme reinventions**.
  - **Rock & Progressive**: **"Orchestral" for dramatic finales**.
  - **Electronic & Ambient**: **"Minimal" for subtle motif callbacks**.

### **Track Structure Recommendation**
- **[intro: Gentle string introduction with a main theme]**
- **[verse: Variation of the theme with light piano support]**
- **[bridge: Expansion into different harmonic territory]**
- **[recapitulation: Full orchestral return of the main melody]**
- **[outro: Quiet resolution with a softened reprise]**

---

## [register]
- **Meaning**: Specifies the **pitch range** where a melody or harmony is played.
- **Placement**: Typically used within `[harmony]` or `[orchestration]`.
- **Accepted Parameters**:
  - **low** - Deep bass registers.
  - **mid** - Middle range instruments or vocals.
  - **high** - Treble instruments or falsetto vocals.
  - **extended** - Unusually high or low registers for an instrument.
  - **shifted** - The melody is transposed up or down an octave.
- **Sample Usage**:
  ```
  [register: High violin melodies soaring over low brass.]
  ```
- **Genre-Based Usage**:
  - **Opera & Classical**: Sopranos sing in **high register**, basses in **low register**.
  - **Electronic & Ambient**: Pads or drones in the **low register** add warmth.
  - **Rock & Pop**: Shifting vocal registers enhances emotional **contrast** in choruses.
  - **Jazz & Blues**: Saxophones explore **extended registers** for expressive solos.

---

## [resolution]
- **Meaning**: Defines how **musical tension is released**, often through chord progressions or phrase endings.
- **Placement**: Typically used within `[harmony]`, `[structure]`, or `[cadence]`.
- **Accepted Parameters**:
  - **strong** - A definitive resolution (e.g., V-I in classical music).
  - **weak** - A soft or unresolved cadence (e.g., IV-I in gospel music).
  - **delayed** - The resolution is postponed for suspense.
  - **suspended** - The resolution is avoided, keeping tension.
  - **chromatic** - The resolution involves non-diatonic steps.
- **Sample Usage**:
  ```
  [resolution: Delayed V-I movement to build anticipation.]
  ```
- **Genre-Based Usage**:
  - **Classical**: Strong resolutions create a **satisfying harmonic closure**.
  - **Jazz**: Weak or chromatic resolutions add **complexity and unpredictability**.
  - **Electronic & Ambient**: Delayed or suspended resolutions create an **open, floating sound**.
  - **Rock & Blues**: Using **blues-style resolutions** (e.g., V-IV-I) keeps a song feeling raw.

---

## [retrograde]
- **Meaning**: Indicates a **melody, motif, or harmony played in reverse**.
- **Placement**: Typically used within `[theme]`, `[variation]`, or `[counterpoint]`.
- **Accepted Parameters**:
  - **melodic** - The notes of the melody are played in reverse order.
  - **harmonic** - Chord progressions move backward.
  - **inverted** - Both retrograde and inversion (flipping the melody upside down).
  - **canon** - Retrograde used in a **fugue-like counterpoint**.
  - **mirrored** - The rhythm is also reversed.
- **Sample Usage**:
  ```
  [retrograde: Melodic retrograde variation for an avant-garde effect.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: Used in **fugues and canons** (e.g., Bach’s **musical riddles**).
  - **Jazz & Avant-Garde**: Reversing licks or motifs adds **unexpected complexity**.
  - **Electronic & Experimental**: Retrograde sequences create **glitchy, surreal effects**.
  - **Horror & Sci-Fi Soundtracks**: Retrograde harmonies can sound **eerie and unnatural**.

---

## [reverb]
- **Meaning**: Specifies **the level and type of reverberation**, controlling depth and space in the track’s mix.
- **Placement**: Typically used **within `[effects]`, `[mixing]`, or `[vocals]`**.
- **Accepted Parameters**:
  - **dry** - Minimal or no reverb.
  - **hall** - Large, expansive reverb.
  - **plate** - Vintage, metallic reverb sound.
  - **cathedral** - Extremely large, church-like reflections.
  - **echoed** - Delayed, bouncing reflections.
- **Sample Usage**:
  ```
  [reverb: Soft hall reverb on vocals with a deep echo on the outro.]
  ```
- **Genre-Based Usage**:
  - **Ambient & Soundscape**: **"Cathedral" for massive, immersive spaces**.
  - **Rock & Shoegaze**: **"Hall" for atmospheric guitars**.
  - **Jazz & Classical**: **"Plate" for warm, natural tone**.
  - **Electronic & Pop**: **"Echoed" for dreamy vocal effects**.

### **Track Structure Recommendation**
- **[intro: Soft piano with plate reverb]**
- **[verse: Vocals with subtle hall reverb]**
- **[chorus: Expansive reverb creating a wide stereo field]**
- **[bridge: Delay-heavy echo effect on vocals]**
- **[outro: Deep, long reverb tail fading into silence]**

---

## [reverberate]
- **Meaning**: Specifies **a strong and continuous reverb effect**, creating an echoing, immersive atmosphere.
- **Placement**: Typically used within **[effects], [mixing], or [vocals]**.
- **Accepted Parameters**:
  - **soft** - Gentle, subtle reverb.
  - **deep** - Pronounced, long-decay reverberation.
  - **distant** - Creates a feeling of space and separation.
  - **metallic** - Sharp, bright reflections.
  - **drenched** - Heavy, all-encompassing reverb effect.
- **Sample Usage**:
  ```
  [reverberate: Deep, atmospheric echo on lead vocals.]
  ```
- **Genre-Based Usage**:
  - **Ambient & Shoegaze**: **"Drenched" for massive, swirling textures.**
  - **Cinematic & Soundscape**: **"Distant" for haunting atmospheres.**
  - **Rock & Blues**: **"Soft" for classic studio-style reverb.**
  - **Industrial & Experimental**: **"Metallic" for sharp, robotic echoes.**

### **Track Structure Recommendation**
- **[intro: Distant reverberating piano fading in]**
- **[verse: Vocals with soft reverberation on the tail]**
- **[chorus: Expansive reverberate effect on backing vocals]**
- **[outro: Deep, slow echo fade-out into silence]**

---

## [rhythm]
- **Meaning**: Defines **the rhythmic pattern and overall groove** of the track.
- **Placement**: Typically used within **[tempo], [pulse], or [structure]**.
- **Accepted Parameters**:
  - **steady** - Even, predictable rhythm.
  - **syncopated** - Off-beat accents and complexity.
  - **driving** - Strong, propulsive beat.
  - **loose** - Free, unstructured rhythm.
  - **polyrhythmic** - Layered, multiple rhythms at once.
- **Sample Usage**:
  ```
  [rhythm: Syncopated percussion with a driving bassline.]
  ```
- **Genre-Based Usage**:
  - **Jazz & Funk**: **"Syncopated" for groovy rhythms.**
  - **Rock & Metal**: **"Driving" for relentless energy.**
  - **Electronic & House**: **"Steady" for dance floor beats.**
  - **Orchestral & Classical**: **"Polyrhythmic" for layered, complex motion.**

### **Track Structure Recommendation**
- **[rhythm: Driving beat with syncopated percussion]**
- **[verse: Light rhythmic presence with hi-hat groove]**
- **[chorus: Full-on, steady kick and bass lock]**
- **[outro: Rhythmic fade-out with low percussion echoes]**

---

## [rhythmic-motif]
- **Meaning**: Specifies a **recurring rhythmic pattern or idea** that defines the groove of a piece.
- **Placement**: Typically used within `[rhythm]`, `[structure]`, or `[theme]`.
- **Accepted Parameters**:
  - **syncopated** - Offbeat rhythmic patterns.
  - **driving** - Repetitive, high-energy patterns.
  - **sparse** - Minimal rhythmic elements, creating space.
  - **polyrhythmic** - Overlapping rhythms of different time signatures.
  - **irregular** - Unpredictable rhythmic phrasing.
- **Sample Usage**:
  ```
  [rhythmic-motif: Driving polyrhythms layered with syncopated hi-hats.]
  ```
- **Genre-Based Usage**:
  - **Classical & Minimalist**: Used in **Steve Reich’s** works (e.g., **phasing motifs**).
  - **Jazz & Funk**: Syncopated motifs create a **groove-heavy feel**.
  - **Electronic & House**: Repeating motifs define the **core pulse** of the track.
  - **Progressive Rock & Metal**: **Odd-time signatures** make rhythm motifs feel **complex and dynamic**.

---

## [ritardando]
- **Meaning**: Indicates a **gradual slowing down of tempo**, commonly used in classical, cinematic, and dramatic music.
- **Placement**: Typically placed **within [tempo], [structure], or [dynamics]**.
- **Accepted Parameters**:
  - **gradual** - Smooth, drawn-out slowing.
  - **sudden** - Abrupt tempo reduction.
  - **expressive** - Emotional, flexible tempo shift.
  - **orchestral** - Large-scale slowing for dramatic effect.
- **Sample Usage**:
  ```
  [ritardando: Gradual orchestral slowdown leading into the outro.]
  ```
- **Genre-Based Usage**:
  - **Classical & Film Score**: **"Orchestral" ritardando for cinematic moments.**
  - **Jazz & Ballads**: **"Expressive" ritardando for emotional phrasing.**
  - **Progressive Rock & Metal**: **"Sudden" tempo changes for impact.**
  - **Electronic & Experimental**: **"Gradual" ritardando for transitions.**

### **Track Structure Recommendation**
- **[intro: Steady tempo with melodic buildup]**
- **[verse: Moderate pacing with slight tempo variations]**
- **[bridge: Gradual ritardando leading into the climax]**
- **[outro: Full ritardando to silence]**

---

## [riff]
- **Meaning**: Defines **a recurring instrumental phrase**, typically for guitars, bass, or synths.
- **Placement**: Typically used within **[structure] or [theme]**.
- **Accepted Parameters**:
  - **heavy** - Distorted, strong rock/metal riff.
  - **groovy** - Funky, rhythm-driven riffs.
  - **melodic** - A tuneful, repeating phrase.
  - **minimal** - Subtle, background riffing.
- **Sample Usage**:
  ```
  [riff: Heavy distorted guitar riff driving the chorus.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **"Heavy" for dominant, powerful riffs.**
  - **Funk & Jazz**: **"Groovy" for rhythmically engaging motifs.**
  - **Electronic & Synthwave**: **"Melodic" for repeating synth leads.**
  - **Minimalist & Experimental**: **"Minimal" for atmospheric textures.**

### **Track Structure Recommendation**
- **[intro: Solo bass riff leading into the verse]**
- **[verse: Light accompaniment, riff building up]**
- **[chorus: Full-band riff repetition with harmonies]**
- **[bridge: Riff transforms into a more complex variation]**
- **[outro: Stripped-down riff fading out]**

---

## [rise]
- **Meaning**: Specifies a **buildup or gradual increase in energy**, often used before a climax or drop.
- **Placement**: Typically used **within [structure], [build-up], or [dynamics]**.
- **Accepted Parameters**:
  - **slow** - Gradual, long buildup.
  - **fast** - Quick, tension-building rise.
  - **orchestral** - Swelling, cinematic rise.
  - **synth-driven** - Filter sweeps and pitch risers.
- **Sample Usage**:
  ```
  [rise: Fast synth build leading into an explosive drop.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Dance**: **"Synth-driven" for high-energy transitions.**
  - **Rock & Metal**: **"Fast" for intense lead-ins to choruses.**
  - **Orchestral & Film Score**: **"Orchestral" for swelling crescendos.**
  - **Ambient & Experimental**: **"Slow" for gradually intensifying textures.**

### **Track Structure Recommendation**
- **[intro: Soft piano with distant pads]**
- **[verse: Gradual instrument layering]**
- **[rise: Orchestral crescendo into the chorus]**
- **[chorus: Full-blown sound with intense energy]**
- **[outro: Decaying echo after the final rise]**

---

## [rondo]
- **Meaning**: Defines a **musical structure based on a recurring main theme (A) alternating with contrasting sections (B, C, etc.)**, typically structured as **ABACA** or **ABACABA**.  
- **Placement**: Typically used within **[structure], [form], or [theme]**.  
- **Accepted Parameters**:  
  - **classical** - Traditional rondo form as found in sonatas and concertos.  
  - **modern** - A flexible interpretation with contemporary instrumentation.  
  - **fast** - A rapid, lively rondo typical in finales.  
  - **lyrical** - A slower, expressive form of rondo.  
- **Sample Usage**:  
  ```
  [rondo: Classical fast rondo with a recurring violin melody.]
  ```
- **Genre-Based Usage**:  
  - **Classical & Baroque**: **"Classical" for authentic rondo structures.**  
  - **Jazz & Improvisation**: **"Modern" for thematic call-and-response phrasing.**  
  - **Progressive Rock & Metal**: **"Fast" for energetic repeating motifs.**  
  - **Electronic & Cinematic**: **"Lyrical" for evolving soundscapes.**  

### **Track Structure Recommendation**  
- **[intro: Soft piano theme establishing the main melody]**  
- **[rondo: Main theme played on violin, alternating with variations]**  
- **[section: Contrasting percussive transition before the theme returns]**  
- **[secondary theme: A new melody introduced for variation]**  
- **[outro: Recap of the main theme, fading into an orchestral swell]**  

---

## [sad]
- **Meaning**: Specifies a **melancholic or emotional mood** for the track.  
- **Placement**: Typically used within **[mood], [dynamics], or [harmony]**.  
- **Accepted Parameters**:  
  - **melancholic** - Gloomy, sorrowful tone.  
  - **introspective** - Thoughtful, nostalgic feel.  
  - **haunting** - Dark, eerie sadness.  
  - **soft** - Gentle, emotional sadness.  
  - **tragic** - Deep, dramatic expression of sorrow.  
- **Sample Usage**:  
  ```
  [sad: Introspective piano chords with deep string harmonies.]
  ```
- **Genre-Based Usage**:  
  - **Classical & Orchestral**: **"Tragic" for operatic, sorrowful climaxes.**  
  - **Indie & Folk**: **"Soft" for delicate, emotional songwriting.**  
  - **Ambient & Cinematic**: **"Haunting" for atmospheric sadness.**  
  - **Blues & Jazz**: **"Melancholic" for expressive phrasing.**  

### **Track Structure Recommendation**  
- **[intro: Solo violin introducing a melancholic theme]**  
- **[verse: Soft piano chords with distant echoing guitar]**  
- **[chorus: Layered vocal harmonies intensifying the emotion]**  
- **[bridge: Slow cello solo with fading resonance]**  
- **[outro: Gentle decrescendo into silence]**  

---

## [scale]
- **Meaning**: Defines the **musical scale or mode** used in the composition.  
- **Placement**: Typically used within **[harmony]**.  
- **Accepted Parameters**:  
  - **major** - A bright, uplifting scale.  
  - **minor** - A darker, more melancholic scale.  
  - **chromatic** - A scale using all 12 notes of the octave.  
  - **modal** - Specific modes like Dorian, Phrygian, Mixolydian.  
  - **pentatonic** - Five-note scale common in blues and folk.  
- **Sample Usage**:  
  ```
  [scale: Phrygian mode for a mystical, Middle Eastern feel.]
  ```
- **Genre-Based Usage**:  
  - **Classical & Jazz**: **"Modal" for harmonic variety.**  
  - **Blues & Rock**: **"Pentatonic" for expressive solos.**  
  - **Metal & Darkwave**: **"Phrygian" for exotic tension.**  
  - **Electronic & Experimental**: **"Chromatic" for avant-garde dissonance.**  

### **Track Structure Recommendation**  
- **[intro: Flute solo introducing a minor pentatonic melody]**  
- **[verse: Gently evolving harmonic phrases in Dorian mode]**  
- **[chorus: Expansive major key modulation for contrast]**  
- **[bridge: Chromatic scale run leading into an energetic climax]**  
- **[outro: Modal resolution with subtle cadences]**  

---

## [scherzo]
- **Meaning**: Defines a **lively, fast-paced musical section**, often humorous or energetic.  
- **Placement**: Typically used within **[structure], [theme], or [rhythm]**.  
- **Accepted Parameters**:  
  - **playful** - Light, whimsical feel.  
  - **dramatic** - Intense, dynamic contrast.  
  - **orchestral** - Traditional classical scherzo form.  
  - **modern** - Contemporary, fusion scherzo styles.  
- **Sample Usage**:  
  ```
  [scherzo: Playful, rapid string interplay with unexpected shifts.]
  ```
- **Genre-Based Usage**:  
  - **Classical & Romantic**: **"Orchestral" scherzos in symphonies.**  
  - **Jazz & Swing**: **"Playful" with improvisatory phrasing.**  
  - **Rock & Metal**: **"Dramatic" scherzo-style fast breaks.**  
  - **Electronic & Experimental**: **"Modern" for glitchy, unpredictable textures.**  

### **Track Structure Recommendation**  
- **[intro: High-energy piano arpeggios]**  
- **[scherzo: Playful violin and flute interactions]**  
- **[section: Rhythmic variation with unexpected accents]**  
- **[outro: Decrescendo into a light, fading motif]**  

---

## [secondary theme]
- **Meaning**: Defines a **contrasting melody or motif** introduced after the main theme.  
- **Placement**: Typically used within **[theme], [development], or [structure]**.  
- **Accepted Parameters**:  
  - **contrasting** - Distinctly different from the main theme.  
  - **harmonized** - Played in parallel with the main theme.  
  - **variational** - A variation of the original theme.  
  - **dramatic** - High-impact, contrasting intensity.  
- **Sample Usage**:  
  ```
  [secondary theme: A darker, harmonized variation of the main melody.]
  ```
- **Genre-Based Usage**:  
  - **Classical & Romantic**: **"Contrasting" for sonata forms.**  
  - **Jazz & Fusion**: **"Variational" for evolving solos.**  
  - **Rock & Metal**: **"Dramatic" for intense counter-melodies.**  
  - **Electronic & Ambient**: **"Harmonized" for rich layering.**  

### **Track Structure Recommendation**  
- **[intro: Main theme introduced by solo piano]**  
- **[secondary theme: Contrasting melody introduced by strings]**  
- **[development: Expansion of both themes into interweaving motifs]**  
- **[outro: Final resolution where both themes blend together]**  

---

## [sforzando]
- **Meaning**: Indicates a **sudden, strong accent on a note or chord**, creating dramatic impact.
- **Placement**: Typically used within **[dynamics] or [harmony]**, marking specific sections that need extra emphasis.
- **Accepted Parameters**:
  - **single-hit** - One strong, immediate accent.
  - **repeated** - Several forceful accents in succession.
  - **orchestral** - Emphasized brass or strings.
  - **percussive** - Applied to drums or rhythmic hits.
- **Sample Usage**:
  ```
  [sforzando: Sudden brass stabs leading into the chorus.]
  ```
- **Genre-Based Usage**:
  - **Classical & Romantic**: **"Orchestral" for bold symphonic hits.**
  - **Jazz & Big Band**: **"Single-hit" for sharp brass accents.**
  - **Rock & Metal**: **"Repeated" for aggressive drum fills.**
  - **Electronic & Experimental**: **"Percussive" for rhythmic punches.**

### **Track Structure Recommendation**
- **[intro: String crescendo into sforzando brass explosion]**
- **[verse: Subtle build-up with occasional accented piano notes]**
- **[chorus: Repeated sforzando orchestral stabs]**
- **[outro: Single sforzando impact followed by silence]**

---

## [sfx]
- **Meaning**: Inserts **non-musical sound effects**, such as ambient noises, environmental recordings, or mechanical sounds.
- **Placement**: Typically used **within [effects], [mixing], or [atmosphere]**.
- **Accepted Parameters**:
  - **wind** - Background wind or stormy gusts.
  - **whispering** - Eerie vocal whispers.
  - **industrial** - Mechanical clanks, gears, factory sounds.
  - **nature** - Birds, water, natural ambiance.
  - **glitch** - Digital distortion effects.
- **Sample Usage**:
  ```
  [sfx: Distant whispering layered over orchestral swells.]
  ```
- **Genre-Based Usage**:
  - **Ambient & Experimental**: **"Nature" for immersive soundscapes.**
  - **Horror & Industrial**: **"Whispering" for eerie effects.**
  - **Electronic & Cyberpunk**: **"Glitch" for digital distortions.**
  - **Cinematic & Sci-Fi**: **"Industrial" for futuristic settings.**

### **Track Structure Recommendation**
- **[intro: Distant sfx of wind gusts and mechanical hum]**
- **[verse: Subtle use of whispered sfx in the background]**
- **[chorus: Heavy industrial sounds layered under percussion]**
- **[outro: Distant echoes of glitching, distorted sfx fading out]**

---

## [shout]
- **Meaning**: Defines **a shouted or forcefully spoken vocal element**, typically for intensity or emphasis.
- **Placement**: Typically used **within [vocals], [effects], or [background-vocals]**.
- **Accepted Parameters**:
  - **single** - One loud, emphasized shout.
  - **group** - A collective shout, chant-like.
  - **layered** - Blended with other vocal harmonies.
  - **distorted** - Aggressive, processed shouting.
- **Sample Usage**:
  ```
  [shout: Group chant layered over the chorus for intensity.]
  ```
- **Genre-Based Usage**:
  - **Rock & Punk**: **"Single" for raw emotional delivery.**
  - **Hip-Hop & Trap**: **"Layered" for hype vocals.**
  - **Metal & Hardcore**: **"Distorted" for growling or aggressive shouts.**
  - **Electronic & Industrial**: **"Group" for robotic crowd effects.**

### **Track Structure Recommendation**
- **[intro: Gradual rise leading to a shouted exclamation]**
- **[verse: Tense buildup with occasional shouted words]**
- **[chorus: Group shouts layered for anthem-like energy]**
- **[bridge: Intense, distorted shouting transitioning into climax]**
- **[outro: Final lingering echoes of the last shout]**

---

## [signal-processing]
- **Meaning**: Defines **digital or analog audio effects** applied to instruments, vocals, or the entire mix to **enhance or alter** the sound.
- **Placement**: Typically used within `[effects]`, `[mixing]`, or `[instruments]`.
- **Accepted Parameters**:
  - **reverb** - Adds **depth and space** to the sound.
  - **delay** - Creates **echo-like repetitions**.
  - **compression** - Balances **volume dynamics**.
  - **saturation** - Adds **harmonic warmth or analog distortion**.
  - **bitcrush** - Reduces sound quality for a **lo-fi or glitchy effect**.
  - **phaser** - Creates **swirling, modulated movement**.
  - **flanger** - Produces **sweeping, jet-like effects**.
  - **chorus** - Thickens the sound by **doubling and detuning**.
  - **distortion** - Adds **clipping and grit**.
- **Sample Usage**:
  ```
  [signal-processing: Heavy saturation on synth bass for a warm, analog feel.]
  ```
- **Genre-Based Usage**:
  - **Electronic**: **Bitcrush** and **phaser** for lo-fi or cyberpunk aesthetics.
  - **Rock & Metal**: **Saturation** and **distortion** for aggressive, high-energy tracks.
  - **Ambient & Cinematic**: **Reverb** and **delay** for wide, spacious soundscapes.
  - **Funk & Disco**: **Chorus and flanger** for groovy textures.

### **Track Structure Recommendation**
- **[intro: Dry signal]**
- **[verse: Light reverb on vocals, subtle compression]**
- **[chorus: Heavy delay and saturation on guitars]**
- **[bridge: Phased-out synths for psychedelic effect]**
- **[outro: Bitcrushed drums fading into silence]**

---

## [silence]
- **Meaning**: Inserts **intentional moments of complete silence** into the track, often used for dramatic effect or transitions.  
- **Placement**: Typically used within **[structure], [dynamics], or [effects]**, often in conjunction with **[drop], [break], or [pause]** to create contrast.  
- **Accepted Parameters**:
  - **short** - A brief moment of silence, lasting milliseconds to a few seconds.  
  - **sudden** - An immediate, unexpected cut-off.  
  - **gradual** - A slow fade into silence.  
  - **echoed** - A silence followed by reverberating echoes.  
- **Sample Usage**:
  ```
  [silence: Sudden, dramatic pause before the chorus drop.]
  ```
- **Genre-Based Usage**:
  - **Electronic & EDM**: **"Sudden" before a bass drop for extra impact.**  
  - **Cinematic & Orchestral**: **"Gradual" for suspense-building moments.**  
  - **Jazz & Funk**: **"Short" to create rhythmic breathing space.**  
  - **Metal & Industrial**: **"Echoed" for a mechanical glitch effect.**  

### **Track Structure Recommendation**
- **[intro: Soft pad textures leading into rhythm]**  
- **[verse: Build-up of rhythmic energy]**  
- **[silence: Short, dramatic pause before the chorus]**  
- **[chorus: Full-on instrumental explosion]**  
- **[outro: Gradual silence leading to a final reverb tail]**

---

## [sincopation]
*(Often written as "syncopation")*  
- **Meaning**: Defines **off-beat rhythmic accents**, often creating a more dynamic and unpredictable groove.  
- **Placement**: Typically used within **[rhythm], [pulse], or [structure]** to alter the beat pattern.  
- **Accepted Parameters**:
  - **light** - Subtle syncopation, slightly off-grid but smooth.  
  - **complex** - Multi-layered, unexpected rhythmic accents.  
  - **jazzy** - Swung and groovy syncopation.  
  - **heavily-accented** - Extreme offbeat accents, commonly in funk and experimental music.  
- **Sample Usage**:
  ```
  [sincopation: Jazzy groove with subtle off-beat snare accents.]
  ```
- **Genre-Based Usage**:
  - **Jazz & Funk**: **"Jazzy" for swing-influenced beats.**  
  - **Rock & Progressive Metal**: **"Complex" for intricate time signatures.**  
  - **Hip-Hop & Trap**: **"Light" for smooth yet unpredictable rhythms.**  
  - **Electronic & Drum & Bass**: **"Heavily-accented" for breakbeat patterns.**  

### **Track Structure Recommendation**
- **[intro: Straight beat with occasional syncopated kicks]**  
- **[verse: Lightly syncopated snare rhythm for groove]**  
- **[chorus: Full, complex syncopation with layered percussions]**  
- **[outro: Slow fading groove with light rhythmic stutters]**

---

## [solo]
- **Meaning**: Highlights **a single instrument or voice performing an exposed lead passage** within the track.  
- **Placement**: Typically used within **[instrument] or [bridge]** to indicate a featured instrumental performance.  
- **Accepted Parameters**:
  - **guitar** - A classic electric or acoustic guitar solo.  
  - **saxophone** - A jazz or blues-inspired lead.  
  - **synth** - A lead solo using synthesizer sounds.  
  - **piano** - A melodic or virtuosic piano passage.  
  - **drum** - A rhythmically intense drum solo.  
- **Sample Usage**:
  ```
  [solo: Melodic piano improvisation leading into the final chorus.]
  ```
- **Genre-Based Usage**:
  - **Rock & Metal**: **"Guitar" for shredding lead breaks.**  
  - **Jazz & Blues**: **"Saxophone" for smooth, expressive leads.**  
  - **Electronic & Synthwave**: **"Synth" for atmospheric or arpeggiated solos.**  
  - **Funk & Fusion**: **"Drum" for a high-energy breakdown.**  

### **Track Structure Recommendation**
- **[intro: Slow melodic buildup]**  
- **[verse: Establishes theme with groove]**  
- **[solo: Extended guitar solo with harmonic layering]**  
- **[chorus: Return of the main theme with higher intensity]**  
- **[outro: Synth fade-out featuring final soloing phrases]**

---

## [sonority]
- **Meaning**: Describes the **overall tonal quality and richness** of a sound.
- **Placement**: Typically used within `[harmony]`, `[tone]`, or `[mixing]`.
- **Accepted Parameters**:
  - **bright** - Crisp, high-frequency emphasis.
  - **dark** - Lower, mellow tones.
  - **warm** - Smooth and full.
  - **rich** - Harmonically dense and layered.
  - **thin** - Lacking fullness, sparse.
  - **harsh** - Overly bright or aggressive.
- **Sample Usage**:
  ```
  [sonority: Warm, rich brass sections to add cinematic depth.]
  ```
- **Genre-Based Usage**:
  - **Orchestral & Classical**: **Rich and warm sonority** for full-bodied compositions.
  - **Jazz**: **Dark and warm sonorities** for saxophone and double bass.
  - **Electronic & Industrial**: **Bright and harsh sonorities** for intense leads.
  - **Lo-Fi & Chill**: **Thin and soft sonorities** to create a relaxed vibe.

### **Track Structure Recommendation**
- **[intro: Thin sonority with only ambient pads]**
- **[verse: Warm piano chords with dark cello layers]**
- **[chorus: Rich orchestration, deep strings, and bright brass]**
- **[bridge: High, bright synth arpeggios for contrast]**
- **[outro: Dark ambient tones fading into silence]**

---

## [spoken word]

**Category:** Vocal delivery / genre tag  
**Primary use:** To request non-sung, rhythmic or prose-like speech instead of traditional melodic singing.

**Behavior and intent**  
`[spoken word]` encourages the model to treat the delivery more like poetry performance, narration, or rap‑adjacent speech, often with loose pitch but clear rhythm. It differs from `[rap]` by leaning less on strict flow patterns and more on poetic or storytelling cadence.

**Placement and syntax**  

- *Lyrics field:*  
  - As a section tag:  
    - `[spoken word | intimate, close-mic, almost whispered]`  
    - `[verse | spoken word over minimal piano]`  
- *Style of Music field:*  
  - “ambient spoken word piece with sparse chords and vinyl crackle”

**Typical use-cases**  

- Poetry over drones or ambient beds  
- Narrative interludes between sung sections  
- Concept tracks where storytelling is more important than melody

Combine `[spoken word]` with clear, well‑punctuated text. Very complex rhyme schemes or forced line breaks may reduce the natural feel of the delivery.

---

## [staccato]
- **Meaning**: Specifies **short, detached musical notes**, often used for rhythmic sharpness.  
- **Placement**: Typically used within **[harmony] or [rhythm]**.  
- **Accepted Parameters**:
  - **sharp** - Strong, abrupt articulation.  
  - **soft** - Light but detached playing.  
  - **accented** - Heavily pronounced and rhythmically emphasized.  
  - **orchestral** - Typically applied to string sections.  
- **Sample Usage**:
  ```
  [staccato: Sharp, syncopated brass stabs punctuating the chorus.]
  ```
- **Genre-Based Usage**:
  - **Classical & Film Score**: **"Orchestral" for dramatic tension-building.**  
  - **Funk & Groove**: **"Accented" for punchy horn stabs.**  
  - **Rock & Metal**: **"Sharp" for palm-muted guitar chugging.**  
  - **Electronic & House**: **"Soft" for bouncy, short synth plucks.**  

### **Track Structure Recommendation**
- **[intro: Staccato string plucks over soft pads]**  
- **[verse: Playful interplay between staccato horns and rhythm guitar]**  
- **[chorus: Heavy accented brass stabs leading into a full sound]**  
- **[outro: Subtle fading staccato arpeggios]**

---

## [start]
- **Meaning**: Specifies **how the track begins**, controlling the intro's structure and impact.  
- **Placement**: Typically used **before [intro]**, defining the opening.  
- **Accepted Parameters**:
  - **sudden** - An immediate, high-energy start.  
  - **gradual** - A slow, evolving intro.  
  - **orchestral** - A symphonic overture-like beginning.  
  - **percussive** - A rhythm-driven introduction.  
  - **fade-in** - A slow volume increase from silence.  
- **Sample Usage**:
  ```
  [start: Gradual, orchestral swelling leading into full instrumentation.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Ambient**: **"Fade-in" for smooth transitions.**  
  - **Rock & Punk**: **"Sudden" for immediate impact.**  
  - **Hip-Hop & Trap**: **"Percussive" for beat-driven introductions.**  
  - **Classical & Cinematic**: **"Orchestral" for dramatic overtures.**  

### **Track Structure Recommendation**
- **[start: Percussive, high-energy drum fills]**  
- **[intro: Deep synth bass rumbling in the background]**  
- **[verse: Beat drops with full melodic elements]**  
- **[chorus: Peak intensity with layered instruments]**  
- **[outro: Gradual fade-out to silence]**

---

## [stereo]
- **Meaning**: Controls the **stereo width and spatial balance** of the track, affecting how instruments and sounds are positioned in the left-right stereo field.
- **Placement**: Typically used **before [mixing] or [effects]**, but can also appear independently to guide the track’s overall stereo imaging.
- **Accepted Parameters**:
  - **narrow** - Focused, centered mix with little stereo spread.
  - **wide** - Broad, spacious stereo imaging.
  - **panning** - Dynamic left-right movement of elements.
  - **immersive** - Full stereo depth with layered sounds.
  - **mono** - Collapsed stereo for vintage/lo-fi sound.
- **Sample Usage**:
  ```
  [stereo: Wide mix with immersive spatial reverb.]
  ```
- **Genre-Based Usage**:
  - **Electronic & Ambient**: **"Immersive" for deep, spatially rich mixes.**
  - **Rock & Metal**: **"Wide" for guitars panned left/right.**
  - **Lo-Fi & Vintage**: **"Mono" for old-school tape-style sound.**
  - **Orchestral & Cinematic**: **"Panning" for dynamic instrument movement.**

### **Track Structure Recommendation**
- **[stereo: Wide panning for an immersive intro]**
- **[verse: Instruments focused in the center with slight stereo spread]**
- **[chorus: Wide stereo mix for an expansive, open feel]**
- **[outro: Gradual stereo collapse into mono for a vintage fade-out]**

---

## [stretto]
- **Meaning**: A **contrapuntal technique where overlapping melodic phrases** occur in close succession, commonly found in fugues and polyphonic compositions.
- **Placement**: Typically used within `[counterpoint]` or `[structure]`.
- **Accepted Parameters**:
  - **tight** - Very close entries of the theme.
  - **moderate** - Slightly spaced-out but still overlapping.
  - **dense** - Multiple themes layered simultaneously.
  - **descending** - The entries come in progressively lower registers.
  - **ascending** - The entries rise in pitch.
- **Sample Usage**:
  ```
  [stretto: Tight, ascending theme entries increasing tension.]
  ```
- **Genre-Based Usage**:
  - **Classical & Baroque**: **Fugue compositions**.
  - **Jazz & Improvisation**: **Call-and-response phrasing**.
  - **Progressive Rock & Metal**: **Layered, interwoven guitar parts**.
  - **Electronic & Experimental**: **Synth arpeggios in contrapuntal motion**.

### **Track Structure Recommendation**
- **[intro: Single melody stated clearly]**
- **[stretto: Additional voices entering in close succession]**
- **[development: Expansion of the theme in different registers]**
- **[recapitulation: Full-scale overlapping entry of all voices]**
- **[outro: Resolving back into a single voice, fading out]**

---

## [structure]
- **Meaning**: Defines the **overall song arrangement**, specifying how sections like **intro, verse, chorus, and bridge** are organized.
- **Placement**: **Before structural meta-tags (intro, verse, chorus, etc.)**, outlining their sequence.
- **Accepted Parameters**:
  - **standard** - Conventional verse-chorus form.
  - **through-composed** - Continuous, evolving structure without repetition.
  - **loop-based** - Repeating segments forming a cyclic composition.
  - **progressive** - Gradually evolving, dynamically shifting structure.
  - **experimental** - Unconventional, unpredictable development.
- **Sample Usage**:
  ```
  [structure: Progressive, evolving sections with gradual build-up.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **"Standard" for radio-friendly verse-chorus structures.**
  - **Orchestral & Film Score**: **"Through-composed" for evolving storytelling.**
  - **Electronic & House**: **"Loop-based" for continuous dance grooves.**
  - **Metal & Progressive Rock**: **"Progressive" for complex arrangements.**

### **Track Structure Recommendation**
- **[structure: Through-composed with seamless transitions]**
- **[intro: Soft synth textures building tension]**
- **[verse: Vocal-driven melody with deep harmonies]**
- **[chorus: Expansive, anthemic instrumental swells]**
- **[bridge: Unexpected tempo shift and modulation]**
- **[outro: Gradual fade into atmospheric soundscapes]**

---

## [subharmonic]
- **Meaning**: Refers to **frequencies below the fundamental pitch**, often used to enhance **low-end power**.
- **Placement**: Typically used within `[bass]`, `[mixing]`, or `[instruments]`.
- **Accepted Parameters**:
  - **deep** - Emphasized low-end, rumbling bass.
  - **saturated** - Enhanced with harmonic overtones.
  - **modulated** - Varying frequency for movement.
  - **layered** - Multiple subharmonic layers for impact.
- **Sample Usage**:
  ```
  [subharmonic: Deep sub-bass layered with modulated synth tones.]
  ```
- **Genre-Based Usage**:
  - **Trap & Hip-Hop**: **Heavy 808 sub-bass** for deep, rolling basslines.
  - **Electronic & Techno**: **Modulated subharmonics** for club-shaking power.
  - **Cinematic & Horror**: **Low-end subharmonic drones** for tension.
  - **Industrial & Metal**: **Saturated subharmonic distortion** for intensity.

### **Track Structure Recommendation**
- **[intro: Soft subharmonic pulse under ambient textures]**
- **[verse: Sub-bass only slightly present for subtle groove]**
- **[chorus: Layered deep subharmonic frequencies with distortion]**
- **[bridge: Modulated subharmonic sweeps for transition]**
- **[outro: Fading, rumbling bass tones]**

---

## [sustain]
- **Meaning**: Defines how **long a note or sound is held before fading**.
- **Placement**: Typically used within `[dynamics]`, `[instruments]`, or `[mixing]`.
- **Accepted Parameters**:
  - **long** - Notes are held for a prolonged period.
  - **short** - Notes decay quickly.
  - **moderate** - Balanced sustain between short and long.
  - **swelling** - Gradual increase in sustain intensity.
- **Sample Usage**:
  ```
  [sustain: Long-held string pads for atmospheric depth.]
  ```
- **Genre-Based Usage**:
  - **Cinematic & Orchestral**: **Long sustain** for strings and brass.
  - **Jazz & Blues**: **Short sustain** for percussive articulation.
  - **Rock & Metal**: **Saturated sustain on guitars** for a powerful effect.
  - **Electronic & Ambient**: **Swelling sustain** for evolving soundscapes.

### **Track Structure Recommendation**
- **[intro: Short percussive elements with no sustain]**
- **[verse: Moderate sustain on vocals and chords]**
- **[chorus: Long, swelling synths and string pads]**
- **[bridge: Sudden contrast with short sustain piano notes]**
- **[outro: Gradually fading sustained guitar notes]**

---

## [swell]
- **Meaning**: Defines a **gradual increase in volume or intensity**, often leading into climactic sections.
- **Placement**: Typically used **before [dynamics], [chorus], or [build-up]**, signaling increasing energy.
- **Accepted Parameters**:
  - **orchestral** - Expanding instrumentation, often with strings or brass.
  - **synth-driven** - Electronic rise with filter automation.
  - **percussive** - Gradual increase in drum intensity.
  - **dramatic** - High-impact crescendo leading to a climax.
- **Sample Usage**:
  ```
  [swell: Dramatic orchestral crescendo before the final chorus.]
  ```
- **Genre-Based Usage**:
  - **Orchestral & Film Score**: **"Orchestral" for sweeping, symphonic rises.**
  - **Electronic & Dance**: **"Synth-driven" for pre-drop build-ups.**
  - **Rock & Metal**: **"Percussive" for drum-driven energy lifts.**
  - **Ambient & Experimental**: **"Dramatic" for cinematic suspense.**

### **Track Structure Recommendation**
- **[swell: Percussive crescendo leading into climax]**
- **[intro: Subtle textures gradually growing in volume]**
- **[verse: Light instrumentation with rising tension]**
- **[chorus: Full dynamic explosion following the swell]**
- **[outro: Swelling strings resolving into soft ambience]**

---

## [syncopation]
- **Meaning**: Defines **offbeat rhythmic emphasis** that disrupts a regular pattern.
- **Placement**: Typically used within `[rhythm]` or `[structure]`.
- **Accepted Parameters**:
  - **funky** - Offbeat groove, typical in funk and jazz.
  - **irregular** - Unexpected offbeat accents.
  - **subtle** - Light syncopation for a slight groove.
  - **heavy** - Strong syncopation that dominates the rhythm.
  - **polyrhythmic** - Overlapping syncopated patterns.
- **Sample Usage**:
  ```
  [syncopation: Funky offbeat hi-hats layered with irregular snare hits.]
  ```
- **Genre-Based Usage**:
  - **Funk & Jazz**: **Heavy syncopation** to create groove.
  - **Reggae**: **Offbeat rhythmic patterns** for laid-back feel.
  - **Hip-Hop & Trap**: **Irregular hi-hats and kicks** for rhythmic bounce.
  - **Progressive Rock & Metal**: **Complex polyrhythmic syncopation** for dynamic motion.

### **Track Structure Recommendation**
- **[intro: Subtle syncopation in hi-hats]**
- **[verse: Irregular bass and drum groove]**
- **[chorus: Heavy syncopated guitar riffs and percussion]**
- **[bridge: Polyrhythmic overlapping elements]**
- **[outro: Simplified rhythm gradually fading]**

---

## [tension-release]
- **Meaning**: Defines the **contrast between musical tension and resolution**, essential for emotional impact.
- **Placement**: Typically used within `[harmony]`, `[structure]`, or `[dynamics]`.
- **Accepted Parameters**:
  - **gradual** - Slow buildup of tension leading to resolution.
  - **sudden** - Sharp contrast between tension and release.
  - **sustained** - Prolonged tension without immediate resolution.
  - **layered** - Different instrumental groups build tension in stages.
  - **chromatic** - Tension created by non-diatonic movement.
- **Sample Usage**:
  ```
  [tension-release: Gradual orchestral buildup resolving into a peaceful melody.]
  ```
- **Genre-Based Usage**:
  - **Cinematic & Orchestral**: Tension swells using **strings and brass**, resolved with open chords.
  - **Jazz & Blues**: Chromatic chords build suspense before resolving into smooth progressions.
  - **Electronic & EDM**: Sudden release after **a filtered buildup**, often leading into a drop.
  - **Rock & Metal**: Guitar tremolos and dissonance before resolving into **power chords**.

### **Track Structure Recommendation**
- **[intro: Subtle drone pads establishing tension]**
- **[verse: Gradual harmonic tension with unresolved phrases]**
- **[chorus: Sudden release into a wide, open melody]**
- **[bridge: Layered tension with orchestral swells]**
- **[outro: Dissolving tension with slow fade-out]**

---

## [tenuto]
- **Meaning**: Marks **notes or phrases that should be sustained for their full value**, often giving them expressive weight.
- **Placement**: Typically used **within [dynamics] or [articulation]**, indicating emphasis on certain musical phrases.
- **Accepted Parameters**:
  - **soft** - Gentle sustain with delicate phrasing.
  - **bold** - Strong, commanding sustain.
  - **orchestral** - Used in symphonic settings for expressive long notes.
  - **legato-tenuto** - Combined with legato phrasing for seamless expression.
- **Sample Usage**:
  ```
  [tenuto: Bold brass accents in the climax section.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: **"Orchestral" for dynamic long notes.**
  - **Jazz & Blues**: **"Soft" for expressive phrasing in solos.**
  - **Rock & Metal**: **"Bold" for sustaining power chords.**
  - **Electronic & Cinematic**: **"Legato-tenuto" for evolving ambient pads.**

### **Track Structure Recommendation**
- **[intro: Soft tenuto strings swelling into melody]**
- **[verse: Light, expressive piano with tenuto emphasis]**
- **[chorus: Bold brass stabs with sustained power]**
- **[outro: Legato-tenuto strings fading to silence]**

---

## [tessitura]
- **Meaning**: Defines the **average vocal or instrumental pitch range** within a composition.
- **Placement**: Typically used within `[vocals]` or `[orchestration]`.
- **Accepted Parameters**:
  - **low** - Notes are concentrated in the lower range.
  - **mid** - Melody stays within a moderate range.
  - **high** - Notes are mostly in the upper range.
  - **wide** - A large range is covered.
  - **focused** - Limited to a small pitch range.
- **Sample Usage**:
  ```
  [tessitura: High soprano melody soaring over deep cellos.]
  ```
- **Genre-Based Usage**:
  - **Opera & Classical**: High tessitura is common for **dramatic soprano parts**.
  - **Jazz & Soul**: Mid-range tessitura enhances warm, expressive vocal lines.
  - **Pop & Rock**: Wide tessitura in the **chorus for emotional intensity**.
  - **Electronic & Ambient**: Focused tessitura keeps **consistency in textures**.

### **Track Structure Recommendation**
- **[intro: Low tessitura for warmth and depth]**
- **[verse: Mid-range vocal tessitura for balance]**
- **[chorus: Wide-range melodic expansion]**
- **[bridge: High tessitura, building to climax]**
- **[outro: Gradual drop back to lower tessitura]**

---

## [texture]
- **Meaning**: Defines **the density and layering of sound** within the composition.
- **Placement**: Typically used **within [style], [mixing], or [harmony]**, describing how elements are combined.
- **Accepted Parameters**:
  - **thin** - Sparse, minimal instrumentation.
  - **dense** - Rich, multi-layered textures.
  - **polyphonic** - Independent melodies playing simultaneously.
  - **homophonic** - Chordal texture with melody and accompaniment.
- **Sample Usage**:
  ```
  [texture: Polyphonic, with layered vocal harmonies and interwoven melodies.]
  ```
- **Genre-Based Usage**:
  - **Classical & Jazz**: **"Polyphonic" for interwoven lines.**
  - **Pop & Rock**: **"Homophonic" for melody-driven sections.**
  - **Ambient & Soundscape**: **"Dense" for lush, immersive textures.**
  - **Minimalist & Experimental**: **"Thin" for spacious, atmospheric compositions.**

### **Track Structure Recommendation**
- **[texture: Gradually shifting from thin to dense layers]**
- **[intro: Sparse, ambient textures fading in]**
- **[verse: Light, minimal layers with open space]**
- **[chorus: Full, rich orchestral density]**
- **[outro: Gradual deconstruction into a thin, fading texture]**

---

## [theme]
- **Meaning**: Establishes **a recurring melodic, rhythmic, or harmonic idea**, serving as the track’s central motif.
- **Placement**: Typically used **within [structure]**, guiding how the main idea develops.
- **Accepted Parameters**:
  - **primary** - The main recurring motif.
  - **secondary** - A contrasting yet complementary idea.
  - **variational** - A transformed version of the original theme.
  - **layered** - Multiple interwoven themes.
- **Sample Usage**:
  ```
  [theme: Primary melody introduced by flute, later developed with strings.]
  ```
- **Genre-Based Usage**:
  - **Classical & Soundtrack**: **"Primary" for recurring melodic motifs.**
  - **Progressive Rock & Jazz**: **"Variational" for evolving ideas.**
  - **Electronic & Ambient**: **"Layered" for textural depth.**
  - **Folk & Singer-Songwriter**: **"Secondary" for contrast between verses and choruses.**

### **Track Structure Recommendation**
- **[theme: Recurring melodic motif played by piano]**
- **[verse: Thematic development through harmonic expansion]**
- **[chorus: Secondary theme introduced for contrast]**
- **[bridge: Variational transformation of primary theme]**
- **[outro: Theme resolution in soft strings]**

---

## [timbre]
- **Meaning**: Describes the **unique tonal color or character** of a sound.
- **Placement**: Typically used within `[mixing]`, `[tone]`, or `[orchestration]`.
- **Accepted Parameters**:
  - **bright** - Sharp, crisp overtones.
  - **dark** - Low, warm frequencies.
  - **warm** - Smooth, rounded tone.
  - **harsh** - Intense, aggressive tone.
  - **nasal** - Midrange-heavy, thin tone.
  - **resonant** - Rich and ringing.
- **Sample Usage**:
  ```
  [timbre: Dark, resonant synth pads for a moody backdrop.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: Dark timbres in **strings and woodwinds** for depth.
  - **Rock & Metal**: Harsh, distorted timbres for **aggressive guitars**.
  - **Electronic & Ambient**: Bright, resonant pads create **atmospheric layers**.
  - **Jazz & Blues**: Warm, nasal brass timbres add **expressiveness**.

### **Track Structure Recommendation**
- **[intro: Warm, rounded piano chords]**
- **[verse: Bright guitar melodies with soft resonance]**
- **[chorus: Dark, rich brass harmonies]**
- **[bridge: Harsh synth leads for contrast]**
- **[outro: Soft, resonant string sustain]**

---

## [tone]
- **Meaning**: Defines the **overall timbral character** of the track.
- **Placement**: Typically used **before [mood] or [style]**, shaping the emotional and sonic color.
- **Accepted Parameters**:
  - **bright** - Crisp, high-frequency emphasis.
  - **warm** - Smooth, rounded, and full-bodied.
  - **dark** - Heavy, moody, and bass-heavy.
  - **harsh** - Rough, aggressive tonality.
- **Sample Usage**:
  ```
  [tone: Dark, moody piano with deep reverb.]
  ```
- **Genre-Based Usage**:
  - **Jazz & Blues**: **"Warm" for mellow, rich textures.**
  - **Electronic & Industrial**: **"Harsh" for aggressive synths.**
  - **Rock & Metal**: **"Bright" for cutting lead guitars.**
  - **Cinematic & Horror**: **"Dark" for eerie, foreboding soundscapes.**

### **Track Structure Recommendation**
- **[tone: Warm and nostalgic]**
- **[intro: Soft pads and gently plucked guitar]**
- **[verse: Warm, saturated synths with subtle bass]**
- **[chorus: Brightened tone with shimmering reverb]**
- **[outro: Dark, moody shift with fading low notes]**

---

## [tone-cluster]
- **Meaning**: A **dense grouping of notes** played simultaneously, creating **dissonance or texture**.
- **Placement**: Typically used within `[harmony]` or `[structure]`.
- **Accepted Parameters**:
  - **soft** - Light, atmospheric clusters.
  - **harsh** - Dissonant, aggressive clusters.
  - **chaotic** - Unstructured, unpredictable clusters.
  - **minimal** - Sparse clusters for subtle effect.
  - **sustained** - Long-held clusters.
- **Sample Usage**:
  ```
  [tone-cluster: Harsh piano clusters for eerie suspense.]
  ```
- **Genre-Based Usage**:
  - **Avant-Garde & Experimental**: Chaotic tone clusters create **unpredictable tension**.
  - **Horror & Cinematic**: Sustained clusters add **mystery and unease**.
  - **Jazz & Free Improvisation**: Soft, shifting clusters add **expressive complexity**.
  - **Ambient & Drone**: Minimal clusters blend with **soundscapes**.

### **Track Structure Recommendation**
- **[intro: Soft, minimal clusters in synth pads]**
- **[verse: Sparse dissonant clusters in background]**
- **[chorus: Harsh, chaotic piano clusters]**
- **[bridge: Sustained, evolving clusters in brass]**
- **[outro: Fading tone clusters merging into silence]**

---

## [transition]
- **Meaning**: Defines how **sections of the track connect**, shaping smooth or dramatic changes.
- **Placement**: Typically used **within [structure], [tempo], or [dynamics]**, influencing movement between parts.
- **Accepted Parameters**:
  - **smooth** - Gradual shift between sections.
  - **abrupt** - Sudden, sharp transition.
  - **modulated** - Key or harmonic shift to a new section.
  - **filtered** - Using effects (filters, sweeps) to blend sections.
- **Sample Usage**:
  ```
  [transition: Smooth modulation from minor to major in the chorus.]
  ```
- **Genre-Based Usage**:
  - **Pop & Rock**: **"Smooth" for natural verse-chorus flow.**
  - **Orchestral & Classical**: **"Modulated" for key changes.**
  - **Electronic & Dance**: **"Filtered" for filter sweeps and buildups.**
  - **Metal & Punk**: **"Abrupt" for sudden tempo and dynamic shifts.**

### **Track Structure Recommendation**
- **[transition: Smooth tempo shift between sections]**
- **[intro: Soft, gradual build-up]**
- **[verse: Relaxed tempo with warm textures]**
- **[chorus: Slightly faster, modulated key change]**
- **[outro: Slow fading with harmonic resolution]**

---

## [tremolo]
- **Meaning**: Defines **a rapid repetition of a note or oscillation in pitch** to create intensity, tension, or vibrato effects.
- **Placement**: Typically used **within [harmony] or [dynamics]** to specify expressive playing techniques.
- **Accepted Parameters**:
  - **soft** - Light tremolo, subtle and delicate.
  - **dramatic** - Strong, high-intensity tremolo.
  - **orchestral** - Used in strings or brass for cinematic impact.
  - **electronic** - Tremolo applied to synths or effects.
- **Sample Usage**:
  ```
  [tremolo: Dramatic orchestral strings leading into the climax.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: **"Orchestral" for dramatic swelling tension.**
  - **Jazz & Blues**: **"Soft" for expressive guitar or organ tremolo.**
  - **Electronic & Cinematic**: **"Electronic" for synth tremolo effects.**
  - **Metal & Industrial**: **"Dramatic" for intense, fast-picked guitar tremolo.**

### **Track Structure Recommendation**
- **[intro: Soft tremolo strings creating tension]**
- **[verse: Light tremolo piano motif as background texture]**
- **[chorus: Dramatic tremolo in brass leading to climax]**
- **[outro: Slow, fading tremolo on solo violin]**

---

## [trio]
- **Meaning**: Specifies a **three-part instrumental or vocal arrangement**, commonly used in classical music but applicable to modern settings.
- **Placement**: Typically used **within [ensemble], [harmony], or [vocals]** to define the arrangement of performers.
- **Accepted Parameters**:
  - **classical** - Traditional trio structure (e.g., piano, violin, cello).
  - **jazz** - Trio setup with piano, bass, and drums.
  - **rock** - Guitar, bass, and drums as a power trio.
  - **vocal** - Three-part harmony or choral trio.
- **Sample Usage**:
  ```
  [trio: Jazz trio with improvisational piano and upright bass.]
  ```
- **Genre-Based Usage**:
  - **Classical & Chamber Music**: **"Classical" for structured trio compositions.**
  - **Jazz & Fusion**: **"Jazz" for improvisation-driven trio setups.**
  - **Rock & Blues**: **"Rock" for guitar-driven power trios.**
  - **A Cappella & Choral**: **"Vocal" for three-part harmony sections.**

### **Track Structure Recommendation**
- **[trio: Classical trio with piano, violin, and cello]**
- **[intro: Gentle interplay between violin and piano]**
- **[verse: Cello introduces the main melodic line]**
- **[chorus: All instruments harmonizing in counterpoint]**
- **[outro: Soft fade-out with solo piano coda]**

---

## [variation]
- **Meaning**: Specifies **a modified version of a previous musical section**, used to develop and evolve themes.
- **Placement**: Typically used **within [theme] or [structure]** to guide motif transformations.
- **Accepted Parameters**:
  - **melodic** - Variation in melody while retaining the harmonic framework.
  - **harmonic** - Chordal shifts or reharmonization.
  - **rhythmic** - Altered timing or syncopation.
  - **instrumental** - Changing the instrumentation or arrangement.
- **Sample Usage**:
  ```
  [variation: Melodic transformation with syncopated rhythm.]
  ```
- **Genre-Based Usage**:
  - **Classical & Orchestral**: **"Melodic" for theme development.**
  - **Jazz & Improvisation**: **"Harmonic" for chord substitutions.**
  - **Electronic & Sound Design**: **"Rhythmic" for glitch-like re-interpretations.**
  - **Rock & Metal**: **"Instrumental" for dynamic lead guitar alterations.**

### **Track Structure Recommendation**
- **[variation: Melodic shift with added orchestration]**
- **[intro: Theme introduced by solo piano]**
- **[verse: Standard harmonic progression]**
- **[chorus: Variation with richer orchestration]**
- **[outro: Final transformation with rhythmic complexity]**

---

## [vibe]
- **Meaning**: Defines the **general feel, groove, and aesthetic** of the track, guiding mood and instrumentation.
- **Placement**: Typically used **before [mood] or [style]**, influencing the overall musical atmosphere.
- **Accepted Parameters**:
  - **chill** - Relaxed, laid-back energy.
  - **energetic** - High-intensity, driving feel.
  - **dark** - Mysterious or ominous atmosphere.
  - **uplifting** - Positive, feel-good energy.
- **Sample Usage**:
  ```
  [vibe: Dark, moody synths with hypnotic drum grooves.]
  ```
- **Genre-Based Usage**:
  - **Lo-Fi & Chillwave**: **"Chill" for relaxed, nostalgic tones.**
  - **Dance & House**: **"Energetic" for high-BPM movement.**
  - **Gothic & Industrial**: **"Dark" for eerie, brooding production.**
  - **Pop & Acoustic**: **"Uplifting" for feel-good songwriting.**

### **Track Structure Recommendation**
- **[vibe: Chill and nostalgic, evoking sunset imagery]**
- **[intro: Warm synth pads and subtle vinyl crackles]**
- **[verse: Soft, reverb-drenched vocal phrases]**
- **[chorus: Laid-back groove with jazzy chords]**
- **[outro: Slow fade into ambient echoes]**


---

## [vocalist]

**Category:** Vocal role / character tag  
**Primary use:** To describe the main singer’s character, range, or style without tying it to a specific real‑world artist.

**Behavior and intent**  
`[vocalist]` lets you specify who is “front and center” in stylistic terms: gender expression, timbre, age impression, and general vibe. It is more about describing the *role* and *tone* than about structure.

**Placement and syntax**  

- *Lyrics field:*  
  - At the top of the track, or before the first sung section:  
    - `[vocalist | soft female voice, indie folk tone]`  
    - `[vocalist | relaxed baritone, storyteller style]`  
- *Style of Music field:*  
  - “old‑vinyl hip-hop with a mellow male vocalist and distant harmonies”

**Typical use-cases**  

- Clarifying who should lead when you also have choirs, narrators, or duets  
- Indicating age/vibe (“teen pop vocalist”, “mature jazz vocalist”)  
- Steering the vocal tone when Personas are not used, or when you want to override them gently

Pair `[vocalist]` with one or two precise adjectives (warm, raspy, bright, fragile) rather than long backstories.

---

## [vocal-style]
- **Meaning**: Suggests **vocal performance character** — texture, mood, or technique. 
- **Placement**:
  - Use within `[vocals:]` OR inline with `[verse:]`, `[chorus:]`, etc.
  - Most effective in **emotionally charged or stylized genres**.
- **Accepted Parameters**:
  - **`whispered`, `spoken`, `sung`, `breathy`, `shouted`** - Delivery mode
  - **`soaring`, `broken`, `glitchy`, `layered`, `ghostly`, `robotic`** - Style texture
  - **`emotive`, `detached`, `playful`, `dramatic`** - Expressive state
  - **`baroque`, `jazz`, `scat`, `operatic`, `crooning`** - Style genre overlays
- **Sample Usage**:
  ```
  [verse: Breathy whispers deliver surreal lyrics over minimal synth.]
  [vocal-style: whispered, ghostly, detached]
  ```
- **Genre-Based Usage**:
  - **Art pop, cabaret**: theatrical styles like `operatic`, `crooning`.
  - **Jazz/funk**: `scat`, `playful`, `layered`.
  - **Industrial/electronic**: `robotic`, `glitchy`, `detached`.

---

## [voicing]
- **Meaning**: Defines **how notes are distributed across instruments or voices**, affecting **chord texture and balance**.
- **Placement**: Typically used within `[harmony]`, `[orchestration]`, or `[mixing]`.
- **Accepted Parameters**:
  - **open** - Notes are spread out over a large range.
  - **close** - Notes are clustered closely together.
  - **spread** - Wide-range voicings, often used in orchestral settings.
  - **tight** - Compact chord formations.
  - **inverted** - The bass note is moved above.
- **Sample Usage**:
  ```
  [voicing: Open brass harmonies spread across the stereo field.]
  ```
- **Genre-Based Usage**:
  - **Classical & Jazz**: Open voicings create **rich harmonic textures**.
  - **Rock & Metal**: Tight power chord voicings enhance **impact**.
  - **Pop & R&B**: Inverted voicings create **smooth transitions**.
  - **Electronic & Ambient**: Spread voicings enhance **stereo width**.

### **Track Structure Recommendation**
- **[intro: Close voicing for intimacy]**
- **[verse: Inverted harmonies for subtle movement]**
- **[chorus: Open, wide voicings for full sound]**
- **[bridge: Spread-out orchestration to increase depth]**
- **[outro: Gentle, fading harmonic inversions]**

---

## [vulnerable vocals]

**Category:** Vocal emotion / tone tag  
**Primary use:** To shape the emotional quality of the voice toward fragility, intimacy, and emotional openness rather than power or polish.

**Behavior and intent**  
`[vulnerable vocals]` invites a softer, more exposed delivery: less belting, more breath, slight shakiness or tenderness, and a sense of emotional honesty. It can apply to quiet moments in otherwise big productions.

**Placement and syntax**  

- *Lyrics field:*  
  - At the start of emotionally raw sections:  
    - `[verse | vulnerable vocals, soft, nearly breaking]`  
    - `[bridge | vulnerable vocals, confessional tone]`  
- *Style of Music field:*  
  - “indie ballad with vulnerable vocals and sparse piano accompaniment”

**Typical use-cases**  

- Confessional verses revealing inner thoughts  
- Stripped-down intros or outros before/after big choruses  
- Tracks centered around heartbreak, doubt, nostalgia, or quiet hope

For more control, pair `[vulnerable vocals]` with dynamic cues like “low volume”, “close to the mic”, “minimal reverb” or with arrangement hints (“just piano and voice”).

---

## [whisper]

**Category:** Vocal delivery / FX tag  
**Primary use:** To request whisper‑like vocal delivery or subtle whispered layers.

**Behavior and intent**  
`[whisper]` suggests that the main vocal line in that spot is delivered softly and breathily, close to a whisper. Depending on context, Suno may treat it as:
- fully whispered lead, or  
- a hushed, intimate tone with extra breath and less power.

**Placement and syntax**  

- *Lyrics field:*  
  - As a local delivery tag:  
    - `[whisper] the secrets only night can hear`  
    - `[verse | whisper, intimate, close-mic]`  
- *Style of Music field:*  
  - “dark ambient pop with whispered verses over sparse piano”

**Typical use-cases**  

- Intimate or ASMR‑like sections  
- Tension-building passages before a loud chorus / drop  
- Horror / thriller aesthetics with eerie whispers under the main mix

Avoid stacking too many conflicting vocal style tags (e.g., `[whisper]` + `[shouted vocals]` on the same line). Use one primary delivery style per section.

---

## [whispering]

**Category:** Vocal texture / background atmosphere tag  
**Primary use:** To add a continuous or background layer of whispered phrases, often more textural than a clear lead.

**Behavior and intent**  
Where `[whisper]` often focuses on the main vocal delivery, `[whispering]` hints at ongoing murmurs, background phrases, or crowd‑like whisper textures. It works particularly well in atmospheric, horror, or experimental contexts.

**Placement and syntax**  

- *Lyrics field:*  
  - As a background / texture cue, often in brackets or side-notes:  
    - `[whispering voices in the background, unintelligible, eerie]`  
    - `[chorus | main vocal strong, subtle whispering doubles underneath]`  
- *Style of Music field:*  
  - “cinematic dark ambient with constant whispering textures and distant choir pads”

**Typical use-cases**  

- Horror, thriller, or ritual scenes where whispers form a sonic “fog”  
- Contrast between clear lead and ghostly whisper layers  
- Experimental or sound‑design‑heavy compositions

Use short descriptions of what the whispers feel like (“crowd of voices”, “one close voice”, “distant and echoing”) instead of long narrative sentences.

---

## [X solo] : Supported Instrument Solo Tags

| Tag | Notes |
|-----|-------|
| `[guitar solo]` | Electric/acoustic guitar melody |
| `[sax solo]` | Funk, jazz, noir |
| `[violin solo]` | Classical/ambient/baroque |
| `[piano solo]` | Lounge, ambient, ballads |
| `[flute solo]` | Ambient, fantasy |
| `[drum solo]` | Jazz, phonk, rock |
| `[synth solo]` | Synthwave, EDM |

- **Sample Usage**:
  ```
  [guitar solo: electric phaser riff overlays chorus chord structure]
  [violin solo: emotional vibrato lines with echo]
  [sax solo: jazzy improvisation with glissandos]
  [piano solo: baroque-style broken arpeggios]
  ```
