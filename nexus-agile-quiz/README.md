# nexus-agile-quiz — 敏捷开发问答 / Agile Quiz

A single-page agile development quiz (Scrum / Kanban / practices). Demonstrates Nexus [i18n](https://developer.pingcode.com/guide/advanced/translations). Extension entry: [Project — Home navigation](https://developer.pingcode.com/reference/resource/extensions/pjm-project-hub).

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
