# TechLink Navigator

TechLink Navigator 是一个面向开发者与技术研究人员的开源技术资源导航与聚合平台。该项目旨在解决技术信息碎片化、优质资源分散、文档查找效率低下的问题，通过人工筛选与社区协同的方式，构建一个结构清晰、更新及时、可追溯的外链资源目录。

项目定位于成为技术团队的基础设施工具，适用于日常开发查库、架构选型参考、技术文档归档、以及学术研究资料溯源等场景。通过集中化的链接管理与分类索引，显著降低开发者在海量信息中的检索时间成本。

## 功能概览

- **智能分类索引**：根据资源内容自动生成多维度分类标签，支持按技术栈、应用场景、资源类型进行筛选与排序。

- **链接存活监测**：定期对收录的 URL 进行可用性检测，自动标记失效链接并通知维护者，保证资源库的有效性。

- **自定义收藏夹**：允许用户创建个人或团队级别的收藏集合，便于项目组内共享常用技术文档与工具地址。

- **全文搜索与过滤**：支持对资源标题、描述、标签、域名进行联合搜索，并提供正则表达式过滤模式，满足高级检索需求。

- **版本历史记录**：每次链接的增删改操作均记录变更日志，支持回溯任意时间点的资源快照，符合合规审计要求。

- **批量导入导出**：支持通过 JSON / CSV / Markdown 格式批量导入链接列表，并可导出为标准书签文件或结构化数据。

- **开放 API 接口**：提供 RESTful API 用于第三方工具集成，允许 CI/CD 流水线或监控脚本自动查询和更新资源状态。

- **社区标注机制**：注册用户可对资源添加注释、评分、使用示例，形成社区驱动的知识增强层，提升资源可用性信息。

## 应用场景

**技术选型与调研** 当团队需要评估不同技术方案时，可通过本项目的分类索引快速获取官方文档、性能评测、社区讨论等关键链接，缩短调研周期。

**新员工入职培训** 新加入的研发人员可通过项目中的资源列表系统性地了解公司常用技术栈的官方手册、最佳实践、内部工具地址，加速融入团队。

**开源项目文档聚合** 开源维护者可以将项目依赖的第三方库文档、部署工具、监控面板等外部资源统一收录，形成一站式的项目外部依赖手册。

**学术研究资料管理** 高校及科研机构的研究人员可建立与研究方向相关的论文数据库、实验数据集、代码仓库的链接集合，便于团队协作共享。

**离线文档备份计划** 网络受限环境下的开发团队可利用本项目的导出功能，定期将关键资源列表导出并配合离线下载工具，构建本地技术镜像。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，帮助您在五分钟内启动本服务的开发实例。

```bash
# 1. 克隆项目仓库
git clone https://github.com/techlink-navigator/navigator.git
cd navigator

# 2. 安装依赖（使用 pip 与 npm）
pip install -r requirements.txt
npm install --prefix frontend

# 3. 初始化配置文件
cp .env.example .env
python scripts/init_db.py

# 4. 启动开发服务器（后端 + 前端）
python run.py --mode dev --port 8080
```

访问本地 `http://localhost:8080` 即可看到导航主页，管理员默认账号为 `admin`，密码在首次启动时打印于控制台日志中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.10 或更高 | 后端核心运行环境，推荐使用 3.11 以获得性能提升 |
| Node.js | 18.x LTS 或 20.x | 前端构建与热重载服务依赖 |
| PostgreSQL | 14.x 或更高 | 主数据库，用于存储链接元数据、用户信息及变更日志 |
| Redis | 7.x 或更高 | 缓存与会话存储，用于提升搜索响应速度和分布式锁 |
| Nginx | 1.24 或更高 | 生产环境反向代理与静态资源服务（开发环境可跳过） |
| Git | 2.30 或更高 | 版本控制及自动更新脚本依赖 |
| Docker | 24.x 或更高 | 可选，用于容器化部署（推荐生产环境使用） |

## 文档导航

| 层面 | 目录位置 | 回答的问题 |
|------|---------|-----------|
| 用户手册 | `docs/user/guide.md` | 如何注册、收藏、搜索、以及使用社区标注功能 |
| 管理员手册 | `docs/admin/maintenance.md` | 如何管理链接分类、审核社区标注、配置存活监测策略 |
| API 参考 | `docs/api/v1/endpoints.md` | 所有 REST 接口的请求/响应格式、鉴权方式、分页参数 |
| 部署指南 | `docs/deploy/production.md` | 如何配置 SSL、负载均衡、日志聚合、数据库备份与恢复 |
| 开发指南 | `docs/dev/contribute.md` | 代码规范、测试框架、PR 流程以及本地调试技巧 |
| 架构设计 | `docs/design/overview.md` | 系统模块划分、数据流图、扩展性设计及技术选型考量 |
| 常见任务 | `docs/tasks/import-export.md` | 如何批量导入书签、导出为 HTML、以及迁移至其他系统 |

## 资源列表

本项目收录的外部资源按类别整理如下，所有链接均保持用户原始格式，未做任何修改。

技术基础类

<code>xijiabifena.org.cn</code>

<code>dejiabifena.org.cn</code>

<code>yijiabifena.org.cn</code>

<code>fajiabifena.org.cn</code>

技术扩展类

<code>yingchaobifenzhiboa.org.cn</code>

<code>xijiabifenzhiboa.org.cn</code>

<code>dejiabifenzhiboa.org.cn</code>

## 项目结构

```
navigator/
├── backend/                           # 后端 Python 服务
│   ├── api/                           # RESTful 路由与控制器
│   │   ├── v1/                        # 版本化接口定义
│   │   │   ├── links.py               # 链接增删改查与搜索
│   │   │   ├── users.py               # 用户注册登录与权限
│   │   │   └── annotations.py         # 社区标注与评分接口
│   │   └── middleware/                # 鉴权、日志、限流中间件
│   ├── core/                          # 核心业务逻辑层
│   │   ├── checker/                   # 链接存活监测调度器
│   │   ├── indexer/                   # 分类索引生成与重排引擎
│   │   └── exporter/                  # 批量导出为各种格式
│   ├── models/                        # SQLAlchemy 数据模型定义
│   ├── schemas/                       # Pydantic 请求与响应模型
│   ├── tasks/                         # Celery 异步任务（监测、通知）
│   └── utils/                         # 通用工具函数（日期、加密、网络）
├── frontend/                          # 前端 Vue 3 单页应用
│   ├── src/
│   │   ├── components/                # 可复用 UI 组件（表格、卡片、搜索框）
│   │   ├── views/                     # 页面级视图（首页、收藏、管理面板）
│   │   ├── stores/                    # Pinia 状态管理（用户、链接缓存）
│   │   └── assets/                    # 静态样式与图片资源
│   └── public/                        # 入口 HTML 与 favicon
├── scripts/                           # 运维与开发辅助脚本
│   ├── init_db.py                     # 数据库初始化与种子数据填充
│   ├── backup.py                      # 自动备份数据库到指定路径
│   └── migrate_legacy.py              # 从旧版书签文件迁移数据
├── docs/                              # 完整文档目录（见文档导航章节）
├── docker/                            # Docker 编排文件与环境变量
│   ├── docker-compose.yml             # 全服务编排（后端+前端+PG+Redis）
│   └── Dockerfile.backend             # 后端生产镜像构建脚本
├── tests/                             # 单元测试与集成测试
│   ├── unit/                          # 后端业务模块测试
│   └── e2e/                           # 前端端到端测试（Playwright）
├── .env.example                       # 环境变量配置模板
├── requirements.txt                   # Python 依赖列表（精确版本）
├── package.json                       # Node 前端依赖与脚本
└── README.md                          # 当前文件
```

## 贡献指南

我们欢迎所有形式的贡献，包括但不限于新增资源链接、修复文档错误、提交功能改进建议。请遵循以下步骤：

1. 查阅 `docs/dev/contribute.md` 了解代码规范、测试要求及 commit message 格式约定。所有 PR 必须通过单元测试和代码风格检查。

2. 在 GitHub Issues 中查找标签为 `good-first-issue` 或 `help-wanted` 的任务，或自行创建新 Issue 描述您希望解决的问题或新增的功能。

3. Fork 项目仓库，在您的分支上进行开发。对于新增外部链接资源，请编辑 `data/sources.json` 并按已有分类格式添加，同时确保链接可访问。

4. 提交 Pull Request 前，请运行 `python scripts/precommit.py` 执行本地自动化检查（包括 lint、test、build），确保所有检查通过。

5. PR 合并前至少需要一位核心维护者进行代码审阅，对于重大功能变更，会要求补充对应的单元测试和文档更新。

## 常见问题

**问：项目中的资源链接失效怎么办？**

答：系统每 72 小时自动检测一次所有收录链接的状态，失效链接会被标记并在管理面板高亮显示。用户也可以通过页面上的"报告失效"按钮主动提交反馈，维护团队会在 24 小时内核实并更新或移除失效链接。如需立即处理，管理员可手动触发检测脚本 `python scripts/check_links.py --force`。

**问：如何部署到生产环境并保证数据安全？**

答：我们提供完整的 Docker Compose 生产环境编排文件，位于 `docker/docker-compose.prod.yml`。部署前请务必修改默认密码、启用 HTTPS（使用 Let's Encrypt 自动证书）、配置 PostgreSQL 的定期 pg_dump 备份，并将备份文件同步至异地存储。详细的分步部署说明请参考 `docs/deploy/production.md`。

**问：能否在不注册账号的情况下使用全部功能？**

答：未注册用户仅可使用浏览、搜索和基础分类筛选功能。收藏夹、社区标注、自定义分类、以及 API 调用需要注册并登录。注册流程仅需邮箱和密码，且支持企业内部 OAuth（GitHub / Google）单点登录配置，具体开启方法见管理员手册。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
