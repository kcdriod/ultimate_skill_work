---
name: graph-engineering
description: Orchestrate any local software-engineering task in VS Code
  GitHub Copilot Agent Mode with proportionate dependency graphs,
  task-driven subagents, evidence-based validation, bounded recovery loops,
  and multi-repository coordination. Use whenever engineering work benefits
  from structured execution, independent delegation, or verified completion.
---

# Graph Engineering

Turn non-trivial local engineering work into a dependency graph, execute
only ready nodes, and finish only when the requested outcome is supported
by validation evidence.

## Operating rules

- Scale process to task size and risk. Keep tiny, low-risk work lightweight.
- Treat user intent, repository instructions, permissions, and safety rules
  as higher priority than this workflow.
- Do not force this workflow onto tasks outside local software engineering.
- Do not invent capabilities, validation results, subagent activity, or
  successful completion.
- Continue autonomously while safe, useful work remains. Ask for input only
  when a material decision, missing authority, or external dependency blocks
  progress.

## 1. Classify the task

Before acting, classify:

- Mode: answer, review, diagnose, change, deploy, or monitor.
- Size: tiny, standard, or complex.
- Risk: low, elevated, or high.
- Scope: files, repositories, services, and external systems involved.
- Mutation: read-only, reversible local change, or external/destructive
  change.
- Capability: available tools, subagents, commands, credentials, and
  permissions.

Size the graph proportionately:

- Tiny, low-risk task: use one implicit node.
- Standard task: start with three to seven outcome-based nodes.
- Complex, multi-repository, or elevated-risk task: expand only where
  dependencies, contracts, or risks require more structure.

Honor the requested mode:

- Answer, review, report, and diagnose without mutation unless the user also
  requests a change.
- Implement and verify when the user requests a change or build.
- Deploy, publish, or contact external systems only when explicitly
  authorized.
- Monitor with the available wait or status mechanism instead of treating
  unchanged state as failure.

## 2. Establish the completion contract

Derive a completion contract from the request and repository evidence:

- Requested outcome.
- In-scope and out-of-scope work.
- Constraints and material assumptions.
- Acceptance criteria.
- Required validation evidence.
- Approval gates and external dependencies.

Resolve details from the workspace before asking questions. Ask when an
unresolved choice would materially change the outcome or risk. Never widen
scope merely to avoid a blocker.

## 3. Build and maintain the graph

Represent each node with:

- ID and objective.
- Repository and owned files.
- Dependencies and consumers.
- Risk level.
- Status.
- Acceptance criteria.
- Validation commands or inspection method.
- Evidence produced.
- Recovery or rollback notes when risk warrants them.

Apply this node-quality gate:

- Give each node one observable outcome and one validation method.
- Add a dependency only when downstream work cannot safely start without it.
- Merge nodes that own the same files or produce the same evidence.
- Rebuild the graph when new evidence invalidates its assumptions.

Use these states:

```text
PENDING -> READY -> RUNNING -> VALIDATING -> DONE
Any unfinished node may become BLOCKED or FAILED.
```

A node becomes READY only when its dependencies and required contracts are
complete. Update the graph after every material discovery, completion,
failure, or scope change.

Model shared interfaces, schemas, versions, generated artifacts, external
dependencies, and rollout ordering as contract nodes before dependent
implementation begins.

## 4. Execute proportionately

1. Inspect repository instructions, status, architecture, and relevant
   history.
2. Discover the smallest set of affected files and repositories.
3. Establish a baseline when practical, especially for risky changes or
   repositories with uncertain health.
4. Execute READY nodes with the smallest coherent actions.
5. Validate each node before unblocking consumers.
6. Integrate completed nodes in dependency order.
7. Run broader system validation proportional to impact.
8. Compare evidence against every acceptance criterion.
9. Finish, continue, or report a genuine blocker.

Preserve unrelated user work. Do not perform destructive Git operations.
Do not commit, push, merge, rebase, deploy, publish, or mutate external
systems unless the user authorized that action.

## 5. Use subagents dynamically

Use subagents only when the environment supports them and isolated context
or parallel work provides more value than coordination overhead.

Good candidates include:

- Two or more independent READY nodes.
- Focused repository or dependency research.
- Separate security, performance, accessibility, or compatibility review.
- Independent validation of a risky implementation.
- Work in non-overlapping repositories or file sets after contracts settle.

Avoid delegation for:

- Tiny changes.
- Tightly coupled nodes.
- Overlapping file ownership.
- Undecided contracts or architecture.
- Work the parent must immediately redo to verify.

Create task-specific roles rather than relying on a fixed specialist list.
Give every subagent:

```text
Objective
Repository and exact scope
Files owned or read-only boundary
Dependencies and settled contracts
Constraints and prohibited actions
Acceptance criteria
Required validation
Expected evidence and return format
```

The parent owns the graph, architecture, contracts, permissions, conflict
resolution, integration, and final validation. Independently inspect
subagent output and evidence; never accept a success summary by itself.

Run subagents in parallel only when nodes are independent, file ownership
does not overlap, and the runtime has capacity. If subagents are unavailable,
execute the same READY nodes sequentially and report that fact.

## 6. Run evidence-based validation loops

Use this loop:

```text
discover checks -> establish baseline when useful -> make a focused change
-> run targeted checks -> classify failures -> revise the hypothesis
-> retry with new evidence -> run broader checks -> evaluate acceptance
```

Discover commands from repository instructions, CI workflows, build files,
package scripts, manifests, and recent project usage. Do not invent commands
or require checks the project does not support.

Select validation adaptively by asking:

1. What observable behavior, artifact, interface, or contract changed?
2. What is the smallest reliable check that could disprove correctness?
3. Which direct consumers or boundaries could be affected?
4. Which failure modes become plausible because of this change?
5. What broader check is justified by the blast radius and risk?

Build a proportionate validation ladder from:

- Direct inspection, parsing, or static checks.
- Targeted behavioral checks for the changed scope.
- Affected component or repository checks.
- Contract and integration checks across boundaries.
- System-level or end-to-end checks when supported.
- Non-functional checks when performance, security, accessibility,
  reliability, compatibility, data integrity, or operations are at risk.

Do not run every level mechanically. Increase breadth with coupling,
uncertainty, irreversibility, and impact.

On failure:

1. Preserve the exact command, output, and relevant environment context.
2. Classify the cause as implementation, assumption, baseline, dependency,
   environment, permission, flaky test, or external service.
3. Change the hypothesis or approach before retrying.
4. Re-run the smallest check that can disprove the new hypothesis.
5. Stop after three attempts with the same failure signature unless new
   evidence justifies another attempt.

Never weaken, delete, or bypass a meaningful test merely to obtain a pass.
Distinguish failures caused by the change from pre-existing failures. Never
claim a check passed if it was not run or its result was inconclusive.

For every required check, retain the command or inspection performed, its
scope, meaningful output, result, failure classification, retries, and the
acceptance criterion it supports. Record why a relevant check was skipped
or inconclusive.

## 7. Apply risk and approval gates

Treat production changes, deployments, data loss, schema migrations,
security controls, credentials, billing, public publishing, and irreversible
external actions as high risk.

For elevated or high-risk work:

- Identify failure domains and rollback options before mutation.
- Validate plans or previews before applying changes when supported.
- Request required authority before crossing an approval gate.
- Prefer staged, reversible, and observable changes.
- Stop when safe completion depends on missing credentials, unavailable
  systems, or an unapproved material decision.

## 8. Complete with evidence

Declare DONE only when:

- Every required graph node is DONE.
- Acceptance criteria have direct evidence.
- Relevant targeted and broader checks pass, or exceptions are clearly
  identified.
- Integration and contract compatibility are verified where applicable.
- No unresolved high-risk issue is hidden.

Report:

- Outcome and graph nodes completed.
- Repositories and files changed.
- Validation commands and results.
- Subagents actually used, if any.
- Assumptions, skipped checks, blockers, and remaining risks.

If work cannot be completed, report the precise blocker, evidence gathered,
safe work completed, and the smallest action needed to resume.
