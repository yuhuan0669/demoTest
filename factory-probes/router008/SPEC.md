# FACTORY-ROUTER-PROBE-008 — Bounded real delivery

## Goal
Prove a real version-pinned handoff from Chat-authored GitHub specification to a locally executed Codex edit, followed by deterministic verification and GitHub PR delivery.

## Source binding
- repository: `yuhuan0669/demoTest`
- approved base before this spec: `feb284d9f24cfa95c7ebbe9415d55763ef9f3f94`
- this specification must be consumed by its exact commit SHA, not by a mutable branch name.

## Allowed implementation change
Create exactly one new file:

`factory-probes/router008/delivery.txt`

Its complete UTF-8 content must be exactly:

```text
ROUTER008_DELIVERY_PASS
```

including exactly one trailing newline.

Expected SHA-256 of the file bytes:

`4570d4cb4a51377ce79bdb7c5d763c34bab0cc2ef826aa7e2f17975cf54d13f4`

## Codex boundary
- Codex may read this exact specification and repository state.
- Codex may write only the allowed implementation file above.
- Codex must not commit, push, create a PR, modify the specification, use network access, or change any other file.
- Git commit/push/PR creation are deterministic router responsibilities after verification.

## Deterministic acceptance
Before any push, the router must verify:
1. implementation started from the exact specification commit;
2. `git status --porcelain` contains only the allowed new file;
3. no tracked file was modified or deleted;
4. the file SHA-256 equals the expected value above;
5. no unexpected untracked files exist in the delivery worktree;
6. Codex completed normally and returned a machine-readable completion event.

Only after all checks pass may the router commit the allowed file on a dedicated implementation branch, push it, and create a draft PR. The PR must not be merged automatically.

## Expected final state
- one implementation commit after the specification commit;
- one draft PR to `master` containing the specification plus the allowed delivery file;
- one result record bound to the event ID, exact spec commit, implementation commit, and PR number;
- `master` remains unchanged.
