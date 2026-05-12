# gst-graph-packages

Curated, ready-to-install packages for
[gst-graph](https://github.com/gak4u/gst-graph) — the GStreamer pipeline
editor.

Each subdirectory under `packages/` is a self-contained package: a
`gst-package.json` manifest plus the pipeline JSON(s) it ships. The
gst-graph app discovers this repository via the GitHub topic
[`gst-graph-package`](https://github.com/topics/gst-graph-package) and
installs packages directly into the user's local pipelines.

> **Looking for documentation on the package format**, the
> `gst-package.json` schema, or how to author your own package? See the
> companion repo
> [gak4u/gst-graph-package-examples](https://github.com/gak4u/gst-graph-package-examples).

---

## Packages

| Package | Platforms | What it does |
| --- | --- | --- |
| [`rtmp-livestream`](packages/rtmp-livestream/) | all | Encode video + audio with x264 / AAC and push to an RTMP endpoint (Twitch, YouTube, Restream). |
| [`webcam-preview-macos`](packages/webcam-preview-macos/) | macOS | Open the default webcam via AVFoundation and show it in a preview window. |
| [`webcam-preview-linux`](packages/webcam-preview-linux/) | Linux | Open a V4L2 webcam (e.g. `/dev/video0`) and show it in a preview window. |
| [`webcam-preview-windows`](packages/webcam-preview-windows/) | Windows | Open a webcam via Kernel Streaming and show it in a preview window. |
| [`screen-record-macos`](packages/screen-record-macos/) | macOS | Record the screen with AVFoundation, encode H.264, and write MP4. |
| [`screen-record-linux`](packages/screen-record-linux/) | Linux (X11) | Record an X11 display with `ximagesrc`, encode H.264, and write MP4. |
| [`screen-record-windows`](packages/screen-record-windows/) | Windows 10+ | Record the desktop with Direct3D11 screen capture, encode H.264, and write MP4. |

Each package's manifest declares the GStreamer elements it requires.
gst-graph's marketplace shows a "Ready to install" pill only when those
elements are present locally — so e.g. the macOS-only packages cleanly
show "Missing required plugins" on Linux.

---

## Installing

1. Open gst-graph and go to the **Marketplace** tab.
2. Search for the package you want, or browse the list.
3. Click **Install…** and confirm in the preview modal.

The pipelines are added to your local library with fresh IDs. Variables
declared in the manifest (RTMP host, output file path, monitor index,
…) are populated with sensible defaults that you can change before
running.

---

## Layout

```
.
├── gst-index.json          (optional but fetched first by the marketplace)
├── packages/
│   ├── <package-id>/
│   │   ├── gst-package.json
│   │   └── pipelines/<name>.json
│   └── …
├── README.md
└── LICENSE
```

`gst-index.json` lists every package's id and path. If the marketplace
can't find the index it falls back to walking `packages/*/`.

---

## License

PolyForm Noncommercial 1.0.0 — see [`LICENSE`](LICENSE). For commercial
licensing of either gst-graph or these packages, please contact the
author.
