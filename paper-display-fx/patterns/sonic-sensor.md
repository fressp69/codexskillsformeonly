# Sonic Sensor · one normal for a whole device

**OBSERVED.** A thrown sensor has two spinning parts attached to a projectile. impact accepts a vertical wall and offsets the device outward along the hit face. ensureRendered derives yaw from atan2(normal.x,normal.z), rotates mounting offsets as well as their orientations, and builds a base, two frame rails, lens and four brackets. A separate nonpersistent Interaction supplies the physical hit target. The durable record stores ID, owner, world, location, face and cooldown deadline.

Over six controller updates the brackets unfold in mirrored pairs. animateLens moves the glass along the face normal: this lens itself reads as a vibrating diaphragm. On discharge it moves through light blue and orange into red cooldown. The wave center advances along the same normal as the detector. Twelve samples form an ellipse in the lateral/vertical plane, with radii growing with discharge progress. Occupancy checks project player displacement onto the face and lateral axes and test sight; a new entrant while armed triggers the response. Ring samples are a visualization, not the detector's exact rectangular boundary.

Sounds originate at the device; aggregated owner alerts use a separate private two-note cue. Lens updates check nearby FX viewers. Unloaded sensors lose visuals; loaded records can recreate them. Destruction clears visuals and record. Shutdown removes flights and model handles and saves sensor state.

**GENERALIZED.** Use one mount frame for a security camera housing, swivel, field-of-view query and scan fan. For a bulkhead, attach its indicator to the frame and its door-edge emitter to the moving leaf.

**RECOMMENDED.** To support ceilings or sloped surfaces, construct a full basis around the face normal, including a deliberate roll direction. Check support removal explicitly if the device must fall when its mounting block disappears.
