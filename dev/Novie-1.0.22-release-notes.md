# Novie Desktop APP DEV 1.0.22

适用平台：Apple Silicon（arm64），macOS 14 或更高版本。

## 发布内容

- DEV Control Plane 使用 `https://control.api.novamind-labs.co.nz/`。
- DEV Ingest 使用 `https://ingest.api.novamind-labs.co.nz`。
- 客户端配置、安装包校验和运行时允许列表与这组新域名保持一致。
- 已配对至旧 Control Plane 域名的设备，需要使用应用中的 **Start new pairing** 重新配对；保留既有环境隔离和历史数据归属规则。
- 已完成签名、公证、安装及真实登录验收，客户端进入 Observing，后台 Agent 正常运行。

## 制品信息

| 字段 | 值 |
| --- | --- |
| 本地安装包 | `Novie-1.0.22-arm64.dmg` |
| 大小 | 46,417,796 字节 |
| SHA-256 | `a3a7d46f584754abb04dbcece6efb056fc7ff13b2ca3b84ded41c592cc9bb62a` |
| 制品状态 | `notarized-stapled` |
| 源码及可信工作流提交 | `6af50d694b21a248b679205cd71bcd78ec8bfa50` |
| 签名构建 | `44180904682` |
| 签名构建完成时间 | 2026-11-18 10:38:03 NZDT（2026-11-17 21:38:03 UTC） |

补录的 appcast 条目采用签名构建完成时间作为 `pubDate`。已有的较新 1.0.23 条目保留原内容和顺序，仍位于 1.0.22 之前。

安装包及最终 DEV appcast 均使用已有 DEV Sparkle 身份签署，并使用 1.0.22 已公证包内的公钥独立验证。

## 本地发布准备状态

本地已包含安装包、校验文件、来源记录、版本说明和已签名清单。目标公开地址为：

[DEV 1.0.22 安装包](https://github.com/Novamind-Labs-Ltd/Novie_Downloads/releases/download/dev-v1.0.22/Novie-1.0.22-arm64.dmg)

该链接用于后续版本 Release 发布；本次未上传 GitHub Release，也未替换远程更新通道附件。

全仓库 appcast 检查结果：DEV 11 条、UAT 11 条、PROD 3 条，均不超过 20 条。本地旧 1.0.19 安装包及校验文件已清理，其清单历史条目仍在保留窗口内。
