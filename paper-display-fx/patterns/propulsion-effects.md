# Jet Fuel · propulsion without a separate render rig

**OBSERVED.** MechanicalGlider.booster starts a 200-tick boost on an existing Flight and layers firework launch, respawn-anchor charge and blaze shoot at the player. thrust decrements the remaining ticks and invokes boostVelocity. Its envelope ramps at both ends. A bounded delta steers toward a heading-derived target velocity. Boost also biases wing flex. The effects read these flight signals; they create no persistent jet display.

On alternating updates animate emits sparks behind both inner wing stations, at station minus 0.35 × player velocity. During boost it places end rods behind the two outer trail stations at minus 0.6 × velocity. Gliding supplies the outer dust trail. Spark counts drop near the end, crackle repeats at 40-tick intervals, and an extinguish cue occurs with ten boost ticks left. Once the timer expires the boost-only emissions cease; the normal glide trail can continue. The observed sustained exhaust uses sparks and end rods. Flame particles and a cached ribbon of previous positions are possible extensions.

**GENERALIZED.** Treat an engine as a socket, a direction, and ignition/sustain/shutdown envelopes. A hovercraft may emit along its local nozzle even when drifting sideways. For an aircraft wake, offset particles against actual velocity instead. Those two choices convey different physical behavior.

**RECOMMENDED.** Inherit some vehicle velocity for exhaust in world space. Use engine load to vary color or cadence before increasing point count. Clear trail history on world change or teleport, and cancel pending shutoff sounds when an owner-bound rig is replaced.
