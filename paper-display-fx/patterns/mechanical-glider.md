# Mechanical Glider · a wearable frame under load

**OBSERVED.** MechanicalGlider.Flight owns the player, ordered components, animation age, boost timer, heading, pitch, previousSpeed, flex and spring velocity. deploy builds seven panel/rib pairs per side plus five pack parts (33 displays). animate teleports each part to a body-relative station and sets its orientation. mounted applies a body quaternion once and neutralizes the anchor's yaw/pitch. During native gliding the root height, panel lift and body pitch convention change together.

Heading follows 36% of the shortest yaw delta per tick. Pitch follows 28% of its error. The nine-update opening uses a cubic ease-out. Span determines the outer station and bend grows with squared span fraction. A bounded turn term adds opposing lift to the two wings. The load driver is clamp(5 × change in speed + boost bias,0,1). Spring velocity becomes 0.69 × (spring + 0.16 × (load−flex)); flex advances by spring and is clamped. This measures scalar speed change per sample. A turn at constant speed has vector acceleration but contributes no speed-change load.

Every other animation tick the outer station emits trail points while gliding. That socket is the outer panel station, not its exact transformed mesh corner. Landing after native flight, depletion, manual retraction, disconnect, death and world changes remove the components; retraction removes them immediately with optional sound.

**GENERALIZED.** For sails, paired wings or mechanical creatures, compute a root frame, mirror span stations, weight outer-station deformation more heavily, and sample emitters after posing. For a true geometric tip use the transformed mesh point at the outer edge, including leaf rotation and scale.

**RECOMMENDED.** For variable sampling compute acceleration (vNow−vPrev)/Δt and project it onto the desired axis. Seed previous velocity on activation to avoid a false initial impulse. Tune longitudinal flex separately from lateral bank. An authored folded landing transition needs its own brief visual lifetime; keep the motion controller free to release flight immediately.
