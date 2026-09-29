# intake

An agent skill for deciding whether something you found (an article, repo,
video, paper, skill, plugin, MCP server, or tool) is worth adding to your
agent setup, and bringing in only the part that is.

The agent reads the source itself, separates the author's claims from facts
it verified, compares the candidate with what your setup already has, and
gives one decision per candidate:

| Decision | Meaning |
|---|---|
| ADOPT | Install or add as-is |
| MERGE | Take one idea into an existing skill or instruction; do not install |
| CONDITIONAL | Keep on demand for a named task |
| PILOT | Try on one project for a set period with a before/after measure |
| SKIP | Record why, and when it would be worth revisiting |

It stops after the report. Nothing is installed, edited, or recorded until
you approve the named items.

## Install

The skill is the folder `skills/intake/`. It works with any agent that reads
`SKILL.md` skills (Claude Code, Codex, and others).

Clone and link it, so `git pull` updates it:

```bash
git clone https://github.com/korenl137/intake.git ~/src/intake
ln -s ~/src/intake/skills/intake ~/.claude/skills/intake    # Claude Code
ln -s ~/src/intake/skills/intake ~/.agents/skills/intake    # Codex
```

## Use

Share the source and ask, for example: "intake: is this worth adding to my
setup?" followed by a link.

## Optional: keep review records

Decisions are most useful when the next review can find them. Tell the agent
where records live, in your request or your global instructions, e.g.:

```markdown
Intake review records live in `~/agent-config/docs/reviews/`, one file per
candidate plus a row in its README.
```

The skill then checks earlier decisions before reviewing and writes new
records there after you approve. Without a location, the report itself is
the record.

## Requirements

Required: an agent with a shell, file reading, and web fetch. Everything else
is optional and has a built-in fallback, so the skill works without it:

| Optional tool | Improves | Without it |
|---|---|---|
| [`defuddle`](https://github.com/kepano/defuddle) CLI | clean text from web pages | the agent's web fetch |
| `git` | reading a candidate repo in full | fetching its README and raw files |
| [`watch`](https://github.com/bradautomates/claude-video) skill, or `yt-dlp` + `ffmpeg` | video captions and on-screen names | a transcript you provide |
| A reference manager MCP server (e.g. Zotero) | papers already in your library | the PDF or abstract page |

The skill has no scripts of its own and never installs a candidate during a
review. Fetching a source sends its URL to that source's host, as a browser
would.

## Evaluating the skill

`skills/intake/evals/scenarios.json` lists test prompts with checkable
expected behavior. Run one in a fresh agent session with the skill installed
and check each claim against the transcript.

## License

[MIT](LICENSE).
