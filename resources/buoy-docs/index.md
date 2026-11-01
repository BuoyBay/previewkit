---
title: "PreviewKit"
summary: "Runtime preview hosting, explicit control registration, and structured geometry/readiness snapshots."
category: "Overview"
order: 0
keywords: ["preview", "snapshot", "geometry", "readiness", "native controls"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# PreviewKit

PreviewKit wraps an already constructed native Window in a `PreviewSession`. Hosts explicitly register controls with member names, then obtain structured runtime geometry and accessibility-property snapshots. No reflection, source parser, or Python runner is required by the library itself.

A snapshot includes the Window title, content dimensions and scale, tracked controls’ bounds/visibility/enabled state, Buoy accessibility properties, selected splitter-pane observations, and first-level menu observations.

## What a snapshot means

Coordinates are relative to each control’s actual parent, in Buoy layout units. They are not screenshot pixels. Accessibility values are Buoy property observations, not proof that native accessibility-provider associations work. Menu snapshots observe object state; callback dispatch and keyboard behavior need separate interaction tests.

PreviewSession runs real application/control code on the UI thread. It is not a security sandbox and does not create a safe control tree from untrusted source. Pixel capture, OS permissions, and compositor synchronization belong to platform adapters.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
