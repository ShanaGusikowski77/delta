# ResourceHub

ResourceHub 是一个面向开发者与技术研究人员的优质外链与技术资源汇总平台。项目定位于对互联网上分散的高价值技术内容、工具站点、学术资源及行业动态进行系统性整理与结构化呈现，解决技术人员在信息检索过程中面临的海量数据筛选效率低下、优质资源难以持续追踪、知识碎片化等问题。通过人工筛选与社区贡献相结合的方式，ResourceHub 致力于成为技术领域可靠的中文导航与参考信息中心。

## 功能概览

- **分类资源索引**：按编程语言、开发框架、运维监控、数据库、人工智能等一级分类对资源进行划分，支持快速定位至细分领域。
- **站点状态监测**：内置周期性可用性检查机制，对收录的外链进行响应状态与证书有效性验证，降低死链与风险站点的访问概率。
- **社区贡献工作流**：基于 Pull Request 的资源提交与审核流程，允许社区成员新增或更新资源条目，保持收录列表的动态活性。
- **标签与全文检索**：为每条资源赋予多维度标签（如 "vue3"、"k8s"、"postgres"），配合标题与描述的轻量级全文搜索，提升查找效率。
- **资源变更历史记录**：记录每条收录资源的添加时间、最后验证时间、状态变更日志，便于追溯信息演变过程。
- **访问热度统计**：展示各资源站点的社区点击频次与收藏数量，辅助判断内容的实用性与社区认可程度。
- **RSS 订阅源生成**：为资源更新与新增条目提供 RSS 订阅接口，方便用户通过阅读器接收动态，减少重复访问成本。
- **深色与浅色主题切换**：基于 CSS 变量实现的前端主题适配，满足不同光照环境下的阅读习惯。

## 应用场景

- **技术选型调研**：当架构师或开发负责人需要评估某一技术栈（如消息队列、ORM 框架、日志采集器）时，可通过 ResourceHub 的对应分类快速获取官方文档、社区对比文章、性能测试报告及生产案例链接，显著缩短调研周期。
- **新人入职培训**：团队新成员可借助 ResourceHub 的编程语言与工具链章节，一站获取编码规范、调试工具、常用依赖库及内部运维平台的地址，避免因信息分散导致的初期效率损耗。
- **技术文章写作参考**：技术博主或文档撰写者在准备教程或解决方案时，可通过平台检索相关主题的高质量参考资料与官方规格说明，确保引用的权威性与时效性。
- **离线环境资源准备**：运维人员可在网络受限的生产环境中，预先通过 ResourceHub 收集所需软件包镜像站、离线文档及补丁下载地址，提高变更操作的准备效率。
- **社区贡献与知识沉淀**：技术小组可将团队内部常用的工具站点与知识库链接通过 PR 形式提交至 ResourceHub，形成团队共享的知识导航，减少重复沟通成本。

## 快速开始

以下步骤指导您在本地环境中快速启动 ResourceHub 的开发或部署实例。

```bash
# 1. 克隆项目仓库至本地
git clone https://github.com/resourcehub/resourcehub.git
cd resourcehub

# 2. 安装项目依赖（基于 Node.js 22 LTS 与 pnpm）
corepack enable
pnpm install

# 3. 配置环境变量（复制示例配置并修改数据库连接等参数）
cp .env.example .env.local

# 4. 执行数据库迁移与初始数据填充
pnpm run db:migrate
pnpm run db:seed

# 5. 启动开发服务器（默认监听 3000 端口）
pnpm run dev
```

访问 `http://localhost:3000` 即可浏览本地实例。生产环境部署请参考 `docs/deployment.md` 中的容器化或传统运维方案。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 22.x LTS 或更高 | 运行时环境，推荐使用官方二进制或 nvm 管理 |
| pnpm | 9.x 或更高 | 包管理器，用于依赖安装与工作区管理 |
| PostgreSQL | 15.x 或更高 | 主数据库，存储资源条目、用户及元数据 |
| Redis | 7.x 或更高 | 缓存与会话存储，用于提升检索性能与速率控制 |
| Git | 2.40 或更高 | 版本控制，用于拉取仓库及贡献操作 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | `docs/user-guide/` | 如何浏览、检索、收藏及反馈资源；如何订阅 RSS 更新 |
| 贡献者手册 | `docs/contributing/` | 资源提交规范、PR 流程、标签体系定义及审核标准 |
| 运维部署 | `docs/operations/` | 生产环境安装、反向代理配置、备份策略与监控告警设置 |
| 开发设计 | `docs/development/` | 项目架构、核心数据模型、API 设计规范及前端组件库说明 |

## 资源列表

本章节按照类别整理所有收录的外部资源链接。每个链接均保留原始格式，不添加协议前缀或路径修改。

### 类别一：综合内容平台

<code>rihanmeinvzhongwenzimub.org.cn</code>

<code>qingqingcaoyuanzhongwenzimub.org.cn</code>

### 类别二：直播与视频类站点

<code>wanghongzhibozaixianshipin.org.cn</code>

<code>wanghongfulizhibo.org.cn</code>

<code>guochanwanghongzhibozhuzaixian.org.cn</code>

<code>guochanwanghongshipinzhibo.org.cn</code>

<code>wanghongzhibomianfeiguankan.org.cn</code>

## 项目结构

```
resourcehub/
├── apps/
│   ├── web/                           # 主站前端应用（Next.js 14，App Router）
│   ├── admin/                         # 后台管理面板（React + Vite，用于审核与配置）
│   └── worker/                        # 定时任务与监测服务（Node.js + cron）
├── packages/
│   ├── database/                      # Prisma 数据模型、迁移脚本与种子数据
│   ├── core/                          # 共享业务逻辑（分类校验、标签规范化）
│   ├── api-client/                    # 统一外部请求客户端（含重试与熔断）
│   └── ui/                            # 通用 UI 组件库（Button, Card, Table 等）
├── configs/
│   ├── eslint/                        # ESLint 共享配置（含 TypeScript 与 React 规则）
│   ├── tsconfig/                      # TypeScript 路径映射与编译选项
│   └── vitest/                        # 单元测试与集成测试通用配置
├── docs/                              # 完整文档（用户手册、运维指南、API 参考）
├── scripts/
│   ├── seed/                          # 初始资源分类与示例数据生成脚本
│   └── health/                        # 站点可用性检测与报警脚本
├── .env.example                       # 环境变量模板（含数据库、Redis、OAuth 等）
├── .github/
│   └── workflows/                     # CI/CD 流水线（测试、构建、镜像发布）
├── docker-compose.yml                 # 本地开发与测试用容器编排
├── Dockerfile.prod                    # 生产环境多阶段构建文件
├── package.json                       # 根工作区依赖与脚本定义
├── pnpm-workspace.yaml                # pnpm 工作区声明
└── README.md                          # 项目入口说明文档（本文件）
```

## 贡献指南

1. 查阅 `docs/contributing/resource-criteria.md` 了解资源收录的客观标准，包括内容原创性、站点可用性、安全合规及技术相关性，确保提交的资源符合社区质量要求。
2. 在 `packages/database/seed/resources.ts` 中按分类与标签结构添加新资源条目，并在本地执行 `pnpm run db:seed` 验证数据格式与关联正确性，同时检查是否存在重复条目。
3. 运行 `pnpm run test` 执行单元测试与链接格式校验，确保新增或修改的内容未破坏现有功能，且所有外部链接均通过初始连通性检查。
4. 提交 Pull Request 至 `develop` 分支，在 PR 描述中清晰填写资源来源说明、分类依据及使用价值，并关联对应的 Issue 编号（如有）。
5. 等待项目维护者或社区核心贡献者的 Code Review，根据反馈意见进行修改，合并后您的贡献将出现在下一版本的生产环境中并记录于贡献者列表。

## 常见问题

**问：ResourceHub 与通用搜索引擎或书签管理工具有何本质区别？**

答：ResourceHub 不提供网页级全文检索，而是聚焦于站点级资源的元数据组织与人工审核。与搜索引擎的自动化爬取不同，每条收录链接均经过贡献者主观筛选与维护者复核，优先保证信息密度与参考价值。相较于本地书签，ResourceHub 提供共享上下文、状态监测和社区评价机制，适合团队协作与知识传承。

**问：如何报告资源链接失效、内容变更或分类错误？**

答：您可以通过两种方式反馈：其一，在每个资源详情页底部点击"报告问题"按钮，填写具体现象与建议操作；其二，在 GitHub Issues 中选择"Resource Report"模板提交。维护者会定期处理报告并更新资源状态，处理结果将通过关联的 Issue 或邮件通知您。

**问：生产环境部署时，是否必须使用 Redis 和 PostgreSQL 的特定扩展？**

答：Redis 用于缓存与速率限制，不依赖特殊模块，标准 7.x 版本即可。PostgreSQL 需启用 `pg_trgm` 扩展以支持高效模糊检索，该扩展在大部分托管服务中默认安装，自建实例需执行 `CREATE EXTENSION IF NOT EXISTS pg_trgm;`。此外，建议开启 `uuid-ossp` 扩展用于生成主键标识，但非强制。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
