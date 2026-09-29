# Where an agent setup usually lives

Starting points for step 3's inventory. Check what exists; paths vary by
version and platform (on Windows, `~` is `%USERPROFILE%`). If an installed
file is a link, follow it to the managed source.

| What | Claude Code | Codex |
|---|---|---|
| Global instructions | `~/.claude/CLAUDE.md` | `~/.codex/AGENTS.md` |
| Project instructions | `CLAUDE.md`, `.claude/CLAUDE.md` | `AGENTS.md` |
| Skills | `~/.claude/skills/`, `.claude/skills/` | `~/.agents/skills/`, `.agents/skills/` |
| Settings and hooks | `~/.claude/settings.json`, `.claude/settings.json` | `~/.codex/config.toml`, `~/.codex/hooks.json` |
| MCP servers | `~/.claude.json`, `.mcp.json` | `[mcp_servers]` in `~/.codex/config.toml` |
| Plugins | `claude plugin list` | the host's plugin list |

For another agent, look for its documented equivalents of the same rows.
