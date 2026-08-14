# XenoLink 技术资源聚合门户

XenoLink 是一个面向开发人员、技术研究人员与基础架构工程师的高性能外链聚合与导航系统。项目定位于将分散于互联网各处的优质技术文档、社区入口、工具站点与运维面板进行结构化整理，并通过轻量级检索与分类体系提供统一访问入口。目标用户包括但不限于运维工程师、全栈开发人员、技术决策者以及开源软件贡献者。XenoLink 解决的核心问题是降低技术信息检索成本，消除书签栏混乱与链接失效带来的重复劳动，同时提供可私有化部署的导航底座，便于团队内部共享知识资产。

## 功能概览

- **智能分类与标签体系**：每个链接资源可赋予多维度标签，系统根据标签自动生成动态分类视图，支持按技术栈、语言、用途、更新频率等维度筛选。

- **链接健康度监控**：内置异步 HTTP 探测任务，定时检测每条外链的可达性、响应时间与 TLS 证书有效期，状态变更时通过日志系统输出告警。

- **全文检索与模糊匹配**：基于倒排索引实现标题、描述、标签与路径的快速检索，支持拼音首字母模糊匹配与拼写纠错建议。

- **用户自定义收藏夹**：允许注册用户将任意链接加入个人收藏夹，并支持嵌套目录与拖拽排序，收藏夹数据以 JSON 格式导出导入。

- **外链访问统计与热力排行**：记录每条链接的点击次数、最近访问时间与来源 IP 地域分布，生成按小时、日、周聚合的热力排行视图。

- **暗色主题与阅读模式**：内置两套视觉主题，并针对长文档类链接提供剥离导航栏与广告的纯净阅读模式，提升技术阅读体验。

- **开放 API 与 Webhook 集成**：提供 RESTful API 用于链接增删改查、分类管理与状态查询，支持通过 Webhook 将链接变更事件推送至外部工单或通知系统。

## 应用场景

- **团队内部技术文档导航**：研发团队可将常用代码仓库地址、CI/CD 面板、日志查询入口与数据库管理界面统一纳入 XenoLink，通过权限控制实现内网资源的集中化管理，新成员入职时无需反复询问各类平台地址。

- **开源项目推荐聚合**：开源社区维护者可将优秀的依赖库、在线 API 测试工具、性能压测平台与漏洞数据库收录为精选推荐，帮助社区用户快速上手并减少环境搭建过程中的迷路时间。

- **个人开发环境书签替代**：独立开发者使用 XenoLink 替代浏览器自带的书签栏，通过标签过滤与全文检索快速找回数月前收藏的罕见配置文件语法参考或网络抓包工具下载页，避免翻找历史记录。

- **技术培训与课程资料包**：培训机构或高校实验室可将课程所需的虚拟机镜像下载地址、实验手册在线版、代码示例仓库与提交评分系统入口预先配置为课程模板，开课时一键分发给学生，显著降低课前准备环节的咨询量。

- **运维监控面板汇聚**：运维团队将多套环境的 Grafana、Kibana、Prometheus AlertManager 以及云厂商控制台入口集中到 XenoLink 的运维专属视图中，结合健康度监控第一时间发现面板域名解析异常或证书过期，提前规避故障排查时的入口不可用问题。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/xenolink/xenolink-core.git
cd xenolink-core

# 2. 安装项目依赖（使用 pnpm 或 npm）
npm install -g pnpm
pnpm install

# 3. 配置环境变量
cp .env.example .env
# 编辑 .env 文件，至少修改 DATABASE_URL 与 SECRET_KEY

# 4. 初始化数据库与种子数据
pnpm run db:migrate
pnpm run db:seed

# 5. 启动开发服务器（默认监听 3000 端口）
pnpm run dev
```

生产环境部署请参考 `docs/deployment.md`，推荐使用 PM2 或 Docker Compose 方式运行。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x LTS 或 20.x LTS | 运行时环境，建议使用 NVM 管理多版本 |
| PostgreSQL | 14.x 或 15.x | 主数据存储，需启用 pg_trgm 扩展用于模糊检索 |
| Redis | 6.2.x 或 7.x | 缓存层与会话存储，用于提升检索响应速度 |
| PNPM | 8.x 或 9.x | 包管理工具，使用 workspace 协议管理 Monorepo |
| Docker | 20.10.x 以上 | 可选依赖，用于本地启动数据库容器与集成测试 |
| Git | 2.30.x 以上 | 版本控制，用于克隆仓库与提交变更 |
| OpenSSL | 1.1.1 或 3.x | 用于生成安全令牌与签名校验，系统一般预装 |

## 文档导航

| 层面 | 目录文件 | 回答的问题 |
|---|---|---|
| 用户指南 | `docs/user-guide/quick-start.md` | 如何注册账户、添加第一条链接、创建分类与收藏夹？ |
| 管理员手册 | `docs/admin/configuration.md` | 如何配置 SMTP 邮件、OAuth 第三方登录、日志级别与巡检间隔？ |
| 开发参考 | `docs/developer/architecture.md` | 项目的模块划分、数据流方向、核心类图与扩展点设计？ |
| 部署运维 | `docs/operations/deployment-options.md` | 支持哪些部署方式（K8s、Docker Compose、原生系统）以及各方式的参数调优建议？ |
| API 文档 | `docs/api/endpoints.md` | 所有 RESTful 接口的请求方法、路径参数、请求体示例与错误码定义？ |
| 贡献规范 | `CONTRIBUTING.md` | 代码风格、提交信息格式、PR 流程与测试覆盖率要求？ |

## 资源列表

### 综合直播资源聚合

<code>guochanwanghongzhibozhuzaixian.org.cn</code>

<code>guochanwanghongshipinzhibo.org.cn</code>

<code>wanghongzhibomianfeiguankan.org.cn</code>

### 垂直分类直播内容

<code>meinvzhibozaixiankan.org.cn</code>

<code>guochanwanghongfulishipin.org.cn</code>

<code>rihanzhibofulishipin.org.cn</code>

<code>rewuzhibowanghongzhibo.org.cn</code>

## 项目结构

```
xenolink-core/
├── apps/
│   ├── web/                         # 主应用前端 (Next.js App Router)
│   │   ├── app/                     # 页面路由与布局
│   │   ├── components/              # 可复用 UI 组件 (shadcn/ui)
│   │   └── hooks/                   # 自定义 React Hooks
│   └── api/                         # 后端服务 (Fastify)
│       ├── routes/                  # 路由定义 (链接、分类、用户、统计)
│       ├── controllers/             # 请求处理与响应格式化
│       ├── services/                # 业务逻辑层 (健康检查、索引更新)
│       └── workers/                 # 后台任务 (探测调度、统计聚合)
├── packages/
│   ├── database/                    # Prisma Schema 与迁移脚本
│   │   ├── migrations/
│   │   └── seeds/                   # 初始分类与示例链接
│   ├── core/                        # 共享工具库 (日志、配置、加密)
│   ├── search/                      # 检索引擎封装 (基于 PostgreSQL + Redis)
│   └── types/                       # TypeScript 类型定义与 Zod 校验
├── docs/                            # 完整文档 (见上文文档导航)
├── scripts/                         # 运维辅助脚本 (备份、数据迁移)
├── tests/                           # 单元测试与集成测试 (Vitest + Supertest)
├── docker-compose.yml               # 本地开发环境编排
├── Dockerfile.prod                  # 生产多阶段构建
├── .env.example                     # 环境变量模板
├── package.json                     # 根目录工作区配置
└── README.md                        # 本文件
```

## 贡献指南

1. 查阅 `issues` 列表，认领标记为 `good-first-issue` 或 `help-wanted` 的任务，或在发起新 Issue 前检索是否已有类似讨论，避免重复劳动。

2. 派生项目仓库至个人账户，基于 `develop` 分支创建功能分支，分支命名遵循 `feature/描述` 或 `fix/描述` 格式，并确保分支名称与关联 Issue 编号对应。

3. 编写代码时严格执行 `.prettierrc` 与 `.eslintrc` 规则，所有新增 API 或工具函数必须附带 JSDoc 注释，同时补全对应的单元测试用例，测试覆盖率不得低于 85%。

4. 提交信息使用 Conventional Commits 规范（如 `feat: 添加链接批量导入功能`、`fix: 修复探测任务超时导致主进程阻塞的问题`），PR 描述中详细说明变更动机、影响范围与手动测试步骤。

5. PR 合入前至少需要一名项目维护者审阅批准，所有 CI 检查（构建、测试、代码风格）必须全部通过，若有冲突请及时变基并解决冲突后重新请求审阅。

## 常见问题

**Q: 部署后首次启动提示数据库连接失败，但 PostgreSQL 容器确实在运行，应如何排查？**

A: 请依次检查以下几点：第一，确认 `.env` 文件中的 `DATABASE_URL` 格式正确，尤其注意主机名是否填写为容器名称或宿主机 IP 而非 `localhost`（若使用 Docker Compose 内部网络）；第二，检查 PostgreSQL 的 `pg_hba.conf` 是否允许当前来源 IP 访问；第三，验证数据库是否已通过 `pnpm run db:migrate` 完成 Schema 初始化，若迁移失败可尝试手动执行 `npx prisma migrate deploy` 并观察具体错误输出。

**Q: 链接健康度监控任务会影响主页面响应速度吗？如何调整检测频率？**

A: 健康度监控设计为异步后台队列执行，默认使用独立的 Worker 进程，不会阻塞 HTTP 请求线程。检测频率通过环境变量 `HEALTH_CHECK_INTERVAL` 控制，单位分钟，默认值为 60。若需要降低系统负载，可在 `.env` 中调大该值至 120 或 240；若需要更实时检测，可配合外部调度系统（如 Linux Cron）触发 `pnpm run health:check` 脚本，同时将 `HEALTH_CHECK_ENABLED` 设为 `false` 以禁用内置调度器。

**Q: 是否支持从浏览器书签 HTML 文件批量导入链接？**

A: 支持。XenoLink 在 `apps/web/app/import` 页面提供了书签导入工具，接受 Netscape Bookmark HTML 格式文件（大多数浏览器导出格式）。系统会解析每个书签的标题、URL 与文件夹层级，自动映射到 XenoLink 的分类与标签体系，重复链接会根据 URL 哈希自动去重并给出合并提示。若导入量超过 500 条，建议通过 API 接口分批提交以避免超时。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
