# 辰星 Muse 接入说明

这是公开说明入口，不是 ERP、网络代理或业务执行端。

**当前状态：仅开放无凭据健康页测试，正式接入仍未就绪，不能登记新客户端。**

运行方验证完成后，会在 [connection.json](connection.json) 中填入实际可用的公开 HTTPS 来源，并同步更新本页。私网地址不作为远端 Muse 可用入口。

## 给新 Muse

复制 [MUSE_PROMPT.txt](MUSE_PROMPT.txt) 的内容给新 Muse。一次性邀请链接由用户另外私下提供，不写入本仓库。

正常流程：读取公开 bootstrap → 按其长度与 SHA-256 校验客户端资源 → 使用单独提供的邀请登记独立客户端 → 读取自己的 capabilities → 申请目标窗口短码 → 用户只在指定 Chrome 窗口确认。

登记、配对和真实商品读取是不同结果。网络或登记未完成时如实报告，不能宣布已接通。

## 地址与资源

只使用 connection.json 已标为 verified 的来源。公开 bootstrap 为 `chenxing.muse-bootstrap/v1`；资源清单中的 `files[].filename`、`bytes`、`sha256`、`content_base64` 用于保存前校验。资源更新读取 `chenxing.muse-resources/v1` 清单并按同样规则校验；该资源接口使用客户端自己的本地身份，不公开身份文件。

具体路径、命令和可用操作以最终发布的服务合同为准。本仓库不提供未发布客户端脚本，也不会通过 GitHub Actions 执行业务。

已有请求结果不明确时保留原请求号，只查询原状态，不自动重发。

## 现在只测试健康页

临时无凭据地址：[GET 健康页](https://collectibles-wallet-offices-stocks.trycloudflare.com/onboard/v1/health)。只做一次普通 GET，不附带凭据。

运行方本机已记录正常 TLS 和 HTTP 200；尚未证明云端或 Dot 能访问。当前状态为 `transport_only=true`、`onboarding_ready=false`、`protected_paths=closed`，只能说明传输健康检查，不能据此领取邀请、登记或调用业务。若 TLS 失败，停止并报告原始错误；不要忽略证书校验或绕过警告。

GitHub 是固定说明入口，不是网络代理或业务中转。该临时健康地址可能更换，正式 `public_origin` 仍为 null，等待真实公开接入 gate 上线和验通。
