---
name: use-nexus-agile-quiz
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-agile-quiz example app. Use when the user asks to 一键部署本示例, deploy,
  install, set up, or run this Nexus agile quiz example.
---

# Use nexus-agile-quiz

Help the user run this example end-to-end. Work from `nexus-agile-quiz` (this app root). Ask for secrets/URLs when missing; do not invent CLI commands.

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

(Default environment: `development`. Build frontend assets as required by this app before or via your local workflow if `nexus deploy` expects them.)

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode **project**, then in the project home navigation under the default **应用** section, open **敏捷开发问答** / **Agile Quiz** (manifest `pages[].title.i18n` → `app.title`), or go to `/pjm/projects/apps/{appId}/{envId}/agile-quiz`.
2. Confirm the quiz loads in the user's PingCode language (personal preference), questions/options render correctly, score on finish.

### 9. Optional local development

```bash
nexus serve
```

Start the frontend dev server as needed for this app (e.g. workspace `start-web` on port `3100`) alongside `nexus serve` per `nexus.json`.

## Notes

- Do not add Storage, REST, or other services for this example.
- Locale strategy: `i18n.createTranslator()` with no args follows host `view.getContext().user.locale` (PingCode user language preference).
- Run `nexus` commands from `nexus-agile-quiz/` so local `nexus.json` is picked up.
