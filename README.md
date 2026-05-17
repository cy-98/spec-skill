# spec-html-phased-planning

Cursor / agent skill: phased specs as HTML in `.spec/`, assets in `public/`, **linked CDN CSS** (Tachyons or Pico), **percent** progress—**no** Tailwind Play.

## Install

```bash
npx skills add <package-or-github-repo>
npx skills add .                    # from a clone of this repo
```

Needs Node.js. Installs into agent-specific skill dirs (e.g. `.cursor/skills/`).

## Cursor (manual)

Copy `skills/spec-html-phased-planning/SKILL.md` to `.cursor/skills/spec-html-phased-planning/SKILL.md`.

Edit only `skills/.../SKILL.md`; keep `.cursor/...` in sync if you use both.

## Publish

`npm login` → `npm publish` (scoped packages: add `--access public`).

## License

[MIT](./LICENSE)
