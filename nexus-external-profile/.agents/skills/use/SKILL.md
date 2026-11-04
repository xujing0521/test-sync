---
name: use-nexus-external-profile
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-external-profile example app. Use when the user asks to 一键部署本示例,
  deploy, install, set up, or run this Nexus external profile example.
---

# Use nexus-external-profile

Help the user run this example end-to-end. Work from `nexus-external-profile` (this app root). Ask for the site URL when missing; do not invent CLI commands. Leave local CLI config as-is.

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

Ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com` → pass as `-s`. Check `nexus settings list` for `default-site` before asking.

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

1. Open PingCode **account settings** (`/account/...`).
2. In the side nav, open section **外部资料**, then the **GitHub** page (route `github`).
3. The first visit loads the public profile for `octocat` (demo only, not stored) and shows a **绑定** button.
4. Enter a GitHub username and choose **绑定** (empty input binds the currently shown name). The current value becomes that username and the button becomes **重新绑定**. Reopen the page; it loads the bound username without typing it again.
5. Enter another username and choose **重新绑定** to replace the binding. A missing user shows an error and does not replace the saved username. No token, OAuth, or environment variable is required.

### 9. Optional local development

Start the frontend and the Nexus tunnel together. The Angular `ng serve` port is `3110` (`nexus.json` `serve.resources.main.port`).

```bash
npm run start-web
nexus serve
```

Or `npm start` to run both.

## Notes

- Do not call GitHub from the browser. The resolver uses `fetch.request` for `GET https://api.github.com/users/{username}`.
- A successful **绑定 / 重新绑定** stores only the GitHub username with [KVS](https://developer.pingcode.com/reference/functions/storage/kvs). The manifest scope is `pcp:storage:app`. The key includes the PingCode user id, so each person keeps their own binding.
- `permissions.external.fetch.backend` includes `api.github.com`. The avatar host is `https://avatars.githubusercontent.com` under `permissions.external.images`.
- Anonymous GitHub requests are limited to 60 per hour for each egress IP. The resolver caches a successful lookup for 10 minutes.
- Run `nexus` commands from `nexus-external-profile/`.
