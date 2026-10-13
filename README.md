# Skills

Claude skills for AI video and motion-graphics pre-production. Each skill lives in `skills/<name>/SKILL.md`.

| Skill | Use it for |
|---|---|
| [`ai-video-director`](skills/ai-video-director/SKILL.md) | Turning a brief into a script, shot list, camera directions, per-shot prompts, transitions and QC for AI commercials, cinematic clips and social videos. |
| [`ai-video-continuity-bible`](skills/ai-video-continuity-bible/SKILL.md) | Building consistent character, location, prop, product and brand references before multi-shot generation. |
| [`blocking-map-builder`](skills/blocking-map-builder/SKILL.md) | Locking seats, props, object counts and camera viewpoints when AI video drifts or duplicates objects. |
| [`motion-graphics-director`](skills/motion-graphics-director/SKILL.md) | Planning editable motion graphics: kinetic typography, explainers, diagrams, UI/product animations and data visuals. Includes 853 reference prompts for code-built animations. |
| [`analyze`](skills/analyze/SKILL.md) | Breaking down a Reel, TikTok, Short or a whole creator account: transcript, hook, format, story structure, visual layout, pacing, why it works, and a reusable template. |

## How they fit together

1. **ai-video-director** plans the piece and calls out which shots need continuity or blocking work.
2. **ai-video-continuity-bible** defines the recurring assets and their stable IDs.
3. **blocking-map-builder** pins down spatial layout for multi-person or multi-prop shots.
4. **motion-graphics-director** covers graphic, typographic and code-driven sequences.

## Installing

Copy a skill folder into `~/.claude/skills/` (personal) or `.claude/skills/` in a project, or zip the folder and upload it in Claude's Skills settings.
