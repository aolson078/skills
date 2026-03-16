---
name: meta-meta-kaizen
description: Project-level iterative process-improvement engine that audits, refines, and orchestrates improvement processes across an entire project through structured kaizen-style cycles. Trigger when the user says "meta-meta-kaizen", requests project-wide process audit, or asks to improve an improvement process/skill/workflow.
---

# Meta-Meta-Kaizen: Iterative Process-Improvement Engine

## 1. Purpose

Meta-Meta-Kaizen applies structured, multi-pass kaizen-style improvement to improvement processes themselves. Where Meta-Kaizen loops over an artifact (analyze, improve, evaluate, compare, redirect), Meta-Meta-Kaizen loops over the processes that produce those improvements. It operates at the project level: reading project context, auditing all improvement processes holistically, and orchestrating multi-area improvement recommendations.

Three capabilities:

- **(A) Single-process deep improvement:** Take one improvement process (a CI pipeline, a code review workflow, a testing strategy) and iteratively make it more effective at producing quality.
- **(B) Project-wide holistic audit:** Catalog all improvement processes active in a project, assess their effectiveness, identify gaps and contradictions, and recommend changes across the system.
- **(C) Project-context-aware recommendations:** Ground all analysis in the project's actual conventions, structure, history, and constraints -- not generic best practices.

### Three-Level Hierarchy

| Level | Skill | Operates On | Purpose |
| ----- | ----- | ----------- | ------- |
| L0 | Kaizen | Code and artifacts directly | Philosophy: continuous improvement, poka-yoke, standardized work, JIT |
| L1 | Meta-Kaizen | Any improvable artifact | Execution engine: iterative analyze-improve-evaluate-compare-redirect loops |
| L2 | Meta-Meta-Kaizen | Improvement processes themselves | Process-improvement engine: audits, refines, and orchestrates improvement processes |

L2 is the ceiling. There is no L3. If the user requests improvement of the improvement-of-improvement process, redirect to running Meta-Meta-Kaizen on itself (the canonical self-application case, capped at 3 iterations).

## 2. When to Use

Trigger this skill when the user:

- Says "meta-meta-kaizen" or "run meta-meta-kaizen"
- Asks to audit project-wide improvement processes
- Wants to diagnose why a refinement loop is stalling or producing diminishing returns
- Asks to optimize a skill's, workflow's, or pipeline's effectiveness at producing quality
- Requests coordination of improvement efforts across multiple project areas
- Asks to evaluate how well the project's processes produce quality overall
- Wants to identify which project areas lack improvement processes entirely

Do NOT trigger for:

- Improving a specific artifact (that is Meta-Kaizen, L1)
- Applying kaizen philosophy to code (that is Kaizen, L0)
- One-off code review or refactoring (use standard tools)

## 3. Supported Targets

### Single-Process Mode

Improve one improvement process at a time:

- Refinement skills (Meta-Kaizen itself, code review bots, linting configurations)
- Code review workflows (PR review cadence, reviewer assignment, feedback quality)
- CI/CD quality gates (build checks, test gates, deployment approval processes)
- Testing strategies (what gets tested, how, coverage goals, test maintenance)
- Monitoring and alerting processes (what triggers alerts, escalation paths, incident response)
- Documentation workflows (when docs get written, review cycles, staleness detection)
- Architecture decision processes (ADR workflows, design review cadence, decision authority)
- Onboarding processes (new developer ramp-up, knowledge transfer, mentoring)
- Retrospective practices (how the team reflects, what changes stick, follow-through)

### Project-Wide Mode

Audit all improvement processes as a system. In this mode, the target is not a single process but the entire network of processes and how they interact:

- Which processes exist and how effective each one is
- Where processes reinforce each other (CI catches what code review misses)
- Where processes contradict each other (documentation standards conflict with speed-focused review norms)
- Which project areas have no improvement process at all (orphaned areas)
- Whether the total cost of all processes is justified by their combined output

## 4. Project Context Discovery

Before any iteration, gather context from four essential sources. This grounds all analysis in the project's reality rather than generic advice.

**Source 1 -- Project conventions:** Read `CLAUDE.md` and `CLAUDE.local.md` (if they exist) for coding standards, architectural decisions, and AI collaboration instructions.

**Source 2 -- Project structure:** Quick scan of directory layout -- feature folders, vertical slices, monorepo boundaries, test locations, configuration file locations.

**Source 3 -- CI/test configuration:** Identify linters (ESLint, Prettier, StyleCop), test frameworks (xUnit, Vitest, Playwright), pre-commit hooks, CI pipeline definitions (GitHub Actions, Azure Pipelines), and quality gates.

**Source 4 -- Recent git history:** Last 20 commits -- change patterns, review cadence (time between PR open and merge), merge habits (squash vs. merge commits), who reviews what.

**Additional sources (if available):** Architecture Decision Records (ADRs), retrospective notes, runbooks, changelogs, incident postmortems. Read these only when they exist and are relevant to the current target.

After gathering context, build a **Process Inventory**: a catalog of all active improvement processes in the project, with a one-line description and initial effectiveness assessment for each.

## 5. Input Parsing

Before starting, parse the user's request to extract four parameters:

| Parameter | How to detect | Default |
| --------- | ------------- | ------- |
| **Target** | Process name or "project" for project-wide mode | Required -- ask if unclear |
| **Iteration count** | Explicit number (e.g., "3 times", "5 iterations") | Auto (stop when plateaued) |
| **Effectiveness lens** | Constraint keyword (e.g., "focus on iteration speed", "leverage ratio only") | Unconstrained (full scope) |
| **Area filter** | Scope limiter (e.g., "frontend only", "backend only", "infra only") | All areas (project-wide mode only) |

### Parsing Examples

| User input | Target | Iterations | Lens | Area filter |
| ---------- | ------ | ---------- | ---- | ----------- |
| "Run meta-meta-kaizen on our code review process" | code review process | auto | unconstrained | n/a (single-process) |
| "Run meta-meta-kaizen on this project" | project (project-wide) | auto | unconstrained | all areas |
| "Run meta-meta-kaizen 3 times on our CI pipeline" | CI pipeline | 3 | unconstrained | n/a (single-process) |
| "Run meta-meta-kaizen on the project, backend only" | project (project-wide) | auto | unconstrained | backend |
| "Run meta-meta-kaizen on meta-kaizen itself" | Meta-Kaizen skill (canonical self-application) | auto | unconstrained | n/a (single-process) |

If the target is ambiguous, ask the user to clarify before beginning. If the user says "project" but the project is very large, suggest an area filter or confirm they want the full audit.

## 6. Process Effectiveness Metrics

Assess improvement processes using these heuristic metrics. These are observational judgments, not quantitative measurements -- assess them as Strong / Adequate / Weak / Absent based on available evidence.

### Per-Process Metrics (apply in both modes)

**Leverage Ratio** -- How much improvement does one iteration of this process produce?

- Strong: Each cycle produces visible, measurable quality gains
- Weak: Process runs but artifacts barely improve between cycles

**Iteration Efficiency** -- What fraction of process effort produces substantive change vs. overhead?

- Strong: Most time spent on actual improvement; minimal ceremony
- Weak: Heavy on meetings, templates, approvals; light on actual improvement

**Plateau Speed** -- How quickly does this process hit diminishing returns?

- Strong: Continues producing meaningful gains across many iterations
- Weak: First pass helps, subsequent passes are cosmetic

**False-Progress Detection Rate** -- Does this process catch cosmetic or lateral changes that look like improvement but aren't?

- Strong: Process explicitly distinguishes substantive from cosmetic change
- Weak: Process counts any change as progress; no quality gate on the improvement itself

**Scope Discipline** -- Does this process stay focused on its intended target?

- Strong: Clear boundaries; process knows what it improves and what it doesn't
- Weak: Scope creep; process tries to fix everything and fixes nothing well

**Stopping Calibration** -- Does this process stop at the right time?

- Strong: Stops when further effort would not justify the cost; neither too early nor too late
- Weak: Either stops before meaningful improvement or grinds on past diminishing returns

### Project-Wide Metrics (apply only in project-wide mode)

**Cross-Process Coherence** -- Do improvement processes reinforce or contradict each other?

- Strong: Processes form a coherent system; what one catches, another reinforces
- Weak: Processes work at cross-purposes; one undoes what another builds

**Coverage Gap Score** -- Which project areas lack improvement processes?

- Strong: Every area that produces quality-sensitive output has at least one improvement process
- Weak: Significant areas (security, documentation, onboarding) have no improvement process at all

## 7. Execution Protocol

### Phase 0: Process Baseline

Before the first iteration:

1. **Run Project Context Discovery** (Section 4). Read the four essential sources and any available additional sources.
2. **Build the Process Inventory:**
   - In **project-wide mode**: Catalog every active improvement process. For each, note: name, what it improves, how often it runs, who owns it, and initial assessment on all 8 metrics. Identify cross-process interactions (reinforcement, contradiction, gaps).
   - In **single-process mode**: Understand the target process fully. Mentally simulate running it on a representative target. Assess it on the 6 per-process metrics.
3. **State the baseline assessment** before starting iteration 1. In project-wide mode, present the Process Inventory as a table.

### Phase 1: Process Iteration Loop

For each iteration, execute all seven steps in order:

#### Step 1 -- Analyze Current Process Effectiveness

Examine the process (or process system) as it stands now -- not the original, the latest version after any prior iterations. In project-wide mode, analyze the system of processes, not just individual ones. Look for: effectiveness gaps, structural flaws, wasted effort, missing feedback loops, contradictions between processes.

#### Step 2 -- Identify Highest-Leverage Process Weakness

From all weaknesses found, select the single one where improvement would produce the most meaningful gain. Priority order:

1. **Structural flaws** -- the process is fundamentally broken or missing
2. **Targeting failures** -- the process improves the wrong things
3. **Evaluation blindness** -- the process cannot tell whether it is working
4. **Stopping miscalibration** -- the process stops too early or too late
5. **Iteration overhead** -- the process costs more than it produces
6. **Scope drift** -- the process wanders from its purpose
7. *(Project-wide only)* **Cross-process gaps** -- redundant, contradictory, or missing processes

Do NOT select cosmetic process issues (renaming steps, reformatting templates) when structural ones remain.

#### Step 3 -- Apply Process Improvements

Make the changes to the process design itself. This may involve:

- Modifying a single process's steps, triggers, or evaluation criteria
- Adding a feedback loop that was missing
- Removing a redundant checkpoint that adds overhead without catching problems
- In project-wide mode: adding a missing process, removing a redundant one, or rewiring how two processes connect

Changes must be substantive -- not relabeling steps, not adding ceremony. Each change should be something that would alter the process's behavior when next executed.

#### Step 4 -- Critical Review

After applying changes, review with fresh eyes:

- Does the process now produce better improvements, or just different ones?
- Is the improved process measurably more effective than the previous version?
- Did the change introduce new overhead, complexity, or failure modes?
- *(Self-check)* Does the improved process have the very flaw it is supposed to detect? (Anti-pattern 8)

#### Step 5 -- Compare Process Versions

Explicitly state what improved and what (if anything) regressed compared to the prior iteration. Use the metrics from Section 6. Be honest -- if the change was minor, say so.

#### Step 6 -- Progress Assessment

Classify the iteration's impact on process effectiveness:

- **Major**: Structural process improvement, fundamental redesign, significant capability added to the process
- **Moderate**: Meaningful refinement that noticeably improves how the process produces quality
- **Minor**: Small process polish, marginal gains in one metric
- **Negligible**: Essentially cosmetic process change, no real advancement in effectiveness

#### Step 7 -- Choose Next Direction

Based on the current state, deliberately select what the next iteration should target. In project-wide mode, this may mean switching to a different process area. Do not repeat the same critique without new action. Do not drift aimlessly.

### Phase 2: Stopping

Stop the loop when any of these conditions is true:

1. **Requested count reached**: The user specified N iterations and N have been completed.
2. **Process plateau**: The last 2 consecutive iterations produced Minor or Negligible impact.
3. **Diminishing process returns**: Remaining weaknesses are primarily cosmetic or procedural.
4. **Substantial process completion**: The process (or process system) has reached an effectiveness level where further passes would yield limited additional value.
5. **Meta-plateau**: The improvement rate of the improvement rate has stabilized (second derivative). Each iteration still produces Minor impact, but the trajectory is flat -- no acceleration, no new categories of improvement being discovered.

When stopping on auto-mode, state which condition triggered and why.

## 8. Project-Wide Recommendations

This section applies only in project-wide mode. After building the Process Inventory and completing iterations:

**Priority ranking:** Rank project areas by improvement-process quality, worst first. Areas with no improvement process rank below areas with a weak one.

**Meta-Kaizen run recommendations:** For each area that would benefit, recommend a specific Meta-Kaizen invocation:

- What to target (the specific artifact or artifact class)
- Suggested iteration count
- Suggested focus area
- Expected leverage (why this run would produce meaningful improvement)

**Cross-area dependency tracking:** Document which processes feed into which:

- Example: "Backend API test coverage process feeds frontend integration test confidence"
- Example: "Architecture decision process outputs feed CI pipeline configuration"
- Identify broken links: processes that should feed each other but don't

**Orphaned area identification:** List project areas with no improvement process. For each:

- What kind of process would help
- How critical the gap is (regulatory risk > user-facing impact > developer velocity)
- Suggested starting point (minimal viable process)

**Cost-benefit assessment:** Is the total process overhead justified? Are there processes that cost more than they produce? Recommend removal or simplification where warranted.

## 9. Output Format

### Per-Iteration Output

```markdown
## Process Iteration [N]

**Process focus:** [Which process or process-system aspect this round targets]

**Changes made:**
[Concrete description of process design changes -- what was modified, added, removed, or rewired]

**Effectiveness metrics:**
| Metric | Before | After | Direction |
| ------ | ------ | ----- | --------- |
| [relevant metrics only] | ... | ... | improved/unchanged/regressed |

**Self-critique:**
[Did the process actually improve, or just change? Does the improved process have any of the flaws it should detect?]

**Impact:** [Major | Moderate | Minor | Negligible]

**Remaining weaknesses:**
[Ordered by leverage, with brief rationale for ordering]

**Next target:**
[What the next iteration will address and why it is the highest-leverage remaining weakness]
```

### Final Summary Output

```markdown
## Meta-Meta-Kaizen Summary

**Iterations completed:** [N]
**Stop reason:** [Which stopping condition triggered and why]
**Mode:** [Single-process | Project-wide]

**Metric trajectory:**
| Metric | Baseline | Final | Trend |
| ------ | -------- | ----- | ----- |
| [each relevant metric] | Strong/Adequate/Weak/Absent | ... | improved/stable/regressed |

**Process Inventory (project-wide mode only):**
| Area | Process | Before | After | Recommendation |
| ---- | ------- | ------ | ----- | -------------- |
| [project area] | [process name] | [baseline assessment] | [final assessment] | [next step] |

**Cross-process interaction map (project-wide mode only):**
- [Process A] -> feeds -> [Process B]: [status: healthy/broken/missing]
- [...]

**Coverage gap analysis:**
- [Orphaned area]: [recommended process] ([priority: critical/important/nice-to-have])
- [...]

**Key improvements across all passes:**
1. [Most impactful improvement]
2. [Second most impactful]
3. [...]

**Rationale for stopping:**
[Why further iteration would not produce meaningful gains at the process level]
```

## 10. Anti-Patterns

These behaviors constitute fake progress at the process level. Actively guard against them:

1. **Process-cosmetic counting** -- Renaming process steps, reformatting templates, or reorganizing documentation is not process improvement. Detect: the process would behave identically if executed. Instead: change something that alters process behavior or output quality.

2. **Indicator gaming** -- Optimizing the metrics in Section 6 instead of actual process quality. Detect: metrics improve but the process's actual output hasn't changed. Instead: use metrics as signals, not targets; always verify by mentally simulating the process on a real target.

3. **Abstraction escape** -- Dropping from process level (L2) to artifact level (L1) mid-iteration. Detect: you find yourself editing code, refactoring components, or improving a specific document instead of improving the process that produces them. Instead: stay at the process level; note the artifact-level issue as evidence of a process weakness.

4. **Process overfitting** -- The improved process works well for the one target you tested it against but would fail on different targets. Detect: improvements are highly specific to one context. Instead: mentally simulate the process on 2-3 different targets before declaring improvement.

5. **Infinite regress temptation** -- Wanting to create L3 (a process for improving the process that improves improvement processes). Detect: you feel the urge to go "one level higher." Instead: redirect to running Meta-Meta-Kaizen on itself (self-application, capped at 3 iterations). L2 is the ceiling.

6. **Cargo-cult phasing** -- Adding more steps, phases, or checkpoints to a process without evidence that additional structure produces better outcomes. Detect: process has more steps after improvement but no evidence of better output. Instead: fewer, better steps; measure by output quality, not step count.

7. **Critique recycling at process level** -- Identifying the same process weakness in consecutive iterations without making a new attempt to address it. Detect: the weakness list looks the same as last iteration. Instead: either try a different approach to the same weakness or acknowledge it as a constraint and move on.

8. **False-progress acceptance** -- The process has the very flaw it is supposed to detect. Detect: the code review process has unclear acceptance criteria; the testing strategy has no test for the testing strategy's own assumptions. Instead: apply the process's own standards to the process itself as a litmus test.

9. **Silo optimization** -- Improving one process in isolation while degrading cross-process coherence. Detect: one process got better but now contradicts or duplicates another. Instead: in project-wide mode, always check cross-process coherence after modifying any single process. In single-process mode, note potential cross-process impacts.

## 11. Edge Cases

1. **Already highly effective process**: State this in the baseline. Perform 1-2 iterations focusing on minor refinement. Stop early with explanation. Do not manufacture weaknesses to justify more iterations.

2. **Fundamentally broken process**: State this in the baseline. First iteration must address the foundational problem (wrong target, missing feedback loop, no stopping criteria) before any refinement.

3. **Target is Meta-Kaizen itself**: This is the canonical demonstration case. Run normally -- analyze Meta-Kaizen's iteration loop for effectiveness, identify where it produces the most and least improvement, and suggest process-level changes. Document this as an example for future users.

4. **Informal or undocumented process**: Before iterating, formalize the process by writing down what actually happens (not what should happen). Use git history and project artifacts as evidence. Then improve the formalized version.

5. **User changes scope mid-run**: Acknowledge the redirect. Re-baseline from current state with new scope. Continue iterations with new target. Do not retroactively reinterpret prior iterations.

6. **Improvement introduces overhead exceeding benefit**: Flag immediately. Revert the process change. Note the overhead constraint as a boundary condition for future iterations. Prefer simplification over elaboration.

7. **Recursive self-application (Meta-Meta-Kaizen on Meta-Meta-Kaizen)**: Run normally but cap at 3 iterations. After 3 iterations, state: "L2 self-application complete. Further meta-levels produce diminishing returns that do not justify the abstraction cost." Do not create L3.

8. **Greenfield project (no existing improvement processes)**: Skip the audit phase. Instead, bootstrap a minimal Process Inventory by reading the project structure and conventions, then recommend which improvement processes to create first. Priority: testing strategy > CI quality gates > code review workflow > documentation. Each recommendation should be a minimal viable process, not a comprehensive framework.

9. **Massive project (too many areas to audit)**: Triage by impact: regulatory risk > user-facing impact > development velocity. Audit the top 3-5 areas in depth. For remaining areas, provide a one-line assessment and defer to future runs. If the user provided an area filter, respect it and only audit the filtered scope.

## 12. Interaction with Existing Skills

### Three-Level Hierarchy

| Level | Skill | What It Improves | How It Uses the Level Below |
| ----- | ----- | ---------------- | --------------------------- |
| L0 | Kaizen | Code quality directly | -- (foundation) |
| L1 | Meta-Kaizen | Any artifact iteratively | Applies Kaizen philosophy within each iteration |
| L2 | Meta-Meta-Kaizen | Improvement processes | Uses Meta-Kaizen's loop structure as the template for process iteration |

**L2 is the ceiling.** Rationale: each meta-level produces diminishing returns on the abstraction investment. L0 provides philosophy. L1 operationalizes it into a reusable loop. L2 ensures the loop itself is effective and coordinates across a project. L3 would be "improving the process of improving the process of improving processes" -- the abstraction cost exceeds the improvement yield. Self-application at L2 (edge case 7) covers the same ground without adding a new skill.

### How Meta-Meta-Kaizen Uses Lower Levels

**From Kaizen (L0):**

- Apply **Continuous Improvement** principle: small process changes, verified individually
- Apply **Poka-Yoke** thinking: design processes that make bad improvements impossible (e.g., a code review process that structurally prevents rubber-stamping)
- Apply **Standardized Work**: follow established process patterns before inventing new ones
- Apply **JIT**: do not add speculative process steps; do not build process frameworks before proving they are needed
- Apply **"Good enough today, better tomorrow"** to process stopping: do not pursue process perfection

**From Meta-Kaizen (L1):**

- The 7-step iteration loop (analyze, identify weakness, improve, review, compare, assess, redirect) is the structural template for process iteration at L2
- The 4 stopping conditions (count, plateau, diminishing returns, completion) are inherited and extended with meta-plateau (condition 5)
- The priority ordering (structural > strategic > functional > clarity > performance > polish) is elevated to process-level equivalents
- The output format (per-iteration + final summary) is inherited and extended with process-specific metrics and project-wide tables
