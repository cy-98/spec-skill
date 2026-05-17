# spec-html-phased-planning

Cursor / agent skill：在仓库根目录的 `.spec/` 用 **HTML** 维护**分阶段长期规划**，静态资源放 `public/`，样式用 **CDN 纯 CSS**（正文推荐 **Tachyons** 或 **Pico**，无构建、无样式类 JS）；每阶段一个页面，用**百分比**跟踪进度，spec 内**尽量无脚**。

## 安装（skills CLI）

在项目根目录执行（需已安装 Node.js）：

```bash
npx skills add <npm 包名或 GitHub 仓库>
```

发布到 npm 后，将 `<npm 包名>` 换成你在 [npmjs.com](https://www.npmjs.com/) 上的实际包名（默认约定为 `spec-html-phased-planning`；若被占用请改用 scope，例如 `@你的用户名/spec-html-phased-planning`）。

仅本地 Git 仓库、尚未发布时，可从**本仓库路径**安装：

```bash
npx skills add /path/to/this/repo
```

或使用当前目录：

```bash
npx skills add .
```

安装后，`skills` 会把技能装到各 agent 约定的目录（Cursor 等项目下常见为 `.cursor/skills/` 等，以 CLI 提示为准）。

## Cursor 直接使用

也可手动复制 `skills/spec-html-phased-planning/SKILL.md` 到项目的 `.cursor/skills/spec-html-phased-planning/SKILL.md`。

## 维护约定

- **发布用正文**以 `skills/spec-html-phased-planning/SKILL.md` 为准；若同时保留 `.cursor/skills/...`，修改后请两端保持一致（或只维护 `skills/`，安装时再同步到 Cursor）。
- 技能说明全文见该 `SKILL.md`。

## 发布到 npm

1. 在 `package.json` 中确认 `name` / `version`，必要时添加 `repository`、`author`。
2. 登录：`npm login`
3. 首次使用 scope 公开包：`npm publish --access public`
4. 无 scope：`npm publish`

## 许可证

MIT，见 [LICENSE](./LICENSE)。
