---
name: mintlify-api
description: 通过编程方式与 Mintlify REST API 交互，以管理部署、触发构建并查询文档站点元数据。
license: MIT
compatibility: 任何 HTTP 客户端。通过 API 密钥进行身份验证。
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-api">
  # Mintlify API
</div>

使用 Mintlify API 以编程方式管理文档站点。本技能涵盖部署管理、构建触发和站点元数据查询。

<div id="authentication">
  ## 身份验证
</div>

所有 API 请求都需要在 `Authorization` 标头中传入 API 密钥：

```
Authorization: Bearer <your-api-key>
```

在 [Mintlify 仪表板](https://dashboard.mintlify.com) 的“设置”&gt;“API 密钥”中生成 API 密钥。

<div id="core-capabilities">
  ## 核心功能
</div>

<div id="trigger-deployments">
  ### 触发部署
</div>

当代码库的变更不是通过 Git push 事件发生时，可通过编程方式触发文档重新构建。

<div id="query-site-metadata">
  ### 查询站点元数据
</div>

获取文档站点的信息，包括部署状态、已配置的域名和导航结构。

<div id="manage-preview-deployments">
  ### 管理预览部署
</div>

为拉取请求 (PR) 和分支创建并管理预览部署，以便在文档改动正式上线前进行查看和审核。

<div id="resources">
  ## 资源
</div>

* [API 参考](https://mintlify.com/docs/api)
* [仪表板](https://dashboard.mintlify.com)
* [部署指南](https://mintlify.com/docs/deploy)