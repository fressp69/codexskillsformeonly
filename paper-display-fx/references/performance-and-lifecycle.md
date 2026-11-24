# Budget the assembly and its audience separately

**OBSERVED.** AEGIS registers its physical parts through FxService and tracks short-lived beam parts separately. FxService caps registered displays, routed sounds and particles per viewer. MechanicalArt.part alone creates a nonpersistent tagged display; calling it does not enroll a component in that service. Wiretrap and sensor also use direct world particle bursts. Audit actual spawn paths before quoting a global cap.

| Lifecycle event | Ownership action |
|---|---|
| Activate or rebuild | Reserve budget, build into a local owner list, publish once by site/player ID. On partial failure remove everything acquired. |
| Sample active state | Update moving parts only; interpolate between samples. Gate cosmetic work on viewers. Preserve timings, hitboxes and visible physical silhouettes required for play. |
| Interrupt or replace | Invalidate the generation token first. Clear transient tracks, loop sounds and delayed callbacks. Restore gameplay state through its own controller. |
| Player leaves, dies or changes world | Detach wearer-bound rigs and clear cross-world endpoints. A fixed machine may remain active according to its owner policy. |
| Chunk unload / disable | Remove transient entities explicitly, release tickets/tasks, clear references. Keep durable identity, pose-driving state or absolute deadline only when recovery needs it. |
| Chunk or world returns | Ensure one active assembly per persisted ID, remove stale owned art, and rebuild from current logical state. Use idempotent close. |

**GENERALIZED.** Cost scales along several axes. Persistent parts cost tracked entities and client draw work; short-lived parts add spawn/remove packets. Particles cost roughly samples × viewers × update rate. More pose updates cost transform packets even when no particle is emitted. Long anchor offsets also need sufficient client culling bounds. For a large assembly split into independently visible regions. Reserve structural parts before optional shells, reduce distant samples across the whole shape, and cap total concurrent instances.

**RECOMMENDED measurement.** Count active handles, spawns/removals, transforms, particles and sounds sent per viewer, audience queries and remaining tasks. Compare idle/no-viewer, one active rig, overlapping devices and repeated unload/reload. Profile server tick time separately from client frame time at matching camera positions. Record server settings, clients and sample duration; a source count is not a measured performance ceiling.

Paper's ordinary synchronous scheduler is appropriate for world access on a conventional Paper server. Folia has region and entity ownership; schedule location-bound work on its region and moving-entity work through its entity scheduler. Handle entity retirement, pass immutable snapshots between regions and avoid direct cross-region reads. A metadata flag alone does not port a global tick loop. [Paper scheduling guidance](https://docs.papermc.io/paper/dev/folia-support/)
