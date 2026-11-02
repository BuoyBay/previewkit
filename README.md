# Native preview host and control snapshots

`New PreviewSession(hostWindow)` wraps an existing Window. `Track(memberName,
control)` registers each control whose bounds should appear in `Snapshot()`.
The snapshot includes window title, content dimensions, scale, and named control
bounds/visibility, Buoy accessibility properties, first-level menu observations
and tracked splitter pane limits. These are property snapshots, not a complete
native accessibility-provider audit. Control coordinates are relative to their parents, in Buoy
layout units; they are not screenshot pixel coordinates. Track is explicit and
does not require reflection or a second layout parser.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add previewkit --git https://github.com/BuoyBay/previewkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer previewkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
