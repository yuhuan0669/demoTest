# FACTORY-ROUTER-PROBE-009 — Lean bounded delivery A/B

## Goal
Repeat the same bounded one-file delivery pattern as Probe 008 while reducing unnecessary Codex context and agent work. Functional correctness must remain unchanged; efficiency is measured, not assumed.

## Source binding
- repository: `yuhuan0669/demoTest`
- approved base before this spec: `feb284d9f24cfa95c7ebbe9415d55763ef9f3f94`
- consume this specification by its exact commit SHA, never by a mutable branch name.

## Codex task
Create exactly one new file:

`factory-probes/router009/delivery.txt`

Its complete UTF-8 bytes must be exactly:

```text
ROUTER009_DELIVERY_PASS
```

with exactly one trailing newline.

Expected file size: `24` bytes.
Expected SHA-256: `4a3964fd7bc82cc532bbe05d717ce99a2649bf18c4257ac0f3439502f0824eb0`.

Codex may read this exact specification and the minimum repository context needed to perform the edit. Codex may write only the delivery file above.

After writing the allowed file, Codex must stop. Codex must not run acceptance checks, hashes, byte counts, git status/diff verification, tests, commits, pushes, PR creation, GitHub access, network access, or modify any other file. Those checks are deterministic Router responsibilities.

## Per-invocation Codex execution policy
The Router must start one new ephemeral workspace-write session and apply the one-run configuration override:

`memories.use_memories=false`

Do not change global Codex configuration. Do not resume any previous session. Do not supply model or reasoning overrides unless required to preserve the same environment; if an override is used, record it explicitly.

## Deterministic Router acceptance
After Codex exits, and before any commit or push, the Router must verify:
1. checkout started from this exact specification commit;
2. Codex produced normal machine-readable completion;
3. `git status --porcelain` contains only `factory-probes/router009/delivery.txt`;
4. no tracked file was modified or deleted;
5. delivery file size is exactly `24` bytes;
6. delivery file SHA-256 equals `4a3964fd7bc82cc532bbe05d717ce99a2649bf18c4257ac0f3439502f0824eb0`;
7. no unexpected untracked file exists.

Only after all checks pass may the Router create one implementation commit, push the dedicated implementation branch, and create one draft PR to `master`. Never merge automatically.

## Efficiency evidence
Preserve the raw Codex JSONL and derive these measurements from it:
- input, cached input, output, and reasoning tokens;
- number of Codex `command_execution` starts;
- number of command executions referencing `/.codex/memories/` or `MEMORY.md`;
- number of Codex post-write acceptance/verification command executions;
- number of failed command executions;
- whether Codex attempted commit, push, PR, GitHub, or network operations.

Probe 008 baseline for comparison:
- input tokens: `222351`
- cached input tokens: `200192`
- output tokens: `3143`
- reasoning output tokens: `1499`
- command executions started: `8`
- memory-reading command executions: `3`
- post-write verification command executions: `3`
- failed command executions: `2`

Do not declare an efficiency PASS from token reduction alone. Functional acceptance must pass first. Report the measured differences without inventing billing or cost conclusions.

## Expected final state
- one specification commit after the unchanged `master` base;
- one implementation commit whose parent is the specification commit;
- one draft PR to `master` containing only this SPEC plus the allowed delivery file;
- one Issue result record bound to event ID, exact spec commit, implementation commit, PR number, functional result, and efficiency measurements;
- `master` unchanged and no merge performed.
