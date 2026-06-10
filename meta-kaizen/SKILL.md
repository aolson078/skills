---
name: meta-kaizen
description: Iterative multi-pass refinement engine that repeatedly analyzes, improves, verifies, and redirects any target (prompts, pages, components, systems, architecture, UX, docs, workflows) through structured kaizen-style improvement cycles with rubric-based scoring until a meaningful quality threshold is reached or the requested iteration count is completed. Trigger when the user says "meta-kaizen", "run meta-kaizen", or asks for iterative/multi-pass refinement on any artifact.
---

# Meta-Kaizen: Iterative Self-Improving Refinement Engine

## Purpose

Meta-Kaizen applies structured, multi-pass kaizen-style improvement to any user-specified target. Unlike single-pass review, Meta-Kaizen loops: analyze, identify the highest-leverage weakness, improve, verify, compare, then decide the next direction. It continues until real progress plateaus or the requested number of iterations completes.

Two design principles distinguish it from "just keep editing":

1. **Evidence over impression.** Every run defines an explicit evaluation rubric at baseline and re-scores it every iteration. Claims of improvement must be backed by the scorecard and, for code, by objective verification (tests, builds, linters).
2. **Recoverability.** Every iteration's previous version remains recoverable. A regression is reverted, not papered over.

## When to Use

Trigger this skill when the user:
- Says "meta-kaizen" or "run meta-kaizen"
- Asks for iterative, multi-pass, or repeated refinement on any artifact
- Requests continuous improvement cycles on a specific target

Do NOT trigger for:
- Improving an improvement process itself (that is Meta-Meta-Kaizen, L2)
- A one-off review with no changes requested (use standard review)

## Supported Targets

Meta-Kaizen operates on any improvable artifact:
- Prompts and prompt chains
- Landing pages, marketing copy, CTAs
- Front-end components, pages, layouts
- Back-end systems, APIs, data flows
- App flows, user journeys, onboarding
- Architecture, system design, infrastructure
- UX patterns, accessibility, interaction design
- Monitoring, logging, observability setups
- Product concepts, feature specs, PRDs
- Documentation, READMEs, guides
- Any page, section, feature, file, or workflow

## Input Parsing

Before starting, parse the user's request to extract three parameters:

| Parameter | How to detect | Default |
|---|---|---|
| **Target** | The object, file, section, or concept being improved | Required -- ask if unclear |
| **Iteration count** | Explicit number (e.g., "3 times", "5 iterations") | Auto (stop when plateaued, hard cap 5) |
| **Focus area** | Constraint keyword (e.g., "front-end only", "focus on monitoring", "UX only") | Unconstrained (full scope) |

### Parsing examples

| User input | Target | Iterations | Focus |
|---|---|---|---|
| "Run Meta-Kaizen on this landing page" | landing page | auto | unconstrained |
| "Run Meta-Kaizen 3 times on this prompt" | prompt | 3 | unconstrained |
| "Run Meta-Kaizen on the front-end only" | current project | auto | front-end |
| "Run Meta-Kaizen 5 times on the back-end" | current project back-end | 5 | back-end |
| "Run Meta-Kaizen on this feature with focus on monitoring" | feature | auto | monitoring |

If the target is ambiguous, ask the user to clarify before beginning.

## Execution Protocol

### Phase 0: Baseline

Before the first iteration:

1. **Understand the target.** Read its current state fully. For code targets, read the actual files. For text/concept targets, read or receive the content. Establish what exists, what works, and what the intent appears to be.
2. **Define the evaluation rubric.** Choose 3-6 criteria appropriate to the target type, each scored 1-10. Examples:
   - Prompt: clarity of instruction, coverage of edge cases, output-format specificity, robustness to misreading
   - Landing page: message clarity, CTA strength, visual hierarchy, credibility signals
   - Code/component: correctness, structure/cohesion, error handling, readability, test coverage
   - Documentation: accuracy, completeness, findability, example quality
   The rubric is fixed for the duration of the run. Do not add, remove, or reweight criteria mid-run (that invites score gaming); if the rubric proves wrong, say so explicitly and restart the baseline.
3. **Record the baseline scorecard.** Score each criterion honestly, with a one-line justification per score. These justifications are what keep later scores honest.
4. **Identify verification commands** (code targets only). Find the project's existing tests, build, linters, or type checks. Run them once to confirm the baseline passes (or document pre-existing failures so they are not attributed to your changes).
5. **Ensure recoverability.** For files in a git repository, note the starting state (`git status` / `git diff`) so every iteration can be diffed and reverted against it. For untracked or non-file targets, retain each prior version verbatim before producing the next.
6. **Apply the focus area.** If specified, scope all subsequent analysis to that area unless the user explicitly requests broader optimization.
7. **State the baseline assessment** -- including the rubric and baseline scorecard -- before starting iteration 1.

### Phase 1: Iteration Loop

For each iteration, execute all of the following steps in order:

#### Step 1 -- Analyze Current State
Examine the target as it stands right now (not the original -- the latest version). Identify strengths and weaknesses. For code, read the actual current file contents.

#### Step 2 -- Identify Highest-Leverage Weakness
From all weaknesses found, select the single one where improvement would produce the most meaningful gain. Prioritize:
1. Structural or architectural problems
2. Strategic misalignment (wrong approach, missing the point)
3. Functional gaps (missing capability, broken logic)
4. Clarity and communication failures
5. Performance or efficiency issues
6. Polish and presentation

Do NOT select cosmetic issues when structural ones remain.

#### Step 3 -- Apply Improvements
Make the changes. For code targets, edit the actual files. For text/concept targets, produce the revised version. Changes must be substantive -- not rephrasing, not cosmetic shuffling.

#### Step 4 -- Verify and Critically Review
Verification comes before opinion:

1. **Objective verification (code targets):** Run the verification commands identified in Phase 0. A failing check that passed before is a regression -- go directly to the regression rule below. Never report an iteration as an improvement while verification is failing.
2. **Fresh-eyes critique:** Review the result as if seeing it for the first time. Ask:
   - Did this actually improve the target, or just change it?
   - Is the new version measurably better than the previous version?
   - Did the change introduce any new problems?
3. **Independent review (when available):** If subagent delegation is available, hand the current version plus the rubric -- and nothing else, not the iteration history or your rationale -- to a fresh-context reviewer and ask it to score and critique. An independent reviewer cannot be anchored by your intentions, which counters self-confirmation bias. Reconcile any large gap between its scores and yours before proceeding.

#### Step 5 -- Compare Against Previous Version
Re-score the full rubric and present the delta against the previous iteration's scorecard. Every score change needs a one-line justification grounded in a concrete change. Explicitly state what improved and what (if anything) regressed. Be honest -- if the change was minor, say so, and score it accordingly.

**Regression rule:** If verification fails, or the total rubric score drops, revert to the previous version (via git or the retained copy), record the iteration as a regression with the reason, and choose a different direction in Step 7. A reverted iteration still counts toward the iteration count and the hard cap.

#### Step 6 -- Progress Assessment
Classify the iteration's impact, consistent with the scorecard delta:
- **Major**: Structural improvement, strategic redirect, significant capability added
- **Moderate**: Meaningful refinement that noticeably improves quality
- **Minor**: Small polish, marginal gains
- **Negligible**: Essentially cosmetic, no real advancement

An iteration whose scorecard barely moved cannot be classified Major or Moderate, no matter how much effort it took.

#### Step 7 -- Choose Next Direction
Based on the current state, deliberately select what the next iteration should target. Do not repeat the same critique without new action. Do not drift aimlessly. After a regression, the next direction must differ from the approach that failed.

### Phase 2: Stopping

Stop the loop when any of the following conditions is true:

1. **Requested count reached**: The user specified N iterations and N have been completed.
2. **Plateau detected**: The last 2 consecutive iterations produced Minor or Negligible impact (equivalently: the total rubric score barely moved across both).
3. **Diminishing returns**: Remaining weaknesses are primarily cosmetic or stylistic.
4. **Substantial completion**: The target has reached a quality level where further passes would yield limited additional value.
5. **Hard cap (auto mode)**: 5 iterations have completed without an explicit user-requested count. Offer to continue if meaningful weaknesses remain, but do not continue unprompted.
6. **Regression loop**: 2 consecutive iterations were reverted. The current approach is not working; stop and report what was tried and why it failed rather than thrashing.

When stopping on auto-mode (no explicit count), state which stopping condition triggered and why.

## Output Format

### Per-Iteration Output

For each iteration, output the following structure:

```
## Iteration [N]

**Focus:** [What this round targets]

**Changes made:**
[Concrete description of what was changed and how]

**Why these changes matter:**
[The leverage -- why this particular change produces meaningful improvement]

**Verification:** [Checks run and results, or "n/a (non-code target)"]

**Scorecard:**
| Criterion | Previous | Current | Justification for change |
|---|---|---|---|
| [criterion] | n/10 | n/10 | [one line, or "unchanged"] |

**Self-critique:**
[Honest assessment of whether the changes achieved their goal]

**Impact:** [Major | Moderate | Minor | Negligible | Reverted (regression)]

**Remaining weaknesses:**
[What still needs work, ordered by leverage]

**Next target:**
[What the next iteration will address and why]
```

### Final Output

After the last iteration, output:

```
## Meta-Kaizen Summary

**Iterations completed:** [N] ([R] reverted, if any)
**Stop reason:** [Which stopping condition triggered]

**Score trajectory:**
| Criterion | Baseline | Final | Net change |
|---|---|---|---|
| [criterion] | n/10 | n/10 | +/-n |
| **Total** | n | n | +/-n |

**Key improvements across all passes:**
- [Improvement 1]
- [Improvement 2]
- [...]

**Final state:**
[The final refined version, or a pointer to the edited files]

**Rationale for stopping:**
[Brief explanation of why further iteration would not produce meaningful gains]
```

## Anti-Patterns to Avoid

These behaviors constitute fake progress. Actively guard against them:

- **Rephrasing without restructuring**: Moving words around is not improvement.
- **Cosmetic counting**: Do not count formatting, whitespace, or naming tweaks as Major or Moderate impact.
- **Self-grading inflation**: Scores drifting upward each iteration without scorecard justifications that name a concrete change. The justification column exists precisely to catch this; an unjustifiable score change is a fabricated one.
- **Verification skipping**: Declaring a code iteration an improvement without running the Phase 0 verification commands. "It should still pass" is not verification.
- **Rubric gaming**: Adding, dropping, or reweighting rubric criteria mid-run so the numbers look better. The rubric is fixed at baseline.
- **Critique recycling**: Do not identify the same weakness in consecutive iterations without making a new attempt to address it.
- **Scope inflation**: Do not expand beyond the user's specified focus area without explicit permission.
- **Perfection paralysis**: Do not continue iterating on diminishing returns. "Good enough and getting better" beats "still polishing."
- **Passive observation**: Each iteration must produce changes, not just commentary. Analysis without action is not an iteration.
- **Regression denial**: Keeping a change that made verification fail or scores drop because reverting feels like wasted work. Revert fast; the retained version is one command away.

## Interaction with Related Skills

Meta-Kaizen is the L1 execution engine in a three-level hierarchy:

| Level | Skill | Operates on |
|---|---|---|
| L0 | Kaizen | Code and artifacts directly (philosophy: continuous improvement, poka-yoke, JIT) |
| L1 | Meta-Kaizen (this skill) | Any improvable artifact, iteratively |
| L2 | Meta-Meta-Kaizen | Improvement processes themselves, including this skill |

When running Meta-Kaizen, apply L0 principles within each iteration (where the Kaizen skill is installed, defer to its phrasing; otherwise these summaries suffice):
- Incremental over revolutionary: one weakness per iteration, verified before moving on
- Prioritization: critical > important > nice-to-have
- "Good enough today, better tomorrow" as the stopping mindset
- Poka-Yoke thinking when improving error handling or validation
- JIT thinking: do not add speculative improvements

If the user asks to improve Meta-Kaizen itself or any other improvement process, escalate to Meta-Meta-Kaizen (L2) rather than running this skill on its own definition.

## Edge Cases

- **Target is already high quality**: State this in the baseline (the baseline scorecard will show it). Perform 1-2 iterations focusing on polish. Stop early with explanation. Do not manufacture weaknesses to justify more iterations.
- **Target is fundamentally flawed**: State this in the baseline. First iteration should address the foundational problem before any refinement.
- **No verification available** (code target with no tests, build, or linter): Proceed in judgment-only mode -- the rubric is the only evaluation instrument. Say so explicitly, flag reduced confidence in the final summary, and recommend adding verification as a follow-up.
- **Very large target** (whole codebase, long document): Do not spread one iteration thinly across everything. Break into logical sections, baseline only the highest-leverage section, complete its run, then offer the next section as a fresh run.
- **User changes scope mid-run**: Acknowledge the redirect, re-baseline (including a fresh rubric) from current state, continue with new scope.
- **Mixed targets** (e.g., "the whole page"): Break into logical sections, address the highest-leverage section first, then move to the next.
