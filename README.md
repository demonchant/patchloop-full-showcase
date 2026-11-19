# PatchLoop Full Showcase target

This is a small, real Node.js task application intended to be selected from PatchLoop's repository picker. It has an Active list, completion checkboxes, an Archived list, and archive/restore actions backed by a JSON data file.

## Purpose

The initial commit deliberately contains one documented repair challenge: restoring an archived completed task clears its completed state. The bundled Kane objective catches that defect. A successful demonstration records two failures of the same fixed objective, a human-approved Codex repair in a disposable worktree, a reviewable diff, and a Kane rerun of the unchanged objective.

The challenge bug is intentional and isolated to this showcase repository. Do not copy it into a production application.

## Use it with the hosted PatchLoop site

PatchLoop's UI is hosted at [patchloop-web.onrender.com](https://patchloop-web.onrender.com). Kane and Codex run on your computer through PatchLoop's paired local worker.

Clone both the PatchLoop worker and this target repository on the computer where Kane and Codex are installed:

### Windows PowerShell

```powershell
git clone https://github.com/demonchant/kane-cli.git patchloop-runner
git clone https://github.com/demonchant/patchloop-full-showcase.git
cd patchloop-runner
npm ci
$env:PATCHLOOP_TARGET_REPO = (Resolve-Path ..\patchloop-full-showcase).Path
npm run worker -- --url https://patchloop-web.onrender.com --pair-code 'PASTE_CODE_FROM_CONNECT_LOCAL_RUNNER'
```

### macOS / Linux

```sh
git clone https://github.com/demonchant/kane-cli.git patchloop-runner
git clone https://github.com/demonchant/patchloop-full-showcase.git
cd patchloop-runner
npm ci
export PATCHLOOP_TARGET_REPO="$HOME/patchloop-full-showcase"
npm run worker -- --url https://patchloop-web.onrender.com --pair-code 'PASTE_CODE_FROM_CONNECT_LOCAL_RUNNER'
```

Get the one-time code from **Connect local runner** on the hosted site and replace the sample value above. The code expires after one use. Keep the worker terminal open; it prints the ready repository count. Sign in to the hosted site with the same Google account, refresh the target picker, and select **PatchLoop Full Showcase**. PatchLoop uses this committed baseline to create an isolated Git worktree and leaves the selected checkout unchanged.

## Repair challenge

**Coding task**

> Fix task restoration so restoring an archived completed task preserves its completed checkbox and title.

**Fixed Kane acceptance objective**

> On the Tasks page, create a task named “PatchLoop repair proof,” mark it complete, archive it, verify it is absent from Active and present in Archived, restore it, then verify it appears in Active with its completed checkbox still checked and its title unchanged.

Kane should first expose the defect after restoration. Replay the same objective once. After the repeated failure, inspect the recorded evidence and explicitly request Codex. Review its diff and run the unchanged objective again. A repair is verified only if Kane returns a passing final event and exits successfully.

## Runtime contract

`patchloop.target.json` supplies the start command and readiness URL. PatchLoop also sets `PORT`, `PATCHLOOP_PORT`, `PATCHLOOP_HOST`, and a fresh `PATCHLOOP_DATA_DIR` for each run. The app binds to loopback and stores each run's task data in that isolated directory.
