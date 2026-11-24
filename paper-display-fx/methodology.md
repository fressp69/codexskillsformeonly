# Extraction notes and file inventory

**OBSERVED** identifies code inspected in the SkillsSMP Java 21 project targeting Paper 1.21.11. **GENERALIZED** describes a transferable method or an original worked design. **RECOMMENDED** identifies an improvement or validation procedure. The implementation is evidence for these decisions; measuring visual quality or cost requires a client and server.

Paths in the table start at src/main/java/dev/skillssmp. The skill itself needs none of these classes at runtime.

| Source path and entry points | What the code establishes |
|---|---|
| engineer/turret/TurretMachine.java · track, muzzle, fire, meltdownTick | Shared authoritative state, limited tracking, snapshot at discharge and terminal lifecycle. |
| engineer/turret/ReactorModel.java · pose, place, discharge, eject | Tagged mount families, exact rotated centers, contiguous shell segments and recycled plates. |
| engineer/turret/CannonBeam.java · bounds, firstContact, clearLength | Continuous oriented volume, a world-space broad phase and a common obstruction distance. |
| engineer/turret/ReactorEffects.java · charging, arcs, overload, shockwave | Local charge guide, transverse distortion, inward overload pulses and spherical release samples. |
| engineer/glider/MechanicalGlider.java · mounted, animate, thrust, boostVelocity, retract | Pose-relative stations, change-in-speed flex, boost envelope, paired velocity-offset traces and ownership of flight art. Jet Fuel uses this controller. |
| engineer/wiretrap/WiretrapController.java · impact, anchor, winding, detonate, tick | Projectile-to-web handoff, mixed terrain/target endpoints, opposing windings, separate authoritative restraints and web expiry. |
| engineer/sensor/SoundSensorController.java · ensureRendered, tick, animateLens, removeVisuals | Persisted wall frame, bracket deployment, optical diaphragm, forward ellipse and independent Interaction entity. |
| engineer/visual/MechanicalArt.java · part, beam, updateBeam, remove | Transient tagged displays and endpoint fitting. The simple beam offset is an approximation under rotation. |
| fx/FxService.java · trackDisplay, trackMachineBody, point, sound | Registered-display cap, audience predicates, essential silhouette visibility, particle payload routing and viewer budgets. These controls apply to calls routed through the service. |

**Inventory.** Modified SKILL.md. Added ten technical references (coordinates, transformations, articulation, interpolation, procedural geometry, volumetric effects, particles, sound, performance/lifecycle, testing), five source patterns and three original worked examples. Their individual files are linked by the entry point. Additional files are methodology.md, installation.md and validation-report.md.

The key transferable boundary is the immutable action input to the renderer: a mount pose, beam result, target endpoint or remaining boost duration. Changing particle density or omitting an optional part should leave that input valid.
