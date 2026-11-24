# Install the structure skill

Extract the archive to a temporary folder. Copy the complete minecraft-structure-architect directory, including references and examples, into one skills directory below. SKILL.md must sit directly inside minecraft-structure-architect. A project install scopes discovery to that project.

| Client | Personal directory | Project directory | Explicit invocation |
|---|---|---|---|
| OpenAI Codex | ~/.agents/skills/ | .agents/skills/ | $minecraft-structure-architect |
| Claude Code | ~/.claude/skills/ | .claude/skills/ | /minecraft-structure-architect |

On Windows, ~ represents your user profile. For example, the personal Claude Code entry point is %USERPROFILE%\.claude\skills\minecraft-structure-architect\SKILL.md. Open a new session in the intended project and invoke the skill with a concrete brief, such as “Design a ridge watchtower with a walkable lookout and a downhill entrance.” No plugin build or server installation is required.

See [Codex skills](https://developers.openai.com/codex/skills) and [Claude Code skills](https://code.claude.com/docs/en/skills).
