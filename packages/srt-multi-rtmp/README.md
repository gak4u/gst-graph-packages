# SRT → Multi RTMP

Take one SRT input and broadcast it to multiple RTMP destinations in parallel — YouTube + Twitch + Facebook + your own server, all at once.

## How it works (in plain English)

Your encoder (OBS, FFmpeg, hardware streamer) sends one SRT MPEG-TS stream to this pipeline. The pipeline demuxes video + audio, then fans both out into N parallel branches via a **loop group**. Each branch publishes to its own RTMP destination. Adding a destination = adding a row to the table; removing one = deleting the row. No rewiring.

Each destination row picks a **streaming service** from a built-in preset library (YouTube, Twitch, Facebook — extend it with any RTMP endpoint) plus your **stream key** for that service. The full RTMP URL is assembled automatically at runtime: `${service URL}${key}`.

## How to use

1. Click **Install** on the marketplace card.
2. Open the pipeline in the editor (or just stay on the Home tile).
3. **Configure your destinations** in the RTMP Targets table on the Home tile:
   - Each row has a display **name**, a **service** dropdown (the preset endpoint), and a **key** input.
   - Click `+ add row` to add a destination, or the ✕ on a row to remove one.
   - The preset library lives in the `endpoints` key-value variable inside the editor — open it to add new services or change a default URL. It's hidden from the Home tile to keep the screen focused on per-stream config.
4. **Point your encoder** at this machine on `srt://<this-host>:5000?mode=caller` (or override the **SRT Port** variable to use a different port).
5. Click **▶ Run**. Each destination publishes simultaneously; the editor shows them as one canvas branch but unrolls to N at runtime.

## Requirements

- GStreamer 1.18 or newer with `gst-plugins-bad` (for `srtsrc`, `rtmp2sink`)
- Plugins: `srtsrc`, `tsdemux`, `h264parse`, `aacparse`, `tee`, `queue`, `flvmux`, `rtmp2sink`
- A network path from your encoder to the host running gst-graph

## What you configure

| Variable | Default | What it is |
| --- | --- | --- |
| **SRT Port** | `5000` | Local port the SRT listener binds on (0.0.0.0) |
| **RTMP Targets** (table) | one starter row | One row per destination: name + service + stream key |
| `endpoints` (kv, hidden) | YouTube / Twitch / Facebook | Service → base RTMP URL map. Add new services here. |

## Adding a new streaming service

1. Open the editor, click the `endpoints` Variable node.
2. Add an entry — e.g. `Restream` → `rtmp://live.restream.io/live/`.
3. On the Home tile, add a row to **RTMP Targets**, pick `Restream` from the dropdown, paste your stream key.
4. **▶ Run** — the new destination joins the fan-out alongside the others.

## Going further

Want to also record locally while streaming? Tap an extra branch off the `vtee` / `atee` and pipe it to `mp4mux` + `filesink`. The loop group only owns the RTMP branches; everything else around it is normal pipeline editing.

## License

[PolyForm-NC-1.0](../../LICENSE). Free for non-commercial use; commercial use requires a separate license — contact [gak4u](https://github.com/gak4u).

## Source

Browse the pipeline JSON in this folder under `pipelines/`. Open it in [gst-graph](https://github.com/gak4u/gst-graph) for the visual graph.
