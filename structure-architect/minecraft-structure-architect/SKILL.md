---
name: minecraft-structure-architect
description: Design and implement terrain-aware Minecraft world structures with procedural block geometry, walkable routes, persistent placement and optional animated displays. Use for monuments, buildings, arenas, underground facilities or landmarks where architecture and gameplay must agree.
---

# Minecraft structure architect

Build from a common plan that the terrain survey, block writer, decoration renderer and validation code can all inspect. Keep the architectural brief in player-scale units. A build should still communicate where to enter and what to do when particles are disabled.

| Phase | Decision and working output |
|---|---|
| A. Requirements | Record the purpose, theme, target server/API, approximate envelope, players or mobs using it, interaction reach, headroom, terrain edits allowed, lifespan, and budget for writes, chunks and entities. For an arena, include combat sightlines and escape routes. For a dungeon, include its route back to the surface. |
| B. Architecture | Draw a footprint and a section through the main route. Mark the origin, facing, floor levels, major masses, gateways, vertical transitions, focal point and swept extent of moving parts. Assign materials by architectural role. Use the [design principles](references/design-principles.md). |
| C. Geometry | Produce a pure coordinate-to-block-state plan plus named attachment points. Compose foundations, floors, walls, supports, roofs and trim in explicit priority order. Reserve walking and interaction volumes. See [geometry](references/geometry.md). |
| D. World integration | Survey the complete envelope and approaches, choose a support strategy, then preflight every planned change. Commit the site before activation and place in bounded batches. See [world generation](references/world-generation.md). |
| E. Decoration | Attach moving or fractional geometry to the finished architecture. Give transient effects a spatial source, cue and end condition. See [display entities](references/display-entities.md). |
| F. Refinement | Check the rasterized plan, routes, site transitions and lifecycle. Review from an approach, directly above and at the interaction point. Use the [validation guide](references/validation.md). |
| G. Delivery | Supply complete source, necessary configuration and migration, the coordinate convention, budget assumptions, actual build/check results and outstanding live checks. Identify permanent edits separately from disposable entities. |

For worked designs, use the [hilltop watchtower](examples/procedural-monument.md) or the [underground pump hall](examples/animated-structure.md). The [extraction report](methodology.md) distinguishes observed source behavior from transferable techniques and proposed improvements.
