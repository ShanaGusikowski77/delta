# ResourceBridge

ResourceBridge 是一个面向开发人员与技术研究者的外链资源聚合与导航系统。项目定位为轻量级、可自托管的网络资源目录，帮助技术团队在碎片化的网络环境中快速定位有价值的工具、文档与社区入口。ResourceBridge 不生产内容，而是通过人工筛选与社区提交，构建高质量外链索引，解决信息过载与入口分散问题。

本项目适用于需要维护内部技术资源列表的研发团队、开源社区贡献者以及个人知识管理者。通过结构化的目录分类与全文检索，用户可在数秒内定位至项目文档、视频教程、社区讨论或依赖镜像站。ResourceBridge 本身不存储任何第三方文件，仅提供元数据与跳转链接，确保合规性与轻量化。

## 功能概览

- 多维度资源分类：按技术领域、资源类型、适用人群组织外链，支持快速筛选与批量导出。
- 关键词检索与标签过滤：内置简单全文检索引擎，支持按标题、描述、标签及域名检索资源。
- 每日自动可用性检测：定时探测已收录外链的 HTTP 状态码，自动标记失效链接并生成报告。
- 用户提交与审核队列：允许社区通过 Web 表单或 Git PR 提交新资源，管理员审核后合并。
- 个性化收藏集：注册用户可创建公开或私有收藏集，用于项目研究或团队知识沉淀。
- 导入导出标准格式：支持 JSON、CSV 与 Markdown 列表格式的批量导入导出，便于迁移与备份。
- 访问统计与热度排序：记录各资源点击量与引用次数，提供热门资源周榜与月榜。

## 应用场景

- 技术团队内部文档聚合：研发团队可使用 ResourceBridge 统一存放常用开发文档、API 参考、内部工具面板及运维手册入口，避免每次搜索重复信息。
- 开源项目外部依赖导航：开源维护者可将项目所需的外部依赖、镜像站、插件市场与示例代码仓库集中管理，降低新手贡献者的环境配置门槛。
- 在线课程与教程资源索引：教育机构或技术社区可创建专题资源集，将视频教程、配套源码、习题解答与讨论区链接结构化呈现，辅助学员自主学习。
- 个人知识体系构建：独立开发者或研究员可利用收藏集功能，按研究方向（如机器学习、前端工程、系统设计）组织书签，并配合失效检测保持资源有效性。

## 快速开始

以下命令适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash。

```bash
# 克隆代码仓库
git clone https://github.com/resource-bridge/resource-bridge.git
cd resource-bridge

# 安装 Node.js 依赖（需 Node 18+ 与 pnpm）
pnpm install

# 复制环境变量模板并填写配置
cp .env.example .env

# 初始化 SQLite 数据库结构
pnpm run migrate

# 启动开发服务器（默认监听 3000 端口）
pnpm run dev
```

生产环境部署请参考 `docs/deployment.md`，推荐使用 PM2 或 Docker Compose 进行进程管理。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或 20.x LTS | 运行时环境，推荐使用官方二进制或 nvm 管理 |
| pnpm | 8.x 或 9.x | 包管理器，用于依赖安装与工作区管理 |
| SQLite | 3.35+ | 嵌入式数据库，用于存储资源元数据与用户信息 |
| Git | 2.30+ | 用于克隆仓库及版本控制，提交 PR 需配置 GPG 签名 |
| Nginx / Caddy | 任意稳定版 | 生产环境推荐作为反向代理，处理 TLS 与静态资源缓存 |
| 系统内存 | 最低 512 MB | 开发模式建议 1 GB 以上，生产模式建议 2 GB |
| 磁盘空间 | 最低 200 MB | 用于存储代码、数据库及日志文件，实际随资源量增长 |
| 操作系统 | Linux / macOS / WSL2 | 原生支持 Windows 尚未经充分测试 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user/` | 如何使用收藏集、提交资源、查看统计与导出数据？ |
| 管理员指南 | `docs/admin/` | 如何审核提交、管理标签、处理失效链接与备份数据库？ |
| 开发文档 | `docs/developer/` | 如何扩展解析器、添加新的分类规则或修改前端主题？ |
| 部署运维 | `docs/ops/` | 如何配置反向代理、设置定时任务、迁移数据库与性能调优？ |
| 设计说明 | `docs/design/` | 系统架构图、数据模型 ER 图与 API 设计决策依据是什么？ |

## 资源列表

### 影视与字幕相关资源

<code>oumeizaixianguankanshipin.org.cn</code>

<code>rihanshipinmianfeizaixianguankan.org.cn</code>

<code>mianfeigaoqingshipinzaixianguankan.org.cn</code>

<code>renqixiliezhongwenzimuw.org.cn</code>

<code>rihanmeinvzhongwenzimu.org.cn</code>

<code>qingqingcaoyuanzhongwenzimu.org.cn</code>

<code>guochanjingpinzaixianmianfeikanb.org.cn</code>

## 项目结构

```
resource-bridge/
├── apps/
│   ├── web/                         # 主前端应用（Next.js 14，App Router）
│   └── api/                         # 后端 API 服务（Fastify，独立进程）
├── packages/
│   ├── core/                        # 核心数据模型与验证逻辑（TypeScript）
│   ├── crawler/                     # 可用性检测与状态码抓取模块
│   ├── parser/                      # 用户提交资源解析与标准化过滤
│   └── ui/                          # 共享 UI 组件库（Radix UI + Tailwind）
├── configs/
│   ├── eslint/                      # ESLint 共享配置（扁平配置格式）
│   ├── tsconfig/                    # TypeScript 路径映射与编译选项
│   └── prettier/                    # Prettier 代码风格统一配置
├── docs/
│   ├── user/                        # 用户手册章节（含截图与 FAQ）
│   ├── admin/                       # 管理员操作流程与脚本说明
│   ├── developer/                   # 贡献者 API 文档与插件编写指南
│   ├── ops/                         # 部署拓扑、监控告警与灾备方案
│   └── design/                      # 架构决策记录（ADR）与数据流图
├── scripts/
│   ├── migrate.mjs                  # 数据库迁移脚本（支持回滚）
│   ├── seed.mjs                     # 初始示例数据填充
│   └── health-check.mjs             # 手动触发全量外链检测
├── tests/
│   ├── unit/                        # 单元测试（Vitest，覆盖 core 与 parser）
│   ├── integration/                 # API 集成测试（Supertest）
│   └── e2e/                         # 端到端测试（Playwright，模拟用户操作）
├── .env.example                     # 环境变量模板（含 JWT、数据库路径与日志级别）
├── docker-compose.yml               # 生产级容器编排（含 Redis 缓存与 Traefik 路由）
├── Dockerfile                       # 多阶段构建镜像（基于 Alpine Linux）
├── LICENSE                          # MIT 许可协议全文
└── README.md                        # 项目入口文档（本文件）
```

## 贡献指南

1. 查阅 `docs/developer/` 目录下的贡献者入门文档，理解代码规范、提交信息格式与测试要求。所有 PR 必须通过 ESLint 与单元测试。
2. 在 GitHub Issues 中搜索现有议题，避免重复工作。对于新功能或重大变更，建议先创建议题进行设计讨论，获得核心维护者反馈后再编码。
3. Fork 本项目至个人账户，创建功能分支（命名格式为 `feature/描述` 或 `fix/描述`），提交代码时遵循 Conventional Commits 规范（feat、fix、docs、chore 等）。
4. 为新增功能或修复补充对应的单元测试与集成测试，确保测试覆盖率不低于现有基线。提交前运行 `pnpm run test` 与 `pnpm run lint` 进行自检。
5. 创建 Pull Request 至主仓库的 `main` 分支，填写 PR 描述模板，关联相关议题编号。合并前至少需要一名维护者 Approve，且所有 CI 流水线通过。

## 常见问题

问：ResourceBridge 是否存储视频文件或第三方内容副本？

答：否。ResourceBridge 仅存储用户提交的 URL、标题、描述及标签等元数据。所有外链资源仍托管于原始服务器，本项目不缓存或代理任何媒体内容。若版权方要求移除特定链接，可通过管理员联系渠道提交删除请求，审核通过后将在 24 小时内从索引中移除。

问：如何批量导入现有书签或收藏夹？

答：您可以在用户设置页面的「导入导出」功能区，上传符合模板格式的 CSV 或 JSON 文件。系统支持从主流浏览器导出的 HTML 书签文件（需转换为约定格式）。批量导入默认为私有状态，仅导入者本人可见，如需公开可后续编辑设置。

问：失效链接检测机制如何工作？是否影响用户访问速度？

答：系统每日凌晨 2:00 至 4:00 执行全量检测任务，使用 HEAD 请求并发探测所有收录链接，超时时间设为 5 秒。检测任务在独立工作进程中运行，不干扰主服务响应。检测结果会更新至数据库并标记失效状态，前端展示时会附带提示。用户正常访问资源时不会触发实时检测，因此无额外延迟。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
