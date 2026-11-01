# CoBeing 面向独立应用的最小接入约定

CoBeing 服务于 WorldDesk、个人聊天助手和未来独立产品，**不要求任何产品先接入 CoBeing 才能完成其核心业务**。优先做少量稳定、可验证的应用服务，而不是建设新的开发者门户、模型网关或全功能社交平台。

## 服务选择

| 模块 | 上层应用为什么需要它 | 当前成熟程度 |
|---|---|---|
| Account | 明确建立稳定身份，跨应用同步或分享的信任基础 | CoBeing 自己的 GitHub 登录已有；**对第三方发布 OIDC 仍未交付** |
| Memory | 用户主动保存、纠正、删除的基础偏好与背景，按 App 许可读取 | R0 增删改查、导出及手工授权只读 MCP；**尚无独立 App 作用域 Token** |
| CoBeing Network | 经双方确认的关系及未来明确指定的共享 | 双向邀请/断开；**没有自动跨人共享授权** |
| Personal Mesh | 已有 Local Bridge / Cloud Agent / 本地资源按需连接 | 独立能力组件；私有节点声明不等于配对或任务执行 |
| Service Discovery | 让其他应用准确了解当前部署支持什么 | 私有 R0 分支新增 `GET /api/services`，尚未发布线上 |

## 真实用户体验

WorldDesk 当前公开预览独立运行，拥有本地收藏/地图、观察画面和已打包的 Local Bridge。CoBeing 只能在用户主动启用同步、共享或身份功能时出现，不应把已有观察流程搬进账户内核。

Companion / 个人聊天助手当前可以从用户主动选择的文本生成沟通建议。用户点击“帮我记”时，才有理由连接 CoBeing Memory 保存**用户明确选中的内容**；不默认同步私信、微信历史和 Agent 的完整本轮上下文。

企业应用和其他第三方产品可以独立提供自己的 SSO、数据权限与本地 Agent。CoBeing 不替换其业务授权系统。

## 核心安全界面

- **目前的 GitHub 登录只证明 CoBeing 是 GitHub OAuth 的客户端**。其他 App 不能复制 CoBeing Account Console 的浏览器 Cookie，也不能把手工 MCP 记忆 Bearer Token 当作用户登录。
- 未来跨应用登录按标准 OAuth/OIDC Authorization Code + PKCE 处理。每个 App 有独立 `client_id`、精确回调、授权同意及可撤销的范围。首先只为 WorldDesk 与 Companion 两个首方客户端试点；不默认向任意公网来源开放客户端动态注册。
- 初步 Scope 规划：`openid profile` 用于确认身份；`memory:read` 与 `memory:write` 仅在用户选择记忆功能后请求。更敏感的关系分享、设备调用需另行批准，不属于身份登录的默认权限。
- **现有手工 `memory:read` MCP 授权可以读取当前及之后新增的全部 Basic Memory 记录**（一个用户的范围）；不是逐条记忆授权，也不是“任何 App 读我的资料”的通用通道。接入其他 App 前要进一步缩小。
- Network 的好友关系不是权限，Mesh 的节点声明也不是真实在线或可调用的证据。
- 可公开的服务能力描述仅用于发现，不能代替端点校验、身份验证、权限或用户同意。

## 为什么先有一个小型服务能力描述

在私有 R0 中新增 `GET /api/services`（`cobeing.services.v1`），用 JSON 声明当前的可用性及缺失功能，供独立应用**在用户要求启用 CoBeing 时**进行无 Cookie 的只读能力检查。它不包含用户数据、应用授权密钥或内部节点信息。

该接口并非 OAuth/OIDC 的 `/.well-known` 发现端点，也不属于 MCP 规范认证元数据。等真正实现 OIDC Provider / MCP OAuth 之后，必须分别发布各自的**标准元数据和资源受众**，不能用 CoBeing 的私有描述字段冒充标准。

## 迭代次序

1. 当前 CoBeing Basic 的用户身份、记忆、邀请保持可用；不要引入破坏现有用户 ID 和 Session 的数据库重构。
2. 在私有分支实现并验证基于现有 Better Auth 的最小 OIDC Provider，先只向两个明确登记的首方 App 开放；不新建一个身份项目。
3. Companion 按需读取/写入用户明确同意的记忆，完成访问撤销；WorldDesk 首次接入只选择一个明显有价值的同步/分享场景。
4. 后续有跨人的实际使用需求时实现单项共享/撤销，再考虑更广泛第三方开发者接入。
5. Personal Mesh / Local Bridge 本机调用完全独立于 CoBeing Account；跨设备采用已有合法通道或验证过的 P2P/Relay，不强迫安装额外 VPN。

## 当前交付状态

本公开仓库描述的是架构方向；**不代表 CoBeing 已作为可供第三方使用的 OIDC 提供方、跨人权限系统或远程 Agent 网关**。独立应用可以先保持自己的功能，只有明确需要时再考虑可选的 CoBeing 服务。

参考：[RFC 9700 OAuth 最佳实践](https://www.rfc-editor.org/rfc/rfc9700) · [Better Auth OAuth Provider](https://www.better-auth.com/docs/plugins/oauth-provider) · [MCP 授权](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization)
