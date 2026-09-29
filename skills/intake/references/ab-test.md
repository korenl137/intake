# A/B test for a candidate

Use this only when the decision hinges on a quality claim that reading the
candidate cannot settle, and only after the user agrees to the cost.

## Setup

- **Scenario**: one real task from the user's work that the candidate claims
  to improve, written as the exact user message. Prefer a task that ends
  early (at a confirmation step) and give fixtures (a saved transcript, a
  cloned repository) instead of live downloads.
- **Checks**: 2–5 claims about the outcome that can be verified by reading
  the transcript or diff ("reads the existing config before editing", not
  "does a good job"). Write them before running.
- **Conditions**: candidate **off** (the current setup) and candidate **on**.
  Nothing else differs: same message, same fixtures, same model the user
  actually runs.

## Run

Run each condition in a fresh subagent or session that does not inherit this
conversation (in Claude Code, a new agent rather than a fork; in Codex, a
spawned agent without forked turns). The reviewing session must not judge a
run it influenced. If the host has no subagents, give the user the exact
message and conditions to run in two new sessions, and score the
transcripts they bring back.

- Take the subagent's user-facing reply as its result. Do not ask it to
  write a report file unless the file is the deliverable under test.
- If a tool is blocked and the subagent reaches the result another way,
  score it as an adherence failure.

## Score

Pass or fail per check, per condition. State the number of runs. One run per
condition shows a large difference at best; a one-check difference from a
single run is noise, so say so rather than deciding on it.

## Cost

Each run starts cold and rereads everything, and an A/B doubles that. Before
running, tell the user the number of runs and what they fetch; run only what
the decision needs.
