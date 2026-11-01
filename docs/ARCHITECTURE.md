# CoBeing Foundation — 产品与网络边界

> 这是方向和安全边界，不代表所有功能均已实现。CoBeing 是共用的后端能力网络，而非一个新的日常主应用。

## 两个不同但相互连接的网络

**Personal Mesh：个人的能力自治网络。** 用户拥有自己的 PC/Mac、Local Bridge、Agent、云 Bot、现有文件和消息服务；CoBeing 帮助本人发现、配对并在受控范围内调用这些资源。即使用户没有建立任何好友关系，Personal Mesh 仍然有价值。

**CoBeing Network：跨人和 Agent 的授权共生网络。** 不同人各自管理自己的 Personal Mesh，通过双方认可的关系、具体资源权限和确认完成协作。仅加为联系人不开放对方节点列表、设备、聊天、文件或私人 Vault。

**CoBeing Account / Identity Core**：最小共享身份内核，只负责稳定用户身份、登录方式、应用身份及授权、账户生命周期。**Memory Service、Personal Mesh Service、CoBeing Network Service** 各自拥有自己的业务数据和具体资源授权；它们是可选功能，不属于 Account Core。CoBeing 不充当每项任务的强制代理网关、完整个人数据仓库或社交聊天平台。

```text
个人聊天助手          WorldDesk            更多独立产品
     |                   |                    |
     +------------- 按需调用 -----------------+
                         |
         Memory     Personal Mesh    CoBeing Network
           |            |                |
           +------------+----------------+
                         |
                   CoBeing Account
             用户身份 / 登录 / App 授权

 Personal Mesh 独立技术 → Local Bridge / Cloud Claw
 （本机无需 CoBeing 账号即可正常工作）
```

## 上层应用的责任

- **个人聊天助手**：用户自己选定沟通文本，形成建议与关系体验；不默认将私信搬进共享 Basic。实际消息收发由原应用或已授权的 Provider 负责。
- **WorldDesk**：观察、任务与桌面体验；可以默认打包 Local Bridge，但 Bridge 核心继续独立，不认识 WorldDesk 或特定企业应用。
- **其他应用**：用清晰的身份与作用域复用 CoBeing 的基础能力，不因“同一个用户”就默认互读每个 App 的全部私有数据。
- **CoBeing Console**：身份、记忆、授权和设备管理的必要入口，不发展为第三个消费者主应用。

## 连接与权限的三层区别

1. **节点声明**：资源所有者记录“我有一个 Local Bridge / Cloud Agent”；此时不表示已安装、在线或能远程调用。
2. **可信配对**：双方以一次性挑战和设备私钥证明关联，建立撤销能力；只有通过真实验证才能显示为已连接。
3. **执行授权**：按调用者、目标、动作、时间、范围明确许可；发送消息、写文件等操作需特别确认。授权不因关系建立而自动出现。

**Personal Mesh ≠ 强制物理 Mesh、P2P、VPN 或新通讯协议。** 先复用同机 MCP/HTTP、现有 Local Bridge、已授权 Cloud Agent；异机需求出现时再选可靠的出站安全连接或中转。只有用户实际需要实时双向通道时才评估长期 WebSocket/其他传输。

## 控制面与执行面

| 部分 | 应当负责 | 不承担 |
| --- | --- | --- |
| Account / Identity Core | 登录、稳定身份、应用身份/基本授权和账户生命周期 | 记忆正文、好友关系、设备目录、Agent 执行 |
| 可选 Memory / Mesh / Network 服务 | 各自的数据、资源权限与撤销；复用 Account 验证主体 | 自动共享好友设备、强制 AI 模型托管 |
| Personal Mesh 节点 | 执行已授权任务、管理本机资源和原系统权限 | 将私有资源全部上传 Cloudflare |
| CoBeing Network | 让指定用户按明确请求安全协作 | 公开好友的 Agent、自动互授权限 |
| 上层应用 | 用户目标、场景、选择数据、用户确认、结果体验 | 自建另一套 CoBeing 网络 |

用户自己的 Personal Vault 可存详细历史；Basic 仅存用户确认的少量基础记忆。托管 Basic 在授权访问时服务端可能读取明文；若未真正实现 E2EE，不得声称“服务端不可见”。

## 对第三方和开发者的最小契约

- 区分用户身份、App 客户端身份、节点身份和特定调用授权。
- External Agent 不直接拿用户登录 Cookie 或对方的第三方密钥；远程 MCP 逐步按官方 OAuth 资源受众绑定规范互通。
- 关系可断开、具体授权可撤销；撤销不能消除外部已保存的内容。
- 跨用户只公开 Owner 主动声明的某个**可申请能力**，不展示私人节点拓扑、IP/主机名、文件路径或凭据。
- 各 App 不依赖 CoBeing 才能完成自己的全部核心操作；CoBeing 增强跨应用记忆和协作。

## 实际发布边界

R0 的少量账号、记忆、关系邀请与只读 MCP 能力正在私有孵化；单个节点登记到真实设备配对、跨设备任务、跨用户授权执行都需要独立实测。公开仓库没有自动包含私有孵化代码。

Local Bridge / Cloud Claw 等继续是独立能力供应者，既可被 CoBeing 应用使用，也可服务其他客户端；不为 CoBeing 强制重写。
