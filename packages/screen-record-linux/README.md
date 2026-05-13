# Screen Record (Linux (X11))

Record your screen to a self-contained MP4 file. Linux (X11)-native capture path; no third-party recorders required.

## How to use

1. Click **Install** on the marketplace card.
2. On the Home screen tile, set:
   - **Output file** — where to write the MP4 (default goes to `/tmp/`; change to a path you can find later)
   - **Video Bitrate (kbps)** — default 6000 is good for documentation; raise to 10000+ for game recordings
   - `displayName` is the X DISPLAY (e.g. `:0`, `:0.1`)
3. Click **▶ Run** to start recording.
4. Click **■ Stop** to finalize the MP4. Without a clean stop the file may be unplayable.

## Requirements

- GStreamer 1.18+ with the platform-specific capture element for Linux (X11)
- Plugins: H.264 encoder (`x264enc`) + `mp4mux`
- Wayland sessions are not supported by this package — use an X11 session, or check whether your DE exposes Xwayland.

## Variables

| Variable | Default | Notes |
| --- | --- | --- |
| `location` | `/tmp/screen-record.mp4` | Output file path |
| `kbps` | `6000` | x264enc target bitrate |
| `displayName` | `:0` | X DISPLAY value |

## License

[PolyForm-NC-1.0](../../LICENSE). Free for non-commercial use; commercial use requires a separate license — contact [gak4u](https://github.com/gak4u).

## Source

Browse the pipeline JSON in this folder under `pipelines/`. Open it in [gst-graph](https://github.com/gak4u/gst-graph) for the visual graph.
