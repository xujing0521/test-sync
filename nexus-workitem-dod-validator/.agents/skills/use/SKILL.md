---
name: use-nexus-workitem-dod-validator
description: >-
  One-click environment setup, deploy, distribute, and install guidance for the
  nexus-workitem-dod-validator example app. Use when the user asks to
  一键部署本示例, deploy, install, set up, or run this Nexus work item DoD
  validator example.
---

# Use nexus-workitem-dod-validator

Help the user run this example end-to-end. Work from `nexus-workitem-dod-validator` (this app root). Ask for secrets/URLs when missing; do not invent CLI commands.

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

- Ask for the PingCode enterprise site used for distribute, e.g. `https://{domain}.pingcode.com` → pass as `-s` (domain only is also fine if the CLI accepts it). Prefer asking the user; check `nexus settings list` for `default-site` if present.

### 5. Install and deploy

```bash
npm install
nexus deploy
```

Default environment: `development`. This is React Native UI: `nexus deploy` bundles `web/main` through the CLI builder. Do not run a separate frontend build.

### 6. Distribute

```bash
nexus distribute -s <site-url-or-domain> -e development
```

### 7. Enterprise install (manual)

There is **no** `nexus install` command. Tell the user to open the enterprise admin **App review** list and install this app.

### 8. Verify

1. Open a PingCode **project** → project settings → work item type → **workflow / state transition rules**.
2. Add a rule and choose the extension titled **DoD 校验** (`manifest.extensions[].title`).
3. In the create/edit dialog, toggle the three DoD rules and save.
4. Transition a work item that should fail (e.g. no logged workload, or no linked test cases) and confirm the validation error appears.

### 9. Optional local development

```bash
nexus serve
```

Native UI does not use a separate frontend dev server. `nexus.json` omits `serve.resources`; the CLI assigns a free port.

## Notes

- Backend handler is `dodValidate` (`WorkflowValidatorHandler`), not a UI `Resolver`.
- PingCode reads use `api.invoke` with scopes `pcp:read:pjm:workitem`、`pcp:read:global:workload` and `pcp:read:testhub:testcase`.
- Run `nexus` commands from `nexus-workitem-dod-validator/` so local `nexus.json` is picked up.
