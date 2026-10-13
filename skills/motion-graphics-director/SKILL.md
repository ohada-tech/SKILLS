---
name: motion-graphics-director
description: Turns a message or script into an editable motion-graphics plan or code animation spec. Use for kinetic typography, explainers, diagrams, UI/product animations, and data visuals.
---

# Motion Graphics Director

## Role

Translate an idea into a motion system that can be built, reviewed, and edited. Treat text, labels, illustrations, charts, masks, and camera movement as planned elements—not as decorative effects added at random.

## 1. Define the assignment

Extract:
- message and audience
- desired length, aspect ratio, and delivery platform
- source material, data, brand assets, and exact wording
- intended look (clean, technical, editorial, cinematic, playful, etc.)
- audio/voice/music and whether movement must sync to a beat
- required output: storyboard/specification, HTML/SVG/code animation, or instructions for an existing editor

If an existing project/repository is available, inspect its structure and use its current framework before introducing new dependencies. If no execution target is defined and the user needs a runnable preview, propose a simple self-contained implementation and label that assumption.

## 2. Choose visual techniques intentionally

Possible techniques:
- kinetic typography for a key phrase or number
- technical drawing, grids, diagrams, and line reveals for explanation
- pseudo-3D layering/parallax for depth
- continuous camera/one-shot feel to connect related elements
- match cuts and shape transitions between scenes
- beat-synced entrances and exits
- cinematic lighting/texture only where it supports the purpose

Use a small set of techniques that reinforce the idea. Do not make every object move at once. At any moment, the viewer should know where to look.

### Reference prompts

`references/opus-5-5-prompts/videos.json` contains 853 prompts that produced code-built animations (see its `README.md` for the fields). When the deliverable is code (HTML/Canvas/SVG/Three.js), search the file for prompts that match the category and stack, and use them to see how others phrased length, style and constraints. Example:

```bash
python3 -c "import json,sys; [print(v['post_url'], '|', v['prompt'][:200].replace('\n',' ')) for v in json.load(open(sys.argv[1])) if v['category']==sys.argv[2] and sys.argv[3] in v['tech_tags']]" references/opus-5-5-prompts/videos.json explainer svg
```

Use these prompts as reference only. Credit the creator if you reuse one closely. Records with `prompt_partial: true` contain only part of the original prompt.

## 3. Separate assets from editable graphics

When images are required, generate or request clean source assets first:
- separate illustration elements where practical
- use transparent-background assets for objects that must be layered
- keep text, labels, diagrams, and important brand typography out of generated images when they need to remain editable
- preserve source assets and record their filenames

Claude/code should then build the graphic system around those assets: labels, lines, highlights, motion, masks, hierarchy, camera moves, and transitions.

## 4. Build the animation specification

Create a scene-by-scene timing plan. Use a table like:

| Time | Scene/message | Visible elements/layers | Motion | Camera/focus | Text/audio | Transition | Editability check |
|---|---|---|---|---|---|---|---|

For each element, define:
- layer/ID and source asset
- starting position/scale/opacity
- entrance, hold, and exit timing
- easing or motion character, when appropriate
- relationship to other elements
- whether it moves with the camera or stays in screen space
- how it remains editable after export

Give camera movements a narrative function. Example: begin with the complete illustration, push toward a relevant detail, introduce a magnified inset and connecting lines, animate one moving highlight, then pull back to the complete composition.

## 5. Direct focus and pacing

- Keep the background visually quiet when a detail is being explained.
- Reveal labels when needed, not all at the opening frame.
- Use the camera to connect “big picture” to “detail” or to guide the eye through a process.
- Avoid simultaneous movement that creates competing focal points.
- If music is supplied, map important entrances to beats or accents; do not claim exact synchronization until checked against the actual track.
- Use transitions between scenes only when they help continuity or meaning.

## 6. Implementation guidance

Before coding, confirm or infer a concrete deliverable: existing animation editor, native project, HTML/SVG/Canvas, or another user-specified format. State assumptions.

When generating code:
1. create/modify files inside the selected project directory
2. preserve originals and avoid destructive overwrites
3. prefer native editable text and vector shapes for titles, labels, charts, and diagrams
4. keep timing, copy, colors, and positions easy to locate and change
5. comment major scene/layer blocks
6. render or run a preview when the environment supports it
7. verify the export opens and check that the promised elements remain editable

A screenshot of a timeline is not proof of editability. Where the output becomes outlines/shapes or a flattened video, disclose that limitation.

## 7. Review and iterate

Evaluate each pass against:
- message hierarchy
- legibility at intended display size
- pacing and duration
- hierarchy of movement
- camera path and scene continuity
- correctness of data, text, logo, and source assets
- editability and export quality

Fix one category at a time where feasible. If the logo is too early, change its timing without rebuilding the whole animation. Preserve all elements that already work.

## Default output

1. brief recap and assumptions
2. storyboard/concept
3. timed scene plan
4. asset list
5. layer and motion specification
6. implementation approach and files needed
7. QA checklist
8. known limitations / items that need human review

## Boundaries

Do not replace/overwrite source projects without approval. Do not install dependencies, upload assets, publish, or trigger paid services without explicit authorization. Check the accuracy of data and copy instead of assuming a visually polished animation is correct.
