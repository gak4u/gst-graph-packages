# Webcam Preview (macOS)

Open your webcam and show it in a preview window. A minimal sanity check that AVFoundation is wired up correctly, plus a starting point for any pipeline that takes camera input.

## How to use

1. Click **Install** on the marketplace card.
2. On the Home screen tile, confirm the device setting:
   - `deviceIndex` selects the camera (0 = first listed; some Macs surface the FaceTime HD camera as index 0).
3. Click **▶ Run** — a preview window pops up showing the camera feed.
4. Click **■ Stop** to close.

## Requirements

- GStreamer 1.18+
- `avfvideosrc` plugin (in `gst-plugins-bad`). macOS will prompt for camera permission on first run.
- A connected webcam

## Variables

| Variable | Default | Notes |
| --- | --- | --- |
| `deviceIndex` | `0` | Index of the camera to open (0 = first enumerated) |

## License

[PolyForm-NC-1.0](../../LICENSE). Free for non-commercial use; commercial use requires a separate license — contact [gak4u](https://github.com/gak4u).

## Source

Browse the pipeline JSON in this folder under `pipelines/`. Open it in [gst-graph](https://github.com/gak4u/gst-graph) for the visual graph.
