# 素宣墨韵 · 设计系统文档 v2.0

## 核心理念

**以墨为魂，朱砂仅为印痕。**

- 所有信息层级、交互反馈、功能色彩均来自 **墨色五阶** 体系（焦、浓、重、淡、清）。
- 红色（朱砂）**不参与任何功能性表达**，仅出现在 Logo 小印和页脚印章两处装饰元素。
- 交互状态通过 **同一墨色体系内的深浅变化** 与 **下划线有无** 来传递，不引入第二色系。

---

## 一、色彩系统

### 1.1 色彩角色定义

| 角色 | 浅色模式 | 深色模式 | 说明 |
|------|---------|---------|------|
| 宣纸底色 | `#F8F4EB` | `#25221C` | 叠加 5% 噪点纹理 |
| 主文字（焦墨） | `#2B1E14` | `#ECE4D5` | 最高对比度 |
| 次要文字（浓墨） | `#5E4E3F` | `#B9AD97` | 正文、摘要 |
| 三级文字（淡墨） | `#9B8B7A` | `#7A6E5F` | 日期、备注、占位 |
| 边框/分隔线（清墨） | `#C5B9A5` | `#4A4136` | 最浅墨线 |
| 印章色 | `#B33A3A` | `#D87070` | **仅用于装饰小印，无交互功能** |
| 选中背景 | `#D9D1BD` | `#40372B` | 淡墨渲染 |

**规则**：
- **禁止出现** 纯黑 `#000` 或纯白 `#FFF`，所有色值均带暖调。
- **印章色占比** 不超过页面可视面积 1%，仅限 Logo 旁小印（22×22px）和页脚版权印。
- **文字层级** 严格遵循五墨梯度：`#2B1E14` → `#5E4E3F` → `#9B8B7A`。

---

## 二、交互状态映射

所有可交互元素的状态变化 **完全在墨色体系内闭环**：

| 元素 | 默认 | 悬停 | 激活/当前 |
|------|------|------|-----------|
| 导航链接 | 淡墨 `#9B8B7A` | 焦墨 `#2B1E14` + 下划线 | 焦墨 + 下划线常驻 |
| 文章标题 | 焦墨，无下划线 | 浓墨 `#5E4E3F` + 下划线 | — |
| 文章项背景 | 透明 | 左侧焦墨竖线 + 右移 | — |
| 引用块竖线 | 淡墨 SVG 笔触 | 无交互 | — |
| 代码关键字 | 焦墨加粗 | 无交互 | — |
| 按钮/切换 | 淡墨边框 | 焦墨边框 + 焦墨文字 | — |

**原则**：无一处使用朱砂作为交互反馈。

---

## 三、朱砂使用限制

- **允许位置**：Logo 旁小印（22×22px）、页脚版权印。
- **最大尺寸**：24×24px。
- **禁止行为**：不得用于链接、按钮、高亮、标签、状态指示、下划线、图标。
- **变量隔离**：印章色使用独立的 `--seal-color` 变量，与 `--link-color`、`--active-indicator` 等互不引用。

---

## 四、质感与纹理

### 4.1 宣纸底纹

通过两层 CSS 实现宣纸的纤维感和自然纸色渐变：

```css
body {
  background-color: var(--paper);
  background-image:
    linear-gradient(0deg, transparent 0%, rgba(180,160,140,0.02) 100%),
    url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.05'/%3E%3C/svg%3E");
  background-repeat: repeat;
}
```

- 噪点透明度固定为 `0.05`（浅色）或 `0.06`（深色），不可随意提高。
- 渐变层自下而上微亮，模拟纸张受光。

### 4.2 毛笔笔触 SVG

所有分隔线、引用线使用 SVG 贝塞尔路径，禁止 CSS `solid` 或 `dashed` 硬边。

#### 水平分隔线（横笔）

```css
.brush-hr {
  width: 120px;
  height: 6px;
  background-image: url("data:image/svg+xml,%3Csvg...");
  background-repeat: no-repeat;
  background-position: center;
  margin: 2.5rem auto;
  border: none;
}
```

#### 垂直引用线（侧锋）

引用线使用淡墨色（`--ink-light`）SVG 枯笔路径：

```css
blockquote::before {
  content: '';
  position: absolute;
  left: 10px;
  top: 15%;
  bottom: 15%;
  width: 3px;
  background-image: url("data:image/svg+xml,%3Csvg...stroke='%239B8B7A'...%3E");
  background-size: 100% 100%;
}
```

### 4.3 无卡片无阴影

空间划分仅依靠留白、渐淡细线、半透明纸层背景。

---

## 五、字体与排版

### 5.1 字体栈

| 角色 | 字体栈 |
| ---- | ------ |
| 正文/标题 | `"Noto Serif SC", "Source Han Serif SC", "Songti SC", serif` |
| 代码 | `"FangSong", "LXGWenkai Mono", "Fira Code", monospace` |

### 5.2 字号与行高规范

| 层级 | 字号 | 行高 | 字重 | 适用场景 |
| ---- | ---- | ---- | ---- | -------- |
| H1（页面主标） | 3.4rem / 54px | 1.3 | 700 | Hero 标题 |
| H2（区块标） | 1.7rem / 27px | 1.3 | 700 | 文章列表标题 |
| H3（卡片标） | 1.4rem / 22px | 1.3 | 700 | 次要标题 |
| Body | 1rem / 16px | 1.8 | 400 | 正文段落 |
| Small | 0.9rem / 14px | 1.6 | 400 | 日期、备注 |
| Caption | 0.8rem / 12px | 1.5 | 400 | 标签、印章辅助文字 |

---

## 六、设计原则（十戒）

1. **宣纸为底**：页面背景永远使用 `#F8F4EB` 或深色模式对应色，绝不使用纯白
2. **功能用墨，装饰用印**：所有功能性颜色来自墨色五阶，朱砂仅用于装饰小印
3. **墨分五色**：所有灰色都必须有暖色调（黄棕底色），无冷蓝灰色
4. **中文 serif**：使用衬线字体；英文 serif 标题
5. **字重锁定**：Serif 重量锁定在 500，不使用 bold
6. **行高分级**：紧凑标题 1.1-1.3 / 密集正文 1.4-1.45 / 阅读正文 1.5-1.55
7. **字距调整**：中文正文 0.3pt，英文正文 0
8. **标签背景**：必须使用实色十六进制，不使用 rgba（WeasyPrint 双重矩形 bug）
9. **无卡片无阴影**：空间划分仅依靠留白与细线
10. **禁止斜体**：任何地方不使用斜体

---

## 七、组件规范

### 7.1 导航栏

- 结构：左侧 Logo + 右侧链接列表
- 背景：透明，不设底色，仅底部一条渐淡细线分割
- 链接状态：默认淡墨 → 悬停/当前焦墨 + 底部下划线

### 7.2 引用块 (Blockquote)

- 结构：半透明纸背景 (`--paper-card`) + 3px 淡墨竖线 (SVG) + 文字
- 竖线颜色：淡墨（`#9B8B7A` / `#7A6E5F`），不使用朱砂

### 7.3 代码块

- 背景：半透纸背景 (`--paper-card`)，左侧 3px 清墨竖线（实线）
- 字体：仿宋/楷体等宽
- 语法高亮：关键字用焦墨色 (`--ink-deep`) + 加粗，不使用朱砂

### 7.4 毛笔分隔线

- 使用 SVG 水平笔触，宽度 120px，居中
- 仅用于大区块分隔

---

## 八、可访问性标准

- **对比度**：
  - 浅色模式主文字 `#2B1E14` 对底色 `#F8F4EB` 对比度约为 **12.5:1**（AAA 级）
  - 深色模式主文字 `#ECE4D5` 对 `#25221C` 对比度约为 **9.6:1**（AAA 级）
- **焦点指示**：所有可交互元素使用 2px 焦墨色外框
- **语义化**：使用标准 HTML 标签（`nav`, `main`, `ul`, `blockquote`），配合 ARIA 属性

---

## 九、深色模式适配

通过 `[data-theme="dark"]` 选择器覆盖 CSS 变量。必须同时调整：

- 底色、纸纹噪点色
- 墨色文字层级反转（浅色字）
- 印章色提亮以保证对比度（`#B33A3A` → `#D87070`）
- 所有 SVG 笔触线条的颜色（需分别提供浅/深两套）

---

## 十、CSS 变量清单

```css
:root {
  --paper: #F8F4EB;
  --paper-card: rgba(245,240,230,0.7);
  --ink-deep: #2B1E14;
  --ink-mid: #5E4E3F;
  --ink-light: #9B8B7A;
  --border-ink: #C5B9A5;
  --select-bg: #D9D1BD;

  /* 印章色（仅装饰用） */
  --seal-color: #B33A3A;

  /* 语义变量（全部来自墨色） */
  --link-color: var(--ink-deep);
  --link-hover: var(--ink-mid);
  --active-indicator: var(--ink-deep);
  --quote-line: var(--ink-light);
  --code-keyword: var(--ink-deep);

  --font: "Noto Serif SC", "Source Han Serif SC", "Songti SC", serif;
  --mono: "FangSong", "LXGWenkai Mono", "Fira Code", monospace;
  --transition: 0.25s ease;
}

[data-theme="dark"] {
  --paper: #25221C;
  --paper-card: rgba(40,36,28,0.8);
  --ink-deep: #ECE4D5;
  --ink-mid: #B9AD97;
  --ink-light: #7A6E5F;
  --border-ink: #4A4136;
  --select-bg: #40372B;
  --seal-color: #D87070;

  --link-color: var(--ink-deep);
  --link-hover: var(--ink-mid);
  --active-indicator: var(--ink-deep);
  --quote-line: var(--ink-light);
  --code-keyword: var(--ink-deep);
}
```

---

## 十一、一句话执行原则

> **功能用墨，装饰用印。红色不过三点，全页墨色当家。**

本规范自 v2.0 起生效。后续迭代需保持 **"墨色当家，朱砂节制"** 的核心不动摇。
