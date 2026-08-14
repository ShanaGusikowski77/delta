# Rihans Resource Aggregator

Rihans Resource Aggregator is a curated technical index and navigation system designed for developers, researchers, and content analysts who need to systematically organize, validate, and monitor a large corpus of media-related domain resources. The project addresses the common challenge of managing dispersed, ephemeral, or unvalidated URL collections by providing a structured, version-controlled, and queryable frontend over raw link data.

The system targets technical users who require reproducible resource catalogs, automated availability checking, and clean presentation layers for domain lists that are frequently updated. It is not a content delivery platform nor a proxy service; it is a metadata management and visualization tool that transforms flat URL lists into an actionable knowledge base with dependency tracking, category tagging, and health status indicators.

## 功能概览

- **批量域名导入与解析** – Accepts plain-text or CSV inputs of domain names, automatically normalizes them to canonical forms, and extracts WHOIS and DNS basic records for each entry.

- **分类标签与多级分组** – Supports user-defined tags such as region, language, content type, and reliability score; enables dynamic grouping by any combination of tags.

- **可用性探测与状态监控** – Periodically performs HTTP HEAD and GET checks against each domain, records response times, status codes, and TLS certificate expiry dates.

- **结构化文档生成** – Renders the entire resource collection as a static Markdown page with clickable sections, anchor links, and auto-generated tables for quick scanning.

- **变更历史追踪** – Every addition, removal, or metadata update is logged with a timestamp and optional commit message, enabling rollback and audit trails.

- **RESTful 查询接口** – Provides a lightweight JSON API for programmatic queries by tag, status, or substring match, suitable for integration into monitoring dashboards.

- **自定义输出模板** – Allows users to define Jinja2 or Handlebars templates to render the resource list in HTML, AsciiDoc, or plain text formats beyond the default Markdown.

## 应用场景

**场景一：内容聚合站点运维**  
Operators of content discovery platforms can use Rihans Resource Aggregator to maintain a curated list of external reference domains. The status monitoring feature alerts them when a domain becomes unreachable, allowing quick removal or replacement before end users encounter broken links.

**场景二：学术研究与数据采集**  
Researchers studying online media distribution patterns can import large domain sets, tag them by geographical origin or language, and export structured reports. The version history ensures that the exact domain set used in a given study period is reproducible for peer review.

**场景三：内部知识库构建**  
Enterprise technical teams can deploy this tool as an internal URL catalog for documentation references, third-party service endpoints, or testing environments. The hierarchical structure and searchable interface reduce time spent locating specific resources across scattered wikis or spreadsheets.

**场景四：合规性审计辅助**  
Compliance officers can periodically export the full resource list with last-check timestamps and HTTP response headers, providing evidence of due diligence when reviewing external dependencies. The tagging system helps flag resources that require special attention based on content categories.

## 快速开始

Clone the repository, install Python dependencies, and run the initial import command to start building your resource index. All commands assume a Unix-like shell environment with Python 3.10 or later.

```bash
git clone https://github.com/rihans-dev/resource-aggregator.git
cd resource-aggregator
pip install -r requirements.txt
python manage.py import --input domains.txt --tag initial
python manage.py check --parallel 4
python manage.py render --output README.md
```

The `domains.txt` file should contain one domain per line, without protocol prefixes. The system will automatically add `https://` for checking purposes while preserving the original form in display.

## 安装要求

The following table lists all mandatory dependencies, optional integrations, and their respective roles. Ensure that your system meets or exceeds these specifications before attempting installation.

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 – 3.12 | Core runtime; type hints and async features require 3.10+ |
| pip | 23.0+ | Package installer for Python dependencies |
| SQLite | 3.35+ | Embedded database for metadata storage and query caching |
| curl | 7.68+ | Used by the availability checker for HTTP requests (fallback mode) |
| git | 2.25+ | Required for version tracking and commit history integration |
| tzdata | 2023c+ | Timezone database for accurate timestamp normalization |
| pytest | 7.0+ | Testing framework (development only) |
| black | 23.0+ | Code formatter (development only) |
| mypy | 1.0+ | Static type checker (development only) |
| docker | 20.10+ | Container runtime (optional, for production deployment) |

## 文档导航

The documentation is organized into four primary layers, each targeting a specific audience and answering distinct operational questions. Refer to the table below to locate the appropriate guide for your current task.

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户入门 | `docs/user/quickstart.md` | How do I import my first domain list? How do I view the generated report? |
| 管理员手册 | `docs/admin/configuration.md` | How do I change the checking interval? Where are logs stored? How do I add custom tags? |
| API 参考 | `docs/api/endpoints.md` | Which endpoints are available? What request/response formats are supported? |
| 开发指南 | `docs/developer/architecture.md` | What is the internal module structure? How do I add a new output formatter? |

## 资源列表

This section contains the complete set of external reference domains managed by the project. They are grouped into logical categories based on inferred content types for easier browsing. All entries are presented exactly as provided by the upstream data source without any normalization of protocol, subdomain, or top-level domain.

### 视频内容与媒体资源

<code>rihanshipinmianfeizaixianguankanb.org.cn</code>

<code>mianfeigaoqingshipinzaixianguankanb.org.cn</code>

<code>renqixiliezhongwenzimuwb.org.cn</code>

<code>rihanmeinvzhongwenzimub.org.cn</code>

<code>qingqingcaoyuanzhongwenzimub.org.cn</code>

### 直播与互动平台

<code>wanghongzhibozaixianshipin.org.cn</code>

<code>wanghongfulizhibo.org.cn</code>

## 项目结构

The source tree follows a modular monolith layout. Core logic resides in the `src/` directory, while `scripts/` contains utility helpers for batch operations. The `data/` folder is used for persistent storage, and `tests/` mirrors the `src/` hierarchy for unit and integration tests.

```
resource-aggregator/
├── src/                          # Main application source code
│   ├── core/                     # Domain models and database abstraction
│   │   ├── models.py             # SQLAlchemy ORM definitions for domains, tags, checks
│   │   └── session.py            # Database connection pool and transaction manager
│   ├── importer/                 # Import pipeline for raw domain lists
│   │   ├── parser.py             # CSV, plain-text, and JSON input parsers
│   │   └── normalizer.py         # Strips protocols, converts to lowercase, validates TLD
│   ├── checker/                  # Availability and health checking subsystem
│   │   ├── http.py               # Async HTTP client using aiohttp with retry logic
│   │   └── scheduler.py          # Interval-based job runner with backoff strategy
│   ├── renderer/                 # Output generation engines
│   │   ├── markdown.py           # Default Markdown table and list renderer
│   │   └── template.py           # Jinja2 environment loader for custom templates
│   ├── api/                      # RESTful endpoint handlers
│   │   ├── routes.py             # Flask/FastAPI route definitions
│   │   └── serializers.py        # JSON response formatters
│   └── cli/                      # Command-line interface entry points
│       ├── main.py               # Argument parser and subcommand dispatcher
│       └── commands.py           # Implementation of import, check, render, clean
├── tests/                        # Test suite organized mirroring src/
│   ├── unit/                     # Isolated unit tests for individual functions
│   └── integration/              # End-to-end tests with temporary database
├── scripts/                      # Operational scripts for deployment and maintenance
│   ├── backup.sh                 # Daily backup script for SQLite and logs
│   └── migrate.py                # Schema migration runner for version upgrades
├── config/                       # Environment-specific configuration files
│   ├── development.toml          # Debug-enabled settings with local SQLite path
│   └── production.toml           # Production settings with connection pooling and logging
├── docs/                         # User, admin, API, and developer documentation
│   ├── user/                     # Quickstart, FAQ, and usage examples
│   ├── admin/                    # Deployment, monitoring, and tuning guides
│   ├── api/                      # OpenAPI specification and endpoint examples
│   └── developer/                # Architecture decisions and contribution workflow
├── data/                         # Persistent storage volume (SQLite, check cache)
│   ├── domains.db                # Main SQLite database file
│   └── cache/                    # Temporary HTTP response cache for checking
├── logs/                         # Rotating log files for debug, info, and error levels
│   ├── app.log                   # General application log
│   └── check.log                 # Detailed health check result log
├── requirements.txt              # Production Python dependencies with pinned versions
├── requirements-dev.txt          # Additional dependencies for testing and linting
├── Dockerfile                    # Container build recipe for production deployment
├── docker-compose.yml            # Multi-container setup with reverse proxy option
└── README.md                     # This document – entry point for the project
```

## 贡献指南

We welcome contributions that improve the core aggregator logic, extend output formats, or enhance the monitoring subsystem. Please follow the steps below to propose changes.

**第一步：选择待处理议题**  
Browse the `issues` tab for open tasks labeled `good-first-issue` or `help-wanted`. Comment on the issue to indicate your intent and avoid duplicate work.

**第二步：复刻与开发环境搭建**  
Fork the repository, clone your fork, and create a new branch with a descriptive name such as `feature/add-json-output` or `fix/checker-timeout`. Install development dependencies using `pip install -r requirements-dev.txt`.

**第三步：代码规范与测试**  
Run `black src/ tests/` to format code, `mypy src/` for static type checking, and `pytest tests/` to ensure all existing tests pass. Add new tests in the appropriate `tests/` subdirectory for any new functionality.

**第四步：提交与合并请求**  
Commit your changes with a clear message following the Conventional Commits style (e.g., `feat(renderer): add AsciiDoc output support`). Push to your fork and open a pull request against the `main` branch. Include a reference to the relevant issue number and a brief description of your changes.

**第五步：代码审查与合并**  
Maintainers will review your pull request within five business days. Address any feedback by pushing additional commits to your branch. Once approved, a maintainer will squash and merge your contribution.

## 常见问题

**Q: 系统如何处理带有国家顶级域或长后缀的域名？**  
The normalizer module treats any valid public suffix (as defined by the Public Suffix List) as part of the domain. It does not strip or modify the original string except for removing accidental whitespace. The `checker` subsystem always attempts `https://` first, falling back to `http://` if the secure connection fails, but this fallback does not alter the stored domain name.

**Q: 能否同时管理数千个域名而不影响性能？**  
Yes. The SQLite backend with proper indexing supports up to 50,000 domains comfortably on a standard virtual private server. The async HTTP checker uses a configurable concurrency limit (default 20) to avoid overwhelming network resources. For larger datasets, we recommend deploying the PostgreSQL adapter (available in the `contrib/` directory) and adjusting the connection pool size.

**Q: 如何自定义状态检查的阈值或超时时间？**  
All timeout, retry, and threshold parameters are exposed in the configuration file under the `[checker]` section. You can set `timeout_seconds`, `retry_attempts`, and `success_threshold` (minimum consecutive successful checks required to mark a domain as healthy). After modifying the configuration, restart the scheduler service using `python manage.py restart-scheduler`.

## 许可证

This project is distributed under the terms of the MIT License. You are free to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to the condition that the copyright notice and permission notice are retained in all copies or substantial portions of the software. The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
