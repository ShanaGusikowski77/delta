# HyperLink Hub

HyperLink Hub 是一个面向技术内容创作者、开源项目维护者及数字资源管理者的外链聚合与导航系统。该项目旨在解决分散在网络各处的优质技术资源难以统一检索、分类维护及版本追踪的问题，通过结构化的数据组织与标准化的外链管理流程，为技术社区提供可自托管的资源目录骨架。目标用户包括开源文档撰写者、技术社区运营人员以及需要构建内部技术知识库的研发团队。

## 功能概览

- **多级分类索引**：支持对收录的 URL 资源进行自定义标签与分类层级绑定，实现按领域、用途或来源的快速过滤。
- **链接状态检测**：内置定时任务对已收录的外链进行可用性探测，自动标记失效或重定向的地址，降低维护成本。
- **Markdown 原生渲染**：所有资源列表与说明字段均以 Markdown 源文件存储，与 Git 工作流无缝对接，便于协作与版本回滚。
- **全文检索过滤**：基于标题、描述、分类及标签字段提供轻量级关键词搜索，支持模糊匹配与精确匹配模式。
- **批量导入导出**：支持从 CSV 或 JSON 文件批量导入外链数据，并可将当前索引完整导出为结构化文档，用于备份或迁移。
- **访问统计看板**：记录每个外链被点击或引用的次数，提供简单的热度排序功能，辅助识别高频使用资源。
- **权限分级控制**：集成基于角色的访问控制（RBAC），区分管理员、编辑者与只读访客的操作权限，适合团队协同维护。

## 应用场景

- **开源项目文档站的外链附录维护**：当项目 README 或 Wiki 需要引用大量第三方依赖、参考文章或工具地址时，可使用 HyperLink Hub 统一管理这些外链，避免直接在文档中散落裸地址导致后续维护困难。
- **技术社区每周资源精选合集**：社区运营人员可将每周收集的优质教程、视频、论文链接录入系统，自动生成带分类与简介的周报文档，并对外发布为静态页面。
- **企业研发内部知识库的导航构建**：将内部常用的 CI/CD 工具链地址、监控面板、日志系统、代码仓库等内部资源统一收录，配合权限控制实现部门内共享，减少新人上手时的信息查找时间。
- **个人技术博客的友情链接与参考文献管理**：博主可将长期引用的学术站点、技术专栏、API 文档归类存放，在写作新文章时快速检索并引用，提升内容生产的一致性。

## 快速开始

以下命令演示如何从代码仓库获取项目、安装依赖并启动开发服务。

```bash
# 克隆项目仓库
git clone https://github.com/hyperlink-hub/hyperlink-hub.git

# 进入项目目录
cd hyperlink-hub

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化数据库与配置
cp .env.example .env
python manage.py migrate

# 启动开发服务器
python manage.py runserver --port 8080
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.10 及以上 | 核心运行环境，用于后端 API 与调度服务 |
| PostgreSQL | 14.0 及以上 | 主数据库，存储外链元数据、分类及统计信息 |
| Redis | 6.2 及以上 | 用于缓存检索结果与分布式任务队列（Celery） |
| Node.js | 18.0 及以上 | 仅在前端构建静态管理面板时需要（生产环境可禁用） |
| Git | 2.25 及以上 | 用于版本管理与钩子脚本执行 |
| Docker（可选） | 20.10 及以上 | 若采用容器化部署，需配合 docker-compose 使用 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/user/` | 如何添加新外链、如何分类、如何查看统计、如何导出列表？ |
| 运维指南 | `docs/ops/` | 如何配置数据库连接、如何调整检测任务间隔、如何备份数据？ |
| 开发文档 | `docs/dev/` | 如何扩展分类模型、如何新增自定义字段、如何编写迁移脚本？ |
| API 参考 | `docs/api/` | 各接口的请求/响应格式是什么、认证头如何传递、分页参数如何使用？ |

## 资源列表

### 视频直播类资源

<code>nvzhubozshipinzaixianguankanw.org.cn</code>

<code>xingganmeinvzhibotiaowuw.org.cn</code>

<code>hanguomeinvzhuborewuw.org.cn</code>

<code>zaixianbofangzhubow.org.cn</code>

<code>zhubozhibozaixianguankanw.org.cn</code>

### 体育数据类资源

<code>zuqiujishibifend.org.cn</code>

<code>zuqiujishibifene.org.cn</code>

## 项目结构

```
hyperlink-hub/
├── src/                               # 后端核心源码
│   ├── core/                          # 配置与全局工具模块
│   │   ├── settings.py                # Django 基础配置（含数据库、Redis）
│   │   └── celery.py                  # Celery 任务队列初始化
│   ├── api/                           # 对外 RESTful 接口
│   │   ├── views/                     # 视图集（分类、链接、统计）
│   │   └── serializers/               # 数据序列化与校验逻辑
│   ├── models/                        # 数据模型定义（Link, Category, Tag, ClickLog）
│   ├── tasks/                         # 定时任务（链接状态检测、统计汇总）
│   └── utils/                         # 辅助函数（URL 规范化、HTML 解析）
├── frontend/                          # 管理面板静态资源（Vue 3）
│   ├── components/                    # 可复用 UI 组件（表格、表单、图表）
│   └── views/                         # 页面级视图（仪表盘、列表、详情）
├── docs/                              # 完整文档（用户手册、运维、开发、API）
├── scripts/                           # 运维脚本（备份、迁移、初始数据加载）
├── tests/                             # 单元测试与集成测试（pytest）
├── requirements.txt                   # Python 依赖清单
├── docker-compose.yml                 # 容器化编排（PostgreSQL + Redis + App）
└── README.md                          # 项目入口文档（本文件）
```

## 贡献指南

1. **问题报告与需求讨论**：请在 GitHub Issues 中搜索是否已有相似话题，若无则新建 Issue，并按照模板填写复现步骤、环境信息与建议方案。
2. **分支开发流程**：从 `main` 分支拉取 `feature/xxx` 或 `fix/xxx` 命名的新分支进行开发，确保提交粒度合理且每个提交信息清晰描述变更内容。
3. **代码规范检查**：提交前执行 `make lint`（包含 flake8, black, isort）与 `make test`，确保代码风格一致且所有测试用例通过。
4. **文档同步更新**：若变更涉及用户可见功能（如新增配置项、修改 API 行为），须同步更新 `docs/` 下对应章节，并补充示例。
5. **提交合并请求**：推送分支后创建 Pull Request，描述中关联对应 Issue 编号，至少需要一名维护者审核通过后方可合并。

## 常见问题

**问：如何导入我已有的外链 CSV 文件？**

答：使用管理后台的“批量导入”功能，或通过命令行工具 `python manage.py import_links --file links.csv --format csv`。系统默认要求 CSV 包含 `url`, `title`, `category` 三列，具体格式说明见 `docs/user/import-export.md`。

**问：链接状态检测任务多久执行一次？是否会消耗大量网络资源？**

答：默认每 24 小时执行一次全量检测，并发线程数限制为 10，超时时间设为 5 秒。您可以通过环境变量 `CHECK_INTERVAL_HOURS` 和 `CHECK_TIMEOUT_SECONDS` 调整频率与超时阈值，详细配置参考 `docs/ops/check-config.md`。

**问：能否将本系统生成的资源列表直接嵌入到其他静态站点中？**

答：可以。系统提供只读的公共 API 端点 `/api/public/links/`，返回 JSON 格式数据，且支持按分类过滤。您也可以使用 `python manage.py export_static --output dist/` 生成纯 HTML 静态页面，便于直接部署到 Nginx 或 GitHub Pages。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
