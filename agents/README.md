# Studio agent workflow

Reusable roles extracted and generalized from the Totonia agent setup on 2026-10-18. These files are reference templates, not an automatically enabled runtime configuration. A project's owner chooses its agent runtime, permissions and tool names.

## Roles

| Role | Display name | Responsibility | Boundary |
|---|---|---|---|
| Coordinator | Pol | Scope, dispatch, validation evidence and final report | Project owner retains creative and release decisions |
| Programmer | Pepe | Implement the requested change and build | Does not approve its own implementation |
| QA | Nina | Independent diff review, regression checks and screenshots | Reports findings; does not fix source |
| Game designer | Lala | Player experience, pacing and evidence-backed recommendations | Does not change code, art or approved design |

Profiles: [programmer](profiles/programmer.md), [QA](profiles/qa.md), [game designer](profiles/game-designer.md).

## Workflow

1. Read the task and the relevant project design, maintenance and coding documents. Search only what is needed.
2. Keep the change small. The programmer implements and builds using that project's official entry point.
3. Verify that build metadata and artifact checksums correspond to the reviewed code and working-tree state.
4. QA independently reviews the diff, runs the appropriate regressions and inspects relevant screenshots.
5. For changes affecting play, request a design review after technical QA. Preserve review evidence without overwriting historical reports.
6. Resolve concrete findings, then create reviewable commits or PRs and report the actual validation and remaining risks.

Prefix delegated task descriptions with the visible name, e.g. `Pepe: fix intro`. Keep titles short. Delegation must follow the user's authorization and the active tool's policies; these templates do not grant access or override those policies.

Documentation-only changes can bypass implementation/design delegation when they do not change behavior and the relevant build inputs are unchanged. For reproducible refactors, compare baseline and proposed artifact checksums for every supported target. Keep one build per checkout; use isolated worktrees for independent builds.

## Project boundaries

Project-specific build commands, hardware budgets, art rules, gameplay decisions, test coverage and historical design reviews belong in the game repository. Do not copy private project source, art, hostnames, addresses, session state, home-directory paths, local environment files, secrets or credentials into this public studio repository.

When adopting the templates, configure local tool permissions explicitly. Keep environment settings outside version control, use placeholders in examples, and review the entire staged diff for sensitive content before publication.

## Migration record

The reusable content came from Totonia's former `CLAUDE.md`, `.claude/agents/{programmer,qa,game-designer}.md`, the workflow section of `docs/CODING_STANDARDS.md` and ADR-001 §3. It was rewritten as studio templates rather than copied wholesale: obsolete task-specific delegation, machine configuration, local paths and internal operational details were excluded. Build/test/hardware knowledge remains in Totonia's `docs/MAINTENANCE.md`. Game decisions and evidence remain in Totonia.

Merge this studio PR before merging the paired Totonia cleanup PR, so the receiving documentation exists before the old configuration is removed from the game branch. No commit history is rewritten.
