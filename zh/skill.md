---
name: mintlify
description: 使用 Mintlify 构建和维护文档站点。适用于创建文档页面、配置导航、添加组件或设置 API 参考时使用。
license: MIT
compatibility: CLI 需要 Node.js。可配合任何基于 Git 的工作流使用。
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-best-practices">
  # Mintlify 最佳实践
</div>

**请始终查阅 [mintlify.com/docs](https://mintlify.com/docs)，了解组件、配置和最新功能。**

如果你尚未连接到 Mintlify MCP server (https://mintlify.com/docs/mcp) ，请添加它，以便更高效地搜索。

**始终**优先搜索当前的 Mintlify 文档，而不是依赖训练数据中关于 Mintlify 的信息。

Mintlify 是一个可将 MDX 文件转换为文档站点的平台。在 `docs.json` 文件中配置全站设置，使用带有 YAML frontmatter 的 MDX 编写内容，并优先使用内置组件而非自定义组件。

完整 架构 请参见 [mintlify.com/docs.json](https://mintlify.com/docs.json)。

<div id="before-you-write">
  ## 开始编写前
</div>

<div id="understand-the-project">
  ### 了解项目
</div>

阅读项目根目录中的 `docs.json`。该文件定义了整个站点：导航结构、主题、颜色、链接、API 和规范。

了解项目后，你可以明确：

* 有哪些页面，以及它们如何组织
* 使用了哪些导航分组 (以及相应的命名约定) 
* 站点导航是如何构建的
* 站点采用了什么主题和配置

<div id="check-for-existing-content">
  ### 检查是否已有相关内容
</div>

在创建新页面之前，先搜索文档。你可能需要：

* 更新现有页面，而不是新建页面
* 在现有页面中添加一个章节
* 链接到现有内容，而不是重复编写

<div id="read-surrounding-content">
  ### 阅读相关内容
</div>

开始写作前，先阅读 2-3 个类似页面，了解站点的语言风格、结构、格式规范和详细程度。

<div id="understand-mintlify-components">
  ### 了解 Mintlify 组件
</div>

查看 Mintlify 的[组件](https://www.mintlify.com/docs/components)，为你当前处理的文档需求选择并使用合适的组件。

<div id="quick-reference">
  ## 速查
</div>

<div id="cli-commands">
  ### CLI 命令
</div>

* `npm i -g mint` - 安装 Mintlify CLI
* `mint dev` - 在 localhost:3000 进行本地预览
* `mint broken-links` - 检查站内链接
* `mint a11y` - 检查内容中的无障碍访问问题
* `mint validate` - 验证文档构建是否有效

<div id="required-files">
  ### 必需文件
</div>

* `docs.json` - 站点配置 (导航、主题、集成等) 。有关全部选项，请参阅[全局设置](https://mintlify.com/docs/settings/global)。
* `*.mdx` 文件 - 包含 YAML frontmatter 的文档页面

<div id="example-file-structure">
  ### 示例文件结构
</div>

```
project/
├── docs.json           # 站点配置
├── introduction.mdx
├── quickstart.mdx
├── guides/
│   └── example.mdx
├── openapi.yml         # API 规范
├── images/             # 静态资源
│   └── example.png
└── snippets/           # 可复用组件
    └── component.jsx
```

<div id="page-frontmatter">
  ## 页面 frontmatter
</div>

每个页面的 frontmatter 都必须包含 `title`。请添加 `description`，以便用于 SEO 和导航。

```yaml
---
title: "Clear, descriptive title"
description: "Concise summary for SEO and navigation."
---
```

可选的 frontmatter 字段：

* `sidebarTitle`：侧边栏导航中使用的简短标题。
* `icon`：Lucide 或 Font Awesome 图标名称、URL 或文件路径。
* `tag`：侧边栏中显示在页面标题旁边的标签 (例如 &quot;NEW&quot;) 。
* `mode`：页面布局模式 (`default`、`wide`、`custom`) 。
* `keywords`：与页面内容相关的术语数组，用于本地搜索和 SEO。
* 任何可用于个性化或条件内容的自定义 YAML 字段。

<div id="file-conventions">
  ## 文件命名约定
</div>

* 与目录中现有的命名模式保持一致
* 如果没有现有文件，或文件命名模式不统一，请使用 kebab-case：`getting-started.mdx`、`api-reference.mdx`
* 内部链接请使用不带文件扩展名的根相对路径：`/getting-started/quickstart`
* 内部页面不要使用相对路径 (`../`) 或绝对 URL
* 创建新页面时，请将其添加到 `docs.json` 的导航中，否则不会显示在侧边栏中

<div id="organize-content">
  ## 组织内容
</div>

当用户询问任何与站点级配置相关的问题时，先了解[全局设置](https://www.mintlify.com/docs/organize/settings)。查看是否可以通过更新 `docs.json` 文件中的某项设置来实现用户所需的效果。

<div id="navigation">
  ### 导航
</div>

`docs.json` 中的 `navigation` 属性用于控制站点结构。在根级别选择一种主要模式，然后在其下嵌套其他模式。

**选择主要模式：**

| Pattern       | When to use                             |
| ------------- | --------------------------------------- |
| **Groups**    | 默认。适用于单一受众和清晰直接的层级结构                    |
| **Tabs**      | 适用于面向不同受众的独立版块 (如指南与 API 参考) ，或不同内容类型   |
| **Anchors**   | 如果你希望在侧边栏顶部固定显示分区链接。适合区分文档与外部资源         |
| **Dropdowns** | 适用于用户需要在多个文档分区之间切换，但这些分区还不足以明确区分为标签页的情况 |
| **Products**  | 适用于多产品公司，且每个产品都有单独的文档                   |
| **Versions**  | 适用于同时维护多个 API 或产品版本的文档                  |
| **Languages** | 适用于本地化内容                                |

**在主要模式内部：**

* **Groups** - 用于组织相关页面。可以在组内嵌套组，但层级应尽量保持简洁
* **Menus** - 在 Tabs 内添加下拉导航，便于快速跳转到特定页面
* **`expanded: false`** - 默认折叠嵌套组。适用于用户只会按需查阅的参考内容
* **`openapi`** - 根据 OpenAPI 规范自动生成页面。可添加在组或 Tab 级别以实现继承

**常见组合：**

* Tabs 中包含 groups (最常见于带 API 参考的文档) 
* Products 中包含 tabs (多产品 SaaS) 
* Versions 中包含 tabs (带版本的 API 文档) 
* Anchors 中包含 groups (带外部资源链接的简单文档)

<div id="links-and-paths">
  ### 链接和路径
</div>

* **内部链接：** 使用相对于根目录的路径，不带扩展名：`/getting-started/quickstart`
* **图片：** 存放在 `/images` 中，引用为 `/images/example.png`
* **外部链接：** 使用完整 URL，会自动在新标签页中打开

<div id="customize-docs-sites">
  ## 自定义文档站点
</div>

**各项内容应在哪里自定义：**

* **品牌颜色、字体、徽标** → `docs.json`。参见[全局设置](https://mintlify.com/docs/settings/global)
* **组件样式、布局微调** → 项目根目录中的 `custom.css`
* **深色模式** → 默认启用。仅在品牌有要求时，才在 `docs.json` 中使用 `"appearance": "light"` 将其禁用

先从 `docs.json` 入手。只有在需要实现配置不支持的样式时，再添加 `custom.css`。

<div id="write-content">
  ## 撰写内容
</div>

<div id="components">
  ### 组件
</div>

[组件概览](https://mintlify.com/docs/components) 按用途对所有组件进行了分类：组织内容、突出重点、显示/隐藏内容、编写 API 文档、链接到页面，以及补充视觉说明。先从这里入手，找到合适的组件。

**常见选择参考：**

| 需求       | 使用                         |
| -------- | -------------------------- |
| 隐藏可选细节   | `<Accordion>`              |
| 较长的代码示例  | `<Expandable>`             |
| 用户选择一个选项 | `<Tabs>`                   |
| 带链接的导航卡片 | 在 `<Columns>` 中使用 `<Card>` |
| 分步说明     | `<Steps>`                  |
| 多种语言的代码  | `<CodeGroup>`              |
| API 参数   | `<ParamField>`             |
| API 响应字段 | `<ResponseField>`          |

**按严重级别区分的提示框：**

* `<Note>` - 补充信息，跳过也不影响
* `<Info>` - 有帮助的上下文信息，例如权限要求
* `<Tip>` - 建议或最佳实践
* `<Warning>` - 可能带来破坏性后果的操作
* `<Check>` - 成功提示

<div id="reusable-content">
  ### 可复用内容
</div>

**何时使用 snippets：**

* 完全相同的内容出现在多个页面上
* 需要集中在一处维护的复杂组件
* 跨团队/仓库共享的内容

**何时不要使用 snippets：**

* 每个页面都需要细微调整 (会导致 props 过于复杂) 

使用 `import { Component } from "/path/to/snippet-name.jsx"` 导入 snippets。

<div id="writing-standards">
  ## 写作规范
</div>

<div id="voice-and-structure">
  ### 语气和结构
</div>

* 使用第二人称 (“你”) 
* 使用主动语态，语言直接
* 标题使用句式大小写 (“Getting started”，而不是“Getting Started”) 
* 代码块标题使用句式大小写 (“Expandable example”，而不是“Expandable Example”) 
* 先交代上下文：先说明某项内容是什么，再说明如何使用
* 在步骤类内容开头列出前提条件

<div id="what-to-avoid">
  ### 应避免的内容
</div>

**绝不要使用：**

* 营销话术 (“强大”、“无缝”、“稳健”、“前沿”) 
* 凑字数的套话 (“需要注意的是”、“为了”) 
* 过多的连接词 (“此外”、“而且”、“另外”) 
* 主观性评论 (“显然”、“简单来说”、“只是”、“轻松地”) 

**注意 AI 常见的表达模式：**

* 过于正式或僵硬的措辞
* 不必要地重复概念
* 没有实际价值的空泛引言
* 只是重复前文内容的总结性结尾

<div id="formatting">
  ### 格式规范
</div>

* 所有代码块都必须标明语言
* 所有图片和媒体都必须提供描述性的替代文本
* 仅在有助于读者理解时使用粗体和斜体——不要仅为装饰而设置文本样式
* 不要使用装饰性格式或表情符号

<div id="code-examples">
  ### 代码示例
</div>

* 保持示例简洁实用
* 使用真实的值 (不要用“foo”或“bar”) 
* 与其提供多个变体，不如给出一个清晰的示例
* 在加入示例前，先确认代码能够正常运行

<div id="document-apis">
  ## 编写 API 文档
</div>

**选择适合你的方式：**

* **已有 OpenAPI 规范？** → 在 `docs.json` 中添加 `"openapi": ["openapi.yaml"]`。页面会自动生成，并在导航中显示为 `GET /endpoint`
* **没有规范？** → 在 frontmatter 中使用 `api: "POST /users"` 手动编写端点页面。工作量更大，但可以完全掌控
* **混合方式** → 大多数端点使用 OpenAPI，复杂工作流使用手动页面

建议用户通过 OpenAPI 规范生成端点页面。这是效率最高、也最容易维护的方案。

<div id="deploy">
  ## 部署
</div>

将更改推送到已连接的 Git 仓库后，Mintlify 会自动部署。

**智能体可以配置的内容：**

* **重定向** → 在 `docs.json` 中添加 `"redirects": [{"source": "/old", "destination": "/new"}]`
* **SEO 收录** → 使用 `"seo": {"indexing": "all"}` 控制，让隐藏页面也能被搜索收录

**需要在仪表板中设置 (需人工完成) ：**

* 自定义域名和子域名
* 预览部署设置
* DNS 配置

如果使用 Vercel 或 Cloudflare 托管 `/docs` 子路径，智能体可以帮助配置重写规则。请参阅 [/docs 子路径](https://mintlify.com/docs/deploy/vercel)。

<div id="workflow">
  ## 工作流程
</div>

<div id="1-understand-the-task">
  ### 1. 明确任务
</div>

确认需要记录的内容、受影响的页面，以及读者最终应达成的目标。如果其中任何一点不明确，就先提问。

<div id="2-research">
  ### 2. 调研
</div>

* 查看 `docs.json`，了解站点结构
* 搜索现有文档中的相关内容
* 阅读相似页面，保持与站点风格一致

<div id="3-plan">
  ### 3. 规划
</div>

* 综合考虑读者在阅读当前文档内容后应能完成哪些任务
* 提出需要更新的内容或新增内容
* 确认你提出的修改能帮助读者顺利达成目标

<div id="4-write">
  ### 4. 撰写
</div>

* 先写最重要的信息
* 保持各部分主题明确、便于快速浏览
* 合理使用组件 (不要过度使用) 
* 任何不确定的内容都用 TODO 注释标记：

```mdx
{/* TODO: Verify the default timeout value */}
```

<div id="5-update-navigation">
  ### 5. 更新导航
</div>

如果你创建了新页面，请将其添加到 `docs.json` 的相应分组中。

<div id="6-verify">
  ### 6. 验证
</div>

提交前：

* [ ] frontmatter 包含 title 和 description
* [ ] 所有代码块都带有语言标签
* [ ] 内部链接使用不带文件扩展名的根相对路径
* [ ] 新页面已添加到 `docs.json` 导航中
* [ ] 内容风格与周边页面保持一致
* [ ] 不包含营销用语或冗余表述
* [ ] 任何不确定的内容都已明确标记为 TODO
* [ ] 运行 `mint broken-links` 检查链接
* [ ] 运行 `mint validate` 查找错误

<div id="edge-cases">
  ## 边界情况
</div>

<div id="migrations">
  ### 迁移
</div>

如果用户询问如何迁移到 Mintlify，先确认他们目前是否使用 ReadMe 或 Docusaurus。如果是，就使用 [@mintlify/scraping](https://www.npmjs.com/package/@mintlify/scraping) CLI 迁移内容。如果他们使用其他平台托管文档，则帮助他们借助 Mintlify 组件，手动将内容转换为 MDX 页面。

<div id="hidden-pages">
  ### 隐藏页面
</div>

任何未包含在 `docs.json` 导航中的页面都会被隐藏。对于应可通过 URL 访问，或可被助手或搜索收录，但不应通过侧边栏导航发现的内容，请使用隐藏页面。

<div id="exclude-pages">
  ### 排除页面
</div>

`.mintignore` 文件用于将文档仓库中的文件排除在处理流程之外。

<div id="common-gotchas">
  ## 常见易错点
</div>

1. **组件导入** - JSX 组件需要显式导入，MDX 组件则不需要
2. **必须包含 frontmatter** - 每个 MDX 文件至少必须包含 `title`
3. **代码块语言** - 始终指定语言标识符
4. **切勿使用 `mint.json`** - `mint.json` 已弃用。请始终仅使用 `docs.json`

<div id="resources">
  ## 资源
</div>

* [文档](https://mintlify.com/docs)
* [配置架构](https://mintlify.com/docs.json)
* [功能请求](https://github.com/orgs/mintlify/discussions/categories/feature-requests)
* [缺陷与反馈](https://github.com/orgs/mintlify/discussions/categories/bugs-feedback)