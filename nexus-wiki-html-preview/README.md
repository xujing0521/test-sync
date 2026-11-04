# nexus-wiki-html-preview — HTML Preview

在 Wiki 页面中插入 HTML 内容块：编辑弹窗左侧输入 HTML，右侧实时预览。演示 Nexus [页面 - 文档内容块](https://developer.pingcode.com/reference/resource/extensions/wiki-document-block) 与 React [Custom UI](https://developer.pingcode.com/guide/development/custom-ui-with-react)。

编辑弹窗通过 [view.submit](https://developer.pingcode.com/reference/interface/bridge/view) 写入 `config.html`。阅读态首次用 `view.getContext()`；之后每次保存宿主派发 `NEXUS_EXTENSION_DATA_CONFIG_CHANGED`（见 [events](https://developer.pingcode.com/reference/interface/bridge/events)），main 订阅后更新渲染。

## Prerequisites

See [Getting started](https://developer.pingcode.com/guide/started/setup).

## Quick start

In Cursor, open this directory and ask the agent:

> 一键部署本示例

See [`.agents/skills/use/SKILL.md`](./.agents/skills/use/SKILL.md).

Or manually (see [CLI](https://developer.pingcode.com/reference/cli/overview)).

```bash
npm install
npm run build-web && nexus deploy
nexus distribute -s <your-domain>.pingcode.com -e development
```

Local debug: `npm start` (frontend dev servers and `nexus serve`), or run `npm run start-web` and `nexus serve` yourself. Ports come from `nexus.json.serve.resources` (`main` 3100, `edit` 3101).

Then install from enterprise admin **App review**.

Related commands: [deploy](https://developer.pingcode.com/reference/cli/deploy), [distribute](https://developer.pingcode.com/reference/cli/distribute), [serve](https://developer.pingcode.com/reference/cli/serve).
