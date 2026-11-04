# Nexus Example Apps

Example apps for [Nexus](https://developer.pingcode.com/). This repository collects focused demos you can deploy and try it in PingCode.

> Maintainers: one-way sync to the public mirror is documented in [`docs/sync-public.md`](./docs/sync-public.md).

## Examples

| App | Path | Demonstrates |
|-----|------|----------------|
| **nexus-agile-quiz** | [`nexus-agile-quiz`](./nexus-agile-quiz) | 敏捷开发问答 / Agile Quiz (Scrum / Kanban) on [Project — Home navigation](https://developer.pingcode.com/reference/resource/extensions/pjm-project-hub) + Nexus [i18n](https://developer.pingcode.com/guide/advanced/translations) |
| **nexus-external-profile** | [`nexus-external-profile`](./nexus-external-profile) | GitHub 账号绑定 / 重新绑定 on [Account — Personal settings](https://developer.pingcode.com/reference/resource/extensions/global-personal-setting) + [fetch.request](https://developer.pingcode.com/reference/functions/network/fetch) + [KVS](https://developer.pingcode.com/reference/functions/storage/kvs) |
| **nexus-workitem-live-viewer** | [`nexus-workitem-live-viewer`](./nexus-workitem-live-viewer) | 同一工作项的查看者列表 on [工作项 - 详情后台脚本](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-background) + [工作项 - 详情上下文](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-context) + [realtime](https://developer.pingcode.com/reference/interface/bridge/realtime) (`context` / `workitem`) |
| **nexus-hello-world-angular-native-ui** | [`nexus-hello-world-angular-native-ui`](./nexus-hello-world-angular-native-ui) | Hello World on [Project — Component page](https://developer.pingcode.com/reference/resource/extensions/pjm-project-page) with Angular [Native UI](https://developer.pingcode.com/guide/development/user-interface-native-ui) |
| **nexus-hello-world-react-native-ui** | [`nexus-hello-world-react-native-ui`](./nexus-hello-world-react-native-ui) | Hello World on [Project — Component page](https://developer.pingcode.com/reference/resource/extensions/pjm-project-page) with React [Native UI](https://developer.pingcode.com/guide/development/native-ui-with-react) |
| **nexus-hello-world-react-custom-ui** | [`nexus-hello-world-react-custom-ui`](./nexus-hello-world-react-custom-ui) | Hello World on [Project — Component page](https://developer.pingcode.com/reference/resource/extensions/pjm-project-page) with React [Custom UI](https://developer.pingcode.com/guide/development/custom-ui-with-react) |
| **nexus-hello-world-angular-custom-ui** | [`nexus-hello-world-angular-custom-ui`](./nexus-hello-world-angular-custom-ui) | Hello World on [Project — Component page](https://developer.pingcode.com/reference/resource/extensions/pjm-project-page) with Angular [Custom UI](https://developer.pingcode.com/guide/development/custom-ui-with-angular) |
| **nexus-my-todos-widget** | [`nexus-my-todos-widget`](./nexus-my-todos-widget) | 我的待办 on [工作台 - 仪表盘部件](https://developer.pingcode.com/reference/resource/extensions/global-dashboard-widget), stored with [CES](https://developer.pingcode.com/reference/functions/storage/ces) |
| **nexus-project-attachments** | [`nexus-project-attachments`](./nexus-project-attachments) | 项目附件库（Angular Custom UI）on [Project — Component page](https://developer.pingcode.com/reference/resource/extensions/pjm-project-page) + [Storage](https://developer.pingcode.com/reference/functions/storage) NOS + CES |
| **nexus-wiki-html-preview** | [`nexus-wiki-html-preview`](./nexus-wiki-html-preview) | Wiki HTML Preview（左侧编辑 / 右侧实时渲染，React Custom UI）on [页面 - 文档内容块](https://developer.pingcode.com/reference/resource/extensions/wiki-document-block) |
| **nexus-workitem-dod-validator** | [`nexus-workitem-dod-validator`](./nexus-workitem-dod-validator) | 工作项 DoD 校验（可配置工时 / 子任务 / 关联缺陷）on [工作项 - 工作流验证](https://developer.pingcode.com/reference/resource/extensions/pjm-workitem-validator) + Angular [Native UI](https://developer.pingcode.com/guide/development/native-ui-with-angular) |

## Public snapshot notes

This public mirror ships example apps **without** `manifest.yaml` `app.id` and **without** `nexus.json` `remoteUrl`. Obtain an app id with `nexus register` and point the CLI at your environment before deploy — see the [Nexus developer docs](https://developer.pingcode.com/) and each app's README / one-click skill.
