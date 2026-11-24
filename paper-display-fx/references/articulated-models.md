# Assemble logical joints

**OBSERVED.** AEGIS keeps a Part record with mount family, center, dimensions, rest angle and display. One pose pass selects base, chassis or weapon space. Glider panels and ribs are indexed by side and span station; the controller recomputes all placements from player and flight state. Neither mechanism relies on BlockDisplays inheriting transforms from other displays.

**GENERALIZED model schema.** For each joint record parent, parent-space rest pivot, rest orientation, motion axis, range and driver. For each leaf record joint, joint-local center, rest orientation, dimensions, material and entity handle. Attach emitters as named points and directions on the same joint. Keep mutable state (age, fold, speed, recoil) in the assembly; the renderer owns last sent pose and interpolation duration.

Evaluate joints parent-first. If parent frame is (P,Q), child frame is (P + Qh, Q × qRest × qMotion). A sliding joint adds its extension along its local rail. A leaf at offset c has center Pchild + Qchild c and orientation Qchild × qLeaf. Sample a nozzle's exit and direction before converting either to BlockDisplay corner coordinates.

**Design choices.** A fixed base can keep its first pose. Chassis yaw carries hinge housings; barrel pitch carries the optic and bore; recoil slides the inner tube, leaving the jacket fixed. For wings, mirror span and fold signs around the root. Vary flex with span squared so the tip gives more than the hinge. Mount brackets can counter-rotate in pairs while a lens moves along the face normal. A telescoping antenna can slide nested sleeves by bounded fractions of total extension. Keep engagement overlap at maximum extension.

**RECOMMENDED.** Build one side with asymmetric diagnostic markings. Pose fully folded, half deployed and fully extended before mirroring. Inspect sockets and clearances at the extrema. Use a stable part identifier or typed handle for emitters that must survive model revisions. Allocate replacement entities only when topology changes.
