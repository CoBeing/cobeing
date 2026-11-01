# CoBeing · 共生网络

**People, personal AI agents, memories and digital resources — connected on their own terms.**

CoBeing 是开放的个人 AI 共生网络：连接用户已有手机、电脑、云端 Claw/Bot、社交应用、Agent 和记忆；优先复用，而不是要求用户迁移到封闭平台。

## 最小架构

| 模块 | 职责 |
| --- | --- |
| 1. Mobile Entry（必要） | 手机轻入口、Web、系统能力和现有应用接入 |
| 4. CoBeing Basic（必要） | 身份、个人基础记忆、关系、授权、资源目录 |
| 2. Local Bridge（可选） | 本机 PC/Mac、MCP、微信 Provider 等能力 |
| 3. Cloud Claw / Bot（可选） | 用户自己的云端 Agent 或可授权使用的服务 |

**1 + 4** 形成基本身份、记忆与关系网络；**1 + 4 +（2 或 3）** 形成智能任务能力。Basic 不是必须运行大模型的中心服务。

## 原则

- 成熟成果优先开源；不成熟的中间开发和第三方集成先隔离。
- 优先复用已有设备、应用、Agent 和开放接口。
- 私人记忆按用户隔离，支持授权、撤销、修正与迁移。
- 保持 Mobile、Basic、本地与云端资源之间的松散耦合。

**状态：R0 规划/孵化期。** 此公开仓库发布稳定方向与公开规范，当前不代表已经交付生产服务。可运行组件成熟后将以独立 Public 仓库发布。

[架构边界](docs/ARCHITECTURE.md) · [公开路线图](docs/ROADMAP.md) · [发布规范](docs/OPEN_SOURCE_POLICY.md)

License: [Apache-2.0](LICENSE). 第三方项目保留各自许可证。
