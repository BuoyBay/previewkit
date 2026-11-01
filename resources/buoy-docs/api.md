---
title: "PreviewKit API"
summary: "Public APIs and lifecycle contracts for PreviewKit."
category: "Reference"
order: 20
keywords: ["preview", "snapshot", "geometry", "readiness", "native controls"]
symbols: ["PreviewSession", "PreviewSession.Host", "PreviewSession.ReadyPath", "PreviewSession.ApplicationMenu", "PreviewSession.Track", "PreviewSession.Snapshot", "PreviewSession.MenuSnapshot", "PreviewSession.Show", "PreviewSession.CancelReadiness", "PreviewSession.PublishReady", "PreviewReadyTimer"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# PreviewKit API

| Symbol | Behavior |
| --- | --- |
| `PreviewSession(host As Window)` | Requires a non-Nil existing Window; use on the UI thread. |
| `Host` | Read-only host Window reference. |
| `ReadyPath` | Readiness JSON destination, default `_buoy_preview_ready.json`, relative to the process working directory. Set an explicit destination before `Show()` to avoid writing into the launch directory. |
| `ApplicationMenu` | Explicit application menu fallback for macOS hosts inheriting an application-owned bar. |
| `Track(member, control)` | Registers a nonempty unique name and non-Nil control; invalid/duplicate registration throws. |
| `Snapshot() As JSONItem` | Current host and tracked-control state without capturing pixels. |
| `MenuSnapshot() As JSONItem` | Attached menu state and first-level item observations. |
| `Show(delayMilliseconds = 250)` | Shows the host and schedules readiness publication; delay must be positive. |
| `CancelReadiness()` | Stops pending publication and releases the timer’s session reference. |
| `PublishReady()` | Writes the current snapshot to `ReadyPath`; a failed write throws. |
| `PreviewReadyTimer` | Timer-owned publication callback used by the session. |

Track each control explicitly; child traversal is not implicit. Splitter observations include pane count, size, limits, and collapsed state. The accessibility evidence label explicitly records the absence of a native provider audit.

On macOS, when neither a Window menu nor `ApplicationMenu` is available, inherited application menu attachment is unknown rather than falsely reported absent. Native pixel capture and permissions remain separate from these library calls.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
