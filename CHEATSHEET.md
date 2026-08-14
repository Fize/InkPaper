# inkpaper · Cheatsheet

One-page quick reference — scan before filling a template or tweaking a detail. Full spec in `references/design.md`.

## Ten invariants

1. Page background `#FAF9F5` (paper), never pure white or cold blue-white
2. 文字用墨，功能用石，装饰用印 — text: ink tones (`--ink-*`); function: minerals; decoration: cinnabar seal
3. Neutrals warm-toned (yellow-brown undertone), no cool gray; mineral colors are the only chromatic exception (function only)
4. One serif per page (headings + body); `--sans` = `var(--serif)`; real sans only for genuinely UI-style chrome
5. Serif weight locked at 500, no bold
6. Line-height: headlines 1.1-1.3 / dense 1.4-1.45 / reading 1.5-1.55
7. Letter-spacing: Chinese body with TsangerJinKai 0.1-0.2pt (dense ≤0.3pt); English body 0; small labels / all-caps overlines +0.2-1pt
8. Tag backgrounds solid hex, no rgba (WeasyPrint double-rectangle bug)
9. Depth via ring / whisper shadow, no hard drop shadows
10. No italic in templates or demos

## Sources and Materials

| Trigger | Do first |
| --- | --- |
| Latest product / version / launch / funding / market data | Check reliable sources first |
| Company / product / project branded doc | Confirm logo, product image, or UI screenshot |
| Key number or result | Record the source; if unverifiable, write magnitude or mark missing |
| Missing material | Mark the gap or ask the user; do not use unrelated imagery |

## Color

| Token | Value | Use |
| --- | --- | --- |
| `--paper` | `#FAF9F5` | Page background (jade-white xuan paper, R−B=+5 warm base) |
| `--paper-card` | `rgba(249,248,243,0.75)` | Card / lifted container · code block · chart · status bar |
| `--ink-deep` | `#2B1E14` | Primary text · headings · code keyword |
| `--ink-mid` | `#5E4E3F` | Body · secondary text · table headers |
| `--ink-light` | `#9B8B7A` | Subtext · metadata · nav default · placeholder |
| `--border-ink` | `#C5B9A5` | Borders · dividers · horizontal strokes |
| `--cinnabar` | `#B33A3A` | **Signature**: seal + danger (≤1% surface; logo 22×22, footer 18×18, error bar) — only strong color |
| `--azurite` | `#2B5C8A` | Links · nav · selection · chart series 1 (≤2 per screen) |
| `--malachite` | `#3E8E7E` | Success (3.5:1 — large/UI only, never small text) |
| `--ochre` | `#A96A2E` | Warning · quote-line (never text) |
| `--gamboge` | `#D9A620` | Charts only (1.98:1 — never text) |
| `--select-bg` | `rgba(43,92,138,0.08)` | Selection (`::selection`) fill |
| `--azurite-line` | `rgba(43,92,138,0.30)` | Link underline (default) |

**Discipline (十戒)**: ink ≥85% of page · azurite ≤2 per screen · cinnabar ≤1% · gamboge never text · ≤3 colors per view. Text never takes mineral color; one mineral per job (一色一职).

## Type (pt tokens; convert to px for screen)

| Role | Size | Weight | Line-height |
| --- | --- | --- | --- |
| Display | 36 | 500 | 1.10 |
| H1 | 22 | 500 | 1.20 |
| H2 | 16 | 500 | 1.25 |
| H3 | 13 | 500 | 1.30 |
| Body Lead | 11 | 400 | 1.55 |
| Body | 10 | 400 | 1.55 |
| Body Dense | 9.2 | 400 | 1.42 |
| Caption | 9 | 400 | 1.45 |
| Label | 9 | 600 | 1.35 |
| Tiny | 9 | 400 | 1.40 |

Screen (px) ≈ pt × 1.33. Floor: screen body ≥12px; print body/table ≥8.5pt and auxiliary text ≥7pt. Do not reduce type to force a page count.

## Font stacks

One serif per language for the entire page; `--sans` always equals `var(--serif)`.

English:

```css
--serif: Charter, Georgia, Palatino, "Times New Roman", serif;
--sans:  var(--serif);
--mono:  "JetBrains Mono", "SF Mono", "Fira Code", Consolas, Monaco, monospace;
```

Chinese:

```css
--serif: "TsangerJinKai02", "Source Han Serif SC", "Noto Serif CJK SC", "Songti SC", "STSong", Georgia, serif;
--sans:  var(--serif);
--mono:  "JetBrains Mono", "SF Mono", Consolas, "TsangerJinKai02", "Source Han Serif SC", monospace;
```

Any font-family that may render Chinese needs a CJK fallback — `@page` footer, `pre`, `code`, SVG labels included; a pure mono stack renders missing-glyph boxes in WeasyPrint.

## Spacing (4pt base)

| Tier | Value | Use |
| --- | --- | --- |
| xs | 2-3pt | Inline |
| sm | 4-5pt | Tag padding |
| md | 8-10pt | Component interior |
| lg | 16-20pt | Between components |
| xl | 24-32pt | Section-title margin |
| 2xl | 40-60pt | Between major sections |
| 3xl | 80-120pt | Between chapters |

**Screen-first container (default)**

- Use a continuous document surface, not simulated paper sheets.
- Set a readable `max-width` from the content and viewport; remove forced page heights and page breaks.
- Verify at 1440px, 900px, and 390px: no root horizontal overflow, no clipping, bottom gap ≤48px, and no large local void inside columns, cards, charts, or sections.

**Print margins (A4, only when requested)**

| Document | T · R · B · L |
| --- | --- |
| Resume | 11 · 13 · 11 · 13 mm |
| One-Pager | 15 · 18 · 15 · 18 mm |
| Long Doc | 20 · 22 · 22 · 22 mm |
| Letter | 25 mm all sides |
| Portfolio | 12 · 15 · 12 · 15 mm |
| Equity Report | 16 · 18 · 18 · 18 mm |
| Changelog | 20 · 22 · 22 · 22 mm |

**Radius**: `4pt → 6pt → 8pt (default) → 12pt → 16pt → 24pt → 32pt (hero)`

## Common CSS snippets

### Card

```css
.card { background: var(--paper-card); border: 0.5pt solid var(--border-ink); border-radius: 8pt; padding: 16pt 20pt; transition: box-shadow 0.2s; }
.card:hover { box-shadow: 0 4pt 24pt rgba(0,0,0,0.05); }  /* whisper shadow */
```

### Tag (lightest solid)

```css
.tag { background: var(--tag-bg);  /* solid, never rgba (WeasyPrint double-rectangle bug) */
  color: var(--ink-deep); font-size: 9pt; font-weight: 500;
  padding: 1pt 5pt; border-radius: 2pt;
  letter-spacing: 0.4pt; text-transform: uppercase; }
```

### Section title (left accent bar)

```css
.section-title { font-family: var(--serif); font-size: 14pt; font-weight: 500; color: var(--ink-deep);
  margin: 24pt 0 10pt 0; border-left: 2.5pt solid var(--ink-deep);
  border-radius: 1.5pt; padding-left: 8pt; }
```

### Table (inkpaper-table)

Base class works on bare `<table>` or `.inkpaper-table`. Add variant classes for density/alignment:

```css
table, .inkpaper-table { width: 100%; border-collapse: collapse; font-size: 9.5pt; margin: 12pt 0; break-inside: avoid; }
table th { text-align: left; font-weight: 500; color: var(--ink-mid);
  padding: 6pt 8pt; border-bottom: 1pt solid var(--border-ink); }
table td { padding: 5pt 8pt; border-bottom: 0.3pt solid var(--border-ink); vertical-align: top; }
```

| Variant | Class | Effect |
| --- | --- | --- |
| Compact | `.compact` | 8pt font, tight padding (data-dense tables) |
| Financial | `.financial` | Right-align all columns except first, `tabular-nums` |
| Striped | `.striped` | Alternating `var(--paper-card)` row background |
| Total row | `.total` on `<tr>` | Bold, brand top border, no bottom border |

Combine freely: `<table class="inkpaper-table financial striped">`.

### Metric (data card)

```css
.metric { display: flex; align-items: baseline; gap: 6pt; }
.metric-value { font-family: var(--serif); font-size: 16pt; font-weight: 500; color: var(--ink-deep); font-variant-numeric: tabular-nums; }
.metric-label { font-size: 9pt; color: var(--ink-light); }
```

### Quote

```css
.quote { border-left: 2pt solid var(--ochre); padding: 4pt 0 4pt 14pt; color: var(--ink-light); line-height: 1.55; }
```

## Diagram components

Fourteen built-in diagram types — extract the `<svg>` block into a `<figure>` in long-doc / portfolio:

| Type | File | Use |
| --- | --- | --- |
| Architecture | `assets/diagrams/architecture.html` | Components + connections |
| Flowchart | `assets/diagrams/flowchart.html` | Decision branches / flows |
| Quadrant | `assets/diagrams/quadrant.html` | 2×2 positioning |
| Bar Chart | `assets/diagrams/bar-chart.html` | Comparison (≤8 groups × 3 series) |
| Line Chart | `assets/diagrams/line-chart.html` | Trends (≤12 points × 3 lines) |
| Donut Chart | `assets/diagrams/donut-chart.html` | Breakdown (≤6 segments) |
| State Machine | `assets/diagrams/state-machine.html` | States + transitions |
| Timeline | `assets/diagrams/timeline.html` | Time axis + milestones |
| Swimlane | `assets/diagrams/swimlane.html` | Cross-team process flow |
| Tree | `assets/diagrams/tree.html` | Hierarchies |
| Layer Stack | `assets/diagrams/layer-stack.html` | Stacked system layers |
| Venn | `assets/diagrams/venn.html` | Set intersections |
| Candlestick | `assets/diagrams/candlestick.html` | OHLC history (≤30 days) |
| Waterfall | `assets/diagrams/waterfall.html` | Revenue bridge / decomposition |

**Data chart colors** (only place all five minerals appear): series 1-5 = azurite `#2B5C8A` · malachite `#3E8E7E` · cinnabar `#B33A3A` · ochre `#A96A2E` · gamboge `#D9A620`; container `--paper-card` + `--border-ink`; labels/values always ink.

**Editing**: touch only elements between `<!-- DATA START -->` / `<!-- DATA END -->`, leave CSS untouched; all coordinates divisible by 4.

## Dark section

Alternate light/dark rhythm: add `.sd-alt` to any section container.

- Background `--paper` `#22262E` (黛青夜空) · headings `--ink-deep` `#ECE4D5` · body `--ink-mid` `#B9AD97` · subtext `--ink-light` `#7A6E5F`
- Card `rgba(38,43,54,0.8)` · border `rgba(255,255,255,0.08)` · select-bg `rgba(111,163,201,0.14)` · azurite-line `rgba(111,163,201,0.42)`
- Minerals brightened one step: azurite `#6FA3C9` · malachite `#63B5A4` · cinnabar `#D87070` · ochre `#C98A4B` · gamboge `#E0B64C` — all ≥4.8:1 (AA)
- Restriction: showcase pages only, never in print templates

## Verification checks

For an explicit print/PDF deliverable, `python3 scripts/build.py --verify [target]` checks source templates and slides in sequence:

1. Source file exists
2. WeasyPrint render to PDF for HTML / diagram targets
3. Page count check for strict targets
4. Font embedding check
5. PPTX generation for `slides` / `slides-en`

Source templates intentionally keep `{{...}}` fields. Run `python3 scripts/build.py --check-placeholders path/to/filled.html` on completed documents. For explicit print/PDF output, run `python3 scripts/build.py --check-density path/to/output.pdf`; it flags pages with >12% trailing body whitespace. Visually verify that parallel columns or panels differ in content depth by no more than 18%, because a whole-page pixel scan cannot reliably infer layout regions. An intentional cover is a visual exception, not an automatically skipped page.

## Content quality (one rule per type)

Most important rule per type (full bars in `references/writing.md`):

| Document | Core quality rule |
| --- | --- |
| Resume | Every bullet: Action + Scope + Measurable Result + Business Outcome |
| Portfolio | Open with the problem and stakes, not the project name |
| Slides | Slide titles are full sentences (assertions), not topic labels |
| Equity Report | Lead with variant perception: what you see that the market doesn't |
| Long Document | Each chapter claim paragraph must survive the "so what?" test |
| One-Pager | Metrics are the headline; if the 4 cards don't tell the story, the metrics are wrong |
| Letter | First paragraph states purpose in one sentence |
| Changelog | One sentence per change, verb-led, user-facing language |

## Per-page font size strategy (Resume two-page)

Page 1 carries projects (densest); page 2 carries open source, convictions, impact, skills, education (more room).

| Location | Class | Default | Dense (5 projects) |
| --- | --- | --- | --- |
| Project body | `.proj-text` | 9pt / lh 1.40 | 9pt / lh 1.38 |
| Timeline body | `.tl-body` | 9pt / lh 1.40 | 8.5pt (CN) |
| Summary | `.summary` | 9.2pt | 9pt via body |
| Section titles | `.section-title` | margin-top 5mm | 3.5mm |
| OS intro | `.os-intro` | 9.2pt | unchanged |
| Conviction body | `.conv-body` | 9pt | unchanged |
| Skills body | `.skill-body` | 9pt | unchanged |

**Reference config (5 projects + full page 2)**:

```html
<body class="resume--dense">
  <!-- page 1: 5 projects, timeline, summary -->
  <!-- page 2: OS grid (6), convictions, impact, skills, edu -->
</body>
```

Page 2 stays at template defaults; density tightens page 1 only. Long page 2 → shrink `.os-intro`, `.conv-body`, or `.skill-body` individually, never globally.

## Quick decisions

| Need | Use |
| --- | --- |
| Headline | serif 500, line-height 1.10-1.30 |
| Reading body (EN/CN) | serif 400, 9.5-10pt, 1.55 |
| Emphasize a number | `color: var(--ink-deep)`, no bold |
| Divide two sections | 2.5pt ink-deep left bar, or 0.5pt warm dotted |
| Quote | 2pt ochre left border + ink-light text |
| Code | paper-card bg + 0.5pt border-ink + 6pt radius + mono |
| Primary button | select-bg fill + ink-deep text + border-ink ring |
| Secondary button | select-bg + ink-mid |
| Chapter start | serif heading + 2.5pt ink-deep left bar |
| Cover | Display heading + right-aligned author/date + heavy whitespace |
| Figure SVG | `width: 100%; height: auto; max-height: <safe>` — never `max-height` alone (#17) |
| Metric labels (4-col) | Soft cap 14-18 chars at 9pt Charter; trim, don't wrap (#18) |
| Multi-column body | Lengths within ±10 chars across parallel columns (#19) |
| Image references | Only `assets/demos/images/` or `assets/illustrations/`; never `../../sibling-project/...` (#20) |
| Metric row layout | Vertical stack (`flex-direction: column`); baseline-align breaks when labels wrap (#21) |
| Slide bullets | `1. 2. 3.` or `•`; en-dash reads informal at slide scale (#22); print docs keep en-dash |

Not on the table → first principles: **serif carries authority, sans carries utility, warm gray carries rhythm, ink carries hierarchy, mineral carries function, seal carries signature**.
