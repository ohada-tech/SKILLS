---
name: ai-video-continuity-bible
description: Creates consistent character, location, prop, product, and brand references for AI video. Use before multi-shot ads or scenes where appearance, layout, or object placement must stay consistent.
---

# AI Video Continuity Bible

## Purpose

Prepare stable visual references and written constraints before generating video. The goal is to reduce drift in faces, wardrobe, layout, objects, lighting, and branding across shots.

## Intake

Review the brief and any supplied files. Identify:
- recurring characters
- locations and time-of-day changes
- props, products, packaging, UI screens, logos, and readable text
- shot angles that require continuity or reverse coverage
- details that must remain fixed versus details that may vary

If source references are missing, create a written specification and image-generation prompts; do not imply that images already exist.

## 1. Character Bible

For every recurring character, write:
- stable asset ID and version
- story role and personality cues
- age range and appearance description as supplied/approved
- hair, facial features, wardrobe layers, accessories, and distinctive markers
- expression/energy range
- master reference filename and what it controls
- details that must not change

### Character reference guidance

- Prefer a clean, low-distraction background when constructing the initial character sheet.
- Use a clear face portrait as the identity anchor; add front/back wardrobe views for clothing and proportions.
- Clearly state the purpose of each panel. Do not assume a video model will infer which panel defines the face versus the clothes.
- When a multi-panel sheet confuses identity, use a separate face reference and crop secondary panels to clothing/body details.
- For edits, specify the single requested change, then explicitly preserve face, hair, clothing, pose, lighting, skin texture, and composition as applicable.
- Avoid over-smoothed skin or harsh lighting when the brief calls for natural commercial realism; state desired skin texture and light quality.

## 2. Location Bible

For every location, define:
- stable asset ID and version
- geography/layout and usable space
- time of day and environmental conditions
- key light source, warmth/coolness, direction, contrast, and ambience
- camera-friendly angle (consider a three-quarter view when depth and camera movement matter)
- foreground/midground/background objects
- negative space needed for characters, products, hands, titles, or camera motion
- background anchors visible from each planned angle
- continuity elements to preserve during edits

Build the environment around the action. If a package must be placed on a table, leave room for it in the location reference. If a reverse angle is needed, define where the camera stands and what lies behind the subjects from that viewpoint.

### Local edit rule

When modifying a location, phrase the edit as:
1. change only the requested layout/detail
2. preserve light, texture, color grade, camera angle, and all unaffected objects
3. name what must become visible and what must no longer obstruct the frame

## 3. Props, Products, and Brand Assets

For each reusable object, define:
- ID, shape/material/color, scale, and master reference
- who handles it, which hand is used, and when it changes hands
- exact position/orientation at the beginning and end of a shot
- logo/label visibility requirements
- text/markings that must remain exact

Keep critical logos, app screens, and typography under explicit control. If generated image text cannot be trusted, keep text as a separate editable overlay or composite a verified brand asset during editing.

For a pack/product shot, define the first frame, camera move, moment when the product label becomes readable, final composition, and approximate duration.

## 4. Reference manifest

Return a manifest table:

| Asset ID | Type | Filename / availability | What it controls | Must remain consistent | Used in shots |
|---|---|---|---|---|---|

Use exact IDs in later prompts. If versions differ, explicitly mark the approved master version and avoid silently mixing versions.

Suggested filenames:
- `character_micah_master_v01.png`
- `location_apartment_master_v02.png`
- `prop_phone_master_v01.png`
- `product_packaging_master_v03.png`
- `blocking_table_top_v01.png`

## 5. Continuity checks

Before approving a prompt or take, verify:
- face, hair, wardrobe, accessories, and body proportions
- all characters in their assigned seats/positions
- correct number of people and objects
- prop ownership, hand, direction, and state
- background anchors from the correct camera angle
- lighting direction and color continuity
- room layout and product placement
- logo orientation and legibility

Flag unknowns instead of guessing. For complex scenes, recommend adding a wide establishing/keyframe shot and/or a blocking map before close-ups.

## Output

Return, in this order:
1. asset inventory
2. character bible
3. location bible
4. props/products and brand rules
5. reference manifest with exact IDs
6. continuity checklist per shot
7. prompts for missing references and local edits

## Boundaries

Do not overwrite approved master references without explicit instruction. Preserve originals and version edited copies. Do not invent brand assets or “correct” a logo from memory; ask for or use the supplied source file. Do not spend generation credits or upload assets to external services without approval.
