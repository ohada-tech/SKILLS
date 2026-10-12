---
name: blocking-map-builder
description: Builds precise blocking maps for people, props, counts, spatial anchors, and camera viewpoints. Use when AI video shifts seats, duplicates objects, or struggles with overhead/reverse angles.
---

# Blocking Map Builder

## Goal

Remove spatial ambiguity before video generation. Produce a clear map of people, props, and camera position, then convert it into language the video model can follow.

## Inputs to identify

- location/reference image and intended camera view
- all characters and their IDs
- chairs/seats, tables, plates, phones, products, and other props
- intended action and dialogue
- beginning/end state of objects
- camera viewpoint and movement
- exact counts that must be preserved

If the user has not supplied a visual, make a text-based top-down map first and clearly label any assumptions. Do not fabricate that a visual map file has been created when you have only provided text.

## 1. Establish coordinate language

Use both screen relationships and fixed environmental anchors:
- screen-left / center / screen-right from the specified camera viewpoint
- foreground / middle distance / background
- beside / opposite / behind / in front of
- named anchors such as window, lamp, bookcase, doorway, or building edge

Do not use “left” without stating whose viewpoint defines left. For reverse angles, re-state what appears in front of and behind the camera.

## 2. Build the blocking layout

Start with a top-down map such as:

```text
                    BACK WALL
      [Window]                         [Bookcase]

   A: Micah / seat 1      TABLE      B: Alex / seat 2
                          phone
                 plate A  plate B  plate C
   C: Jenny / seat 3

                 CAMERA (overhead)
```

Replace the example with the actual scene. Give every character and important prop a stable ID. For each, define:
- position/seat
- body orientation and gaze direction
- relationship to nearby objects
- action and timing
- state before and after the action

For a color-coded map, provide a legend in plain text (e.g., orange = Jenny, blue = Alex, green = Micah). Always also name the corresponding characters in the prompt; color alone is not enough.

## 3. Count and validate

Create an exact inventory for the shot, for example:
- 3 people: Micah right, Alex top, Jenny left
- 3 individual plates, 2 shared bowls
- 1 phone face-down beside Jenny
- no fourth seat, no extra plate, no duplicate phone

Check that every object mentioned in the action is present in the map and that the map contains no object the brief does not allow.

## 4. Map the camera

For every shot, record:
- camera start position and viewing direction
- camera height/angle (overhead, eye-level, low, reverse, etc.)
- movement path and direction
- what is foreground/midground/background during movement
- clearance around heads, hands, and props
- any landmark that should remain visible

For reverse angles, write a camera-centric description, not merely “move behind the musicians.” Explain where the camera is located, what object is near the camera, what the subjects are beyond, and what is in the far background.

## 5. Translate the map into a video prompt

Use this pattern:

1. Attach the blocking map and the character/location master references.
2. State what the map controls (positions/counts); state what the photos control (identity, environment, lighting).
3. Map IDs or colors to named characters.
4. Describe one action at a time and its order.
5. State what remains fixed while the camera moves.
6. Name exact exclusions: no extra people/seats/plates/phones, no object switching sides.
7. Describe the desired start and end states.

Example:

```text
Use the attached layout map for seating and object placement. Green is Micah on screen-right beside the window; blue is Alex at the far side of the table; orange is Jenny on screen-left beside the bookcase. There are exactly three characters and three individual plates. The phone stays face-down beside Jenny throughout this shot. The camera starts overhead and rotates smoothly clockwise without changing anyone's seat or moving the plates. Leave clearance around all three heads. Do not add another chair, person, plate, or phone.
```

## 6. Failure diagnosis

If a take is wrong, classify the fault:
- seat/position drift
- object count error
- handoff/state error
- camera viewpoint ambiguity
- background/foreground inversion
- insufficient clearance for camera movement
- reference mismatch

Then update only the relevant part of the map or prompt. Preserve correct actions, identity, lighting, and timing. If seat drift occurs across close-ups, add a short wide establishing shot to anchor the layout before close-ups.

## Output format

1. assumed/confirmed scene inventory
2. top-down ASCII/text map
3. color legend and object counts
4. camera map for each requested angle
5. ready-to-use video prompt
6. exclusion constraints
7. validation checklist

## Boundaries

Do not spend credits, create external assets, or overwrite source maps without approval. If the layout cannot be inferred reliably from the references, call out the ambiguity and ask for clarification rather than making up spatial facts.
