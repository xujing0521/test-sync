---
name: use-nexus-wiki-html-preview
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-wiki-html-preview example app. Use when the user asks to 一键部署本示例,
  deploy, install, set up, or run this Nexus Wiki HTML preview example.
---

# Use nexus-wiki-html-preview

Help the user run this example end-to-end. Work from `nexus-wiki-html-preview` (this app root). Ask for secrets/URLs when missing; do not invent CLI commands.

## Checklist

Copy and track progress:

```text
- [ ] 1. Tooling
- [ ] 2. Login
- [ ] 3. App id / register
- [ ] 4. Site URL
- [ ] 5. Install deps + deploy
- [ ] 6. Distribute
- [ ] 7. Enterprise install (manual)
- [ ] 8. Verify in product
- [ ] 9. Optional local serve
```

### 1. Tooling

- Node.js >= 24: `node -v`
- npm: `npm -v` (ships with Node)
- Nexus CLI: `nexus --version` or `npx nexus --version`
  - Install globally if needed: `npm i -g @pc-nexus/cli@latest`

See [Getting started](https://developer.pingcode.com/guide/started/setup) and [CLI](https://developer.pingcode.com/reference/cli/overview).

### 2. Login

```bash
nexus whoami
```

If not logged in, ask for a developer PAT and run:

```bash
nexus login --token <PAT>
```

### 3. App id / register

Read `manifest.yaml` → `app.id`.

- If deploy fails because the app is not registered on the user's developer account, run `nexus register` (or the current CLI register flow), then write the new UUID back to `manifest.yaml` `app.id`.
- Confirm `app.version` is valid semver.

### 4. Site URL

Check `nexus settings list` for `default-site`. If it is missing, ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com`, and pass it as `-s`.

### 5. Install and deploy

```bash
npm install
npm run build-web && nexus deploy
```

Default environment: `development`. This is React Custom UI: [deploy](https://developer.pingcode.com/reference/cli/deploy) does not build the frontend. `resources[].path` is `web/main/dist` (page view) and `web/edit/dist` (edit dialog), so run `build-web` first. `npm run deploy` does the same.

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

See [distribute](https://developer.pingcode.com/reference/cli/distribute).

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode **Wiki** page and start editing.
2. In the insert menu, choose **HTML Preview** (manifest `extensions[].title`). The edit dialog opens immediately (`edit.openOnInsert`).
3. Confirm the starter HTML appears on the left and renders on the right, optionally edit the HTML, then save.
4. Confirm the page renders the HTML block.
5. Edit the block again, change the HTML, save, and confirm the page view updates.

Extension entry: [页面 - 文档内容块](https://developer.pingcode.com/reference/resource/extensions/wiki-document-block).

### 9. Optional local development

```bash
npm run start-web
nexus serve
```

`npm start` runs both. Vite ports are `nexus.json` `serve.resources.main.port` (`3100`, page view) and `serve.resources.edit.port` (`3101`, edit dialog). See [serve](https://developer.pingcode.com/reference/cli/serve).

## Notes

- Block `config` stores `html` only. The resolver is required by the extension and does not process HTML.
- Edit / page view both use a sandboxed `srcDoc` iframe (styles/scripts stay inside).
- Page view sets `allow-same-origin` and sizes with `contentDocument` + `ResizeObserver`.
- Inline `<script>` needs `permissions.content.scripts: [unsafe-inline]` because srcDoc inherits the extension CSP.
- Run `nexus` commands from `nexus-wiki-html-preview/` so the local CLI config is picked up.



