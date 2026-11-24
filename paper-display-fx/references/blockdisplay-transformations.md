# From model centers to Paper transforms

**GENERALIZED.** For a BlockDisplay rendering a unit cube the mesh runs from (0,0,0) to (1,1,1). Paper's decomposed transform maps a vertex v to t + L(S ⊙ (Rv)), where L and R are the left and right rotations. With R identity, desired center c and dimensions s, set **t = c − L(s/2)**. Subtracting half-size in world axes only works for rotations preserving that offset. With both rotations use t = c − L(S ⊙ R(½,½,½)). For a custom mesh replace the half-vector by its actual model-space center. An ItemDisplay uses an item model and display context; inspect its origin separately.

```java
// Java 21 / Paper 1.21.11. c is relative to a neutral entity anchor.
static org.bukkit.util.Transformation centered(org.joml.Vector3f c,
        org.joml.Quaternionf orientation, org.joml.Vector3f size) {
    var corner = orientation.transform(new org.joml.Vector3f(size).mul(-0.5f)).add(c);
    return new org.bukkit.util.Transformation(corner, new org.joml.Quaternionf(orientation),
            new org.joml.Vector3f(size), new org.joml.Quaternionf());
}
```

**OBSERVED.** ReactorModel.place uses this corner calculation. MechanicalArt.updateBeam instead uses a start anchor and a fixed transverse corner offset. That thin-cable shortcut can move a rotated face off its intended endpoint. For a precise segment A→B, orient +Z along B−A, put c halfway between the endpoints relative to the entity anchor, and use dimensions (w,h,|B−A|).

**GENERALIZED.** For a hinge at H rotating by Q, a rest center p becomes H + Q(p−H); rotate the part orientation as well. Build joint matrices as parent × translate(pivot-in-parent) × rotate(joint); describe child centers relative to that pivot. Equivalent rotation about a pivot in an existing frame uses T(H) Q T(−H). JOML mutates many receivers; copy stored vectors and quaternions before rotating. Put nonuniform visual scale at the leaf. Scaling a parent before rotating its child can shear the child; use a full matrix when shear is intentional.

**RECOMMENDED diagnostic.** Draw three colored axis points, the pivot and the transformed far corner. If the pivot walks, inspect translation order. If the center is fixed but the rim wobbles, inspect local roll or rest half-extents. Mirroring a part reflects positions and reverses handedness. Mirror hinge positions and signed angles, then reconstruct a proper rotation for each side; a quaternion alone cannot represent a reflection.
