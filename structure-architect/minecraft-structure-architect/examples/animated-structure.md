# Worked plan — underground tidal pump hall

**Brief.** A player crosses a maintenance gallery and activates a pump. The distant end of the hall should become visually active while the return path stays open. Scope excavation to an authorized cavity. Use a 25 × 13 room with standing level Y=0, roof soffit at +7 and entrance on the west end.

**Build the physical route.** Place a three-cell central catwalk at z = −1…1, with side basins beyond its rails. Lay the floor at −1 and reserve two clear standing cells above the full route. Put rib frames at x = −10, −5, 0, 5, 10 and keep their arch spring lines above player heads. Separate basin water from the catwalk using real walls. Support the rotating wheel on two real bearing piers. Put the control block on the entrance-facing side, within reach from dry flooring.

**Place the moving assembly.** Anchor a wheel at local (+7,+3.5,+4), in the XY plane, with axle along Z. Construct six display spokes. For spoke i, angle a = 2πi/6 + phase. For a rod extending from radius 0.35 to 2.0 its center is C + 1.175(cos a,sin a,0), its length is 1.65, and its long local X axis rotates about Z by a. Use the centered transform in the [display reference](../references/display-entities.md). Budget six rods and one hub. Verify the full swept disk clears rails, floor and ceiling.

**Operate and recover.** The control changes durable pump state. During spin-up, increase angular speed smoothly, add short bubbles near the intake and play a latch at the control followed by a low motor sound at the wheel. Stop cosmetic updates when the room has no viewers. Reconstruct one wheel from the saved state when its partition loads. If the pump actually changes water blocks, implement that as a separately authorized, bounded simulation.

**Acceptance.** Cycle power while walking the gallery, leave during spin-up, then return. Confirm one assembly, the correct switch state and a clear exit with all effects disabled. Inspect the wheel edge-on for pivot drift. Probe the excavation boundary for an adjoining aquifer before committing any block writes.
