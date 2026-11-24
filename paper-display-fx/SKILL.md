---
name: paper-display-fx
description: Design and implement animated Minecraft Paper BlockDisplay models, procedural particles and spatial vanilla sound cues for gadgets, machines, structures and rituals.
---

# Paper display animation and effects

Start from the action a player should recognize at a distance. Keep its silhouette readable with particles off. Inspect the project's gameplay clock, display helpers, target API and viewer preferences before choosing parts or effects. Load the linked reference for the decision at hand.

| Phase | Working decision |
|---|---|
| A · Visual brief | Name the first readable shape, the moving feature that explains its purpose, the material carrying its weight and the accent that signals activity. |
| B · Decompose | Sketch fixed parts, joints, sliders, emitters and interaction points. Budget independent motion before subdividing decorative surfaces. See [articulated models](references/articulated-models.md). |
| C · Transforms | Declare axes and anchor, then compose from the rest pose. Use [coordinate systems](references/coordinate-systems.md) for mounts and [display transforms](references/blockdisplay-transformations.md) for centered cubes and hinges. |
| D · States | Give each transition a trigger, age, permitted interruption and exit. Drive poses and one-shot cues from the authoritative action. See [interpolation](references/animation-interpolation.md). |
| E · Effects | Choose a [procedural path](references/procedural-geometry.md), [particle envelope](references/particle-systems.md) and [spatial sound score](references/sound-design.md). For thick directed effects, share the [resolved volume](references/volumetric-vfx.md) with gameplay. |
| F · Implement | Keep model definitions, mutable assembly state and game decisions distinct. Spawn reusable parts once. Transform attachment points through the same parents as the parts they follow. |
| G · Budget | Assign an owner, update cadence, viewer policy and teardown to each entity and effect. See [performance and lifecycle](references/performance-and-lifecycle.md). |
| H · Validate | Check basis axes, pivots, timing, interruption, simultaneous devices and empty audiences. Use the [validation guide](references/testing-and-validation.md). |
| I · Deliver | When implementing, provide complete relevant sources, actual build results, observed behavior and checks that still require a client. Keep changes within the requested visual or gameplay scope. |

Choose one source pattern when applicable: [turret](patterns/aegis-turret.md), [glider](patterns/mechanical-glider.md), [wire containment](patterns/nanowire-containment.md), [sensor](patterns/sonic-sensor.md), or [propulsion](patterns/propulsion-effects.md). Original worked designs cover a [survey sentry](examples/articulated-sentry.md), [folding wings](examples/animated-mechanical-wings.md), and [energy structure](examples/procedural-energy-structure.md).

[Source evidence](methodology.md) · [Installation](installation.md) · [Package validation](validation-report.md)
