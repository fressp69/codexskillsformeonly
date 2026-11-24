# Survey, placement and recovery

**Observed surface policy.** AltarTerrain samples every column inside an expanded polygon, including an approach apron. WORLD_SURFACE exposes roofs, canopy and fluids. It descends through at most two approved plant cells, checks natural supporting material, three solid non-liquid cells below and three clear or light-cover cells above. Adjacent accepted feet levels may differ by one and the full range by three. The deck uses the highest feet level. The center's feet level remains available for the ritual anchor.

```java
// Paper 1.21.11, on the world-owning thread, after footprint chunks are available.
int top = world.getHighestBlockYAt(x, z, org.bukkit.HeightMap.WORLD_SURFACE);
org.bukkit.block.Block surface = world.getBlockAt(x, top, z);
// After validating this surface as full-height support:
int feetY = surface.getY() + 1;
int floorBlockY = deckFeetY - 1;
```

A heightmap is a candidate finder. Slabs, deep snow, tree cover, roofs and liquids need explicit decisions. For an underground site survey a bounded 3D cavity, wall thickness, neighbors containing fluids and an exit. For a floating island model the tapered underside as owned architecture and declare intentional air gaps. A surface heightmap cannot certify either site.

**Plan and preflight.** The Nexus fills eligible space beneath each deck cell down to deck−4. Its 16 saved vertex/midpoint heights describe the surveyed layout; the builder discovers actual underfill from the world. A support depth cap bounds cost. The terrain rules make that cap viable. For deeper ravines choose piers with a verified bearing surface or reject the site. Material allowlists cannot distinguish player-placed stone from naturally generated stone. Check claims, block entities, permitted replacement policy, border, and min-inclusive/max-exclusive world height for the complete footprint. Provide an edit preview or a designated build volume for existing settlements.

**Commit and build.** Derive one map from position to final state, including intentional clearance. Validate it before publishing the site. AltarStore commits the durable record before activation; SafeFileStore uses a temporary file, backup and replacement. NexusMasonry skips matching blocks and rechecks unexpected materials at write time. Construction may pause after partial placement. Rerunning the same plan should converge. For directional stairs, doors, waterlogging or orientable logs, compare complete BlockData and place connected components in dependency order. Schedule physics updates where the chosen states require them.

**Bound work.** AltarSearch and AltarGeneration separate candidate selection from obtaining chunks and surveying them. Prefer generated terrain, bound new generation per batch, enforce spacing and back off after exhaustion or save failure. Retain the pending candidate across save retries. Work on the target server's owning thread for Bukkit world reads and writes. A completed async chunk request does not authorize arbitrary worker-thread world access. Release acquired tickets on success, abandonment and shutdown.

**Scale limit and extension.** NexusMasonry examines at most 64 plan entries per site per builder invocation; its manager runs every two ticks. Full surveys and initial preflights are separate costs. For a city-sized generator, time-slice those reads too and share one global budget across sites. Persist a design version and terrain-specific support choices if exact reconstruction must survive terrain edits. Define how an interrupted upgrade reconciles old and new cells before changing the generator.
