---
name: use-nexus-workitem-live-viewer
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-workitem-live-viewer example app. Use when the user asks to 一键部署本示例,
  deploy, install, set up, or run this Nexus work item Live Viewer example.
---

# Use nexus-workitem-live-viewer

Help the user run this example end-to-end. Work from `nexus-workitem-live-viewer` (this app root). Ask for the site URL when missing; do not invent CLI commands. Leave local CLI config as-is.

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

Ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com` → pass as `-s`. Check `nexus settings list` for `default-site` before asking, and use it when present.

### 5. Install and deploy

Custom UI: build the frontend before deploy. `npm run deploy` runs `build-web` and then `nexus deploy`.

```bash
npm install
npm run build-web && nexus deploy
```

(Default environment: `development`.)

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode work item detail page. Presence starts via the work item background extension; no panel click is needed.
2. In the right property sidebar, find the **Live Viewer** context module. Avatars appear inline under that title (horizontal row).
3. Open the same work item with another account (or another browser). Each side’s **Live Viewer** list shows the other person as soon as that person opens the work item detail page.
4. Leave the work item detail page or close the tab. `pagehide` / iframe teardown should publish `leave` and drop the person quickly. `view.onClose` is Dialog-only and does not run on work-item background. If leave is lost during unload, the person disappears after heartbeat stale (~15 seconds).

### 9. Optional local development

Start the frontend and the Nexus tunnel together. The Angular dev server port is `3111` (`nexus.json` `serve.resources.main.port`).

```bash
npm run start-web
nexus serve
```

Or `npm start` to run both.

## Notes

- Channel name is `viewers`. Realtime uses `scope: context` and `context: workitem` so the [background](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-background) publisher and the [context](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-context) subscriber share the same work item channel.
- Presence (heartbeat / leave) runs only in the background extension as soon as the work item detail page opens. The context module only subscribes and renders avatars inline.
- Display name and avatar come from `GET /v1/directory/users/{id}` (`display_name`, `avatar`) via [api.invoke](https://developer.pingcode.com/reference/functions/network/api). The list renders them with [thy-avatar](https://tethys.pingcode.com/components/avatar). Manifest scope: `pcp:read:global:team`. Image hosts are allowed with `permissions.external.images: *` because avatar URLs are chosen by the directory API.
- Manifest changes (new extension targets) require `nexus deploy` + `nexus distribute`; `nexus serve` alone does not register new extension points on the host.
- Run `nexus` commands from `nexus-workitem-live-viewer/`.
