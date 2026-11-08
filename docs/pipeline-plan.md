# Clipping pipeline plan, v0 (first target: CoD Warzone S1 campaign)

## Constraints from this campaign
- **Source is fixed and small.** One trailer and one developer briefing, both from the official content link. This is not stream ingestion.
- **Competition is on the same footage.** 29+ clippers are cutting the same few minutes, so the edge is angle variety, hooks and volume without near-duplicates.
- **Platforms and pay:** TikTok at $2.00 per 1,000 views (pays more, post first) and Instagram Reels at $1.50.
- **Speed:** about $3.3k was spent on day 1, so runway is roughly 10 days. Ship the MVP in 3-4 days and post by hand meanwhile.
- **Unknown until the brief is pasted:** clip length, required tags and disclosure, banned content, music rules, minimum views, review terms. These all feed `rules.json`.

## Who does what
| Step | AI / automation | You |
|---|---|---|
| Brief to rules | Claude turns the brief into `rules.json` | Paste the brief, confirm |
| Ingest | Hash and store sources | Download official files |
| Index | Transcript with word timestamps, scene cuts, loudness peaks, keyframes | - |
| Moment mining | Claude (text plus vision on keyframes) proposes 30-50 candidates with angle, hook options and a score | - |
| Selection | - | Pick about 10, edit hooks (review gate 1) |
| Render | 9:16 reframe, burned captions, hook overlay, zooms and freeze frames | - |
| Compliance | Rule checks plus a Claude review of frames and caption against `rules.json` | - |
| Final review | - | Watch and approve (review gate 2) |
| Post and submit | Draft captions and tags | Post by hand, submit on Content Rewards |
| Track | Merge views into the tracker; weekly report | Enter view counts (manual at first) |
| Learn | Feed the best and worst performers back into the mining prompt as examples | - |

## Angle templates (the differentiation for fixed footage)
1. **"X things you missed"**: freeze frame, zoom and circle on details in the trailer.
2. **Single change explained**: one feature or map change, with a text overlay and a developer-briefing quote.
3. **Developer quote with gameplay underneath**: the newsworthy line from the briefing, cut over trailer footage.
4. **Hot take / question hook**: "Is this the best Warzone map ever?", built to draw comments.
5. **Before/after comparison**: only if the brief allows outside footage.
6. **Commentary voiceover**: your voice is safest; check the brief before using an AI voice.

Avoid near-duplicates: keep a registry of used (time range, angle) pairs so no two posts reuse the same segment with the same angle.

## Architecture (local first)
```
sources/     official files (sha256-named)
index/       transcript.json, scenes.json, keyframes/*.jpg, loudness.json
candidates/  candidates.json (Claude output, scored)
renders/     clip_<id>.mp4 + caption.txt
db.sqlite    clips, posts, views, approvals, used_segments
rules.json   campaign rules (one per campaign)
```
- **Stack:** Python, ffmpeg, faster-whisper (local transcription), PySceneDetect, Claude API (bulk model for mining, stronger model for the final hook pass), SQLite.
- **Review UI:** a CLI and Markdown list first; a small local web page later.
- **Rendering:** ffmpeg with ASS subtitles; layout options are blurred-background letterbox or centre crop.
- **Pipeline stages are swappable adapters,** so GTA streamer VODs later only need a new ingest adapter and a chat-spike signal. The rest is reused.

## Milestones
- **M1 (day 1):** ingest and index the two sources into `index/`.
- **M2 (day 2):** Claude moment mining produces `candidates.json` and a review list.
- **M3 (day 3):** renderer turns selected candidates into postable MP4s with captions.
- **M4 (day 4):** compliance check, caption drafting, tracker and database integration.
- **Later:** performance feedback loop; GTA streamer-VOD adapter (by Nov 19); cloud workers once volume needs them.

## Not automated, on purpose (for now)
- **Posting:** platform APIs need app review, and automated posting from new accounts risks spam flags.
- **Content Rewards submission:** I don't know of a public API.
- **View collection:** manual entry until volume justifies scraping or APIs.

## Open questions
1. The brief's locked rules (paste them).
2. Your computer's OS and whether it has a GPU (sets transcription speed).
3. Will you record voiceovers yourself?
