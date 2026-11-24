# Nanowire · fixed anchors and moving targets

**OBSERVED.** Flight associates an actual Snowball with five casing displays. tick teleports and rotates those pieces; ProjectileHitEvent determines impact. detonate opens nine hub pieces and lays ten outward strands using golden-angle azimuths with varied elevations. During the first ten web updates the hub spreads and an expanding dust ring marks deployment. anchor traces 4.8 blocks outward, then tries a downward ray; if both miss, it returns a free-space point. A visual endpoint therefore does not always lie on terrain.

Web owns all art, an origin, age, deadline, Strand objects (fixed start plus target UUID and height fraction) and Binding objects (target UUID plus winding index). Each bound target gets three external tethers and two six-segment helices. winding uses relative height 0.19+0.62u and opposing angles yaw ± (2.4πu+0.3). Radius scales with target width. Connect consecutive samples within each winding. Binding updates are viewer-gated every third web update. External tethers update independently. Near expiry only the winding radius contracts over the final 250 ms. Dust nodes accent the crossing paths. Release removes the web and optionally emits a chain snap.

The controller uses a separate Restraint map, a movement check and MachineManager.stun. The visual cables do not enforce restrictions. The web's wall-clock deadline and tick-based visual age may diverge during lag.

**GENERALIZED.** A grappling line can keep one immutable terrain socket and one moving hand socket; a mechanical arm instead needs fixed link lengths. A containment field can reuse the sampled helix and switch its radius envelope. Keep the endpoint resolver separate from segment rendering.

**RECOMMENDED.** Track each web's actual remaining budget before adding targets. This implementation can allocate 19 + 15 × targetCount impact displays before flight art, with up to twelve targets. That is a source-derived allocation count, not a performance measurement. Prefer fewer links or particle-only secondary windings under load, and release individual strands when their target disappears.
