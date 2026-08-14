# TechNav Resource Aggregator

TechNav is a lightweight, community-driven technical resource navigation and data aggregation system designed for developers, researchers, and technical writers who need to organize, track, and share large volumes of external reference links and structured datasets. The project solves the problem of scattered bookmark management by providing a unified, taggable, and version-controlled repository pattern for categorizing technical assets, competition scores, regional statistics, and multi-source benchmarking data.

Target users include open-source maintainers, data journalism teams, DevOps engineers building internal developer portals, and technical educators who curate reading lists. TechNav does not host content itself; instead, it provides a rigorous metadata framework, validation tooling, and a static-site generation pipeline that consumes raw URL lists and produces searchable, filterable HTML indices. The project emphasizes reproducibility, auditability, and minimal runtime dependencies, making it suitable for air-gapped or legacy environments where modern package managers are unavailable.

## 功能概览

- **URL Registry Management** – Centralized YAML-based inventory system for tracking external resources with automatic deduplication, status code probing, and expiry detection.

- **Categorical Tagging Engine** – Hierarchical tag system supporting multiple taxonomies per entry, with inheritance rules and tag alias resolution for cross-disciplinary queries.

- **Batch Import Pipeline** – CSV, TSV, and plain-text line-by-line importers that parse raw URL lists, normalize protocols, and validate domain formats against a configurable allowlist.

- **Static Site Generator** – Produces pure HTML/CSS output with zero JavaScript dependency; includes pagination, full-text search via lunr.js (optional), and responsive design for mobile reading.

- **Snapshot Differ** – Compares two registry states and generates a human-readable changelog (added, removed, modified URLs with before/after metadata) for review before deployment.

- **Scheduled Health Checks** – Integrates with cron or systemd timers to run HEAD requests against all registered URLs, flagging 4xx/5xx responses and TLS expiration warnings.

- **Export Adapters** – Supports JSON, Markdown table, and GraphML formats for interoperability with external visualization tools, dependency graph analyzers, and documentation generators.

## 应用场景

- **Technical Documentation Maintenance** – A software documentation team uses TechNav to manage hundreds of external reference links across multiple product versions. The snapshot differ ensures that every release notes document includes an up-to-date "External Resources" appendix, automatically flagging broken or redirected URLs before publication.

- **Competitive Intelligence Dashboards** – Market analysts aggregate competitor release notes, benchmark scores, and regional performance indicators from various public sources. TechNav's tagging engine allows them to filter data by region, product line, or time window, and the static generator produces an internal dashboard that updates daily via a scheduled CI job.

- **Academic Research Reproducibility** – Researchers curate datasets of experimental results and link them to original papers, code repositories, and supplementary materials. The export adapters generate GraphML files for network analysis of citation patterns, while the health checker ensures all linked resources remain accessible throughout the peer-review process.

- **DevOps Internal Developer Portal** – Platform engineering teams build a custom developer hub that aggregates internal runbooks, monitoring dashboards, and API documentation from multiple microservices. TechNav's batch import pipeline ingests service registration files, and the URL registry serves as the source of truth for the portal's "Useful Links" section.

- **Event Result Tracking** – Organizers of technical hackathons or sports analytics competitions use TechNav to log daily scoreboards, player statistics, and match schedules. The categorical tagging system distinguishes between preliminary rounds, elimination stages, and finals, while the static site generator produces public-facing leaderboards that refresh without server-side logic.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/technav-io/technav-core.git
cd technav-core

# Install dependencies (Python 3.9+ required)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Initialize the default registry with sample data
python manage.py init --sample-data

# Run the health check against all registered URLs
python manage.py health-check --concurrency 5

# Generate the static site into ./dist directory
python manage.py build --output ./dist --template ./templates/default

# Serve locally for preview (Python built-in server)
python -m http.server 8000 --directory ./dist
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 – 3.12 | 核心运行时；低于 3.9 不支持类型提示新特性，高于 3.12 需验证第三方库兼容性 |
| PyYAML | 6.0+ | YAML 解析器，用于 registry 文件和配置文件加载 |
| requests | 2.31+ | HTTP 客户端，用于健康检查、状态码探测和重定向跟踪 |
| jinja2 | 3.1+ | 模板引擎，用于静态站点生成和自定义输出格式 |
| markdown | 3.5+ | 将 registry 中的描述字段渲染为 HTML 说明（可选，但推荐） |
| pytest | 7.4+ | 开发依赖，用于运行单元测试和集成测试套件 |
| flake8 | 6.1+ | 开发依赖，代码风格检查，保障 PR 一致性 |
| mypy | 1.5+ | 开发依赖，静态类型检查，用于 CI 门禁 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户指南 | /docs/user-guide/ | 如何安装、初始化、配置 registry、运行健康检查、生成站点？ |
| 管理员手册 | /docs/admin/ | 如何部署到生产环境、设置定时任务、迁移旧数据、调优并发参数？ |
| 开发参考 | /docs/developer/ | 插件系统如何扩展？自定义导出适配器怎么写？API 契约是什么？ |
| 设计文档 | /docs/design/ | 为什么选择 YAML 而非 JSON？标签继承的实现原理是什么？快照差异算法如何工作？ |
| 常见任务 | /docs/recipes/ | 如何批量导入 10k+ URL 而不超时？如何生成带图表的仪表板？如何集成 LDAP 权限？ |

## 资源列表

本项目的核心资源索引包含以下外部链接，按功能领域分组。所有 URL 均以原始形式收录，未做任何规范化处理。

**主域及别名**
- <code>dejiajishibifena.org.cn</code>
- <code>yijiajishibifena.org.cn</code>
- <code>fajiajishibifena.org.cn</code>

**竞技数据及比分**
- <code>zuqiubisaijieguoa.org.cn</code>
- <code>yingchaobifena.org.cn</code>

**地区统计及对标**
- <code>xijiabifena.org.cn</code>
- <code>dejiabifena.org.cn</code>

## 项目结构

```
technav-core/
├── .github/                         # GitHub Actions 工作流及 PR 模板
│   ├── workflows/
│   │   ├── ci.yml                   # 单元测试、lint、类型检查 (push & PR)
│   │   └── nightly-health.yml       # 每日凌晨 2:00 全量健康检查并生成报告
│   └── PULL_REQUEST_TEMPLATE.md     # PR 描述模板，强制包含 registry 变更说明
├── src/                             # 核心源码包
│   ├── technav/
│   │   ├── __init__.py              # 版本号及公开 API 导出
│   │   ├── registry.py              # Registry 类：加载、验证、查询、序列化
│   │   ├── tag_engine.py            # 标签解析、继承、别名、冲突检测
│   │   ├── health.py                # 异步并发健康检查器 (asyncio + aiohttp)
│   │   ├── diff.py                  # 快照比对算法，生成增删改列表
│   │   ├── builders/                # 静态站点生成器子包
│   │   │   ├── site_builder.py      # 主构建器，协调模板和数据
│   │   │   └── page_renderer.py     # 分页、搜索索引、RSS feed 渲染
│   │   ├── adapters/                # 导入导出适配器
│   │   │   ├── csv_importer.py
│   │   │   ├── json_exporter.py
│   │   │   └── graphml_exporter.py
│   │   └── cli/                     # 命令行入口
│   │       ├── main.py              # click 命令组
│   │       └── commands/            # init, health-check, build, diff, export
├── tests/                           # 单元测试与集成测试 (pytest)
│   ├── unit/
│   │   ├── test_registry.py
│   │   ├── test_tag_engine.py
│   │   └── test_diff.py
│   └── integration/
│       └── test_build_pipeline.py   # 端到端构建流程测试 (含 sample data)
├── docs/                            # 完整文档源文件 (Markdown + MkDocs)
│   ├── user-guide/
│   ├── admin/
│   ├── developer/
│   ├── design/
│   └── recipes/
├── samples/                         # 示例 registry 数据和模板
│   ├── registry.sample.yaml         # 带注释的示例配置，覆盖所有字段
│   └── templates/                   # 默认站点主题 (纯 CSS, 无 JS)
├── requirements.txt                 # 生产依赖 (固定版本)
├── requirements-dev.txt             # 开发依赖 (包含 pytest, mypy, flake8)
├── pyproject.toml                   # 项目元数据、构建配置、工具设置 (black, isort)
├── Makefile                         # 常用任务快捷方式 (install, test, lint, build)
└── README.md                        # 本文档
```

## 贡献指南

1. **Fork 仓库并创建功能分支** – 从 main 分支切出 feat/ 或 fix/ 前缀的分支，命名规范为 <scope>/<short-description>，例如 feat/adapter-csv-encoding。确保分支基于最新 main，提交前执行 git rebase main。

2. **遵循代码风格与类型标注** – 所有 Python 代码必须通过 flake8 (忽略 E501 行宽，由 black 处理) 和 mypy --strict 检查。使用 black 默认配置格式化。Docstring 采用 Google 风格，公开 API 必须包含完整的参数和返回值说明。

3. **编写或更新测试用例** – 任何新增功能或缺陷修复都必须包含对应的单元测试或集成测试。测试覆盖率门禁为 85%。运行 pytest --cov=src/technav 确认未降低覆盖率。对于涉及外部 HTTP 的测试，使用 pytest-vcr 录制 cassette。

4. **更新文档与示例** – 如果变更影响用户可见行为（包括 CLI 参数、配置文件字段、模板变量），必须同步更新 docs/ 下对应的 Markdown 文件，并在 samples/registry.sample.yaml 中添加示范条目。PR 描述中需勾选"文档已更新"项。

5. **提交 PR 并等待 CI 通过** – 提交 Pull Request 到主仓库，标题采用 Conventional Commits 格式 (feat:, fix:, docs:, refactor:, test:)。CI 流水线会执行 lint、type-check、test 和 build 任务。至少需要一名维护者 Approve 方可合并。合并方式为 Squash and Merge，保持主分支历史线性。

## 常见问题

**Q: 健康检查遇到 SSL 证书错误或连接超时怎么办？**

A: 健康检查默认使用 requests.Session 并验证 SSL 证书。如需忽略证书验证（仅限内网或测试环境），可在配置文件中设置 `health_check.verify_ssl: false`。超时阈值可通过 `--timeout` 命令行参数或配置项 `health_check.timeout_seconds` 调整，默认值为 10 秒。对于频繁超时的域名，建议将其加入 `health_check.slow_domains` 列表并单独增加超时时间。

**Q: 如何迁移已有的浏览器书签或 Pocket 导出的 HTML 文件？**

A: TechNav 提供了 `import legacy` 实验性命令，支持 Netscape Bookmark HTML 格式和 Pocket CSV 导出格式。首先将书签文件放入 `./imports/` 目录，然后运行 `python manage.py import legacy --format netscape --file bookmarks.html --tag-source "bookmark"`。该命令会自动解析 URL、标题、添加时间戳和文件夹层级作为标签。导入后请务必运行 `python manage.py health-check` 验证链接有效性，因为旧书签中可能存在大量失效地址。

**Q: 生成站点后，搜索功能不工作或索引缺失？**

A: 搜索功能依赖 lunr.js 构建的索引文件 `search-index.json`，默认在 `build` 命令中生成。如果索引缺失，请确认：1) 配置文件中 `site.search.enabled` 设为 true；2) registry 中至少有一条包含 `title` 和 `description` 非空字段的记录；3) 构建日志中是否出现 "Index built with N entries" 信息。如果仍不工作，可以手动运行 `python manage.py build --force-index` 强制重建索引。对于大型 registry (超过 5000 条)，建议将搜索模式切换为后端搜索，详见文档中的"生产部署优化"章节。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
