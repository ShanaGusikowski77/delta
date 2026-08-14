# NovaIndex

NovaIndex 是一个面向技术调研、数据聚合与知识管理场景的轻量化外链资源汇总系统。项目定位为个人开发者、技术团队及研究机构提供一套结构清晰、可快速部署的导航型 Web 应用，用于统一管理高频访问的技术文档、社区入口、数据面板与内部工具地址。NovaIndex 不存储用户数据，不包含后端业务逻辑，完全基于静态资源与前端路由实现，旨在解决多源外链分散、检索效率低、团队共享困难等问题。

NovaIndex 默认以只读仪表盘形态运行，所有资源链接按类别、标签与使用频率组织，并内置全文模糊搜索与按域筛选能力。项目自带可配置的 YAML 数据源，支持单文件维护全部链接清单，便于版本控制与自动化同步。NovaIndex 适用于日均处理 100 至 500 个外链地址的中小型知识库场景，同时可作为内部技术门户的基础骨架，无缝嵌入现有 CI/CD 流程。

## 功能概览

- 分类导航面板：支持按技术领域、服务类型、优先级等多维度分类展示链接，每个分类可独立折叠与展开。
- 即时模糊搜索：基于标题、描述、域名关键词进行客户端全文检索，响应时间低于 100 毫秒。
- 标签过滤系统：每条资源支持多个标签，可按标签交集或并集筛选，支持标签热度排序。
- 自定义元数据扩展：每条链接可附加负责人、更新周期、可用性状态、备注等自定义字段，并支持列表与卡片两种展示模式。
- 本地缓存与离线提示：通过 Service Worker 缓存页面骨架与公共资源，在网络不稳定时提供降级提示。
- 一键复制与直达：每个链接卡片提供复制地址与新窗口打开两种交互，并记录点击频次用于排序权重调整。
- 配置热重载：通过监听 data/sources.yml 文件变更（开发环境），自动刷新页面数据，无需手动重新构建。

## 应用场景

技术团队内部文档门户
开发团队可将 NovaIndex 部署为内部技术文档首页，集中存放设计文档、API 参考、监控面板、日志系统、代码仓库等常用地址，新成员入职时可快速获取所有必要入口。

开源项目外部资源聚合
开源项目维护者可以使用 NovaIndex 整理项目依赖的社区论坛、第三方服务、学习资料、镜像站与备用域名列表，作为项目 README 或 Wiki 的补充导航层。

数据调研与竞品监控
数据分析师或市场调研人员可将日常关注的行业报告、数据看板、竞品官网、公告 RSS 等地址统一收录，利用标签与搜索功能快速定位特定领域信息源。

多环境测试入口管理
测试与运维团队可将不同环境（开发、测试、预发布、生产）对应的控制台、日志聚合、链路追踪、告警管理地址分类存放，并通过自定义字段标注环境状态与维护窗口。

## 快速开始

以下步骤适用于 Linux / macOS / Windows（通过 WSL）环境。

```bash
# 1. 克隆仓库
git clone https://github.com/novaindex/novaindex.git
cd novaindex

# 2. 安装依赖（使用 Node.js 18+ 与 npm 9+）
npm install

# 3. 启动开发服务器（默认端口 3000）
npm run dev
```

启动后，访问控制台输出的本地地址（通常为 http://localhost:3000）即可查看 NovaIndex 实例。如需构建生产环境静态文件，请执行 `npm run build`，产物位于 `dist/` 目录，可直接部署至任意静态托管服务（如 Nginx、S3、Cloudflare Pages 等）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.0.0 或更高 | 用于运行构建脚本与开发服务器，LTS 版本推荐 |
| npm | 9.0.0 或更高 | 依赖管理工具，与 Node.js 捆绑或单独安装 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ / Safari 15+ | 客户端运行时要求 ES2020 与 CSS Grid 支持 |
| 静态托管环境 | 任意支持单页应用的 HTTP 服务器 | 生产部署需要配置 fallback 到 index.html |
| 文件系统权限 | 读取 /data 目录与写入 /dist 目录 | 开发与构建过程中需读写权限 |
| 网络访问 | 外网或内网可达所有收录链接 | 应用本身不代理请求，需客户端直接访问目标地址 |
| Git | 2.30.0 或更高 | 仅需在克隆与版本管理时使用 |
| YAML 解析器 | js-yaml 4.1.0（自动安装） | 用于解析 sources.yml 配置文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide.md | 如何添加、编辑、删除链接？如何切换布局与排序？搜索语法是什么？ |
| 配置手册 | docs/configuration.md | sources.yml 的完整字段说明、数据类型、默认值与示例模板 |
| 开发指南 | docs/development.md | 项目目录结构详解、新增组件流程、本地调试与热重载原理 |
| 部署参考 | docs/deployment.md | 针对 Nginx、Apache、S3、Netlify、Vercel 的部署配置示例与环境变量说明 |
| 设计原则 | docs/design-principles.md | 性能预算、可访问性标准、渐进增强策略与浏览器兼容决策 |
| 版本记录 | CHANGELOG.md | 每个版本的新增功能、修复项、破坏性变更与升级注意事项 |

## 资源列表

本项目的核心数据资源来源于以下链接，所有链接按原始格式收录，不进行任何改写或补全。

社区与论坛
- <code>yijiabifenzhibob.org.cn</code>
- <code>fajiabifenzhibob.org.cn</code>

技术文档与参考
- <code>yingchaojishibifenc.org.cn</code>
- <code>xijiajishibifenc.org.cn</code>
- <code>dejiajishibifenc.org.cn</code>

数据与扩展服务
- <code>yijiajishibifenc.org.cn</code>
- <code>fajiajishibifenc.org.cn</code>

以上链接在 NovaIndex 的默认数据源中已预置为示例条目，并分别归属于“社区动态”、“技术参考”、“扩展数据”三个分类。用户可根据自身需求在 data/sources.yml 中启用、禁用或替换这些地址。

## 项目结构

```
novaindex/
├── dist/                         # 生产构建输出目录（自动生成，不纳入版本控制）
├── docs/                         # 完整文档集合
│   ├── user-guide.md             # 用户操作手册
│   ├── configuration.md          # YAML 配置完整参考
│   ├── development.md            # 本地开发与调试指引
│   └── deployment.md             # 各类托管环境部署步骤
├── data/
│   └── sources.yml               # 核心链接数据源（YAML 格式，支持注释与多文档）
├── src/
│   ├── assets/                   # 静态资源（图标、字体、全局样式）
│   │   ├── icons/
│   │   └── styles/
│   ├── components/               # 视图组件（卡片、搜索栏、筛选器、导航树）
│   │   ├── LinkCard/
│   │   ├── SearchBar/
│   │   ├── FilterPanel/
│   │   └── CategoryTree/
│   ├── hooks/                    # 自定义 React / Vue 组合式函数（根据框架调整）
│   │   ├── useSearch.ts
│   │   ├── useFilter.ts
│   │   └── useClickTracker.ts
│   ├── utils/                    # 工具函数（缓存、解析、格式化、防抖）
│   │   ├── cache.ts
│   │   ├── yamlParser.ts
│   │   └── urlHelper.ts
│   ├── worker/                   # Service Worker 注册与缓存策略
│   │   └── sw.js
│   ├── App.tsx                   # 主应用入口
│   └── main.tsx                  # 渲染启动脚本
├── tests/                        # 单元测试与集成测试
│   ├── unit/
│   └── integration/
├── .eslintrc.js                  # ESLint 代码规范配置
├── .prettierrc                   # 代码格式化配置
├── index.html                    # 主页面模板
├── package.json                  # 项目依赖与脚本定义
├── tsconfig.json                 # TypeScript 编译配置
├── vite.config.ts                # 构建工具配置（Vite 或 Webpack）
└── README.md                     # 项目概述与快速入门（本文件）
```

## 贡献指南

NovaIndex 欢迎任何形式的贡献，包括但不限于新增数据源、优化搜索算法、改进移动端适配、修复文档错误等。请遵循以下步骤：

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。建议在 feat/ 或 fix/ 前缀的分支上进行修改，例如 feat/add-dark-mode。
2. 本地运行 `npm run dev` 启动开发服务器，确保所有现有功能正常。新增或修改组件后，请补充对应的单元测试（位于 tests/unit/ 目录），并执行 `npm run test` 验证全部用例通过。
3. 提交代码前，运行 `npm run lint` 与 `npm run format` 统一代码风格，并确保无控制台警告或错误。若涉及数据源变更，请同步更新 docs/configuration.md 中的示例与字段说明。
4. 推送分支到远程仓库，并创建 Pull Request（PR）。PR 标题须遵循 Conventional Commits 规范（如 feat: 增加按域名分组排序），正文需描述变更动机、影响范围及测试方式。
5. 项目维护者将在 3 个工作日内进行 Code Review。如有修改意见，请及时响应并更新 PR。合并后，您的贡献将出现在 CHANGELOG.md 的相应版本中。

## 常见问题

问：NovaIndex 是否支持 MySQL 或 PostgreSQL 作为数据源？
答：不支持。NovaIndex 定位为静态外链汇总站，所有数据来源于单一的 YAML 文件，不依赖任何关系型数据库或持久化存储层。如需动态数据，可结合 CI 定时任务自动更新 YAML 文件并重新构建部署。

问：搜索时无法找到某些链接，即使关键词完全匹配？
答：请检查该链接是否处于禁用状态（enabled: false）或属于未加载的分类。默认搜索仅在当前激活的分类范围内执行。您可以在 sources.yml 中将对应条目的 enabled 改为 true，或在搜索前展开全部分类。另外，搜索字段仅匹配 title、description 和 tags，不匹配 URL 本身。

问：如何备份或迁移我的链接数据？
答：只需复制 data/sources.yml 文件即可。该文件包含所有链接的完整元数据，迁移到新实例时，将文件放入相同路径后重启服务或重新构建即可生效。建议将 sources.yml 纳入 Git 版本控制以追踪变更历史。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:05
