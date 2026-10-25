# Voice directions

Use these bracket tags in the script. They are plain text, so any TTS tool or voice agent can read past them or map them.

| Tag | Meaning |
| --- | --- |
| `[pause]` | A short pause, about half a second. |
| `[long pause]` | A pause of about one second, before a new segment. |
| `[warm]` | A friendly tone, for the intro and the sign-off. |
| `[upbeat]` | More energy, for a big number or a launch. |
| `[measured]` | Slower and calm, for a serious or uncertain item. |
| `[emphasis: word]` | Stress this word. |
| `[laughs]` | A light laugh. Use at most once per episode. |
| `[music in]`, `[music out]` | Intro and outro music cues for the editor. |

Speaker labels go at the start of the line: `HOST A:` and `HOST B:`. For a spoken briefing use `VOICE:`.

## Map to a TTS service

Many services accept SSML, the W3C Speech Synthesis Markup Language. This is a standard SSML mapping:

| Tag | SSML |
| --- | --- |
| `[pause]` | `<break time="500ms"/>` |
| `[long pause]` | `<break time="1s"/>` |
| `[emphasis: word]` | `<emphasis level="moderate">word</emphasis>` |
| `[measured]` | `<prosody rate="slow">...</prosody>` |
| `[upbeat]` | `<prosody rate="medium" pitch="+2st">...</prosody>` |
| `[warm]`, `[laughs]`, `[music in]`, `[music out]` | No SSML equivalent. Remove the tag, or keep it as a note for the editor. |

Services support different parts of SSML, and some use their own tags. Check the service's current documentation before you convert. If you are not sure, keep the bracket tags and give the user both tables.

## Pronunciation

Add a pronunciation note for any name that a voice can get wrong. Example: `Legora (leh-GOR-ah)`. Put the notes at the top of the script.
