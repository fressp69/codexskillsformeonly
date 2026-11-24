# Package validation

Validated against the audited SkillsSMP source and cached Paper 1.21.11 API using Java 21.

| Check | Scope and result |
|---|---|
| Entry point | Parsed YAML with SnakeYAML. Directory and skill name match paper-display-fx; the description is present. |
| Routing and package | Checked local Markdown links and their targets. Installed copies in disposable Codex and Claude project layouts were checked for the expected entry point and identical file content. |
| API examples | Extracted both Java methods from the transformation and particle references, wrapped them in a class and compiled with javac --release 21. |
| Geometry | Evaluated 16 combinations of yaw and elevation, including both vertical poles. Center reconstruction passed at 0.00001 blocks and forward direction at 0.0001 vector distance. A near-π case exceeded the initial 0.00001 direction tolerance by about 0.0000385 with float quaternions. |
| Evidence and portability | Compared the five case studies to their implementing methods. The core workflow and examples require no SkillsSMP classes. Reviewed the source distinctions between registered and unregistered displays, speed change and vector acceleration, and normal emission cutoff and animated retraction. |
| Live behavior | No Paper server or Minecraft client was launched. No frame rate, tick time, visual quality, Folia runtime compatibility or interactive client skill discovery was measured. |

The repository package modifies only the existing paper-display-fx directory. The original worked designs are implementation guides; only the two Java fragments above were compiled.
