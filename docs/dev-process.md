# Software Development Process

## Task Size (decide first)
- **Small** (bug fix, tweak, question): skip Stages 1–3. Implement with MUST FOLLOW, Definition of Done, and tests.
- **Medium** (feature within the existing design): short Explore, then a short markdown plan. No HTML design doc or mockups.
- **Large** (new system or major change): run all four stages.
- If the size is unclear, state your call and ask the stakeholder.

## Stage 1: Explore
1. Clarify the requirement; ask if unclear or insufficient.
2. Research options, compare pros/cons and feasibility, recommend one.
3. Record measurable acceptance criteria. Revise until approved.

### Stage 1a: Spikes (optional, when the stakeholder asks)
1. One spike per open question or option, each in its own thread; independent spikes run in parallel.
2. Keep it lightweight: a throwaway prototype or experiment that answers one question, time-boxed, on a scratch branch or folder, never merged.
3. Spikes skip Stages 2–4: no design doc, plan, phases, PR, or full test suite.
4. Each spike reports back briefly: question, what was tried, evidence, verdict (works / doesn't / partly), and the recommendation it supports.
5. Feed the spike results into step 2 of Stage 1 before the stakeholder approves an approach.

## Stage 2: Design & Mockup (large tasks only)
1. Write an HTML design doc with diagrams: overview, approach, high- and low-level design, usage, troubleshooting. Embed hidden AI-readable notes.
2. After approval, build HTML UI mockups. Feed new requirements back into the design doc.

## Stage 3: Planning
1. Write a phased plan (markdown for medium tasks); each phase executable, testable, traceable, with its own done criteria derived from the acceptance criteria.
2. For each phase, list its prerequisites (`depends on: P1, P2`) and the files or components it touches.
3. Group phases into waves: a wave holds phases whose prerequisites are all in earlier waves. Phases in the same wave may run in parallel only if they don't touch the same files; otherwise split them into sequential waves.
4. Show the dependency order as a short table or diagram, and mark the critical path.

## Stage 4: Implementation
1. Confirm which phases or waves to work on; work on a new feature branch.
2. Start a phase only when all its prerequisites meet their Definition of Done.
3. Run phases of the same wave in parallel (separate sub-agents, each on its own branch or worktree). Per phase: implement, run its tests, commit when Definition of Done is met.
4. After each wave: merge its phases into the feature branch, resolve conflicts, and run the tests of all phases completed so far before starting the next wave.
5. If a phase fails or is blocked, pause only the phases that depend on it; keep independent phases going.
6. After all waves: full test suite, check acceptance criteria, update docs, open a PR.
7. Review for improvements, tech debt, and security; ask the stakeholder to fold them into a phase or add them to a later checklist.

## Definition of Done (per phase)
- Meets the phase's done criteria in the implementation plan.
- Code builds.
- Tests pass.
- Docs are updated.
- The change is committed.

## Implementation Rules
- **Closed-loop testing**: implementation must produce inputs and outputs that test cases validate automatically, with no manual stakeholder intervention.
- **Test samples**: create test data for every testable behavior.
- **Security**: apply relevant, feasible standard security measures (input validation, least privilege, safe secret handling, no injection risks).
- **Coding standards**: follow standard conventions and principles.

## Prefer closed-loop pipelines
Automate the loop end to end (build, test, verify, fix) with minimal human input.
Humans step in only for approvals and irreversible actions.