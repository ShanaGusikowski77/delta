# NetLink Resource Aggregator

NetLink Resource Aggregator is a high-performance, community-driven indexing system designed to organize, categorize, and distribute curated external resource links for technical research, media analysis, and content discovery workflows. The project targets developers, data analysts, and research engineers who require structured access to niche content domains without relying on centralized search engines or proprietary recommendation algorithms.

The system solves the fundamental problem of link rot, domain drift, and manual bookmark fragmentation by providing a version-controlled, queryable registry of validated resource URLs. Each entry is periodically verified for availability, content-type consistency, and metadata freshness. NetLink does not host, proxy, or cache any third-party content; it functions strictly as a deterministic reference layer that enables automated ingestion pipelines, custom scrapers, and academic studies requiring reproducible source lists.

## 功能概览

- **Automated Link Validation** – Periodic health checks with HTTP status tracking, response time logging, and TLS certificate expiry warnings for every registered domain.

- **Categorical Tagging Engine** – Multi-dimensional classification using both automatic keyword extraction and manual curation tags, supporting intersectional filtering across content types, geographic origins, and update frequencies.

- **Versioned Snapshot Export** – Full registry exports in JSON, YAML, and plain-text formats with ISO-timestamped manifests for reproducibility in longitudinal studies.

- **RESTful Query API** – Expose search, filter, and random-sample endpoints with pagination, field selection, and CORS support for integration into dashboards or monitoring tools.

- **CLI Bulk Operations** – Command-line interface for batch import, deduplication, regex-based pattern removal, and diff reporting between registry versions.

- **Webhook Notification System** – Configurable alerts for domain status changes, new addition approvals, or scheduled rotation reminders via Discord, Slack, or generic HTTP endpoints.

- **Audit Trail Logging** – Complete write-ahead log recording all add, remove, update, and verify actions with actor identification (API key or user ID) and timestamp.

- **Custom Field Extensibility** – User-defined key-value schemas per entry to accommodate project-specific metadata such as geopolitical region, language, or institutional affiliation.

## 应用场景

- **Academic Content Collection for Media Studies** – Researchers compiling longitudinal datasets of online video sharing platforms can use NetLink as a stable seed list for crawlers, ensuring that domain name changes or redirects are tracked without modifying analysis pipelines.

- **DevOps Monitoring of External Dependencies** – Engineering teams that rely on third-party resources for CDN assets, font files, or API gateways can integrate NetLink's validation outputs into Prometheus or Datadog to detect downtime before it affects production services.

- **Data Pipeline Bootstrapping for NLP Projects** – Natural language processing engineers needing diverse textual sources from specific regional domains can query NetLink's category filters to obtain fresh URL lists, reducing the manual effort of searching and vetting each source individually.

- **Regulatory Compliance Reference Archiving** – Legal and compliance officers who must maintain auditable records of external references used in filings or publications can leverage NetLink's snapshot and audit features to prove the provenance and availability timestamps of each linked resource.

- **Personal Knowledge Base Automation** – Independent researchers and technical writers can replace static bookmark files with NetLink's CLI tools to programmatically generate Markdown or HTML index pages from filtered subsets, updating documentation sites on each commit.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/netlink-org/netlink-aggregator.git
cd netlink-aggregator

# Install dependencies (Python 3.10+ required)
pip install -r requirements.txt

# Initialize local configuration and database
cp config/example.env .env
python scripts/init_db.py --force

# Run the validation pipeline on the default registry
python validator.py --registry data/registry.json --output reports/status.json

# Start the API server (development mode)
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.10 – 3.12 | Core runtime; 3.13 not yet fully tested with aiohttp |
| aiohttp | 3.9.0+ | Asynchronous HTTP client for parallel link checking |
| sqlite3 | 3.35.0+ | Embedded database for audit logs and cache tables |
| redis | 7.0+ | Optional but recommended for distributed locking and rate limiting |
| uvicorn | 0.24.0+ | ASGI server for production API deployment |
| pytest | 7.4.0+ | Required only for running test suites (dev dependency) |
| docker | 24.0+ | Required for containerized deployment using provided compose file |
| git | 2.30+ | Source control and automatic version tagging during releases |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/user-guide/ | 如何安装、配置、运行验证器、使用CLI和API的基本操作 |
| 管理员指南 | docs/admin/ | 如何管理用户权限、配置webhook、调优验证间隔、处理异常域名 |
| 开发者文档 | docs/developer/ | API端点规范、数据库schema、添加新的分类器插件、扩展自定义字段 |
| 运维部署 | docs/ops/ | 使用Docker Compose进行高可用部署、Prometheus监控指标、日志归档策略 |

## 资源列表

本项目的资源注册表包含以下经过初步分类的外部链接。所有链接均按用户原始输入原样收录，未做任何协议补全、域名规范化或路径修正。

### 综合内容聚合类

- <code>guochanwanghongfulishipinw.org.cn</code>
- <code>rihanzhibofulishipinw.org.cn</code>

### 直播与实时内容类

- <code>rewuzhibowanghongzhibow.org.cn</code>
- <code>wanghongmeinvrewuzhibow.org.cn</code>

### 垂直领域专题类

- <code>wufuyewanghongzhibow.org.cn</code>
- <code>wufuyemeinvzhibow.org.cn</code>
- <code>meinvwufuyiezhibow.org.cn</code>

## 项目结构

```
netlink-aggregator/
├── api/
│   ├── __init__.py               # FastAPI application factory
│   ├── main.py                   # Entry point for uvicorn, registers routers
│   ├── routes/
│   │   ├── registry.py           # GET/POST/PUT/DELETE endpoints for entries
│   │   ├── validation.py         # Trigger on-demand checks, retrieve status
│   │   └── webhooks.py           # Manage subscription and delivery logs
│   └── schemas/
│       ├── request.py            # Pydantic models for incoming payloads
│       └── response.py           # Serialization schemas for outgoing JSON
├── core/
│   ├── validator/
│   │   ├── checker.py            # aiohttp session pool, timeout logic, retry policy
│   │   ├── parser.py             # Extract title, meta description, content-type
│   │   └── reporter.py           # Generate diff reports and summary statistics
│   ├── storage/
│   │   ├── sqlite_backend.py     # All database CRUD operations with connection pooling
│   │   └── redis_cache.py        # Optional cache layer for frequent queries
│   └── scheduler/
│       ├── cron.py               # APScheduler integration for periodic runs
│       └── worker.py             # Background task queue using asyncio queues
├── cli/
│   ├── main.py                   # Click-based command group entry
│   ├── import_cmd.py             # Bulk import from CSV/JSON/plaintext
│   ├── export_cmd.py             # Snapshot export with format selection
│   └── filter_cmd.py             # Regex and tag-based filtering operations
├── config/
│   ├── example.env               # Template for environment overrides
│   ├── logging.yaml              # Rotating file and console log configuration
│   └── categories.json           # Predefined category tree with i18n labels
├── tests/
│   ├── unit/
│   │   ├── test_checker.py       # Mock aiohttp responses, simulate timeouts
│   │   └── test_parser.py        # HTML/JSON parsing edge cases
│   └── integration/
│       └── test_api_lifecycle.py # Full create-validate-update-delete flow
├── docs/                         # Markdown documentation (see Docs Navigation)
├── docker-compose.yml            # Multi-container setup with redis + api + scheduler
├── Dockerfile                    # Multi-stage build for production image
├── requirements.txt              # Production dependencies pinned
├── requirements-dev.txt          # Linting, testing, and formatting tools
├── LICENSE                       # MIT license text
└── README.md                     # This file
```

## 贡献指南

1. **Fork 仓库并创建功能分支** – 从 `main` 分支切出 `feature/your-feature-name` 或 `fix/issue-number` 分支，确保分支名称简洁描述变更目的。

2. **运行测试套件并保持覆盖率** – 在提交前执行 `pytest tests/ --cov=core --cov=api --cov-report=term`，确保新代码的测试覆盖率不低于 85%，且所有现有测试通过。

3. **更新资源注册表时附加验证记录** – 若新增或修改 `data/registry.json` 中的任何 URL，必须同时在该条目的 `history` 字段中添加操作时间、操作人（GitHub 用户名）和变更原因。所有新增链接需在提交前通过本地 `validator.py` 的至少一次成功检查。

4. **遵循代码风格和提交信息规范** – 使用 `black` 和 `isort` 自动格式化 Python 代码，提交信息采用 Conventional Commits 格式（`feat:`, `fix:`, `docs:`, `chore:` 等），并引用相关 issue 编号。

5. **提交 Pull Request 至主仓库** – 向 `netlink-org/netlink-aggregator` 的 `main` 分支发起 PR，描述中需包含变更摘要、测试结果截图（如适用）以及文档更新链接。PR 至少需要一位维护者审核批准后方可合并。

## 常见问题

**问：NetLink 是否存储或缓存外部链接的实际内容？**  
答：不存储。NetLink 仅保存 URL 字符串、元数据（标题、描述、最后验证时间）和分类标签。所有内容获取操作均通过 HTTP HEAD 或 GET 请求进行，且仅提取响应头信息和可选的 `<title>` 标签。项目不保留任何文件副本、截图或页面快照，完全遵守源站点的 robots.txt 和 `Cache-Control` 指令。

**问：如何处理链接失效或域名过期的情况？**  
答：验证器在连续三次检查失败（HTTP 状态码 4xx/5xx、连接超时、DNS 解析错误）后，会将该条目标记为 `degraded` 状态并发送 webhook 通知。若在随后的 7 天内仍无法恢复，则自动转为 `dead` 状态并从活跃查询结果中排除，但条目仍保留在审计日志和归档快照中以便追溯。管理员可手动设置 `override` 标志以强制保留特定条目。

**问：是否支持私有部署下的自定义分类体系？**  
答：完全支持。您可以通过修改 `config/categories.json` 文件并重启服务来覆盖默认的分类树。API 提供 `/categories` 端点供客户端动态获取当前生效的分类列表。对于需要多租户隔离的场景，可以启用 `CUSTOM_SCHEMA` 环境变量，让每个 API 密钥关联独立的分类命名空间和标签集合。

## 许可证

MIT License. See the LICENSE file in the repository root for full terms and conditions.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
