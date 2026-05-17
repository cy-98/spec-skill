# spec-html-phased-planning

Agent skill: maintain **phased long-range plans** as HTML in `.spec/`, static assets in `public/`, **linked CDN CSS** only (Tachyons default; Pico optional), **percent-based** progress, **no** Tailwind Play.

## Install (`skills` CLI)

From the consumer project root (requires Node.js):

```bash
npx skills add <npm package or GitHub repo>
```

Pre-publish / local path:

```bash
npx skills add .
npx skills add /path/to/this/repo
```

The CLI installs into each agent’s skills directory (e.g. `.cursor/skills/`, per tool prompts).

## Cursor (manual)

Copy `skills/spec-html-phased-planning/SKILL.md` to `.cursor/skills/spec-html-phased-planning/SKILL.md`.

## Maintenance

- **Source of truth:** `skills/spec-html-phased-planning/SKILL.md`.
- Mirror `.cursor/skills/...` when changing content.

## Publish (npm)

1. Confirm `name` / `version` in `package.json`; add `repository` / `author` as needed.
2. `npm login`
3. Scoped public package: `npm publish --access public`
4. Unscoped: `npm publish`

## License

MIT. See [LICENSE](./LICENSE).
