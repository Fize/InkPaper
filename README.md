<div align="center">
  <h1>InkPaper</h1>
  <p><b>Good content deserves good paper.</b></p>
  <a href="https://github.com/Fize/inkpaper/stargazers"><img src="https://img.shields.io/github/stars/Fize/InkPaper?style=flat-square" alt="Stars"></a>
  <a href="https://github.com/Fize/inkpaper/releases"><img src="https://img.shields.io/github/v/tag/Fize/InkPaper?label=version&style=flat-square" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
  <a href="https://twitter.com/HiTw93"><img src="https://img.shields.io/badge/follow-Tw93-red?style=flat-square&logo=Twitter" alt="Twitter"></a>
</div>

## See it

<table>
<tr>
  <td align="center" width="25%">
    <a href="assets/demos/demo-tesla.pdf"><img src="assets/demos/demo-tesla.png" alt="Tesla equity report"></a>
    <br><b>Equity Report</b> · 中文
    <br><sub>Tesla Q1 2026 财报点评</sub>
  </td>
  <td align="center" width="25%">
    <a href="assets/demos/demo-agent-slides.pdf"><img src="assets/demos/demo-agent-slides.png" alt="Agent keynote slides" /></a>
    <br><b>Slides</b> · English
    <br><sub>Agent keynote, 6 slides</sub>
  </td>
  <td align="center" width="25%">
    <a href="assets/demos/demo-musk-resume.pdf"><img src="assets/demos/demo-musk-resume.png" alt="Elon Musk resume"></a>
    <br><b>Resume</b> · English
    <br><sub>Founder CV, 2 pages</sub>
  </td>
</tr>
</table>

## Design

Warm paper canvas, ink blue as the sole accent, serif carries hierarchy, no hard shadows or flashy palettes. Not a UI framework; a constraint system for printed matter. Documents should read as composed pages, not dashboards.

Eight document types (One-Pager, Long Doc, Letter, Portfolio, Resume, Slides, Equity Report, Changelog) with dedicated EN/CN templates. Fourteen inline SVG diagram types included. InkPaper picks the right variant based on the language you write in.

| Element     | Rule                                                                            |
| ----------- | ------------------------------------------------------------------------------- |
| Canvas      | `#F8F4EB` paper, never pure white                                               |
| Accent      | Ink blue `#B33A3A` only, no second chromatic hue                                |
| Neutrals    | All warm-toned (yellow-brown undertone), no cool blue-grays                     |
| Serif       | Body 400, headings 500. Avoid synthetic bold                                    |
| Line-height | Tight titles 1.1-1.3, dense body 1.4-1.45, reading body 1.5-1.55                |
| Shadows     | Ring or whisper only, no hard drop shadows                                      |
| Tags        | Solid hex backgrounds only. `rgba()` triggers a WeasyPrint double-rectangle bug |

**Fonts**: Each language uses a single serif font for the entire page. Chinese: TsangerJinKai02. English: Charter. TsangerJinKai is free for personal use, commercial use requires a license from [tsanger.cn](https://tsanger.cn). All other fonts are system-bundled.

Full spec: [design.md](references/design.md). Cheatsheet: [CHEATSHEET.md](CHEATSHEET.md).

## Travel

The same constraint system doubles as a brief you can hand to any drawing tool. Point it at the [references folder](references/) and the output inherits warm paper, cinnabar restraint, single-line geometric icons, and editorial typography.

> Apply the InkPaper design system from github.com/Fize/InkPaper/tree/main/references

<table>
<tr>
  <td align="center" width="33%">
    <img src="assets/illustrations/travel-tesla-optimus.png" alt="Tesla Optimus patent overview">
    <br><b>Evidence layout</b> · 中文
    <br><sub>Tesla Optimus 手部和前臂专利图一览</sub>
  </td>
  <td align="center" width="33%">
    <img src="assets/illustrations/travel-spatialvla.png" alt="SpatialVLA architecture redraw">
    <br><b>Architecture redraw</b> · English
    <br><sub>SpatialVLA Figure 1, schematic</sub>
  </td>
  <td align="center" width="33%">
    <img src="assets/illustrations/travel-3d-representations.png" alt="3D representation tradeoffs">
    <br><b>Concept tradeoff</b> · 中文
    <br><sub>3D 表示的算力-推理性取舍</sub>
  </td>
</tr>
</table>

<sub>Rendered by ChatGPT Images 2.0 in a single pass with no manual touch-up. InkPaper specifies, the renderer draws.</sub>

## Background

I like investing in US equities and ask Claude to write research reports all the time. Every output landed in the same default-doc look: gray, flat, a different layout each session. The structure was hard to scan, the formatting felt dated, and nothing about the page made me want to keep reading. So I started fixing the typography, the palette, the spacing, one rule at a time, until the report became a page I actually enjoyed.

Later I needed to present "The Agent You Don't Know: Principles, Architecture and Engineering Practice." I already had the document and didn't want to build slides from scratch, so I used Claude Design to lay it out in my own style, tweaked it round after round, and eventually got it to a place I was happy with. That process added inline SVG charts, a unified warm palette, and a tighter editorial rhythm. It kept growing until it covered every document I regularly ship, so I kept abstracting the process, and it became inkpaper: one quiet design system I can hand to any agent and trust the output.

## License

MIT License for inkpaper code and templates. Feel free to use and contribute.

**Fonts**: TsangerJinKai02 (Chinese) is free for personal use only; commercial use requires a license from [tsanger.cn](https://tsanger.cn). Charter (English), and CJK fallbacks are system-bundled or open-licensed.
