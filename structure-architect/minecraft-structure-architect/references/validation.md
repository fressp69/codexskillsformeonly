# Validation and fault isolation

Validate the exact integer block plan and attachment coordinates consumed by the builder. Pure geometry tests cannot assess lighting, packet interpolation or how a player reads an entrance.

| Symptom or risk | Check | Correction or acceptance condition |
|---|---|---|
| Mirrored gate or off-center decoration | Generate all quarter turns, including negative coordinates. Track a deliberately asymmetric marker. Compare its cap cell, block center and display center. | Use one transform convention for cells, directional states and mounts. Compare endpoints after snapping. |
| Missing corners or repeated pillars | Check distinct snapped anchors, last-to-first edge, edge lengths and rim connectivity. | Increase scale or simplify the motif if adjacent anchors collapse onto one cell. |
| Floating underside or buried floor | Supply flat, gentle, stepped and cliff height grids. Inspect downhill bearing cells, floor Y and ascent into every gateway. | Each intended footing reaches support within budget. Add access steps or reject a site whose level deck strands an entrance. |
| Broken navigation | Flood-fill traversable standing positions from each approach to the objective. Account for headroom, width, step height and partial shapes. | Verify doors, wall connections and stairs in the target server's real collision model. Check the return route and intended combat escape paths. |
| Unloaded corners or partial builds | Place across chunk boundaries, interrupt a batch, reload twice, simulate save failure and a changed destination block. | No activation before durable commit, no duplicate assembly, safe resumption, justified tickets only. Protect already-owned cells without claiming nearby constructions. |
| Leaks or frame spikes | Count block reads, writes, active displays, visual updates and retained tickets for several sites. Compare active, distant and unloaded states. | Set measured global budgets, terminate temporary effects and return entity/task counts to baseline. |
| Visually flat or awkward | Inspect overhead, approach, eye-level and downhill views with reduced particles, then watch one full animation. | Distinct silhouette, clear threshold, supported masses, intact focal sightline, seamless return to idle. |

**Evidence boundary.** The Nexus test sources include edge reconstruction, solid architecture and crowns, terrain acceptance, legacy data, failed saves, search budgets, assembly cleanup and ritual range. A test definition provides an invariant to reproduce. Report execution, server version and observations separately. If the user reserves live testing for themselves, supply a short route and expected observations.
