# Score a transition in space

**OBSERVED cue sheets.** Times below are relative to the particular source action, not universal cadences.

| Action | Entry | Sustained or advancing | Exit |
|---|---|---|---|
| AEGIS charge | Lock click/bit at the reactor | Respawn-anchor charge at muzzle ages 0, 4 and 8 with increasing pitch | Warden sonic boom and firework crack at the muzzle; piston at the base. Vent hiss during recovery. |
| Glider deploy / boost | Piston on deployment; trapdoor and anvil cues scheduled four and eight ticks later. Fuel ignition layers launch, anchor charge and blaze shoot near the player. | Light firework crackle at 40-tick boost intervals | Extinguish cue near the final ten ticks; retraction uses piston and chain. |
| Wiretrap | Bobber throw plus piston at launch; chain, piston and anchor at impact | A trapdoor lock during opening and a quieter amethyst resonance every 32 web updates | Chain break at timed release in a loaded chunk. |
| Sonic sensor | Sculk click and beacon at the mounted device on trigger | Two descending note-block tones at the notified owner, three ticks apart | Persisted cooldown controls eligibility for another alert. |

**GENERALIZED.** Give a sound one job: material contact, energy onset, sustained load, release, or distant warning. Combine a short high transient with a lower body tone at discharge. Put the strike at the hit position, recoil at the mount and a private notification at the listener. Let the charge climb in pitch or cadence so the player can anticipate release. Tighten alarm intervals approaching failure; leave gaps early so the final rapid sequence is perceptible.

**RECOMMENDED.** Resolve vanilla Sound keys against the target registry; a syntactically valid namespaced key alone does not prove a sound exists. Choose an audience radius independently from playback volume. Higher volume can alter audible distance. Audition two nearby emitters and a listener moving across the boundary. Rate-limit per listener, prioritize warnings, stagger decorative loops, and guard delayed notes by assembly generation. If a sustained layer uses repeated short samples, schedule intervals and stop further emission on exit. Baseline cues should work on a vanilla client.
