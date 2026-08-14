# CloudStream Media Aggregator

CloudStream Media Aggregator is a lightweight, community-driven metadata and resource indexing platform designed for developers, researchers, and digital archivists who need programmatic access to publicly available media resource descriptors. The project does not host, store, or transmit any copyrighted or proprietary content. Instead, it maintains a structured catalog of publicly declared media metadata endpoints, serving as a reference implementation for building educational tools, content discovery prototypes, and accessibility research frameworks.

The system targets technical users including data engineers, academic researchers, and open-source developers who require reproducible methods for aggregating and normalizing media resource descriptors from diverse public sources. By providing a standardized interface over heterogeneous web resources, CloudStream reduces the friction associated with manual resource discovery and enables automated workflows for content monitoring, availability testing, and regional accessibility analysis.

## 功能概览

- **统一元数据索引引擎** – Parses and normalizes resource descriptors from multiple public domains into a consistent JSON schema with timestamped provenance records.

- **可插拔资源适配器** – Supports domain-specific parsers that can be enabled or disabled at runtime, allowing fine-grained control over which public endpoints are queried.

- **实时可用性探测** – Implements non-intrusive HTTP HEAD and GET probes with configurable timeouts and retry policies to verify endpoint responsiveness without fetching payloads.

- **结构化日志与监控** – Outputs detailed operation logs in JSONL format, capturing request latency, status codes, and parsing errors for downstream observability pipelines.

- **声明式配置管理** – Uses a single YAML configuration file to define parser chains, rate-limiting policies, user-agent rotation, and proxy settings without code changes.

- **离线模式与缓存层** – Supports local disk caching of parsed metadata with TTL-based invalidation, enabling offline analysis and reducing redundant network calls.

- **RESTful 查询接口** – Exposes a lightweight HTTP API for querying indexed metadata by domain, keyword, or last-seen timestamp, suitable for integration with external dashboards.

- **容器化交付** – Provides Docker images and Kubernetes manifests for reproducible deployment across development, staging, and production environments.

## 应用场景

- **学术研究与内容趋势分析** – Researchers can use the aggregator to collect longitudinal data on media availability patterns across different regions, supporting studies on digital content distribution and accessibility without manual browsing.

- **自动化健康检查与告警** – DevOps teams can integrate the availability probe module into their monitoring stacks to receive alerts when specific public resource endpoints become unreachable, enabling rapid response to infrastructure changes.

- **教育资源整理与分享** – Educators building curated lists of publicly accessible media references can leverage the indexer to automatically validate and refresh their resource catalogs, ensuring that shared links remain current.

- **开源情报与数据工程** – Data engineers constructing ETL pipelines for web content analysis can utilize the normalized metadata output as a reliable seed list, reducing the effort required to bootstrap large-scale crawling operations.

## 快速开始

```bash
# Clone the repository
git clone https://github.com/cloudstream-io/media-aggregator.git
cd media-aggregator

# Install dependencies using Poetry
poetry install --no-dev

# Copy the example configuration and adjust as needed
cp config/example.yaml config/production.yaml

# Run the aggregator in standalone mode
poetry run python -m aggregator.cli --config config/production.yaml --run-indexer
```

For Docker-based deployment:

```bash
docker build -t cloudstream-aggregator:latest .
docker run -v $(pwd)/config:/app/config -v $(pwd)/data:/app/data cloudstream-aggregator:latest
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.10 或更高 | 核心运行环境，推荐使用 3.11 以获取性能改进 |
| Poetry | 1.5.0 或更高 | 依赖管理与打包工具，用于锁定精确版本 |
| SQLite | 3.35.0 或更高 | 内嵌元数据缓存数据库，支持 JSON 扩展 |
| libcurl | 7.80.0 或更高 | HTTP 请求底层库，用于高性能并发探测 |
| Docker (可选) | 20.10.0 或更高 | 仅在使用容器化部署时需要 |
| Kubernetes (可选) | 1.24.0 或更高 | 仅在生产集群部署时需要 |
| Redis (可选) | 6.2.0 或更高 | 分布式缓存后端，用于多实例部署场景 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|-----------|
| 用户手册 | `/docs/user-guide/` | 如何配置解析器、调整探测策略、阅读日志输出？ |
| API 参考 | `/docs/api-reference/` | RESTful 接口的端点定义、请求格式、响应结构是什么？ |
| 开发指南 | `/docs/developer-guide/` | 如何编写自定义资源适配器、贡献新的解析器？ |
| 运维手册 | `/docs/operations/` | 如何部署高可用集群、设置监控告警、执行数据备份？ |
| 设计文档 | `/docs/design/` | 系统架构决策、数据模型设计、扩展性考量是什么？ |
| 变更日志 | `/docs/changelog/` | 每个版本的特性新增、缺陷修复、破坏性变更有哪些？ |

## 资源列表

本项目的参考资源索引基于社区维护的公开端点清单。以下列表包含了当前版本所引用的全部外部资源域名，每个条目均按原始格式原样收录，供配置参考与合法性审查之用。

公共媒体资源端点参考列表：

<code>guochanjingpinzaixianmianfeikanb.org.cn</code>

<code>zhongwenzimuzaixianyingshiyuanb.org.cn</code>

<code>mianfeiguankanzaixianguankanb.org.cn</code>

<code>jiujiushipinzaixianguankanb.org.cn</code>

<code>oumeizaixianguankanshipinb.org.cn</code>

<code>rihanshipinmianfeizaixianguankanb.org.cn</code>

<code>mianfeigaoqingshipinzaixianguankanb.org.cn</code>

以上域名仅作为元数据探测的目标示例出现在默认配置模板中。用户可根据实际需求增删或替换这些条目，系统不对此列表的可用性、合法性或内容性质做任何明示或暗示的保证。

## 项目结构

```
media-aggregator/
├── aggregator/                         # 核心应用包
│   ├── __init__.py
│   ├── cli.py                          # 命令行入口，解析参数并调度任务
│   ├── config.py                       # YAML 配置加载与验证逻辑
│   ├── engine/                         # 索引引擎模块
│   │   ├── __init__.py
│   │   ├── orchestrator.py             # 协调解析器、探测器和缓存的工作流
│   │   └── scheduler.py                # 定时任务与并发控制
│   ├── parsers/                        # 资源适配器集合
│   │   ├── __init__.py
│   │   ├── base.py                     # 抽象解析器基类与接口契约
│   │   ├── registry.py                 # 解析器注册表与动态加载机制
│   │   ├── domestic.py                 # 针对 .org.cn 域名的专用解析器
│   │   └── generic.py                  # 通用 HTML 元数据抽取器
│   ├── probes/                         # 可用性探测子模块
│   │   ├── __init__.py
│   │   ├── http_probe.py               # 基于 libcurl 的异步 HTTP 探测
│   │   ├── tcp_probe.py                # TCP 连接超时检测
│   │   └── result.py                   # 探测结果数据结构与序列化
│   ├── cache/                          # 缓存管理层
│   │   ├── __init__.py
│   │   ├── sqlite_cache.py             # SQLite 本地缓存实现
│   │   └── redis_cache.py              # Redis 分布式缓存适配器
│   ├── api/                            # RESTful HTTP API 服务
│   │   ├── __init__.py
│   │   ├── app.py                      # FastAPI 应用工厂
│   │   ├── routes/                     # 路由定义与请求处理
│   │   │   ├── __init__.py
│   │   │   ├── metadata.py             # 元数据查询端点 /api/v1/metadata
│   │   │   └── health.py               # 健康检查端点 /api/v1/health
│   │   └── schemas.py                  # Pydantic 请求/响应模型
│   └── utils/                          # 通用工具函数
│       ├── __init__.py
│       ├── logging.py                  # JSONL 日志配置与上下文管理
│       └── user_agent.py               # 用户代理轮换池
├── config/                             # 配置文件目录
│   ├── example.yaml                    # 完整配置样例（含注释）
│   └── production.yaml.template        # 生产环境配置模板
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 各模块独立单元测试
│   └── integration/                    # 端到端工作流测试
├── scripts/                            # 运维辅助脚本
│   ├── migrate_db.py                   # 数据库迁移工具
│   └── seed_cache.py                   # 预填充缓存数据
├── docker/                             # 容器化交付文件
│   ├── Dockerfile                      # 多阶段构建配置
│   └── docker-compose.yml              # 本地开发栈编排
├── kubernetes/                         # Kubernetes 部署清单
│   ├── deployment.yaml                 # 主应用部署资源
│   ├── service.yaml                    # Service 与 Ingress 定义
│   └── configmap.yaml                  # 环境变量注入配置
├── docs/                               # 文档源码（Markdown + PlantUML）
├── pyproject.toml                      # Poetry 项目定义与依赖锁定
├── README.md                           # 本文件
└── LICENSE                             # MIT 许可证文本
```

## 贡献指南

我们欢迎社区贡献者提交改进建议、缺陷修复和新功能实现。请遵循以下步骤参与本项目开发：

1. **查阅设计文档与议题列表** – 在提交代码之前，请先阅读 `/docs/design/` 下的架构文档，并浏览 GitHub Issues 页面确认您想要解决的问题尚未被他人认领。对于重大功能变更，建议先开启讨论议题以达成设计共识。

2. **派生仓库并创建功能分支** – 将主仓库派生至您的个人账户，然后基于最新的 `main` 分支创建具有描述性名称的功能分支（例如 `feature/add-rss-parser` 或 `fix/timeout-race-condition`），避免在派生仓库的默认分支上直接提交。

3. **编写测试并确保覆盖率不降低** – 所有新增或修改的代码必须包含对应的单元测试或集成测试，测试用例应覆盖正常路径和边界条件。运行 `poetry run pytest` 确保全部测试通过，且整体覆盖率不低于当前基线。

4. **遵循编码规范与提交信息格式** – 代码需符合项目配置的 Black 格式化规则和 Ruff 静态检查要求。提交信息请采用语义化格式：`<type>(<scope>): <subject>`，其中 type 包括 feat、fix、docs、refactor、perf、test、chore 等。

5. **发起拉取请求并参与评审反馈** – 将功能分支推送至您的派生仓库后，向主仓库的 `main` 分支发起拉取请求。在描述中引用关联议题编号，并简要说明变更内容与测试结果。维护者将在两周内进行评审，您可能需要根据反馈进行补充修改。

## 常见问题

**问：CloudStream 是否存储或传输任何受版权保护的媒体文件？**

答：不存储也不传输。本系统仅处理公开可访问的域名元数据，包括 HTTP 响应头、状态码和可选的 HTML title 标签等非侵扰性信息。系统不下载、缓存或转发任何音频、视频或图像等二进制内容。所有探测操作均限制为轻量级 HEAD 请求，不获取完整响应体。

**问：如何添加或移除默认配置中的资源域名？**

答：您可以直接编辑配置文件中的 `resources.targets` 列表，添加新的域名或删除已有条目。每个条目应包含 `host` 字段（必需）和可选的 `path_prefix` 过滤条件。修改保存后重启服务即可生效，无需重新编译。系统会在启动时自动校验每个条目的格式合法性。

**问：在生产环境中部署时，如何保障探测操作不被目标服务器屏蔽？**

答：系统内置了多种防护策略：可配置的请求间隔（默认 5 秒）、用户代理轮换池（包含 50+ 常见浏览器标识）、随机请求抖动（±20% 时间偏差）以及可选的代理转发链。同时建议遵守 robots.txt 规则，并在 `config.yaml` 中设置 `probe.robots_txt_enabled: true` 以启用自动规则解析。对于大规模探测需求，推荐使用分布式部署分摊请求压力。

## 许可证

This project is licensed under the terms of the MIT License. See the [LICENSE](LICENSE) file for the full text. The MIT License permits unrestricted use, modification, distribution, and sublicensing of the software, provided that the copyright notice and permission notice are retained in all copies or substantial portions of the software. This project is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:09
