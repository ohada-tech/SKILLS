---
name: analyze
description: Deep-analyzes a short-form video (Instagram Reel, TikTok, YouTube Short) or a whole creator account the way Sandcastles' /analyze does — transcript, stats, idea, topic, format, hook, storytelling structure, visual layout, editing and why it performs. Use when the user drops a video URL, Drive link or file and says analyze, break down, "תנתח", "פרק לי", or asks why a video or creator is working.
---

# Analyze

## Goal

Turn one video (or a creator's recent videos) into a breakdown someone can copy from: what was said, what was shown, how it was cut, and why it holds attention. Every claim must trace back to a frame, a transcript line or a stat you actually have.

## Never fake the video

If you could not get the video, say so and name the blocker (host denied, login required, file is not a video). Do not describe a video from its URL, title or caption alone. A caption-only or frames-only analysis is allowed but must be labelled as such at the top.

## 1. Get the video — first route that works wins

1. **Sandcastles connector** — if `sandcastles` tools are connected, call its analyze tool with the URL. It fetches on its own servers and returns transcript and stats. Use its output as the evidence base and still run sections 3–5 on top.
2. **Direct download** — `yt-dlp` the URL into a fresh empty directory. If the `watch-editor` skill is installed, run its `watch.py` instead: it does download, scene-change frames, pacing metrics and the 0–10s hook pass in one go.
3. **Google Drive link** — get metadata first. If the mime type is `video/*`, download it with the Drive connector (base64 → decode to `.mp4`). If it is something else (a PDF, a doc), tell the user what it actually is and read it if relevant — do not treat it as the video.
4. **Ask for the file** — if all of the above fail, ask the user to upload the `.mp4`. In a cloud session, a proxy 403 on the host is an environment network policy; tell them which domains to allow (Instagram needs `instagram.com` and `cdninstagram.com`).

## 2. Extract evidence

Without `watch-editor`, do it with ffmpeg:

- **Duration, resolution, fps:** `ffprobe`.
- **Shot frames:** scene-change frames (`select='gt(scene,0.3)'`), plus one frame every ~1s if fewer than 8 shots were found. 512px wide is enough unless on-screen text must be read.
- **Hook frames:** 0–3s at 4 fps, 3–10s at 2 fps.
- **Pacing:** number of cuts, cuts per minute, mean and shortest shot length.
- **Transcript:** native captions → Whisper key (`GROQ_API_KEY` / `OPENAI_API_KEY`) → ElevenLabs `creative_transcribe_audio` → KIE `speech_to_text`. Keep timestamps. Transcription through a paid connector spends credits — say which one you used.
- **Stats:** views, likes, comments, shares, posting date, follower count — only if a source returned them. Never estimate.

Read every frame before writing anything.

## 3. The breakdown

Fill each section, citing timestamps (`0:03`). Skip a section only when there is no evidence for it, and say so.

| Section | What to answer |
|---|---|
| **Stats** | Raw numbers and, when the account's other videos are known, how this one compares (e.g. 4.2× the account median). |
| **Idea** | The one-sentence promise of the video. What does the viewer get? |
| **Topic** | Subject and niche; is it evergreen, trending or news-pegged? |
| **Format** | Talking head, green screen, voiceover + B-roll, tutorial/screen recording, skit, listicle, before/after, POV, interview, etc. Name it in two or three words. |
| **Hook** | Split into *spoken* (first sentence verbatim), *visual* (what moves or changes in 0–2s), and *text on screen*. Name the pattern: question, contrarian claim, result-first, in-medias-res, curiosity gap, callout ("If you're a…"), proof/demo first, negative ("Stop doing…"). Say when the viewer learns what the video is about. |
| **Storytelling structure** | Beats with timestamps: hook → setup → tension/problem → payoff → CTA. Note open loops and where they close. |
| **Visual layout** | Framing (face size, position), captions (style, words per line, placement), B-roll vs A-roll ratio, overlays, graphics, colour. |
| **Editing and pacing** | Cuts per minute, mean shot length, pattern interrupts (zooms, sound effects, angle changes), how the pace changes across the video. |
| **Audio** | Voice delivery (speed, energy), music or trending sound, sound effects. |
| **CTA** | What the viewer is asked to do (comment a keyword, follow, link in bio) and at what timestamp. |

## 4. Why it works

Three to five reasons, each tied to evidence. Good reasons name a mechanism ("the result is shown at 0:01 before any explanation, so the curiosity gap opens instantly"), not adjectives ("engaging", "high quality"). Also list one or two weaknesses or things that would likely lift retention.

## 5. Make it reusable

End with a **template** the user can shoot from:

```text
HOOK (0–2s):    [pattern] — "<fill-in line>" + [visual action]
SETUP (2–6s):   …
BODY:           [n] beats, ~[x]s each, cut every ~[y]s
PAYOFF:         …
CTA:            …
```

If the user has a brand or client in context, add two or three hook lines adapted to it.

## Creator mode

When given an account instead of a video ("analyze @username"):

1. Collect the last ~3 months of videos with whatever source works (Sandcastles connector, `yt-dlp` on the profile URL, or a list the user supplies).
2. Rank by views (or views ÷ follower count) and pick the top 7–8 against the field.
3. Run sections 2–3 on each top video, lighter for the rest.
4. Report patterns that separate the top from the field: topics, formats, hook patterns, length, pacing, posting cadence. Use a chart when comparing more than five videos.

## Output

- One video: answer in chat with the breakdown, then offer a shareable page.
- Creator report or anything meant for a team: publish it as a page with the frames and charts inside.
- Keep quotes verbatim and in the original language; translate in brackets if the user writes in a different language.
- Delete downloaded videos and frames from the scratch directory when the user is done.
