---
title: "PreviewKit getting started"
summary: "Host a small native preview."
category: "Guides"
order: 10
keywords: ["preview", "snapshot", "geometry", "readiness", "native controls"]
related: ["index.md", "api.md", "typed-api.md"]
---

# PreviewKit getting started

Install `previewkit-0.1.0.buipkg` in `packages/`, then import `previewkit`. Create the native Window and apply fixture data normally. Construct a session, register controls with unique nonempty member names, and retain the session for the Window’s lifetime.

This complete example tracks a Label, shows its host, and starts the ordinary event loop. By default it publishes `_buoy_preview_ready.json` after the event loop has advanced for 250 milliseconds.

Set `ReadyPath` before showing if the consumer needs another destination. Consumers should retry incomplete reads and wait separately for native pixels to settle. A ready JSON file does not prove the compositor has presented a frame.

```buoy
Import previewkit

Window PreviewExample
    Title = "PreviewKit example"
    Frame = (80, 80, 360, 140)
    Control Label greeting
        Text = "Hello from a native preview"
        Frame = (24, 24, 300, 28)
    End Control
End Window

Sub Main()
    Dim host As New PreviewExample()
    Dim session As New PreviewSession(host)
    session.Track("greeting", host.greeting)
    session.Show()
    Application.Run()
    session.CancelReadiness()
End Sub
```

Call `CancelReadiness()` when abandoning a pending preview or closing its host. It stops the pending timer and breaks its reference to the session. The session does not own application shutdown or close the host Window. For a component preview, create a host Window and add the component before constructing the session.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
