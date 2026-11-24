# From drawing to block coordinates

**Observed.** AltarGeometry generates a regular octagon once in continuous XZ coordinates. Each edge connects a vertex to its cyclic successor. NexusMasonry rounds these same vertices to place columns. NexusModel uses the rounded positions again for their crowns. The floor mask, edge samples and vertical parts therefore share one scale and orientation.

**Use a declared frame.** A block index identifies a cell. Its horizontal center is (x + 0.5, z + 0.5). State whether Y means supporting block, walking surface or display center. For example, the Nexus uses local XZ offsets and absolute deck Y in its block plan. Adding the site's Y again would bury or elevate the whole build. For new designs, consider local coordinates on all three axes and perform one conversion at placement.

For a local point (u,v) in XZ, define positive planar rotation from +X toward +Z. Then x = ox + u cos θ − v sin θ and z = oz + u sin θ + v cos θ. This convention differs from Bukkit facing yaw. For quarter turns, use the exact integer mapping (u,v) → (−v,u). Rotate directional block states, stair shapes and connections along with positions. For even-width structures choose a between-cell symmetry axis; rounding a mirrored half-cell independently can introduce a one-block bias.

**Regular polygons.** For N sides, angle step h = 2π/N. With a face normal along +X, vertex i is R(cos((i+½)h), sin((i+½)h)). The apothem is R cos(h/2) and bay length is 2R sin(h/2). The Nexus uses N=8 and R=8.25, giving about 6.31 blocks per bay before snapping. For an arbitrary rotation rotate the sample point back into the polygon frame.

```java
// Java 21. Coordinates are relative to the center, in blocks.
static boolean inside(double x, double z, int sides, double radius, double margin) {
    double limit = radius * Math.cos(Math.PI / sides) + margin;
    for (int i = 0; i < sides; i++) {
        double a = 2 * Math.PI * i / sides;
        if (x * Math.cos(a) + z * Math.sin(a) > limit) return false;
    }
    return true;
}
```

**Raster rules.** Fill cells inside the mask. A filled cell touching an unfilled cardinal neighbor is a rim cell. An inlay along a ray through V selects cells with |x Vz − z Vx| / |V| below half the desired width and (x,z)·V positive. Reserve an opening by excluding the middle interval of an edge's interpolation parameter. Check the resulting opening after rounding and after wall block states connect. Nexus uses 20 edge subdivisions; for longer bays derive the sample count from length or use a supercover line. Corner-touching voxels alone form a poor parapet or walkway.

**Extensions.** A circular tower shell accepts cells between two squared radii. An arch occupies a half-annulus in the vertical section above its spring line; extrude its thickness along the passage. A pitched roof can assign each cross-section column a height proportional to its distance from the nearest eave. Derive stairs and ridges from adjacent heights. For a dome use horizontal slices of radius √(R²−y²). Thin rings can disconnect at small scales. Widen the section, inspect one quadrant, then reflect it.

Compute bounds from occupied cells, cleared cells, access stairs and decorative motion extrema. Convert signed block coordinates to chunks with floorDiv(x,16). Include the last cell of an inclusive box. Large diagonal bounds contain much empty space; use masks or subcomponent bounds for expensive queries.
