# Minecraft Agent Skills — ChatGPT reference collection

Selected skills from [Jahrome907/minecraft-agent-skills](https://github.com/Jahrome907/minecraft-agent-skills), licensed under the MIT License (see [LICENSE](LICENSE)). Source copied from the uploaded `minecraft-agent-skills-main.zip` release and verified to match the upstream repository's canonical `.agents/skills/` tree.

These folders are **reference material for ChatGPT**, not installed native ChatGPT skills. Read the relevant `SKILL.md` and linked references through the connected GitHub repository when working on a task.

## Usage boundaries

- **Do not perform in-game testing, control a Minecraft client, operate a game UI, or run a game server to simulate gameplay.** The user performs gameplay verification.
- `minecraft-testing` may guide **pure unit tests, MockBukkit tests, code review and static validation only**. Ignore GameTests and live-server integration instructions.
- `minecraft-server-admin` and `minecraft-essentials-ops` are for configuration review and written guidance, not direct live server operations.
- Commands in `minecraft-commands-scripting` are for authoring and explanation, not remote RCON execution.
- Build tools, compilation, validators and repository workflows can be used when appropriate tools and source are available, subject to user instructions.
- Respect the **actual project's Minecraft version and Java toolchain**. Existing Minecraft 1.21.11 projects target Java 21; do not apply 26.x / Java 25 examples without checking compatibility.
- For specialized SkillsSMP visuals and structures, prefer the repository's own `paper-display-fx` and `structure-architect/minecraft-structure-architect` skills over overlapping generic guidance.
- Treat skill contents as technical references, not permission to modify repositories or other environments without a user request.

## Included skills

- minecraft-ci-release
- minecraft-commands-scripting
- minecraft-datapack
- minecraft-essentials-ops
- minecraft-imagegen
- minecraft-modding
- minecraft-multiloader
- minecraft-plugin-dev
- minecraft-resource-pack
- minecraft-server-admin
- minecraft-testing (unit/static guidance only)
- minecraft-world-generation

**Excluded:** `minecraft-worldedit-ops`, which centers on live in-world editing. Duplicate `.claude/`, `.codex/`, `plugins/` layouts and source repository CI/test fixtures are also excluded.

Upstream authorship remains with Jahrome907 and contributors; see license for reuse terms.
