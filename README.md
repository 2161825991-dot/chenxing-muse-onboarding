# 辰星 Agent 接入说明

**正式 Funnel 入口已上线，等待外部 Dot 实际验证。** Mac 普通 HTTPS、Chrome 健康页和无邀请码接入页已通过；新身份七步登记/配对协议及过期、安全边界已测试。这不代表目标 Chrome 已真实绑定、插件已就绪或 Dot 已连上。

GitHub 是固定说明入口，不是 API、网络代理或业务中转。Agent 是统一入口称谓；当前仅沿用已发布的 public_product 客户端协议，不表示已接入其他 SDK。

## Agent 接入 / 浏览器绑定 / Agent 状态

读取 [Agent接入提示词](MUSE_PROMPT.txt) 和 [connection.json](connection.json)。当前正式来源：

- [无凭据健康页](https://mhcmac-mini.tail54a02e.ts.net/onboard/v1/health)
- [公开 bootstrap](https://mhcmac-mini.tail54a02e.ts.net/onboard/v1/bootstrap)
- [无邀请码接入页](https://mhcmac-mini.tail54a02e.ts.net/onboard/join)
- [正式客户端资源包](https://mhcmac-mini.tail54a02e.ts.net/onboard/client.zip)

先做普通 HTTPS GET，必须正常验证证书及域名，不跟随重定向、不附带凭据。失败时保留实际错误并停止；不要绕过证书警告、改用私网地址或把泛化工具错误直接解释为 TLS 错误。

bootstrap 必须为 `chenxing.muse-bootstrap/v1`，server_id 为 `935ebdcb-83b1-4469-b380-be6d98d0fd2e`，network.endpoint 必须等于 connection.json 的完整 public_origin。只保存白名单四个文件：mac_read_client.py、join.py、endpoint_policy.py、trusted-endpoints.json；逐文件解码并核对 bytes 与 SHA-256，放在同一私密目录。

一次性邀请链接由用户**另外私下提供**。GET 页面或 bootstrap 不兑换邀请。使用验证后的正式客户端独立登记，先读自己的 capabilities，再申请 pair-window 短码；用户只在指定 Chrome 窗口确认。长凭据仅存 Agent 本地私密 profile，不发聊天或 GitHub。

## 范围与当前限制

新身份仅为 public_product：本人窗口配对、本人已绑定窗口中的美客多公开商品 `read_product_json`，以及本人状态和原任务。不开放 ERP 管理或数据、订单、采购、设备执行凭据、付费 AI 或平台修改。首次验证先不创建商品任务；配对接口成功与真实窗口/插件就绪分开报告。

正式来源为上面的单 Mac Funnel HTTPS 地址，旧 Cloudflare 仅由运行方保留作服务回退，客户端不能因 blocked 而自行切域名或代理。`dot_verified=false`，仍需 Dot 在自己的真实环境验证。遇安全拒绝停止并报告原因；未知请求保留原号，只回查，不自动重发。

本仓库始终只有说明和公开合同，不存邀请、profile、秘密或客户端脚本，也不通过 GitHub Actions 执行业务。
