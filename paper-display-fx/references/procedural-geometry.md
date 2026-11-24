# Paths with moving endpoints

**OBSERVED.** MechanicalArt.beam and updateBeam fit a local +Z rod between locations. WiretrapController.anchor casts outwards, then down if the outward ray misses. Binding stores a target UUID and winding index so each target-relative endpoint can be reconstructed. Fixed terrain points and moving endpoints have different lifetimes.

**GENERALIZED.** For endpoints A and B in one world, let D=B−A and interpolate P(u)=A+uD. Build one display per adjacent point pair. Set length and orientation from that pair, using the centered transform reference. Hide a degenerate pair. A fixed number of links preserves handles during movement. When lengths vary considerably, resample a polyline by cumulative arc length to keep visual density uniform.

For a loose cable use P(u)=A+uD−up·4s u(1−u), where s is midpoint sag. For a taut cable drive s toward zero; this parabola approximates a hanging cable and does not simulate tension. A bowed path around an obstruction can use a quadratic Bézier (1−u)²A+2u(1−u)C+u²B. Check intermediate spans against the environment if intersections matter. A rock anchor actually needs a ray hit; select another anchor or omit the strand if both rays miss.

**RECOMMENDED controlled irregularity.** Choose two directions transverse to D, then add seeded offsets in their plane times sin(πu). This keeps both endpoints attached. Evolve the phase continuously instead of rerolling random knots each tick. For chains alternate link roll by 90°; for robotic arms preserve link lengths and solve joints rather than stretching every link. For a retracting bridge shorten the visible interval along its path and remove spent spans. Hold authoritative crossing or restraint state separately from these visual operations.
