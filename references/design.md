# 素宣墨韵 · 设计系统文档

## 设计理念

**素宣墨韵** 源于中国传统水墨画的审美法则，追求 **"墨分五色、计白当黑、朱砂点睛"** 的数字转译。整体风格极简、克制，强调留白与笔触质感。

核心关键词：
- **宣纸底色**：浅米暖白 + 纤维噪点
- **墨色分层**：焦、浓、重、淡、清五阶灰度
- **朱砂唯一强调色**：仅用于链接、印章、重点线
- **毛笔笔触**：所有线条均采用 SVG 枯笔路径，无硬边矩形
- **无卡片无阴影**：以留白和细线划分空间

---

## 一、色彩系统

### 1.1 浅色模式（生宣）

| 色彩角色           | 色值       | 对应水墨含义           |
| ------------------ | ---------- | ---------------------- |
| 页面底色           | `#F8F4EB`  | 生宣纸本色             |
| 卡片/代码块底色    | `rgba(245,240,230,0.7)` | 半透纸层             |
| 主要文字           | `#2B1E14`  | 焦墨（最深）           |
| 次要文字           | `#5E4E3F`  | 浓墨（中深）           |
| 三级文字/占位      | `#9B8B7A`  | 淡墨（浅灰褐）         |
| 边框/分隔线基础色  | `#C5B9A5`  | 清墨（最浅墨线）       |
| 强调色（朱砂）     | `#B33A3A`  | 印章红                 |
| 强调色悬停         | `#8E2D2D`  | 深朱砂                 |
| 选中背景           | `#D9D1BD`  | 淡墨渲染               |

### 1.2 深色模式（拓片）

| 色彩角色           | 色值       | 含义                   |
| ------------------ | ---------- | ---------------------- |
| 页面底色           | `#25221C`  | 古旧墨底               |
| 卡片/代码块底色    | `rgba(40,36,28,0.8)` | 浓墨半透纸         |
| 主要文字           | `#ECE4D5`  | 拓片白字（暖白）       |
| 次要文字           | `#B9AD97`  | 灰度中层               |
| 三级文字           | `#7A6E5F`  | 深灰                   |
| 边框/分隔线基础色  | `#4A4136`  | 拓片纹理线             |
| 强调色（朱砂）     | `#D87070`  | 亮朱砂（深底适配）     |
| 强调色悬停         | `#EA8A8A`  | 更亮朱砂               |
| 选中背景           | `#40372B`  | 金石感标记             |

### 1.3 色彩使用规则

- **禁止出现** 纯黑 `#000` 或纯白 `#FFF`，所有色值均带暖调。
- **朱砂色占比** 不超过页面可视面积 5%，仅用于链接、当前页标识、引用线、印章元素。
- **文字层级** 严格遵循五墨梯度：`#2B1E14` → `#5E4E3F` → `#9B8B7A`，代码块内关键字可用朱砂。

---

## 二、质感与纹理

### 2.1 宣纸底纹

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

- 噪点透明度固定为 `0.05`（浅色）或 `0.06`（深色），不可随意提高，避免干扰文字。
- 渐变层自下而上微亮，模拟纸张受光。

### 2.2 毛笔笔触 SVG 库

所有分隔线、引用线、特殊强调线均使用 SVG 路径，禁止使用 CSS `solid` 或 `dashed` 边框（除全局细微边框外）。

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

```css
blockquote::before {
  content: '';
  position: absolute;
  left: 10px;
  top: 15%;
  bottom: 15%;
  width: 3px;
  background-image: url("data:image/svg+xml,%3Csvg...stroke='%23B33A3A'...%3E");
  background-size: 100% 100%;
}
```

---

## 三、字体与排版

### 3.1 字体栈

| 角色       | 字体栈                                                                     |
| ---------- | -------------------------------------------------------------------------- |
| 正文/标题  | `"Noto Serif SC", "Source Han Serif SC", "Songti SC", serif`               |
| 代码       | `"FangSong", "LXGWenkai Mono", "Fira Code", monospace`                   |
| 印章标签   | 与正文相同，但固定 `font-weight: 500` 并旋转 `-5deg`                       |

### 3.2 字号与行高规范

| 层级           | 字号         | 行高   | 字重    | 适用场景               |
| -------------- | ------------ | ------ | ------- | ---------------------- |
| H1（页面主标） | 3.4rem / 54px| 1.3    | 700     | Hero 标题              |
| H2（区块标）   | 1.7rem / 27px| 1.3    | 700     | 文章列表标题           |
| H3（卡片标）   | 1.4rem / 22px| 1.3    | 700     | 次要标题（极少用）     |
| Body           | 1rem / 16px  | 1.8    | 400     | 正文段落               |
| Small          | 0.9rem / 14px| 1.6    | 400     | 日期、备注             |
| Caption        | 0.8rem / 12px| 1.5    | 400     | 标签、印章辅助文字     |

**规则**：
- 默认全局 `line-height: 1.8`。
- 标题均使用 `letter-spacing: 0.05em ~ 0.08em`。
- 段落间不加额外 `margin`，通过父级的 `gap` 或 `padding` 控制节奏。

---

## 四、设计原则（十戒）

1. **宣纸为底**：页面背景永远使用 `#F8F4EB` 或深色模式对应色，绝不使用纯白
2. **朱砂唯一**：唯一强调色为朱砂 `#B33A3A`，无第二 chromatic 颜色
3. **墨分五色**：所有灰色都必须有暖色调（黄棕底色），无冷蓝灰色
4. **中文**：所有内容使用 serif；英文：serif 标题 + sans 正文
5. **字重锁定**：Serif 重量锁定在 500，不使用 bold
6. **行高分级**：紧凑标题 1.1-1.3 / 密集正文 1.4-1.45 / 阅读正文 1.5-1.55
7. **字距调整**：中文正文 0.3pt，英文正文 0
8. **标签背景**：必须使用实色十六进制，不使用 rgba（WeasyPrint 双重矩形 bug）
9. **深度表现**：通过环形阴影或低语阴影实现，不使用硬投影
10. **禁止斜体**：任何地方不使用斜体

---

## 五、组件规范

### 5.1 导航栏

- 结构：左侧 Logo + 右侧链接列表
- 背景：透明，不设底色，仅底部一条渐淡细线分割
- 链接状态：默认墨色 → 悬停/当前朱砂色 + 底部 2px 朱砂下划线

### 5.2 引用块 (Blockquote)

- 结构：半透明纸背景 (`--paper-card`) + 3px 朱砂竖线 (SVG) + 文字
- 竖线位置：`position: absolute; left: 10px; top: 15%; bottom: 15%;`
- 文字前可加装饰性「『，但本项目省略

### 5.3 代码块

- 背景：半透纸背景 (`--paper-card`)，左侧 3px 清墨竖线（实线）
- 字体：仿宋/楷体等宽
- 语法高亮：关键字用朱砂色 (`--cinnabar`) + 加粗

### 5.4 毛笔分隔线 (`.brush-hr`)

- 使用 SVG 水平笔触，宽度 120px，居中
- 上下间距：`margin: 2.5rem auto`
- 仅用于大区块分隔

---

## 六、可访问性标准

- **对比度**：
  - 浅色模式主文字 `#2B1E14` 对底色 `#F8F4EB` 对比度约为 **12.5:1**（AAA 级）
  - 深色模式主文字 `#ECE4D5` 对 `#25221C` 对比度约为 **9.6:1**（AAA 级）
  - 朱砂链接色对比度均满足 WCAG AA

- **焦点指示**：所有可交互元素必须有可见的焦点样式（2px 朱砂外框）

- **语义化**：使用标准 HTML 标签（`nav`, `main`, `ul`, `blockquote`），配合 ARIA 属性

---

## 七、深色模式适配

通过 `[data-theme="dark"]` 选择器覆盖 CSS 变量。必须同时调整：

- 底色、纸纹噪点色
- 墨色文字层级反转（浅色字）
- 朱砂色提亮以保证对比度
- 所有 SVG 笔触线条的颜色（需分别提供浅/深两套）

**实现方式**：SVG 内联时通过 CSS 变量注入颜色（推荐），或使用两套背景图。

---

## 八、CSS 变量清单

```css
:root {
  --paper: #F8F4EB;
  --paper-card: rgba(245,240,230,0.7);
  --ink-deep: #2B1E14;
  --ink-mid: #5E4E3F;
  --ink-light: #9B8B7A;
  --border-ink: #C5B9A5;
  --cinnabar: #B33A3A;
  --cinnabar-hover: #8E2D2D;
  --select-bg: #D9D1BD;
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
  --cinnabar: #D87070;
  --cinnabar-hover: #EA8A8A;
  --select-bg: #40372B;
}
```

---

本规范自发布起生效，后续迭代需保持 **"留白、墨韵、朱砂节制"** 的核心不动摇。
