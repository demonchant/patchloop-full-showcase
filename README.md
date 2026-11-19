# PatchLoop Full Showcase

A small task app used to demonstrate a real PatchLoop repair cycle. The committed baseline contains one intentional regression: restoring an archived completed task clears its completed state.

## Run the app

Requirements: Node.js 20 or newer. No npm dependencies are required.

```powershell
$env:PATCHLOOP_HOST = '127.0.0.1'
$env:PATCHLOOP_PORT = '4180'
node server.mjs
```

Open http://127.0.0.1:4180. Data is written to `.data` by default. PatchLoop sets an isolated `PATCHLOOP_DATA_DIR` when it launches a run.

## Use it with PatchLoop

1. Clone this repository to the machine running PatchLoop.
2. Set `PATCHLOOP_TARGET_REPO` to the clone's absolute local path before starting PatchLoop.
3. In PatchLoop, choose **PatchLoop Full Showcase** in the target repository selector.
4. Load the bundled task and submit its fixed Kane objective.
5. Let Kane record the seeded failure twice. Review the matching failure, approve Codex repair, inspect the diff, then rerun the exact same objective with Kane.

PatchLoop uses the committed Git baseline and works in a detached worktree. The local checkout remains unchanged. The intended pass condition is that the task is absent from Active while archived, present in Archived, and restored to Active with its original title and completed state.

## Intentional flaw

`server.mjs` sets `completed` to false during restore. That line is intentionally present in the published baseline for the demo. The expected repair removes the completion reset while preserving archive/restore behavior.

This repository demonstrates a testable seeded defect. It does not claim a Codex repair or Kane pass has occurred; publish such a result only after recording an actual PatchLoop run.
