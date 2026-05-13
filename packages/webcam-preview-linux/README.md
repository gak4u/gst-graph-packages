# Webcam Preview (Linux)

Open your webcam and show it in a preview window. A minimal sanity check that V4L2 is wired up correctly, plus a starting point for any pipeline that takes camera input.

## How to use

1. Click **Install** on the marketplace card.
2. On the Home screen tile, confirm the device setting:
   - `device` is the V4L2 device node, typically `/dev/video0`. Run `v4l2-ctl --list-devices` to discover others.
3. Click **▶ Run** — a preview window pops up showing the camera feed.
4. Click **■ Stop** to close.

## Requirements

- GStreamer 1.18+
- `v4l2src` plugin (in `gst-plugins-good`). The user must have read access to the device node.
- A connected webcam

## Variables

| Variable | Default | Notes |
| --- | --- | --- |
| `device` | `/dev/video0` | V4L2 device node path |

## License

[PolyForm-NC-1.0](../../LICENSE). Free for non-commercial use; commercial use requires a separate license — contact [gak4u](https://github.com/gak4u).

## Source

Browse the pipeline JSON in this folder under `pipelines/`. Open it in [gst-graph](https://github.com/gak4u/gst-graph) for the visual graph.
