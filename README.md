# Project Notes

Per-project markdown notes with tags — saved in the project, shared by every agent working in it.

A [workspacer](https://github.com/DJTouchette/workspacer) hub plugin (webview). It opens as an agent-scoped pane and keeps a notebook for that agent's project directory.

## What it does

Notes live in a single JSON file inside the project at `.workspacer/plugins/project-notes/notes.json` (the conventional per-plugin data home; needs workspacer ≥ 0.137, whose `fs.write` creates missing parents), written through the hub's `fs.write` capability scoped to the agent's cwd — nothing outside the project is ever touched, and the notes travel with the directory (commit the file to share them, or gitignore it to keep them local).

- **A notebook per project** — every agent (and every notes pane) in the same directory sees the same notes.
- **Tags** — comma-separated per note; the sidebar builds filter chips from whatever tags exist.
- **Search** — matches titles, bodies, and tags.
- **Markdown** — write / preview toggle with a tiny built-in renderer (headings, bold/italic, inline code, fenced blocks, lists, links).
- **Autosave** — debounced writes, flush on blur; last-write-wins per file.

## Install

Command palette → **Install Plugin…** → `DJTouchette/workspacer-plugin-project-notes`

## Permissions

| Capability | Scope | Why |
|---|---|---|
| `fs.read` | agent cwd | read `.workspacer/plugins/project-notes/notes.json` |
| `fs.write` | agent cwd | save it |

No events consumed, no network, no sidecar process.
