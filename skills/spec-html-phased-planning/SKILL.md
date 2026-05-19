---
name: spec-html-phased-planning
description: Guides phased long-range planning as HTML under `.spec/`, static assets in `public/`, progress as percentages, styling via linked CDN CSS only (no Tailwind Play). For long-term goals, multi-phase delivery, ordered or dependent work; not for single PRs, isolated bugs, or one-session tasks.
disable-model-invocation: true
license: MIT
---

# HTML phased specifications (`.spec/`)

## Non-negotiables

- HTML specs live in `.spec/` at the **active repo or package root**.
- CSS and static assets in `public/`.
- **Linked stylesheets only.** No Tailwind Play or runtime style compilers. Minimal JS; no behavioral scripts in specs.
- One **phase** ↔ one HTML file. Multi-round testing stays in-section unless file size forces a split (cross-link phase id).
- Update the active phase file **after each completed chunk**.
- Quantify **phase progress** and **per-item progress** (percentages).

## When to use

- Long-term **goals** or **roadmaps**.
- Explicit **multi-phase** delivery.
- Multiple work items with **ordering** or **hard dependencies**.

## When not to use

- Single change or **one PR** scope.
- **Single-bug** find/fix, micro-perf tweak, trivial refactor.
- Work completable in **one session** without phase tracking.

If unclear: confirm staged `.spec/` maintenance; otherwise skip this skill.

## Repository layout

Root = Git repo root, **or** monorepo **package root** (alongside that package's source tree).

```
<root>/
├── .spec/           # one HTML file per phase
├── public/          # CSS, fonts, images
└── ...
```

From `.spec/*.html`, reference assets as `../public/...`.

## Styling (CDN CSS)

**Default:** Bulma `1.x` (CSS-only component layout; no JS required for static specs).

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1/css/bulma.min.css" />
```

**Alternative:** Pico `2.x` (classless, semantic markup).

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@2/css/pico.min.css" />
```

Optional project overrides: `public/spec.css` (still no JS).

## Workflow

1. **Gate:** Scope matches “When to use.”
2. **Plan:** Phase list (design, foundation, MVP, test-feedback, optimize, close—edit names as needed).
3. **Execute:** After each merge-worthy chunk—refresh tasks, item %, phase %.
4. **Loops:** Test-feedback ↔ optimize—prefer `## Round N` sections in the same file; split only if needed, label shared phase in header.
5. **Close:** Deliverables, open issues, exit criteria—in closing phase file.

## Progress rules

- State **one aggregation rule** per file (weighted mean, simple average, critical-path gate, etc.).
- Keep **phase %** consistent with item-level %.

## HTML & accessibility

- `lang` matches content (e.g. `en`).
- Single `h1`; descending `h2`/`h3`; no skipped levels.
- Descriptive link text; sufficient contrast (tweak via `public/spec.css` if required).

## Starter template (Bulma)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Phase title — spec</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1/css/bulma.min.css" />
  <link rel="stylesheet" href="../public/spec.css" />
</head>
<body>
  <section class="section">
    <div class="container">
      <div class="content">
        <header>
          <p class="is-size-7 has-text-grey">Phase progress: <strong>0%</strong> · Updated: YYYY-MM-DD</p>
          <h1 class="title is-3">Phase title</h1>
          <p class="subtitle is-6 has-text-grey">One-line phase objective.</p>
        </header>
        <section class="mt-5">
          <h2 class="title is-4">Work items</h2>
          <ul>
            <li>Item A — <strong>0%</strong></li>
            <li>Item B — <strong>0%</strong></li>
          </ul>
        </section>
      </div>
    </div>
  </section>
</body>
</html>
```

(Pico: drop Bulma classes; lean on semantic tags.)

## Checklist

- [ ] In-scope per “When to use”; not in “When not to use.”
- [ ] One HTML file per phase; `public/` for assets.
- [ ] Linked CSS only; no Tailwind Play / style JS; no extra scripts.
- [ ] Phase and item percentages updated with each milestone.
- [ ] Multi-round test/optimize traceable.
- [ ] Correct repo / package root.
