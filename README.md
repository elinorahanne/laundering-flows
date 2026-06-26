# Money-laundering flows

An interactive, live network diagram of money-laundering flows. Nodes are
stages (victim cash, perp dirty crypto, payloads…); arrows show **how much
money flows** along each path (line thickness) and the **proportion lost to
costs** on that hop (the label). All numbers come from a Google Sheet, so you
edit the sheet and the diagram updates itself.

It's a single static `index.html` — no build step, no server.

## Use it

Open `index.html` in a browser, or visit the GitHub Pages URL once deployed.
With no sheet connected it shows built-in demo numbers (the whiteboard model).

## Connect your Google Sheet (go live)

1. Create a Google Sheet with **two tabs**: `Nodes` and `Edges`. Import the
   files in [`sheet-template/`](sheet-template/) as a starting point
   (File ▸ Import ▸ Upload ▸ *Insert new sheet* for each).
2. Make it readable: **File ▸ Share** → "Anyone with the link" → *Viewer*
   (or **File ▸ Share ▸ Publish to web**).
3. Copy the sheet ID from its URL:
   `docs.google.com/spreadsheets/d/`**`THIS_LONG_ID`**`/edit`
4. In `index.html`, set `const SHEET_ID = "THIS_LONG_ID";` and commit.

The page re-reads the sheet every 15 seconds (and on the **Reload** button),
so edits in the sheet show up live.

### Columns

**Nodes**

| column | meaning |
|--------|---------|
| `id`     | unique key, referenced by edges (e.g. `victim_cash`) |
| `label`  | text shown on the node |
| `amount` | optional £ total at this node (shown under the label) |
| `x`, `y` | optional fixed position to recreate a layout; leave blank to auto-place |
| `color`  | optional node colour |

**Edges**

| column | meaning |
|--------|---------|
| `from`, `to` | node `id`s the arrow connects |
| `amount` | £ flowing along this line → sets the **line thickness** |
| `cost`   | proportion lost to costs: accepts `1/20`, `0.05`, or `5%` |
| `step`   | optional step number shown in the label, e.g. `(3)` |

Costlier hops are drawn redder; cheap hops greener.

## Controls

- **Reload** — re-read the sheet now.
- **Freeze layout** — stop the physics so you can drag nodes without them drifting.
- **Fit** — zoom to fit everything.

## Deploy to GitHub Pages

See the commands in the project chat, or: create a GitHub repo, push this
folder, then **Settings ▸ Pages ▸ Branch: `main` / root**. The site appears at
`https://<you>.github.io/<repo>/`.
