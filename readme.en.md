# OnlyViz

OnlyViz is a local, agent-callable data charting app. It works with Codex, DeepSeek harness, Hermes, and similar agents. You can also open a CSV, JSON, or Excel file and chart it directly; parsing and rendering stay on your machine. Charts are saved as self-contained `.onlyviz` documents that you can double-click to reopen in the desktop app with data and settings restored.

Agents pick the chart type and write the document; you finish the final version.

## Downloads (v0.1.0)

| Platform | Package |
|----------|---------|
| Windows (x64) | [OnlyViz_0.1.0_x64-setup.exe](./OnlyViz_0.1.0_x64-setup.exe) |
| Linux (amd64, Debian/Ubuntu) | [OnlyViz_0.1.0_amd64.deb](./OnlyViz_0.1.0_amd64.deb) |

### Install

**Windows:** run `OnlyViz_0.1.0_x64-setup.exe`.

**Linux:**

```bash
sudo dpkg -i OnlyViz_0.1.0_amd64.deb
sudo apt-get install -f   # if dependencies are missing
```

After install, `onlyviz-cli` is available on your PATH (Node.js 18+ required for the CLI).

## What you get

- **Local-first.** Files are read and rendered on your machine. No cloud account, no upload.
- **Portable chart documents.** `.onlyviz` embeds chart type, field mapping, style, and the rows needed to redraw. Double-click or drag into OnlyViz to reopen.
- **60+ chart types.** Lines, bars, scatter, pie, sankey, heatmaps, Gantt, candlestick, funnel, bullet charts, plus statistical plots (boxplot, violin, swarm, QQ, residual, CDF, ACF/PACF, volcano, control charts). Grouped bars and box plots support error bars and significance brackets.
- **Same path for people and agents.** Codex, Claude, DeepSeek harness, Hermes, and other command-capable agents call `onlyviz-cli` on the machine: list chart types, map columns, create and validate `.onlyviz`, then hand back the file path. You open it in the desktop app to tune style and export PNG/JPEG.

## Agent workflow

```bash
onlyviz-cli charts
onlyviz-cli params scatter
onlyviz-cli create \
  --data data.csv \
  --chart scatter \
  --map x_axis=height,y_axis=weight \
  --title "Height vs Weight" \
  --out figures/scatter_demo.onlyviz
onlyviz-cli validate figures/scatter_demo.onlyviz
```

1. Use `charts` / `params` for types, required fields, and style options.
2. Use `create` with `--map` to write a `.onlyviz` file.
3. Use `validate` to check required fields, columns, and embedded row counts.
4. Open the file in OnlyViz to finish styling and export images.

## Privacy

Parsing, aggregation, and rendering run locally. Agents invoke the local CLI or the local HTTP API (default `127.0.0.1:3921`); data is not sent to an online charting service.

## License

MIT
