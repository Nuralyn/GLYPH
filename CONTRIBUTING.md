# Contributing to GLYPH

Thank you for your interest in contributing to GLYPH. This document covers how to contribute site data, report bugs, and submit code changes.

---

## Contributing Site Data

The most valuable contributions are new archaeological site datasets. GLYPH's cross-site comparison and similarity matrix become more powerful with every site added.

### What to include

Each site dataset needs:

| Field | Required | Example |
|-------|----------|---------|
| Site name | Yes | Monte Sierpe (Band of Holes) |
| Location | Yes | Pisco Valley, Peru |
| Cultural attribution | Yes | Inca / pre-Inca |
| Estimated date range | Yes | 1400-1532 CE |
| Data source | Yes | Estimated grid from ~5,000 holes in columnar formation |
| Binary grid data | Yes | Rows of 0s and 1s (see format below) |
| Grid resolution | Recommended | 5m per cell |
| Published reference | Recommended | DOI or citation |

### Data format

Binary grid: one row per line, each character is `0` (feature absent) or `1` (feature present). All rows must have the same number of columns.

See the `examples/` folder for templates:
- `binary-grid.txt` — annotated binary grid
- `csv-coordinates.txt` — coordinate pair format
- `aai-grid.txt` — Esri ASCII Grid format
- `custom-site-template.txt` — blank template with metadata fields

### Before submitting

1. Load your grid into GLYPH and verify it parses correctly
2. Run **Analysis** — confirm the classification makes sense for your site
3. Run **Calibration** — confirm all 4 synthetic tests still pass
4. Run **Significance** — document whether the pattern is statistically significant

---

## Reporting Bugs

Open a [GitHub issue](https://github.com/nuralyn/glyph/issues) with:
- What you expected to happen
- What actually happened
- Your browser and OS
- The input data that triggered the bug (if applicable)

For security vulnerabilities, see [SECURITY.md](SECURITY.md).

---

## Code Changes

### Architecture constraint

GLYPH is a **single HTML file** with zero build dependencies. This is a deliberate design choice, not a limitation. All contributions must maintain this constraint:

- No new external dependencies (no npm packages, no additional CDN scripts)
- No build step, bundler, or package manager
- All code lives in `index.html`
- The file must remain self-contained and openable in any browser

### Before submitting a PR

1. **Calibration must pass.** Open GLYPH, go to the Calibrate panel, and run all 4 synthetic tests. All must produce the expected classification.
2. **Preloaded sites must still work.** Load each of the 8 preloaded sites and verify they parse and analyze without errors.
3. **No new dependencies.** If you need a library, implement the functionality inline.
4. **Test on multiple browsers.** At minimum: Chrome and Firefox.

### Code style

- Functional React with hooks (no class components)
- Pure functions for all analysis logic (no side effects)
- Analysis functions are stateless and separate from UI code
- Use existing SVG chart components (`SVGBarChart`, `SVGLineChart`, `SVGHeatmap`) for visualization
- Follow the existing naming conventions and code organization

### PR format

```
## What this PR does
[1-2 sentence summary]

## Why
[Motivation — what problem does this solve?]

## Testing
- [ ] Calibration: all 4 tests pass
- [ ] Preloaded sites: all 8 load and analyze
- [ ] Browser: tested on Chrome and Firefox
- [ ] Mobile: tested on a small viewport (375px)
```

---

## Questions?

Open a [discussion](https://github.com/nuralyn/glyph/discussions) or reach out to the maintainers at hello@nuralyn.com.
