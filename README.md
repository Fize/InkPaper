<div align="center">
  <h1>InkPaper</h1>
  <p><b>Good content deserves good paper.</b></p>
  <a href="https://github.com/Fize/inkpaper/stargazers"><img src="https://img.shields.io/github/stars/Fize/InkPaper?style=flat-square" alt="Stars"></a>
  <a href="https://github.com/Fize/inkpaper/releases"><img src="https://img.shields.io/github/v/tag/Fize/InkPaper?label=version&style=flat-square" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
  <a href="https://twitter.com/HiTw93"><img src="https://img.shields.io/badge/follow-Tw93-red?style=flat-square&logo=Twitter" alt="Twitter"></a>
</div>

## See it

<div align="center">
  <a href="assets/demos/demo-v2.html"><img src="assets/demos/demo-v2.png" alt="InkPaper v2.0 demo" width="80%"></a>
  <br><sub>素宣墨韵 · 以墨为魂，朱砂仅为印痕</sub>
</div>

## Design

Warm paper canvas, ink-toned functional hierarchy (five ink gradations), decorative cinnabar seal only, serif carries hierarchy, no hard shadows or flashy palettes. Not a UI framework; a constraint system for printed matter. Documents should read as composed pages, not dashboards.

Eight document types (One-Pager, Long Doc, Letter, Portfolio, Resume, Slides, Equity Report, Changelog) with dedicated EN/CN templates. Fourteen inline SVG diagram types included. InkPaper picks the right variant based on the language you write in.

| Element     | Rule                                                                            |
| ----------- | ------------------------------------------------------------------------------- |
| Canvas      | `#F8F4EB` paper, never pure white                                               |
| Hierarchy   | Five ink tones (`--ink-deep/mid/light/border`), no red in functional roles       |
| Seal        | `#B33A3A` decorative stamp only (22×22px max), never for interaction             |
| Neutrals    | All warm-toned (yellow-brown undertone), no cool blue-grays                     |
| Serif       | Body 400, headings 500. Avoid synthetic bold                                    |
| Line-height | Tight titles 1.1-1.3, dense body 1.4-1.45, reading body 1.5-1.55                |
| Shadows     | Ring or whisper only, no hard drop shadows                                      |
| Tags        | Solid hex backgrounds only. `rgba()` triggers a WeasyPrint double-rectangle bug |

**Fonts**: Each language uses a single serif font for the entire page. Chinese: TsangerJinKai02. English: Charter. TsangerJinKai is free for personal use, commercial use requires a license from [tsanger.cn](https://tsanger.cn). All other fonts are system-bundled.

Full spec: [design.md](references/design.md). Cheatsheet: [CHEATSHEET.md](CHEATSHEET.md).

## Background

I like investing in US equities and ask Claude to write research reports all the time. Every output landed in the same default-doc look: gray, flat, a different layout each session. The structure was hard to scan, the formatting felt dated, and nothing about the page made me want to keep reading. So I started fixing the typography, the palette, the spacing, one rule at a time, until the report became a page I actually enjoyed.

Later I needed to present "The Agent You Don't Know: Principles, Architecture and Engineering Practice." I already had the document and didn't want to build slides from scratch, so I used Claude Design to lay it out in my own style, tweaked it round after round, and eventually got it to a place I was happy with. That process added inline SVG charts, a unified warm palette, and a tighter editorial rhythm. It kept growing until it covered every document I regularly ship, so I kept abstracting the process, and it became inkpaper: one quiet design system I can hand to any agent and trust the output.

## License

MIT License for inkpaper code and templates. Feel free to use and contribute.

**Fonts**: TsangerJinKai02 (Chinese) is free for personal use only; commercial use requires a license from [tsanger.cn](https://tsanger.cn). Charter (English), and CJK fallbacks are system-bundled or open-licensed.
