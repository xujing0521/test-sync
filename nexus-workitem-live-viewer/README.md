# nexus-workitem-live-viewer

同一工作项被多人打开时，互相出现在查看者列表里。演示 Nexus [realtime](https://developer.pingcode.com/reference/interface/bridge/realtime)，以及 [工作项 - 详情后台脚本](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-background) 与 [工作项 - 详情上下文](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-context)。

打开工作项详情时，[background](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-background) 扩展即开始心跳上报，对方不必打开任何面板；右侧属性里的 **Live Viewer** 使用 [context](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-context) 内嵌横排头像，直接显示当前查看者。通道名是 `viewers`，`scope` 为 `context`、`context` 为 `workitem`，所以 background 与 context 能在同一工作项下互通。姓名和头像地址来自 `GET /v1/directory/users/{id}` 的 `display_name` 和 `avatar`，由 [api.invoke](https://developer.pingcode.com/reference/functions/network/api) 发起，再用 [thy-avatar](https://tethys.pingcode.com/components/avatar) 显示。离开详情页时通过 `pagehide` / 组件销毁发布 `leave`（[view.onClose](https://developer.pingcode.com/reference/interface/bridge/view) 仅 Dialog 可用，background 上无效）；若 leave 未送达，约 15 秒心跳超时后从列表消失。

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

Local debug: `npm start` (frontend dev server and `nexus serve`), or run `npm run start-web` and `nexus serve` yourself. Port comes from `nexus.json.serve.resources`.

Then install from enterprise admin **App review**.

Related commands: [deploy](https://developer.pingcode.com/reference/cli/deploy), [distribute](https://developer.pingcode.com/reference/cli/distribute), [serve](https://developer.pingcode.com/reference/cli/serve).
