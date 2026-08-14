# Trawler Link Atlas

Trawler Link Atlas is a curated, high-availability resource aggregation and external link inventory system designed for content curators, archival researchers, and infrastructure engineers who maintain large-scale external reference collections. The project addresses the fundamental challenge of organizing, validating, and presenting distributed media references across multiple domain authorities without hosting or proxying any underlying content. It provides a structured metadata layer over heterogeneous external resources, enabling consistent navigation, availability monitoring, and taxonomy-driven discovery.

Target users include digital archivists, research data managers, and system administrators who require a reproducible, version-controlled approach to managing external link registries. Unlike bookmark managers or simple HTML index pages, Trawler Link Atlas treats link collections as infrastructure-as-code, with formal schema validation, automated freshness checks, and multi-dimensional categorization. The project is not a search engine nor a content delivery platform; it is a reference governance toolkit that imposes order on the chaotic landscape of externally hosted media indices.

## 功能概览

- **Declarative Link Registry** – Maintain all external references in YAML-based inventory files with mandatory fields for URL, category, last-verified timestamp, and content-type hint.

- **Multi-Taxonomy Tagging Engine** – Assign each resource to one or more taxonomic dimensions including language, region, media type, and thematic series, with hierarchical tag inheritance.

- **Automated Availability Probe** – Scheduled head-request verification against each registered URL, recording HTTP status codes, response times, and TLS certificate expiry warnings.

- **Metadata Enrichment Pipeline** – Extract and store page titles, description meta tags, and Open Graph hints from referenced endpoints without downloading full payloads.

- **Static Site Generator Integration** – Render the inventory as a navigable HTML static site with search, filter, and sort capabilities, suitable for deployment on any web server.

- **Versioned Snapshot Artifacts** – Archive each inventory state with Git-based commit hashes, enabling rollback and historical comparison of link changes over time.

- **Health Dashboard Exporter** – Output Prometheus-compatible metrics for each domain, showing uptime percentage, average latency, and certificate validity days.

## 应用场景

- **Academic Research Reference Indexing** – Research teams managing large bibliographies with online supplementary materials can use Trawler Link Atlas to track the accessibility of referenced external datasets, media files, or project pages, automatically flagging dead links before publication deadlines.

- **Media Archival Workflow Integration** – Archival engineers responsible for preserving historical media indices can ingest the provided URL lists as inventory seeds, then apply the validation pipeline to distinguish active resources from deprecated or relocated endpoints, maintaining a clean master reference list for downstream crawlers.

- **Regional Content Aggregation Dashboards** – Community portal operators building regional content discovery hubs can utilize the multi-taxonomy engine to categorize resources by linguistic region (Japanese, Korean, Chinese traditional, etc.) and media type, generating filtered views for different audience segments without modifying the underlying source data.

- **Infrastructure Compliance Auditing** – Compliance officers tasked with reviewing external resource dependencies for regulatory adherence can leverage the health dashboard and metadata snapshots to produce periodic reports on external endpoint status, certificate validity, and content-type consistency, supporting due diligence documentation.

## 快速开始

Clone the repository, install dependencies, and run the initial inventory validation using the commands below. The setup assumes a standard Python 3.10+ environment with pip available.

```bash
git clone https://github.com/trawler-dev/link-atlas.git
cd link-atlas
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python atlas.py validate --inventory data/links.yaml
python atlas.py serve --port 8080
```

After executing these steps, the validation command will parse the inventory schema and report any malformed entries. The serve command launches a local development server at `http://localhost:8080` where you can browse the rendered catalog.

## 安装要求

The following table lists mandatory dependencies, optional system-level requirements, and additional notes for each component.

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 或更高 | 核心运行时，用于所有脚本和验证逻辑 |
| PyYAML | 6.0.1 | 解析和序列化 YAML 格式的库存文件 |
| requests | 2.31.0 | 执行 HTTP 探针和元数据提取，支持超时和重试 |
| beautifulsoup4 | 4.12.2 | 解析 HTML 元标签，提取标题和描述信息 |
| prometheus-client | 0.19.0 | 导出健康度指标，支持 Prometheus 抓取 |
| Git | 2.30 或更高 | 用于版本化快照和提交钩子（建议安装） |
| make | 3.82 或更高 | 可选，用于自动化构建任务（如站点生成） |
| curl | 7.68 或更高 | 可选，用于外部探针的备用后端 |

## 文档导航

The table below organizes the project documentation into logical layers, providing direct directory paths and the specific questions each section answers.

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/guides/ | 如何添加新链接、定义标签、运行验证和生成静态站点？ |
| 运维手册 | docs/operations/ | 如何配置探针调度、解读健康指标、处理证书告警？ |
| 开发者参考 | docs/development/ | 如何扩展验证规则、添加新的元数据提取器、提交 PR？ |
| 架构设计 | docs/architecture/ | 数据流如何组织？版本控制策略是什么？扩展性如何保证？ |
| 常见工作流 | docs/workflows/ | 如何批量导入已有列表、执行定期审计、导出合规报告？ |

## 资源列表

本清单收录了来自用户原始数据的全部外部索引资源，按类别分组以便导航。每个 URL 原样呈现，未添加任何协议前缀或路径修饰。

### 综合视频索引类别

<code>jiujiushipinzaixianguankanb.org.cn</code>

<code>oumeizaixianguankanshipinb.org.cn</code>

<code>rihanshipinmianfeizaixianguankanb.org.cn</code>

<code>mianfeigaoqingshipinzaixianguankanb.org.cn</code>

### 字幕与专题资源类别

<code>renqixiliezhongwenzimuwb.org.cn</code>

<code>rihanmeinvzhongwenzimub.org.cn</code>

<code>qingqingcaoyuanzhongwenzimub.org.cn</code>

## 项目结构

The source tree is organized to separate inventory data, core logic, web assets, and operational tooling. Each directory includes a short comment describing its purpose.

```
link-atlas/
├── atlas.py                     # 主入口 CLI，整合验证、服务、导出子命令
├── requirements.txt             # Python 依赖锁定文件
├── Makefile                     # 构建自动化：test, build-site, metrics
├── data/
│   ├── links.yaml               # 主库存文件：所有 URL 及元数据条目
│   ├── schemas/                 # JSON Schema 定义，用于校验 inventory 结构
│   │   ├── entry.schema.json    # 单条链接的字段规范
│   │   └── taxonomy.schema.json # 标签与分类层级约束
│   └── snapshots/               # 按日期归档的历史 inventory 副本
├── src/
│   ├── core/                    # 核心业务逻辑：验证、探针、元数据抽取
│   │   ├── validator.py         # YAML 解析和 schema 校验实现
│   │   ├── probe.py             # HTTP 探针引擎，含重试和超时策略
│   │   └── metadata.py          # 基于 BeautifulSoup 的元数据抓取
│   ├── exporters/               # 输出格式化模块
│   │   ├── prometheus.py        # 将健康指标转为 Prometheus 暴露格式
│   │   └── staticgen.py         # 从 inventory 生成 HTML 静态站
│   └── utils/                   # 通用工具：日志、配置、时间处理
│       ├── logger.py            # 结构化日志封装
│       └── config.py            # 环境变量与配置文件加载器
├── web/
│   ├── templates/               # Jinja2 模板用于静态站点渲染
│   │   ├── index.html.j2        # 主页表格模板
│   │   └── detail.html.j2       # 单条链接详情视图
│   └── static/                  # 前端资源：CSS 样式表和 JavaScript 筛选脚本
├── tests/                       # 单元测试与集成测试套件
│   ├── test_validator.py        # 校验逻辑覆盖测试
│   ├── test_probe.py            # 探针模拟与异常路径测试
│   └── fixtures/                # 测试用的样例 YAML 和 mock 响应
└── docs/                        # 完整文档树，详见文档导航章节
    ├── guides/
    ├── operations/
    ├── development/
    ├── architecture/
    └── workflows/
```

## 贡献指南

We welcome contributions that improve validation rules, extend metadata extractors, add new exporter backends, or enhance documentation. Please follow the steps below to ensure a smooth integration process.

1.  **Fork and Clone** – Fork the main repository to your personal account, then clone your fork locally. Set up the upstream remote to track the main branch for sync.

2.  **Create a Feature Branch** – Use a descriptive branch name prefixed with the change type, for example `feat/add-headers-probe` or `fix/yaml-schema-date`. Always branch from the latest main commit.

3.  **Write Tests and Docs** – For any new functionality, add corresponding unit tests under the `tests/` directory. Update the relevant documentation files in `docs/` to reflect your changes, including new configuration options or CLI flags.

4.  **Run Validation Locally** – Execute `make test` to run the full test suite, and `make lint` to check code style. Ensure all existing tests pass and no new warnings are introduced.

5.  **Submit a Pull Request** – Push your branch and open a PR against the main repository. Include a clear description of the motivation, the changes made, and screenshots or logs if applicable. Reference any related issue numbers.

## 常见问题

**Q: 如何处理外部链接在验证时返回 403 或 429 状态码的情况？**

A: 这些状态码通常表示服务器拒绝或限制了自动请求。项目探针模块会自动将这些结果标记为 "受限" 而非 "失效"，并在健康仪表板中单独分类。您可以配置探针使用自定义 User-Agent 或增加请求间隔（通过 `probe.delay` 配置项）。对于需要特定会话验证的资源，建议在 inventory 中标注 `requires_session: true` 并排除自动探测。

**Q: 如果用户提供的原始 URL 列表中没有包含协议前缀（如 http 或 https），项目如何处理这些条目？**

A: 项目严格遵循用户原始数据格式存储和展示。在探针执行时，默认策略是依次尝试 HTTPS 和 HTTP，并记录首次成功的协议。但资源列表章节中的显示始终保留用户原始值，不会自动补充协议前缀或进行规范化，以保证与上游数据源完全一致。

**Q: 静态站点生成后，搜索和筛选功能是如何实现的？**

A: 生成的 HTML 页面包含纯 JavaScript 前端索引。筛选逻辑基于浏览器端的内存数据过滤，无需额外后端支持。对于超过 5000 条链接的大型库存，项目提供了可选的预计算索引缓存（使用 `--prebuild-index` 标志），生成更高效的二进制查找结构，但仍保持纯静态部署的便捷性。

## 许可证

MIT License. See the LICENSE file in the repository root for full terms. This project is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors be liable for any claim, damages, or other liability arising from the use of the software.

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:12
