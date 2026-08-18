# StatProphet data feed

Generated output of the StatProphet projection model, published for the iOS app
to fetch. Everything here is written by the pipeline — nothing in this repo is
edited by hand, and a commit made by a person will be overwritten by the next
run.

The model, the engine and the backtest live in a separate private repository.
What is here is only its output.

| File | What it is |
|---|---|
| `data/manifest.json` | Schema and model version, build time, matrix dimensions, and the digests used to verify a download |
| `data/players.json` | Identity, projection, uncertainty band, the drivers behind each number, last season's line, and team context |
| `data/samples.bin.z` | The quantized sample matrix, raw DEFLATE. Shape is `(stats, players, weeks, universes)`, one byte each |

`samples.bin.z` decompresses to roughly 40 MB. The app verifies the SHA-256 of
the *decompressed* bytes against `files.samples.sha256` before installing it, so
a truncated or corrupted transfer can never replace working data.

Derived from public play-by-play (nflverse), roster and depth-chart data
(Sleeper), and public average draft position (FFC).
