---
title: "previewkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["PreviewReadyTimer", "PreviewSession"]
dependencies: []
symbols: ["PreviewReadyTimer", "PreviewSession"]
related: ["api.md", "getting-started.md", "index.md"]
---

# previewkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## PreviewReadyTimer

`Public Class PreviewReadyTimer Inherits Timer`

A timer-owned readiness callback; not a platform capture implementation.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Session` | `PreviewSession` | No | No | — | — |

### NotifyTick

`Public Overrides Sub NotifyTick()`

No parameters.

Returns: no value.

## PreviewSession

`Public Class PreviewSession`

Reusable native preview host. Construct and use only on the UI thread. This runs real control code; it provides no security sandbox.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Host` | `Window` | Yes | No | — | — |
| `ReadyPath` | `String` | No | No | `"_buoy_preview_ready.json"` | — |
| `ApplicationMenu` | `MenuBar` | No | No | — | — |

### Constructor

`Public Sub Constructor(host As Window)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `host` | `Window` | `ByVal` | Required |

Returns: no value.

### Track

`Public Sub Track(member As String, control As UIControl)`

Register a named runtime control. Bounds are relative to its actual parent.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `member` | `String` | `ByVal` | Required |
| `control` | `UIControl` | `ByVal` | Required |

Returns: no value.

### Snapshot

`Public Function Snapshot() As JSONItem`

Snapshot values after layout. This does not capture or analyze pixels.

No parameters.

#### Returns

| Type |
| --- |
| `JSONItem` |

### MenuSnapshot

`Public Function MenuSnapshot() As JSONItem`

Observe menu objects, not their callback behaviour or native system menus.

No parameters.

#### Returns

| Type |
| --- |
| `JSONItem` |

### Show

`Public Sub Show(delayMilliseconds As Integer = 250)`

Show the window and publish a snapshot once the event loop has advanced. A capture backend must still wait for native pixels to settle.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `delayMilliseconds` | `Integer` | `ByVal` | `250` |

Returns: no value.

### CancelReadiness

`Public Sub CancelReadiness()`

Stop pending publication when a host closes or abandons its preview.

No parameters.

Returns: no value.

### PublishReady

`Public Sub PublishReady()`

Publish JSON to the configured path; consumers retry incomplete reads.

No parameters.

Returns: no value.
