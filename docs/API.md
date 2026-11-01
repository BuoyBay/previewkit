# PreviewKit · 0.1.0

Reusable native preview hosting and runtime geometry snapshots for Buoy tools.
Import `previewkit` from `previewkit-0.1.0.buipkg`. Build the package with
`python3 tools/build_previewkit.py`; this checks all six desktop targets.

`New PreviewSession(hostWindow)` wraps an existing Window. `Track(memberName,
control)` registers each control whose bounds should appear in `Snapshot()`.
The snapshot includes window title, content dimensions, scale, and named control
bounds/visibility, Buoy accessibility properties, first-level menu observations
and tracked splitter pane limits. These are property snapshots, not a complete
native accessibility-provider audit. Control coordinates are relative to their parents, in Buoy
layout units; they are not screenshot pixel coordinates. Track is explicit and
does not require reflection or a second layout parser.

The standalone library example (not included in this repository) uses this
API directly, with no Python runner or MCP server.

Call `Show()` on the UI thread, then drive `Application.Run()`. Show publishes
a JSON snapshot to `ReadyPath` after the event loop advances (250 ms by default).
Consumers must retry incomplete file reads and still wait for pixels to settle;
readiness is not proof that a compositor has presented a frame. Set `ReadyPath`
before showing, or call `PublishReady()` to publish another snapshot explicitly.
Call `CancelReadiness()` when abandoning a pending preview. It stops the timer
and breaks the timer's reference to the session. Keep the session alive for its
window's lifetime. The library does not own application shutdown or close the
window. For a View/component preview, the caller creates a host Window and adds
the component before constructing the session.

The library constructs no controls from source and rewrites no source. Callers
construct their typed layout and apply fixture data normally, then register it.
Custom constructors and property setters execute as ordinary application code.

Pixel capture and permissions belong to platform adapters. The companion
[preview tools](https://github.com/BuoyBay/devtools/blob/main/tools/preview/README.md) provide Windows, Linux and macOS
adapters, a Python API, CLI, and MCP server. The Mac adapter reuses the installed
Buoy Test Controls app and its existing Screen Recording authorization. This
package introduces no additional permission holder or permission prompts.

For an application-owned menu bar on macOS, set `session.ApplicationMenu` from
the typed application instance when the window inherits it. An unprovided
application fallback is reported as unknown, rather than absent. Callback and
keyboard behaviour need separate interaction probes; merely observing a command
tag or enabled menu item does not test dispatch.
