---
name: use-nexus-my-todos-widget
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-my-todos-widget example app. Use when the user asks to 一键部署本示例,
  deploy, install, set up, or run this Nexus todos dashboard widget.
---

# Use nexus-my-todos-widget

Help the user run this example end-to-end. Work from `nexus-my-todos-widget` (this app root). Ask for secrets/URLs when missing; do not invent CLI commands.

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

- Ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com` → pass as `-s`. Check `nexus settings list` for `default-site` before asking.

### 5. Install and deploy

```bash
npm install
npm run build-web && nexus deploy
```

`npm run deploy` does the same build-then-deploy. This is Angular Custom UI: `resources[].path` is `web/main/dist`, so the frontend must be built before deploy.

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode **dashboard** (工作台). Add the widget **我的待办**.
2. On the dashboard (view mode) add a todo, check it off, and delete one. Each change calls the `save` resolver and writes one CES `todos` record for that widget id. The record's `items` array holds the list, and `[]` means the list was cleared. The visible rows follow config: at most `limit` items (`10`, `20`, or `50`), keeping the most recently created ones when the list is longer, and completed items are hidden when `show_done` is `false`. There is no **取消** / **确定** bar, and `view.submit()` is not used in this mode.
3. Open the widget editor (edit mode). The list and add action are not shown. Set **显示条数** and **显示完成待办** (default `10` and shown), then **确定**, which calls `view.submit({ config })`. Adding a widget has no widget id yet, so **确定** only submits config and does not write CES. This resource cannot call `view.close()`.
4. Refresh the dashboard. The list should still match what was saved, including an empty list, and it should respect the saved display count and completed-item setting.

### 9. Optional local development

```bash
nexus serve
```

Start the frontend dev server (`npm run start-web`, `ng serve` on port `3100`) alongside `nexus serve`. The port is `nexus.json` `serve.resources.main.port`.

## Notes

- View mode stores one [CES](https://developer.pingcode.com/reference/functions/storage/ces) `todos` record per widget through the `save` resolver (`pcp:storage:app`). `items` is the todo array. No record means the widget has not been saved in view mode; `items: []` means the list was cleared. The view resource cannot call `view.submit()`.
- Edit mode only submits display config with [`view.submit()`](https://developer.pingcode.com/reference/interface/bridge/view): `limit` (`10` / `20` / `50`, default `10`) and `show_done` (default `true`). It does not edit the todo list. This module does not support `view.onSubmit`.
- This example has no i18n / locales. UI copy is Chinese, same as `nexus-project-attachments`.
- Run `nexus` commands from `nexus-my-todos-widget/` so local `nexus.json` is picked up.
