# RTMP Livestream

Stream video + audio to Twitch, YouTube, Restream, or any RTMP service. A minimal getting-started template for going live with **gst-graph**.

## What it does

Generates a test video pattern + audio tone, encodes them with H.264 and AAC, muxes them into FLV, and pushes the result to your RTMP destination. Once you confirm the stream is reaching your platform, you can swap the test sources for a webcam or screen-capture pipeline.

## How to use

1. Click **Install** on the marketplace card. After install you'll see the pipeline on the Home screen.
2. Fill in three variables on the tile:
   - **RTMP Host** — e.g. `live.twitch.tv/app` or `a.rtmp.youtube.com/live2`
   - **Stream Key** — your platform's stream key (kept as a secret variable)
   - **Video Bitrate (kbps)** — default 2500
3. Click **▶ Run** to start streaming.
4. Click **■ Stop** when finished.

## Requirements

- GStreamer 1.18 or newer
- Plugins: `videotestsrc`, `videoconvert`, `x264enc`, `audiotestsrc`, `voaacenc`, `flvmux`, `rtmpsink`. Most are in `gst-plugins-good`/`-bad`/`-ugly`; `voaacenc` is sometimes packaged separately.
- Optional: `nvh264enc` for NVIDIA hardware encoding (auto-detected only if you swap it in manually).

## Variables

| Variable | Default | Notes |
| --- | --- | --- |
| `host` | `live.twitch.tv/app` | Base of the RTMP URL — host + application name |
| `streamKey` | _(empty, secret)_ | The stream key issued by your platform |
| `kbps` | `2500` | x264enc target bitrate in kilobits/sec |

## Going further

For broadcasting to **multiple destinations at once** (YouTube + Twitch + Facebook), check out [`srt-multi-rtmp`](../srt-multi-rtmp) — same idea but driven by an iterator table.

## License

[PolyForm-NC-1.0](../../LICENSE). Free for non-commercial use; commercial use requires a separate license — contact [gak4u](https://github.com/gak4u).

## Source

Browse the pipeline JSON in this folder under `pipelines/`. Open it in [gst-graph](https://github.com/gak4u/gst-graph) for the visual graph.
