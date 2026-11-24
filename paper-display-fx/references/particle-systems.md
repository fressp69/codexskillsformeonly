# Sample shapes in an emitter frame

**GENERALIZED.** Use orthonormal transverse vectors R,U, forward F and source O. Define B(θ)=R cos θ + U sin θ. Generate positions as world offsets. Keep phase in radians, distance in blocks and elapsed time in a declared unit.

| Effect | Position or sampling rule |
|---|---|
| Ring / shockwave | O+r(t)B(θ); add F·d(t) to advance the front. Use separate radii along R,U for an ellipse. |
| Helix / spiral | O+F·Lu+r(u)B(2πku+phase). Constant r makes a cylinder, changing r winds inward or outward. |
| Cone / beam envelope | Slice at z=Lu, choose r=z tan(halfAngle) for a cone or fixed r for a tube. For a square trace its four edges in R,U coordinates. |
| Sphere | For i in [0,N), y=1−2(i+½)/N, θ=iπ(3−√5). Offset = r(√(1−y²)cos θ, y, √(1−y²)sin θ). Animate r for a pressure front. |
| Stream / electrical arc | Move a packet along a path by normalized age. Modulate transverse displacement with a seeded wave and an endpoint envelope. Cap amplitude to preserve the silhouette. |
| Moving trail | Store last accepted socket position. Sample along the displacement at fixed world spacing, cap samples per update, reset on teleport. Shrink density and fade color toward the tail. |

Choose N ≈ ceil(2πr/spacing) for a ring, limited by available viewers' budgets. Distribute angular samples around the full ring even when reducing N. Linear color blending uses (1−u)A+uB per channel, clamped before constructing a color. For an implosion reverse the radius envelope while retaining the emission origin.

```java
// Paper 1.21.11, one point on a viewer-local ring. right and up are unit vectors.
static void ringPoint(org.bukkit.entity.Player viewer, org.bukkit.Location origin,
        org.bukkit.util.Vector right, org.bukkit.util.Vector up, double angle, double radius) {
    var at = origin.clone().add(right.clone().multiply(radius * Math.cos(angle)))
            .add(up.clone().multiply(radius * Math.sin(angle)));
    viewer.spawnParticle(org.bukkit.Particle.DUST, at, 1, 0, 0, 0, 0,
            new org.bukkit.Particle.DustOptions(org.bukkit.Color.AQUA, 0.8f));
}
```

**OBSERVED.** FxService.point distributes budgeted points with particle-specific payloads. On this API DUST uses DustOptions and FLASH takes Color. Glider exhaust moves sample *positions* opposite velocity. A directional velocity is a different effect: for particles supporting the count-zero directional convention, use direction offsets and explicit extra speed; confirm behavior for the selected particle on the target client. Cache the audience per update when many samples share an origin. Reserve enough budget for gameplay-critical warnings before cosmetic sparks.
