# CoBeing — 公开发展路线

**方向性路线，不承诺具体日期；先实现一个真实用户场景再扩展抽象。** CoBeing 是后台共生能力网络；用户体验来自个人聊天助手、WorldDesk 等独立应用。

## R0 — 最小 CoBeing Account + 可选服务

- Account 是 CoBeing 在线服务的最小身份依赖；Memory 与 Network 按需独立。Personal Mesh 首先是可离线/本机独立工作的能力组件，远端登记及授权是可选适配。现阶段优先逻辑边界，不为了拆分概念新建 Worker/DB。
- Local Bridge 的本地 Agent 能力不应强制用户登录 CoBeing，CoBeing 不反向依赖 Local Bridge 才能完成身份认证。

- 已有基础：GitHub 身份登录、按用户隔离的 Basic Memory、记忆导出/删除、双方关系邀请、有限只读 Agent MCP。
- 最小个人资源目录：所有者登记自己拥有的设备、Local Bridge、Cloud Agent，**登记与真实配对严格区分**。
- 应用复用统一身份和基本记忆；CoBeing 自身只保留账户/授权管理入口，不开发第三个消费者 App。
- 首次发布稳定、有实测价值的能力，保持未成熟第三方实验私有。

## R0.5 — 给独立应用一个真正可用的入口

- 先让独立应用能够查询**公开、无用户数据的服务能力描述**，区分已实现和未实现模块；当前仅私有 R0 代码，尚未线上发布。
- 在现有 CoBeing Account 之上验证 OAuth/OIDC Provider，先只接入 WorldDesk 和 Companion 两个明确登记的客户端，要求 PKCE、精确回调、受众/权限控制和撤销。**当前 GitHub 登录并不等于 CoBeing 已是 OIDC Provider。**
- 首个实际业务以 Companion 用户主动保存/读取一条基础记忆为目标；WorldDesk 不登录仍应正常运行。不要开放通用 Agent 执行和公开第三方应用市场。
- 并行在私有 integrations-lab 验证 [Capability Sharing V1](CAPABILITY_SHARING_V1.md) 的**种子网络**：新加坡阿里云 QwenPaw + 上海本地服务；先完成单项公开文本任务的合成测试及明确授权，不冒充真实跨人生产调用，也不强制登录 CoBeing。

## R1 — 让能力组件解决真实用户痛点

- Local Bridge 继续优先复用已有本机 Agent 和专业软件；Personal Mesh 只有跨设备或备选能力需求出现时才加入执行链路。
- 不要求用户逐项登记设备和创建网络拓扑，已有组件应优先按原系统权限发现并工作。
- 用户应只看到任务结果或必须处理的配对/权限提示；失败时不虚报执行完成。


- 用户同意的一次性节点配对，可信密钥、有限能力证明与撤销。
- 一个已安装的 Local Bridge 或用户 Cloud Agent 完成一次用户选择的非破坏性任务。
- 个人聊天助手和 WorldDesk 复用该能力，任务在原有 Agent/本地软件执行，不把 CoBeing 变成模型网关。
- Personal Vault、可选备份/同步按真实需求补齐，避免提前建设 VPN/TURN/复杂任务中台。

## R2 — CoBeing Network 的真实价值

- 指定伙伴收到分享邀请、Owner **明确发布一项具体能力 Offer** 后，申请者才能取得有限授权 Grant；有好友关系并不等于自动开放能力。另一位贡献者可复用相同接口接入，不需要修改 CoBeing Core。
- 拥有者确认、能力执行、结果返回、按需最小审计和撤销构成首个跨人协作闭环。
- 经过实测，再扩展到应用间分享与明确受托的 Agent 间协作。

## 延后

全网公开设备目录、自动共享好友记忆、CoBeing 自带完整 Messenger、统一自建 LLM 网关、预设收费协作市场、DAO、无线 Meshtastic 适配、复杂 P2P 隧道与未验证的第三方集成。

稳定组件的独立 Public 仓库按其真实可用程度决定，不批量创建空仓库，不公开未清理的 Private 开发历史。见 [开源发布规范](OPEN_SOURCE_POLICY.md)。
