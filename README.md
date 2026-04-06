# GLYPH

**Ground-Level Yield of Patterned Histories**

*Decoding what was written in earth and stone.*

GLYPH is an archaeological pattern analysis tool that treats terrain-scale sites as structured datasets, not dig sites. It applies information theory, signal processing, and statistical analysis to ancient construction patterns, answering the question: **is this site encoding information, and if so, what kind?**

One HTML file. No dependencies. No build step. No install.
Email it to yourself. Open it on your phone. Analyze ancient civilizations.

**[Live Demo](https://glyph.nuralyn.com)** · **[Download](https://github.com/nuralyn/glyph/releases)**

---

## The Thesis

Sites like Peru's Monte Sierpe ("Band of Holes"), France's Carnac stone rows, and the Nazca Lines have been studied for decades through the lens of archaeology: what were they used for? GLYPH asks a different question: **what do they encode?**

By converting physical features (holes, stones, mounds, geoglyphs) into binary grids and running information-theoretic analysis, GLYPH can detect whether a site contains structured data, classify what type of information architecture it resembles, test whether the structure is statistically significant, and attempt to extract content.

In November 2025, Dr. Jacob Bongers and colleagues at the University of Sydney published a landmark study in *Antiquity* proposing that Monte Sierpe functioned as an indigenous marketplace that evolved into an accounting system under Inca rule, calling it "an Excel spreadsheet for the Inca Empire." They noted structural similarity to Inca khipu (knotted-string counting devices).

GLYPH arrived at the same conclusion independently through pure mathematics. When loaded with a khipu simulation dataset and the Monte Sierpe pattern, the cross-site similarity matrix ranks them as the most similar pair in the catalog at 63.8%, with both classified as Structured Ledger. The shared dominant period of 5 units suggests a common base-counting system. The tool validated the hypothesis without knowing it existed.

> Bongers, J. L. et al. (2025). Indigenous accounting and exchange at Monte Sierpe ('Band of Holes') in the Pisco Valley, Peru. *Antiquity*, 1-19. [DOI:10.15184/aqy.2025.10237](https://doi.org/10.15184/aqy.2025.10237)

---

## What GLYPH Does

### Analysis Engine (8 Modules)
- **Frequency Analysis** — Feature density per row, column, and globally
- **Shannon Entropy** — Information content measurement (bits) per row, column, and total
- **Run-Length Encoding** — Compression ratios revealing structural redundancy
- **Symmetry Detection** — Horizontal mirror, vertical mirror, 180° and 90° rotation, translational periodicity
- **Column-as-Word Vocabulary** — Treats each column as a binary word, computes vocabulary size, hapax legomena, and vocabulary entropy
- **Row Periodicity** — Autocorrelation analysis with peak detection for repeating patterns
- **Spectral Analysis** — 2D Discrete Fourier Transform detecting periodic structure at any orientation
- **Absence Signal** — Identifies where features are conspicuously missing (delimiters, NULL values, field separators)

### Site Classification
GLYPH automatically classifies sites into three information architecture types:

| Type | Signature | Example |
|------|-----------|---------|
| **Structured Ledger** | Low density, strong periodicity, small vocabulary, axis-dominant symmetry, column-compressible | Monte Sierpe, Inca Khipu, Chankillo |
| **Directional Narrative** | High density, gradient decay, large vocabulary, low symmetry, sequential structure | Carnac stone rows |
| **Pictographic** | Very low density, high radial symmetry, maximum vocabulary diversity, uniform compression | Nazca geoglyphs, Göbekli Tepe |

### Statistical Significance
Generates N random grids with matched dimensions and density, runs all analyses, and computes z-scores and p-values for 10 key metrics. Answers the question: "Is this pattern real, or am I seeing structure in noise?"

### Classifier Calibration
Tests the classification engine against known information systems (tally marks, density gradients, radial glyphs, deterministic noise) to verify the classifier works before trusting archaeological results.

### Decode
Attempts content extraction based on classification type:
- **Ledger** — Segments by dominant period, catalogs frame patterns, identifies anomalous entries
- **Narrative** — Detects reading direction via density gradient, identifies phrase boundaries
- **Pictographic** — Flood-fill connected components, builds symbol catalog with frequency counts

### Round-Trip Synthesis
Encode known information as a binary grid, analyze it, classify it, decode it, and verify the round trip. If encode → analyze → classify → decode → verify succeeds, the full pipeline is validated.

### Cross-Site Matrix
NxN similarity heatmap comparing every site against every other site simultaneously. Pearson correlation on entropy profiles, Jaccard index on column vocabularies, compression ratio comparison, and periodicity alignment.

### OpenTopography Integration
Pull elevation data from anywhere on Earth using the OpenTopography Global DEM API. Set coordinates, adjust feature threshold, select grid resolution, and load directly into GLYPH for analysis. Requires a free API key from [opentopography.org](https://opentopography.org).

### AI Interpretation (BYOK)
Optional single-provider AI interpretation layer. Bring your own API key (Claude, GPT, Gemini, or DeepSeek), and GLYPH sends the analysis results for interpretive commentary. No key required to use any other feature. Keys are session-only by default. Optional localStorage persistence is available but stores keys in plaintext.

### Export
- **JSON** — Complete analysis data for programmatic use
- **Markdown Report** — Full report with metadata, all analysis summaries, auto-generated interpretation, and BibTeX citation

---

## Preloaded Sites

GLYPH ships with 8 preloaded datasets (structural approximations based on published descriptions):

| Site | Location | Grid | Classification |
|------|----------|------|---------------|
| Monte Sierpe (Band of Holes) | Pisco Valley, Peru | 20×40 | Structured Ledger |
| Carnac (Menec Alignment) | Brittany, France | 11×50 | Directional Narrative |
| Nazca (Spider Geoglyph) | Nazca, Peru | 30×30 | Pictographic |
| Göbekli Tepe (Enclosure D) | Şanlıurfa, Turkey | 25×25 | Pictographic |
| Stonehenge (Sarsen Circle) | Wiltshire, UK | 30×30 | Pictographic / Ledger (split) |
| Inca Khipu (Decimal Simulation) | — | 20×60 | Structured Ledger |
| Poverty Point (Mound Complex) | Louisiana, USA | 40×40 | Edge case |
| Chankillo (Thirteen Towers) | Casma, Peru | 30×50 | Structured Ledger |

Users can also load custom sites via binary grid input, CSV coordinates, or OpenTopography terrain import.

---

## Quick Start

1. Download `index.html`
2. Open it in any modern browser
3. Click a preloaded site or paste your own binary grid
4. Click **ANALYZE**
5. Explore: Analysis → Significance → Calibrate → Decode → Compare → Matrix → Dashboard

That's it. No server. No install. No dependencies.

---

## Key Finding: Monte Sierpe ↔ Khipu Structural Similarity

GLYPH's cross-site matrix identifies Monte Sierpe and the Inca Khipu simulation as the most structurally similar pair across all 8 preloaded sites (63.8% overall similarity). Both share:

- **Dominant period of 5** — Same base counting unit
- **Structured Ledger classification** — Same information architecture type
- **Column-dominant compression** — Information reads vertically, not horizontally
- **Small, repetitive vocabulary** — Fixed field types with variable data entries
- **Standardized gap patterns** — Consistent delimiter widths (potential field separators)

This computationally validates the hypothesis proposed by Bongers et al. (2025) that Monte Sierpe's structure mirrors Inca khipu, using information theory rather than visual analogy.

---

## What GLYPH Is Not

GLYPH is a pattern analysis tool. It is not proof of anything.

Similarity scores are **hypothesis generators**, not conclusions. When GLYPH reports that two sites share structural features, it means their mathematical signatures overlap — nothing more. Mathematical similarity does not imply historical contact, cultural transmission, or shared origin. Sites separated by thousands of miles and thousands of years can produce similar patterns through convergent design (independent invention of similar solutions to similar problems).

GLYPH cannot distinguish between:
- Two sites that are genuinely related through cultural exchange
- Two sites that independently arrived at similar geometric patterns
- A meaningful pattern and a coincidental one that happens to score well

Researchers must validate any GLYPH finding against domain expertise, stratigraphy, radiocarbon dating, material culture analysis, and physical evidence before drawing historical conclusions. The tool is designed to surface patterns worth investigating, not to replace the investigation itself.

If you find yourself writing "GLYPH proves that..." — stop. GLYPH suggests. Archaeology proves.

---

## Architecture

GLYPH is a single-file React/Babel SPA. No build tools, no bundler, no package manager.

- **Runtime:** React 18.3.1 + ReactDOM (CDN)
- **Transpilation:** Babel Standalone 7.29.1 (CDN)
- **Fonts:** Bebas Neue + Space Mono (Google Fonts)
- **Charts:** Custom inline SVG (no charting library)
- **Storage:** React state (session-scoped), with optional localStorage for API keys
- **Size:** ~292KB

Everything runs client-side. Your data never leaves your browser (unless you use the optional AI interpretation feature with your own API key).

---

## For Researchers

GLYPH is designed to complement, not replace, traditional archaeological methods. The preloaded datasets are structural approximations. For rigorous research, import real survey data via CSV coordinates or OpenTopography integration.

### Citing GLYPH

```bibtex
@software{glyph2026,
  title   = {GLYPH: Ground-Level Yield of Patterned Histories},
  author  = {Nuralyn LLC},
  year    = {2026},
  url     = {https://glyph.nuralyn.com},
  license = {MIT}
}
```

### Contributing Site Data

If you have coordinate data for an archaeological site, GLYPH can analyze it. Accepted formats:
- Binary grid (rows of 0s and 1s, newline-separated)
- CSV with x, y columns (presence data) or x, y, value columns
- OpenTopography API (lat/lon coordinates with your free API key)

See the [`examples/`](examples/) folder for ready-to-paste templates in each format.

We welcome contributions of preloaded site datasets via pull request. See [CONTRIBUTING.md](CONTRIBUTING.md) for data format requirements and PR guidelines.

---

## Roadmap

- [ ] Community site library (shared dataset catalog with pre-computed analyses)
- [ ] LiDAR point cloud import (LAZ/LAS direct ingestion)
- [ ] GeoTIFF elevation model import
- [ ] Multi-resolution sweep analysis
- [ ] OpenTopography catalog search (`/otCatalog` endpoint)
- [ ] PDF report export with embedded charts

---

**Security** — See [SECURITY.md](SECURITY.md) for vulnerability reporting, known limitations, and security architecture details.

**License** — [MIT](LICENSE). Use it, fork it, extend it, cite it. Build something nobody has built before.

**About** — GLYPH is made by [Nuralyn LLC](https://nuralyn.com) in Redmond, Washington. *Finding Truth in Everything.*
