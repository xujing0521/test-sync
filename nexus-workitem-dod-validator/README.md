# nexus-workitem-dod-validator — 工作项 DoD 校验

可配置的工作项完成定义（DoD）校验器：在状态流转时检查已登记工时、子任务完成情况与关联测试用例数量。Demonstrates Nexus [工作项 - 工作流验证](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-validator)（`pcm:pjm:workitem:validator`），配置弹窗使用 React [Native UI](https://developer.pingcode.com/guide/development/native-ui-with-react)。

## Prerequisites

Environment, account, and CLI setup: [Getting started](https://developer.pingcode.com/guide/started/setup).

## Quick start

In Cursor, open this directory and ask the agent:

> 一键部署本示例

See [`.agents/skills/use/SKILL.md`](./.agents/skills/use/SKILL.md).

Or manually (see [CLI](https://developer.pingcode.com/reference/cli/overview)):

```bash
npm install
nexus deploy
nexus distribute -s <your-domain>.pingcode.com -e development
```

Then install from enterprise admin **App review**. Local debug: run `nexus serve` from this directory.

Related commands: [deploy](https://developer.pingcode.com/reference/cli/deploy), [distribute](https://developer.pingcode.com/reference/cli/distribute), [serve](https://developer.pingcode.com/reference/cli/serve).
