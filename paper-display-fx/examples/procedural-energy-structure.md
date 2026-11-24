# Worked design · temporary resonance loom

**GENERALIZED example.** A central spool pays out four luminous threads to fixed sockets, pulses once, then draws them home. Give the loom one owner ID, neutral origin, start tick, four endpoint positions and a fixed array of three segment handles per thread. An optional rotating hub adds one display. The maximum topology is thirteen displays; reserve a cheaper particle-only fallback before activation.

Choose four sockets within the permitted volume. Let A be the spool socket, B an endpoint, U the local up direction and e∈[0,1] the extension. Define P(t)=A+t(B−A)+U·0.35 sin(πt). For link j=0,1,2 fit a rod between P(ej/3) and P(e(j+1)/3). Hide zero-length links. A distinct phase per thread can rotate a particle spark around its tangent while keeping the two physical endpoints exact.

| Example tick | Extension and score |
|---|---|
| 0–12 | e=smoothstep(age/12). Rotate hub forward. Start one spool sound at A. |
| 13–32 | Hold e=1. Send a white packet along P(t); play its arrival at B when it reaches t=1. |
| 33–45 | Decrease e with reversed smoothstep. Trace the shortening prefix back to A and lower the hum. |
| 46 | Close the assembly. Clear rods, hub, packet ages and owner map entry. |

Resolve path and effects on the owning thread. If a socket disappears, apply the selected cancellation policy once. On origin unload, close without loading the socket chunks. Test interruption during payout and return; neither path should issue an arrival sound after close.
