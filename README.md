# 辰星 Agent 接入说明

**服务已就绪，等待 Dot 实际接入验证。** 运行方已用 Mac 空白客户端经公开 HTTPS 完成登记、capabilities 和窗口短码流程；这不代表 Dot 已连上，也不代表已读取商品。

GitHub 是固定说明入口，不是 API、网络代理或业务中转。Agent 是统一入口称谓；当前仅沿用已发布的 public_product 客户端协议，不表示已接入其他 SDK。

## Agent 接入 / 浏览器绑定 / Agent 状态

读取 [Agent接入提示词](MUSE_PROMPT.txt) 和 [connection.json](connection.json)。当前临时来源：

- [无凭据健康页](https://collectibles-wallet-offices-stocks.trycloudflare.com/onboard/v1/health)
- [公开 bootstrap](https://collectibles-wallet-offices-stocks.trycloudflare.com/onboard/v1/bootstrap)

先做普通 HTTPS GET，必须正常验证证书及域名，不跟随重定向、不附带凭据。失败时保留实际错误并停止；不要绕过证书警告、改用私网地址或把泛化工具错误直接解释为 TLS 错误。

bootstrap 必须为 `chenxing.muse-bootstrap/v1`，server_id 为 `935ebdcb-83b1-4469-b380-be6d98d0fd2e`，network.endpoint 必须等于 connection.json 的完整 public_origin。只保存白名单四个文件：mac_read_client.py、join.py、endpoint_policy.py、trusted-endpoints.json；逐文件解码并核对 bytes 与 SHA-256，放在同一私密目录。

一次性邀请链接由用户**另外私下提供**。GET 页面或 bootstrap 不兑换邀请。使用验证后的正式客户端独立登记，先读自己的 capabilities，再申请 pair-window 短码；用户只在指定 Chrome 窗口确认。长凭据仅存 Agent 本地私密 profile，不发聊天或 GitHub。

## 范围与当前限制

新身份仅为 public_product：自己的窗口配对、用户授权的公开商品读取及原任务状态。不授予 ERP 预览/写入、admin、设备执行凭据、付费 AI 或平台修改权限。首次接入验证先不创建商品任务。

本域名为临时 Quick Tunnel，可能更换；稳定入口仍待运行方另行完成。`dot_verified=false`，需要 Dot 在自己的真实运行环境验证。未知请求保留原号，只回查，不自动重发。

本仓库始终只有说明和公开合同，不存邀请、profile、秘密或客户端脚本，也不通过 GitHub Actions 执行业务。
