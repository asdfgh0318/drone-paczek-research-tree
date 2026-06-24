# drone-paczek-research-tree

Companion research tree to the **SoundVisualizer** project, focused on the *drone paczek* (parcel-drone) rig. Tracks experimental nodes (baseline + acoustic-damping material treatments) and links each one to the corresponding SoundVisualizer capture so node status flips automatically when a measurement lands.

Identical editor / git-API / loopback-write surface to [`duct-research-tree`](../duct-research-tree/) — only the `data.json` content differs.

## Layout

- `data.json` — the tree (phases + nodes). Auto-committed on every server-side write.
- `serve.py` — local HTTP editor + git API. Default port `8124` (duct-research-tree owns `8123`).
- `index.html` — single-page editor.

## Run

```bash
python3 serve.py --port 8124 --bind 0.0.0.0
# → http://localhost:8124/
```

The `/api/node/<id>` endpoint stays loopback-only regardless of `--bind`; the LAN bind is only for the editor UI + read-only `data.json`.

## SoundVisualizer integration

SoundVisualizer's `config.toml`:

```toml
[[research_trees]]
name = "drone-paczek"
enabled = true
base_url = "http://localhost:8124"
public_url = ""
```

When a capture finishes that's linked to one of these nodes, the server pushes the SoundVis Results URL back into `soundVisualizerLink` and flips the node's status to `in-progress`.
