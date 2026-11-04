# nexus-my-todos-widget — 我的待办

A personal todo list for the PingCode dashboard. View mode saves each add, check, and delete immediately through the `save` resolver ([CES](https://developer.pingcode.com/reference/functions/storage/ces) entity `todos`), and shows the list according to widget config: display count (`10` / `20` / `50`) and whether completed items are shown. Edit mode only sets that config, then **确定** calls [`view.submit()`](https://developer.pingcode.com/reference/interface/bridge/view). Extension entry: [工作台 - 仪表盘部件](https://developer.pingcode.com/reference/resource/extensions/global-dashboard-widget).

## Prerequisites

See [Getting started](https://developer.pingcode.com/guide/started/setup).

## Quick start

In Cursor, open this directory and ask the agent:

> 一键部署本示例

See [`.agents/skills/use/SKILL.md`](./.agents/skills/use/SKILL.md).

Or manually (see [CLI](https://developer.pingcode.com/reference/cli/overview)).

Custom UI — build the frontend, then deploy ([deploy](https://developer.pingcode.com/reference/cli/deploy) runs against `web/main/dist`):

```bash
npm install
npm run build-web && nexus deploy
nexus distribute -s <your-domain>.pingcode.com -e development
```

Local debug: `npm start` (frontend dev server and `nexus serve`), or run `npm run start-web` and `nexus serve` yourself. Port comes from `nexus.json` `serve.resources`.

Then install from enterprise admin **App review**.

Related commands: [deploy](https://developer.pingcode.com/reference/cli/deploy), [distribute](https://developer.pingcode.com/reference/cli/distribute), [serve](https://developer.pingcode.com/reference/cli/serve).
