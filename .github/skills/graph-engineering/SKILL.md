---
description: Transform software engineering tasks into explicit
  dependency graphs and dynamically orchestrate execution in VS Code
  GitHub Copilot Agent Mode.
name: graph-engineering
---

# Graph Engineering Skill

## Purpose

This skill converts every non-trivial task into a dependency graph
before implementation.

It is designed for **local VS Code GitHub Copilot Chat Agent Mode**.

## Environment

-   Supported:
    -   VS Code GitHub Copilot Chat Agent Mode
    -   Multi-root workspaces
    -   Local repositories
-   Do not depend on:
    -   Copilot CLI
    -   GitHub cloud coding agents
    -   Background cloud execution

## Core workflow

1.  Inspect the workspace.
2.  Discover affected repositories.
3.  Build a dependency graph.
4.  Define shared contracts before implementation.
5.  Execute READY nodes.
6.  Delegate independent work to dynamic subagents if available.
7.  Validate each node.
8.  Integrate results.
9.  Perform system-level validation.
10. Finish only after acceptance criteria are satisfied.

## Dynamic subagent orchestration

Never rely on predefined specialist agents.

For each task:

-   Determine whether subagents provide value.
-   Generate temporary specialist roles from the task.
-   Delegate only isolated graph nodes.
-   Use the minimum useful number of subagents.

Example roles:

-   API compatibility investigator
-   Database migration specialist
-   React accessibility reviewer
-   Terraform dependency analyst
-   Performance investigator
-   Integration validator

If subagents are unavailable, execute the identical graph sequentially.

Never claim subagents were used unless they actually were.

## Multi-repository support

Treat every Git repository in the workspace independently.

Before editing:

-   Discover all repositories.
-   Determine repository responsibilities.
-   Detect repository dependencies.
-   Build one cross-repository dependency graph.

Each graph node must include:

-   Repository
-   Files owned
-   Dependencies
-   Acceptance criteria
-   Validation

Shared APIs, schemas, package versions, infrastructure outputs, and
events must be modeled as contract nodes before implementation begins.

## Parallel execution

Parallel execution is allowed only when:

-   Nodes are READY.
-   Files do not overlap.
-   Contracts are complete.
-   No architectural conflicts exist.

Otherwise execute sequentially.

## Parent agent responsibilities

The parent agent owns:

-   Global graph
-   Architectural decisions
-   Shared contracts
-   Integration
-   Conflict resolution
-   Release ordering
-   Final validation

## Git safety

For every repository:

-   Inspect current branch.
-   Detect uncommitted changes.
-   Preserve unrelated work.
-   Never perform destructive Git operations.
-   Never commit, push, merge, or rebase unless explicitly requested.

## Validation

Every implementation requires:

Repository validation:

-   Build
-   Type checking
-   Unit tests

Cross-repository validation:

-   Contract compatibility
-   Integration
-   End-to-end verification where possible

## Resource control

Prefer the smallest useful number of subagents.

Avoid delegation for:

-   Tiny edits
-   Tightly coupled work
-   Duplicate investigations

## Reporting

Report:

-   Graph nodes completed
-   Repositories changed
-   Files changed
-   Validation executed
-   Remaining risks
-   Whether subagents were actually used

## Fallback

If dynamic subagents are unavailable:

-   Preserve the graph.
-   Execute READY nodes sequentially.
-   Maintain identical acceptance criteria.
-   Report that sequential execution was used.
