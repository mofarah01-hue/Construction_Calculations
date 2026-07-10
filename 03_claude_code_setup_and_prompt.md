# 03_CLAUDE_CODE_SETUP_AND_PROMPT.md

Claude Code, Windows, desktop app or terminal. Same briefs, different harness.

---

## STEP 1: FOLDER

```
BizDev/
  CLAUDE.md
  00_framework.md
  01_concept_a_elder_monitoring.md
  02_concept_b_pregnancy_parenting.md
  .claude/
    settings.json
    agents/
      researcher.md
  research/
    decision_log.md
    registers/
    shared/
    a/
    b/
```

`git init` it. Every phase output becomes a commit. That is your audit trail and your undo button, and it is the single biggest advantage Claude Code has over Cowork for this work.

---

## STEP 2: MODEL AND TOKEN CONTROL

This is the part you were worried about. Three levers.

### Lever 1: pin the session model

`.claude/settings.json`

```json
{
  "model": "sonnet"
}
```

On the Anthropic API the `sonnet` alias resolves to Sonnet 5. Sonnet 5 requires Claude Code v2.1.197 or later. Pin the exact string `claude-sonnet-5` instead of the alias if you want it frozen.

Switch mid session with `/model opus` for the three phases that need judgment, then `/model sonnet` right back.

### Lever 2: `opusplan`

```json
{
  "model": "opusplan"
}
```

Opus does the planning, Sonnet does the execution, automatically. For this project that is close to ideal. The architecture fork and the market synthesis are planning problems. The component sweeps and competitor profiling are execution.

Start here. Fall back to plain `sonnet` if the rate limit bites.

### Lever 3: pin the subagents

This is the one that solves your original problem. A subagent can carry its own model in frontmatter, so a spawned research agent cannot escalate to Opus behind your back.

`.claude/agents/researcher.md`

```markdown
---
name: researcher
description: Bounded web research. Use for component sweeps, competitor profiling, literature search, and pricing lookups. Always returns a table plus register entries. Never makes strategic recommendations.
tools: WebSearch, WebFetch, Read, Write, Edit
model: sonnet
---

You perform bounded research and nothing else.

Rules:
- Your task always names a target and a stop condition. Find exactly what was asked. Stop.
- Never expand scope. Never follow an interesting tangent. Report it as an open question instead.
- Every finding carries a source, a URL, a date, and a confidence rating of HIGH, MEDIUM, or LOW.
- Never invent a price, a lead time, a market size, or a timeline. Write UNKNOWN.
- Read license files directly. Record the exact SPDX identifier. Never infer a license from a README.
- Append every item you evaluate, including rejected ones with reasons, to the correct file in research/registers/.
- Return a table. Not prose.
- Make no recommendation. The main session decides.
```

Verify the frontmatter field names against the current subagent docs before relying on them. Then in `CLAUDE.md`, tell the main session to delegate all enumeration to this agent. Opus never touches a search result. It reads the table.

### Billing caveat

Interactive sessions and programmatic or headless runs (`claude -p`, scheduled jobs, SDK) may bill against different pools. Check the current Claude Code billing docs before you set up the weekly scheduled task, because a headless loop left on Opus is exactly the failure mode you were trying to avoid.

---

## STEP 3: CLAUDE.md

Root of the project. Claude Code reads it at the start of every session.

```markdown
# BizDev Research Program

You are the research and business development analyst for this project. Two concepts are being evaluated for viability. Produce defensible business cases, not enthusiasm.

## Read before any task, in this order
1. `00_framework.md` (authoritative, governs everything)
2. The relevant concept brief
3. `research/decision_log.md` and all prior phase outputs
4. `research/registers/`

Never re research anything a prior phase established and logged.

## Delegation
Delegate all enumeration, search, pricing lookup, and literature retrieval to the `researcher` subagent. It returns tables. You read tables and decide. Do not run broad web searches from the main session.

Never spawn a subagent that is not defined in `.claude/agents/`. Never spawn more than three at once.

## Execution
- One phase per session. Stop at the end of the phase. Report. Wait.
- Ask every question whose answer would change the approach before starting. Ask them all at once.
- Never guess. Never fill a gap silently. Every assumption is stated explicitly and flagged.
- For any technical specific (component, parameter, model, price point, market segment), ask rather than assume.
- No open ended research. Every search has a target and a stop condition.
- When the concept description is technically contradictory or commercially implausible, say so in the output. Do not build around it quietly.

## Evidence
- Every number gets a source, a URL, and a date.
- Never invent a price, lead time, market size, or timeline. Write UNKNOWN and log it as an open question.
- Mark every material claim HIGH, MEDIUM, or LOW confidence.
- Flag sources older than 18 months as stale.
- Distinguish list price from quoted price from estimated volume price.
- Market sizing is bottom up first. Analyst TAM is a secondary check only, never the primary number.
- When sources disagree, present both and say which is more credible and why.
- Primary sources where they exist: datasheets, distributor pricing, FDA and FTC guidance documents, CMS schedules, filings, peer reviewed papers. Avoid content marketing and SEO aggregators.

## Registers
Append continuously to `research/registers/`. Nothing is cited in a phase output without landing in a register. Rejected items stay, with the rejection reason. Read every open source license file directly and record the exact SPDX identifier.

## Output
Every phase writes to the path named in the brief. Every phase output ends with:
- `## Open Questions`
- `## Assumptions Made`
- `## Confidence Summary`

After every phase, append to `research/decision_log.md`: what was decided, what evidence supported it, what was rejected and why. Then commit with the message `phase: <concept> <phase name>`.

Split long deliverables into separate documents by domain (engineering, business, regulatory, market) at your discretion. Do not compress to fit one file.

## Positioning
Both products are general wellness. This is settled and was taken with regulatory counsel. Do not relitigate it. Document and defend it with citations.

The line that matters:
- Self reported input is not a claim.
- Measurement and trend are not a claim.
- Inference of a named disease from passive data is a claim.

Prefer self report for anything affective or cognitive. Prefer measurement for anything physical. Surface the pattern, let a human draw the conclusion.

Risks go in a risk register with mitigations and costs. Never as a refusal to research.

## Style
- No em dashes, no en dashes, no hyphens as punctuation. Hyphens only inside part numbers and proper names.
- C suite engineering leadership tone. Authoritative, precise. No hedging, no filler.
- Tables over prose for anything comparative. Summaries short, blunt, comparative.

## Repo notes
This is a research repository, not a codebase. There is no build, no test suite, and no source to compile. Do not look for one. The deliverables are markdown.
```

---

## STEP 4: KICKOFF PROMPT

Open the project. Enter plan mode first (`shift+tab` twice, or `/plan`). Paste:

```
Read CLAUDE.md, then 00_framework.md, then 01_concept_a_elder_monitoring.md, then 02_concept_b_pregnancy_parenting.md, in full, before doing anything else.

Then ask me every question you need answered before starting. Ask them all at once. Do not begin research until I answer.

After I answer, execute the program in this order, one phase per session, stopping and reporting after each. Do not chain phases.

FOUNDATION
1. The five shared research files in framework section 8. Start with shared_wearable_data_access.md, because both concepts may be invalidated by it.
2. regulatory_precedent_dossier.md
3. regulatory_risk_register.md

CONCEPT A
4. A Phase 0, scope and claims matrix
5. A Phase 1, marker and trend catalog
6. A Phase 2, sensing architecture fork
7. A Phase 3, hardware and BOM
8. A Phase 4, software, models, and open source
9. A Phase 5, data, privacy, and security
10. A Phase 6, development plan, cost, and timeline
11. A Phase 7, market, competition, and channel
12. A Phase 8, business case and capital
13. A Phase 9, synthesis

CONCEPT B
14. B Phase 0 through B Phase 7, same pattern

CLOSE
15. research/PORTFOLIO_DECISION.md

Delegate all enumeration and search to the researcher subagent. Maintain the registers continuously. Every component, every open source project with its exact license, every paper, every dataset, every vendor, every competitor, every fund. Rejected items included, with reasons.

Split any deliverable into multiple documents by domain if one document would be too large to be useful. Use your judgment on where to split.

Commit after every phase.

Right now, do only this: read the four files, then present your plan and your questions. Do not write anything yet.
```

Plan mode means it reads, thinks, and asks before it touches a file. Approve the plan, then run phase by phase.

Each subsequent session is one line:

```
Read CLAUDE.md, the framework, the concept brief, the decision log, and the registers. Execute Concept A Phase 2 only. Stop when it is complete.
```

---

## STEP 5: SLASH COMMANDS, OPTIONAL

If typing that line gets old, put it in `.claude/commands/phase.md` and call `/phase A 2`. Worth doing after the first three phases, once the pattern has stabilized. Not before.

---

## STEP 6: THE SHORT PATH

If rate limit is tight, four phases decide whether either concept is worth funding:

- **A Phase 1**, marker catalog. Is there anything real to measure.
- **A Phase 2**, architecture fork. Does the light bulb survive contact with the gait literature.
- **B Phase 2**, data inputs. Is the wearable dependency fatal.
- **B Phase 5**, market and churn. Does the subscription model survive the ten month pregnancy ceiling.

Run those four on `opusplan`. If all four survive, fund the rest on `sonnet`.

---

## STEP 7: THE LOOP

Claude Code Desktop supports scheduled tasks. Once the phase outputs stabilize:

```
Weekly, Monday 6am.
Re check every finding in research/ marked LOW confidence or flagged stale.
Re check pricing, availability, and lifecycle status for every component in the current BOM.
Re check the competitive landscape for funding events, launches, and shutdowns.
Re check FDA and FTC guidance for changes affecting the wellness positioning.
Write research/weekly_delta.md with only what changed. If nothing changed, say so in one line. Commit.
```

Pin that job to `sonnet` explicitly. Check the billing docs first, per Step 2.

The briefs do not change. The world does.

---

## WHY CLAUDE CODE IS ACTUALLY BETTER HERE

You worried it would be worse. It is not, for three reasons:

1. **Git.** Every phase is a commit. You can diff what changed when you corrected an assumption, and you can revert a bad phase without re running the good ones. Cowork has no equivalent.
2. **Subagent model pinning.** The exact thing you were afraid of, a Sonnet research agent spun up on Opus tokens, is a configuration field. Set it once.
3. **`opusplan`.** Reasoning where you need it, cheap execution everywhere else, automatic.

The tradeoff is that it will not open a browser or read your local Office files. This project does not need either.
