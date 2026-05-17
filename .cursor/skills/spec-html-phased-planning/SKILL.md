---
name: spec-html-phased-planning
description: 指导在仓库 `.spec/` 用纯 HTML 维护分阶段长期规划，外链 CDN 提供的 **纯 CSS**（原子工具类、无构建、无 JS），静态资源放 `public/`，用百分比跟踪进度。当用户表达**长期目标**、**长期规划**、**多个阶段**，或**多件工作且有序或相互依赖**时使用；**单个改动**、**单个 PR**、**单一 bug 排查/修复**、可在一次对话内结束的小任务不算长期规划。
disable-model-invocation: true
license: MIT
---

# HTML 分阶段规格（`.spec/`）

以下内容来自用户需求，编写与更新规格时遵守其字面要求：

- 使用 HTML 文件在**当前工作仓库根目录**的 `.spec/` 下生成（维护）HTML 文件。
- CSS 和其他静态资源放在 `public/`。
- **样式只使用「CDN + `<link rel="stylesheet">`」引入的纯 CSS**：不加载 Tailwind Play/任意在浏览器里**解析或编译样式**的脚本；spec 页**尽量不要有业务向 JS**（参见下文「样式与 JS」）。
- **仅当**属于下方「何时使用」中的长期规划场景时才启用本 skill。
- 将任务拆分为多个阶段，**包括且不限于**：设计阶段、基础工作准备阶段、MVP 版本、测试反馈阶段、优化阶段、结束阶段。**测试反馈阶段**与**优化阶段**可以循环反复进行。
- 每次完成一部分工作都要更新对应的 spec 文件。
- **每个阶段对应一个 spec 文件（一个 HTML）**；同一阶段内多轮测试/优化优先写在**同一文件**的「轮次」小节中（仍算一个阶段文件，见「阶段与工作流」）。
- 每个阶段及其中的工作都可通过**进度百分比**量化。

## 何时使用（触发 / 不触发）

**宜使用**（满足其一且整体跨多日/多提交、需要分阶段推进时）：

- 用户明确说到 **长期目标**、**长期规划**、路线图、分阶段交付。
- 工作自然拆成 **多个阶段**（设计 / 准备 / MVP / 测试反馈 / 优化 / 收尾等）。
- **多件事情**需要推进，且 **有先后顺序** 或 **相互依赖**（上游未就绪则下游不能开始）。

**不使用**：

- **单个改动**、**单个 PR** 就能讲清的范围。
- **找出或修复单个 bug**、单点性能 tweak、单文件小重构。
- 能在**一次会话**内收敛、无须分阶段记录进度的小需求。

边界不清时：先问用户是否要按阶段维护 `.spec/`；若否，不用本 skill。

## 仓库布局

**根目录**指：你当前操作的 **Git 仓库根**；若是 **monorepo 子包**，则 `.spec/` 与 `public/` 放在**该子包根**（与这一包的源码、README 同级），不要随意指到 unrelated 目录。

```
<根>/
├── .spec/
│   ├── 01-design.html
│   ├── 02-foundation.html
│   ├── 03-mvp.html
│   ├── 04-test-feedback.html
│   ├── 05-optimization.html
│   └── 06-closure.html          # 结束阶段；命名可按项目调整
├── public/
│   ├── spec.css                 # 项目专用补充样式（可选）
│   └── ...                      # 字体等静态资源
└── ...
```

- `.spec/`：一阶段一文件；用有序前缀或日期排序。
- 引用 `public/`：从 `.spec/` 内页面使用相对路径，例如 `../public/spec.css`。

## 样式与 JS（外链 CSS，无 Tailwind）

不使用 **Tailwind Play CDN**（`<script src="https://cdn.tailwindcss.com">`）及任何同类「在浏览器里处理样式」的方案。

**推荐 CDN（二选一）**：

1. **Tachyons**（`4.12.0`）：单文件 **原子工具类** CSS，用法接近 utility-first，无需构建。

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tachyons@4.12.0/css/tachyons.min.css" />
```

2. **Pico.css**：偏 **classless**，写法偏语义化 HTML，适合想少写字类名的团队。

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css" />
```

**可选**：在 `public/spec.css` 写少量项目级覆盖（仍不引入脚本）。  
**禁止**：在 spec HTML 里加入依赖 JS 才生效的样式方案、打包脚本、无关业务脚本；尽量不写 `onclick` 等行为脚本。

## 阶段与工作流

1. **启动**：确认符合「何时使用」；打开或新建本阶段对应 HTML。
2. **拆分**：各阶段独立成文件；至少覆盖设计、基础准备、MVP、测试反馈、优化、结束，可按项目增删命名。
3. **执行**：每完成一块工作，**立即**更新当前阶段 HTML（任务列表与**阶段进度**、各项**完成百分比**）。
4. **循环**：测试反馈 ⇄ 优化可多轮。推荐 **在同一阶段文件** 增加 `## 第 N 轮测试反馈` 等小标题；若轮次极重、单文件过大，再拆 `04-test-feedback-02.html` 等，但要在各文件页眉注明「同属阶段：测试反馈」以免与「一阶段一文件」冲突。
5. **收尾**：结束阶段写明交付物、遗留问题、关闭标准。

## 进度百分比约定

在阶段文件内写明：

| 层级 | 含义 | 示例 |
|------|------|------|
| **阶段进度** | 该阶段整体完成度 | `阶段进度：45%` |
| **工作项进度** | 阶段内单项任务 | 每项 `0%–100%` |

在页首「进度说明」中固定一种**汇总口径**（加权 / 简单平均 / 关键路径门槛等），更新子任务时同步更新阶段总进度。

## HTML 结构与可访问性（建议）

- 保持 `lang` 与内容语言一致（如 `zh-CN`）。
- **每页一个 `h1`**；`h2`–`h3` 按大纲递减，勿跳级。
- 链接写明去向（避免「点击这里」）；正文与背景对比度可读（需要时用 `public/spec.css` 微调）。

## 最小页面模板（Tachyons + 可选自建 CSS）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>阶段名称 — 项目规格</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/tachyons@4.12.0/css/tachyons.min.css" />
  <link rel="stylesheet" href="../public/spec.css" />
</head>
<body class="bg-near-white sans-serif pa4 lh-copy">
  <main class="center mw7">
    <header class="mb4">
      <p class="f6 gray">阶段进度：<strong>0%</strong> · 更新：YYYY-MM-DD</p>
      <h1 class="f3 fw6 mt0">阶段标题</h1>
      <p class="mid-gray">阶段目标一句话。</p>
    </header>
    <section>
      <h2 class="f4 fw6">任务清单</h2>
      <ul class="pl3">
        <li>任务 A — <strong>0%</strong></li>
        <li>任务 B — <strong>0%</strong></li>
      </ul>
    </section>
  </main>
</body>
</html>
```

（若选 Pico，可删 Tachyons 的 class，改用语义标签 + Pico 默认样式。）

## 校验清单

- [ ] 符合「何时使用」之一，且不属于「不使用」情形
- [ ] `.spec/` 一阶段一 HTML（多轮次优先同文件分节）；`public/` 承载附加静态资源
- [ ] 样式仅为外链 **CSS**，**无** Tailwind Play / 样式类 JS；spec **无**多余脚本
- [ ] 每次阶段性成果落地后已更新对应 HTML 与百分比
- [ ] 测试反馈 / 优化轮次可追溯
- [ ] 仓库根 / monorepo 子包根路径未搞错
