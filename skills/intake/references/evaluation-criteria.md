# Evaluation criteria

Standing criteria for step 4. Use them to decide what a candidate must show,
not to score it. A summary of the evidence behind them is at the end; check
the current sources before relying on a number.

## Pick the candidate type

| Type | Passes when | Cost to establish |
|---|---|---|
| Functional: a tool, script, data source or real workflow | It does something the setup cannot do yet, and risk and overhead are acceptable. | Reading the code and its install steps. |
| Instruction only: persona, process manual, rules, prompt pack | All three conditions below hold. | Reading plus a comparison or pilot. |
| Mixed | Judge the functional part by its row and the instruction part by its row; take the part that passes. | Both. |

## Conditions for an instruction-only candidate

1. **Not already done.** The current model or the setup does not already
   behave this way. Test it by running the task without the candidate, or
   by naming the existing instruction, skill or built-in that covers it.
2. **A difference was shown.** Either a with/without comparison on one real
   task of the user's (see [ab-test.md](ab-test.md)), or a PILOT with a named
   measure and end date. The author's pitch is not evidence.
3. **It will run, at a known cost.** Check that it is actually invoked (a
   skill that never triggers adds nothing) and count what it loads every
   turn, whether or not it fires.

If any condition cannot be met, decide SKIP, or MERGE the one idea that
passes into an existing instruction.

## Always loaded or on demand

| Loading | Evidence required | Why |
|---|---|---|
| Always loaded: global instructions, hooks, session-start text, a skill listing entry | A with/without comparison before ADOPT. | The cost is paid on every turn even when it does nothing. |
| On demand: invoked for a named task | A PILOT with a measure is enough. | An unused candidate costs little, so a full comparison is not worth its price. |

If the candidate would be used rarely, CONDITIONAL for that task is usually
enough and no comparison is needed.

## Blocking findings

An unresolved risk blocks ADOPT whatever the benefit: data leaving the
machine without the user's choice, writes outside the candidate's own
folder, secrets handled in the clear. Say which fix would unblock it.

## Evidence behind the conditions

Checked 2026-11-16. "Read" means the page was opened; limits are the
limits of that source, not of the claim in general.

| Source | Finding | Limit |
|---|---|---|
| [Evaluating AGENTS.md (arXiv 2602.11988)](https://arxiv.org/abs/2602.11988), abstract read | Context files do not generally improve task success and raise inference cost by over 20% on average; repository overviews were not helpful. | Abstract only; Python repositories. |
| [Vercel agent evals](https://vercel.com/blog/agents-md-outperforms-skills-in-our-agent-evals), read | Baseline 53%, a skill with default behavior 53%, with explicit instructions 79%, a docs index in AGENTS.md 100%; the skill was never invoked in 56% of cases. | One vendor, one framework; run counts not stated. |
| [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices), read | Build evaluations first, measure without the skill, and add only context the model does not already have. | Guidance, not a measurement. |
| [Claude Code skills docs](https://code.claude.com/docs/en/skills) | Skill listing entries add to context every turn whether or not they are used. | Reported by a collector, not reread. |
| [Persona study (arXiv 2311.10054)](https://arxiv.org/abs/2311.10054) | System-prompt personas did not improve accuracy over no persona across four model families. | Factual questions, not code; 2023-24 models. |

Small differences from one run are noise. Retest after a model change,
because a gain measured on one model may not hold on the next.
