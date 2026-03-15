---
name: meta-kaizen
description: Iterative multi-pass refinement engine that repeatedly analyzes, improves, evaluates, and redirects any target (prompts, pages, components, systems, architecture, UX, docs, workflows) through structured kaizen-style improvement cycles until a meaningful quality threshold is reached or the requested iteration count is completed. Trigger when the user says "meta-kaizen", "run meta-kaizen", or asks for iterative/multi-pass refinement on any artifact.
---

# Meta-Kaizen: Iterative Self-Improving Refinement Engine

## Purpose

Meta-Kaizen applies structured, multi-pass kaizen-style improvement to any user-specified target. Unlike single-pass review, Meta-Kaizen loops: analyze, identify the highest-leverage weakness, improve, evaluate, compare, then decide the next direction. It continues until real progress plateaus or the requested number of iterations completes.

## When to Use

Trigger this skill when the user:
- Says "meta-kaizen" or "run meta-kaizen"
- Asks for iterative, multi-pass, or repeated refinement on any artifact
- Requests continuous improvement cycles on a specific target

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
| **Iteration count** | Explicit number (e.g., "3 times", "5 iterations") | Auto (stop when plateaued) |
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

1. Read and fully understand the current state of the target. For code targets, read the actual files. For text/concept targets, read or receive the content.
2. Establish a mental baseline: what exists, what works, what the intent appears to be.
3. If a focus area is specified, scope all subsequent analysis to that area unless the user explicitly requests broader optimization.
4. State the baseline assessment briefly before starting iteration 1.

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

#### Step 4 -- Critical Review
After applying changes, review the result with fresh eyes. Ask:
- Did this actually improve the target, or just change it?
- Is the new version measurably better than the previous version?
- Did the change introduce any new problems?

#### Step 5 -- Compare Against Previous Version
Explicitly state what improved and what (if anything) regressed compared to the prior iteration. Be honest. If the change was minor, say so.

#### Step 6 -- Progress Assessment
Classify the iteration's impact:
- **Major**: Structural improvement, strategic redirect, significant capability added
- **Moderate**: Meaningful refinement that noticeably improves quality
- **Minor**: Small polish, marginal gains
- **Negligible**: Essentially cosmetic, no real advancement

#### Step 7 -- Choose Next Direction
Based on the current state, deliberately select what the next iteration should target. Do not repeat the same critique without new action. Do not drift aimlessly.

### Phase 2: Stopping

Stop the loop when any of the following conditions is true:

1. **Requested count reached**: The user specified N iterations and N have been completed.
2. **Plateau detected**: The last 2 consecutive iterations produced Minor or Negligible impact.
3. **Diminishing returns**: Remaining weaknesses are primarily cosmetic or stylistic.
4. **Substantial completion**: The target has reached a quality level where further passes would yield limited additional value.

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

**Self-critique:**
[Honest assessment of whether the changes achieved their goal]

**Impact:** [Major | Moderate | Minor | Negligible]

**Remaining weaknesses:**
[What still needs work, ordered by leverage]

**Next target:**
[What the next iteration will address and why]
```

### Final Output

After the last iteration, output:

```
## Meta-Kaizen Summary

**Iterations completed:** [N]
**Stop reason:** [Which stopping condition triggered]

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
- **Critique recycling**: Do not identify the same weakness in consecutive iterations without making a new attempt to address it.
- **Scope inflation**: Do not expand beyond the user's specified focus area without explicit permission.
- **Perfection paralysis**: Do not continue iterating on diminishing returns. "Good enough and getting better" beats "still polishing."
- **Passive observation**: Each iteration must produce changes, not just commentary. Analysis without action is not an iteration.

## Interaction with Existing Kaizen Skill

Meta-Kaizen is the execution engine. The Kaizen skill provides philosophy and principles. When running Meta-Kaizen:
- Apply Kaizen's "incremental over revolutionary" principle within each iteration
- Follow Kaizen's prioritization: critical > important > nice-to-have
- Respect Kaizen's "good enough today, better tomorrow" stopping mindset
- Use Poka-Yoke thinking when improving error handling or validation
- Apply JIT thinking: do not add speculative improvements

## Edge Cases

- **Target is already high quality**: State this in the baseline. Perform 1-2 iterations focusing on polish. Stop early with explanation.
- **Target is fundamentally flawed**: State this in the baseline. First iteration should address the foundational problem before any refinement.
- **User changes scope mid-run**: Acknowledge the redirect, re-baseline from current state, continue with new scope.
- **Mixed targets** (e.g., "the whole page"): Break into logical sections, address the highest-leverage section first, then move to the next.
