# Novie_Downloads

Novie 的公开下载仓库，用于分发安装包和 macOS Sparkle 更新清单。源码开发仓库保持私有。

## 环境目录

```text
dev/appcast.xml    DEV 更新清单
uat/appcast.xml    UAT 更新清单
prod/appcast.xml   PROD 更新清单
```

当前三份 XML 都是**未签名的空占位清单**，没有可安装的版本条目。它们用于初始化仓库结构，尚不能作为正式升级源使用。

## 仓库文件和客户端更新地址

Git 中的文件与 GitHub Release 附件是两份独立的内容。提交或推送 `dev/appcast.xml`，不会自动创建名为 `dev-updates` 的 Release，也不会自动上传它的附件。

客户端使用的固定地址规划如下；只有创建相应 Release 并上传 `appcast.xml` 附件后，这些地址才会生效：

| 环境 | 仓库中的源文件 | 托管清单的 Release Tag | 客户端固定地址 |
| --- | --- | --- | --- |
| DEV | [dev/appcast.xml](dev/appcast.xml) | `dev-updates` | [DEV 更新入口](https://github.com/Novamind-Labs-Ltd/Novie_Downloads/releases/download/dev-updates/appcast.xml) |
| UAT | [uat/appcast.xml](uat/appcast.xml) | `uat-updates` | [UAT 更新入口](https://github.com/Novamind-Labs-Ltd/Novie_Downloads/releases/download/uat-updates/appcast.xml) |
| PROD | [prod/appcast.xml](prod/appcast.xml) | `prod-updates` | [PROD 更新入口](https://github.com/Novamind-Labs-Ltd/Novie_Downloads/releases/download/prod-updates/appcast.xml) |

这些入口分别更新，不使用全仓库的 `latest` 为客户端选择环境。

## 安装包下载链接填在哪里

下载链接属于对应环境清单中版本条目的 `enclosure` 元素的 `url` 属性：

```xml
<!-- 字段示意，不是可直接发布的完整更新清单。 -->
<enclosure
  url="安装包在公开 Release 中的实际下载地址"
  length="安装包的实际字节数"
  type="application/octet-stream"
  sparkle:edSignature="发布工具生成的真实安装包签名"
/>
```

完整条目还需要真实的应用构建版本、显示版本、环境和平台约束等信息。使用客户端所信任密钥对应的发布工具生成安装包签名，并按客户端的签名清单要求签署整个 appcast；不要把上述占位值当作发布数据。

清单和它指向的安装包都需要允许最终用户访问。把公开清单指向私有源码仓库的 Release 附件，不能让无权限用户下载该附件。

## 发布顺序

1. 构建并验证对应环境的安装包，完成代码签名、公证和更新签名。
2. 上传安装包到本仓库独立的版本 Release，例如 `dev-v1.2.0`；确认公开下载地址可用。
3. 为该环境生成包含真实下载地址、版本、大小和签名的完整清单，更新对应目录中的文件并提交。
4. 完成该环境的发布批准；PROD 保留人工批准。
5. 在对应的通道 Release（例如 `dev-updates`）上传文件名为 `appcast.xml` 的已签名清单，最后检查固定入口。

首次托管时，在 GitHub 的 Releases 页面选择 **Draft a new release**，创建通道 Tag，并将 `appcast.xml` 上传至附件区域后发布。后续以同一附件名替换该通道的清单。不要仅将下载链接粘贴进 Release 的说明文本。

**固定通道附件必须允许更新。** 如果仓库对新 Release 启用了 Immutable releases，发布后的附件不能替换；不要发布会被锁定的通道清单。应先将清单托管改为 GitHub Pages 或其他支持更新的固定入口，并同步修改客户端配置。安装包的版本 Release 可以保持不可变。

本次初始化不创建远程 Release、不上传附件，也不宣布任何 APP 版本可供自动升级。后续需由发布流程接通清单生成、签名和上传。

参考：[Sparkle 发布文档](https://sparkle-project.org/documentation/publishing/)、[GitHub Release 管理](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)、[GitHub 不可变 Release](https://docs.github.com/en/code-security/concepts/supply-chain-security/immutable-releases)。
