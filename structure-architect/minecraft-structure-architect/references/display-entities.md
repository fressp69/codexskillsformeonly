# Decorating physical architecture

| Medium | Good use | Constraint |
|---|---|---|
| World block | Stair, floor, pillar, gate frame, interactive station | Changes saved terrain and collision. Placement order, permissions and block state matter. |
| BlockDisplay | Tilted crystal, sliding ornamental plate, fractional trim | Provides appearance without walkable collision. Use physical blocks or a separate interaction mechanism where gameplay requires contact. |
| ItemDisplay | A suspended key, tool or artifact | The item model and display context determine its shape. Verify orientation on the intended vanilla client. |
| Particles and sound | Convey direction, timing and state to nearby players | Viewer settings and budgets vary. Preserve readable entrances and interaction cues in the architecture itself. |

**Observed.** NexusModel describes material, center, dimensions, yaw, motion family, phase and luminosity. NexusVisual owns the entities. Each of eight rounded caps gets one 0.88-block amethyst crown and two satellites. Eight stabilizers orbit the three-piece heart. All 35 display origins belong to the anchor chunk. Local transforms place their visible models around the site. Size culling bounds to cover the translated pieces.

**Pivot rule.** A unit block model begins at its lower corner. For center c, rotation Q and size s, set translation to c + Q(−s/2). Keep c relative to the entity origin. The following helper uses Paper 1.21.11 and its JOML types.

```java
static org.bukkit.util.Transformation centered(org.joml.Vector3f center,
        org.joml.Vector3f size, org.joml.Quaternionf rotation) {
    var corner = rotation.transform(new org.joml.Vector3f(size).mul(-0.5f)).add(center);
    return new org.bukkit.util.Transformation(corner, new org.joml.Quaternionf(rotation),
        new org.joml.Vector3f(size), new org.joml.Quaternionf());
}
```

**Animate from the rest pose.** Use y = baseY + amplitude × sin(ωt + phase). A satellite can use x = cx + r cos θ and z = cz + r sin θ. The Nexus tightens crown phase differences as ritual energy rises. This makes eight objects appear to synchronize with one gameplay clock. Use interpolated transforms between samples, leave still parts alone, and stop expensive updates outside viewer range. Place particles along the actual path from source to destination; attach sounds to phase transitions. An effect completing on a client is an unreliable trigger for gameplay.

**Ownership and limits.** Keep a per-site assembly, spawn transient entities once while active and remove them on unload, disable or partial construction failure. Map repeated load notifications to the same assembly. For a sprawling facility partition decorations by room or chunk, since a distant wing can remain visible while the central anchor unloads. Recompute swept bounds for rotation, bobbing and extensions. Verify interpolation, particle payloads and display culling against the target Paper version.
