---
name: paper-display-fx
description: Design and implement animated Minecraft Paper BlockDisplay models, procedural particles, and spatial vanilla sound cues for gadgets, machines, structures, and rituals.
---

# Paper display animation and effects

Start with what a nearby player needs to recognize. Pick a silhouette, a structural material, and an energy accent. Give moving parts a visible reason to move. Read the project's display helpers, effect budgets, gameplay clock, and target Paper version before choosing APIs. In SkillsSMP, start with MechanicalArt and FxService.

## Pose the assembly

- Sketch a pivot hierarchy in model space. For a turret, the base owns yaw, the cradle adds pitch, and the barrel recoils along its local bore. For paired wings, mirror the hinge locations and fold directions. Store a rest pose per part and compose each update from it to prevent drift.
- Choose one forward axis. A unit BlockDisplay starts at a corner. For desired center `c`, rotation `R`, and dimensions `s`, use `translation = c - R(s / 2)` with identity right rotation. For a beam, put the center halfway between its endpoints and scale its forward dimension to their distance. Guard zero-length segments.
- Spawn parts once. Interpolate moving transforms between server samples, reset interpolation delay on each new target pose, and leave fixed parts alone. Derive emitters, trails, and interaction cues from the same transformed attachment points. Displays provide visuals; use the project's actual hitboxes and collision results for gameplay.

## Score the action

- Tie visual and sound cues to elapsed ticks in the existing action. At rest, use sparse motion and quiet accents. Build anticipation with a readable change in pose, color, or pitch. Put the strongest flash and transient at the moment of contact, then show recoil, cooling, or dissipation. Fire one-shot cues on state entry.
- Give particles a path. Move a pulse down a conduit, sample a ring around a pivot, or emit paired trails from wing tips. Build the shape in local coordinates and rotate it with the model. For directional effects, use the resolved endpoint and clip the visible effect to cover when gameplay does.
- Place sounds at their physical source. A latch clicks at its hinge, a charge rises at the core, and the impact sounds where it lands. Reserve low-frequency weight for major beats. Audition overlapping devices for loudness and repetition. Verify sound keys and particle data types against the target API.

## Budget and finish

Keep world and entity updates on the appropriate server thread. Reduce particle samples and pose updates with distance. Preserve essential silhouettes and gameplay timing for players with cosmetic effects disabled. Give each assembly ownership of its parts, temporary effects, and cleanup. Release them on completion, interruption, chunk unload, and disable. Rebuild persistent assemblies from authoritative state.

Compile against the project's actual Paper dependency. For an in-game review, inspect the silhouette from above and at eye level, watch diagonal and vertical movement, listen through a complete cycle, and check cleanup after interruption. Report which checks were performed.
