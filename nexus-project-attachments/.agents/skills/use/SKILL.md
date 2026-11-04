---
name: use-nexus-project-attachments
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-project-attachments example app. Use when the user asks to 一键部署本示例,
  deploy, install, set up, or run this Nexus project attachments example.
---

# Use nexus-project-attachments

Help the user run this example end-to-end. Work from `nexus-project-attachments` (this app root). Ask for secrets/URLs when missing; do not invent CLI commands.

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

- Ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com` → pass as `-s`.

### 5. Install and deploy

```bash
npm install
nexus deploy
```

This app is Angular Custom UI: ensure frontend build runs (`npm run build-web` or via the root `deploy` script) before / as part of deploy so `web/main/dist` exists for `manifest.resources`.

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode **project**. In the project primary navigation, open **附件** (manifest extension title), or go to `/pjm/projects/{identifier}/apps/{appId}/{envId}/attachments`.
2. Confirm the list loads; try upload（`store.upload` + confirm）, rename（点重命名后名称列变为 input，回车保存）, re-upload（新 NOS key 上传后更新 CES 并删除旧对象）, download（`store.download`）, and delete.
3. Confirm keyword search filters by file name; list is `uploaded_at` descending（无列排序、无类型筛选）.

### 9. Optional local development

Custom UI needs both:

```bash
npm run start-web
nexus serve
```

Frontend port is `3100` per `nexus.json` `serve.resources.main.port`.

## Notes

- Storage scope `pcp:storage:app`, directory scope `pcp:read:global:team` (list resolves uploader display names), and CES entity `attachment` are declared in `manifest.yaml`.
- This example intentionally has **no i18n / locales**, **no type filter**, and **no column sorting**.
- File pick uses same-page hidden `<input type="file">`（Custom UI，保留用户手势）.
- Run `nexus` commands from `nexus-project-attachments/` so local `nexus.json` is picked up.
