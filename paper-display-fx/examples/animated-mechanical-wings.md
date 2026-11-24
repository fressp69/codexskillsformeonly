# Worked design · folding courier wings

**GENERALIZED example.** Fit two three-panel wings to a courier drone. In root space, hinges sit at (±0.3,0.15,0); per side, spans are 0.65, 0.5 and 0.4 blocks. Use the root's yaw and bank. Each child hinge starts at its parent's outboard edge. Store a socket at the end of panel three.

For side s ∈ {−1,+1}, each child center in hinge space is (s·length/2,0,0). Advance to the next hinge by (s·length,0,0) after applying the current joint. Start folded by yawing each side toward the tail; with +Z forward, a signed positive Y rotation on the positive-X wing sweeps it toward −Z. Reverse the angle on the other side. Ease fold angles toward zero during deployment.

Sample velocity every simulation step. Let longitudinal acceleration be ((v−vPrev)/Δt)·F. Clamp it through a configurable response curve, smooth with a damped spring and apply local signed bend angles weighted by station. Initialize vPrev at deploy. This version can model unloading during deceleration by allowing a negative target. Keep a rate and range limit so a launch impulse cannot invert the wings.

Evaluate the hierarchy once per sample. The trail starts at the **world-space end of the third panel**, not a fixed distance from the drone. Dot the traveled interval evenly; omit a trail across teleports. On landing, disable propulsion, play the latch, finish the cosmetic folding envelope and release all handles. Acceptance: hinge gaps stay closed at half-fold, left/right tips mirror under neutral bank, and tips remain attached in a tight turn.
