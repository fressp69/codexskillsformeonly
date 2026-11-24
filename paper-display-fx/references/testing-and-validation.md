# Diagnose with observable invariants

| Fixture | Expected result | Where to look on failure |
|---|---|---|
| Unit cube stretched 1×2×5 and rolled 90° | Transformed model midpoint equals requested center | Check rotated half-size, degrees/radians and extra entity yaw. |
| Child at a hinge, then fully deployed | The hinge point remains fixed relative to its parent and emitter follows the endpoint | Check matrix order, pivot subtraction and accidental mutation of rest vectors. |
| Direction crosses ±180° or points straight up | Short turn with stable roll | Wrap angular differences; keep previous transverse axis near a pole. |
| Identical animation clock sampled twice | Same rest-derived pose, one transition cue | Locate incremental rotations, time-dependent random calls or repeated entry callbacks. |
| Wide pulse grazing diagonal cover | Volume and visible cutoff agree; impact occurs once | Compare frame, travel interval and pre-muzzle clearance. |
| Fast travel or teleport during a trail | Bounded samples; no line between worlds | Reset previous socket and distance accumulator. |
| Remove target mid-cable, unload device during warning, reconnect wearer | Defined gameplay outcome; no leaked art or later sounds | Compare owner maps, expiry clocks, teardown and generation tokens. |

**GENERALIZED review.** Compile extracted API fragments against the exact dependency version. Verify particle payload classes and sound identifiers. Compare pose and volume fixtures independently of the client. When authorized, inspect the model from above, behind and along its local forward axis; replay at reduced particles and cross an audience boundary mid-action. Check two devices with distinct phases for shared mutable state. Include server/client versions and recorded evidence in delivery. Separate source inspection, mathematical checks, compilation, client review and performance measurements.
