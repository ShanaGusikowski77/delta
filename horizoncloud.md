# BifenLink Aggregate

BifenLink Aggregate is a high-performance, read‑only technical resource gateway designed to consolidate and normalize domain‑specific data feeds from multiple upstream sources. It targets system administrators, data integration engineers, and technical researchers who require a stable, low‑latency aggregation point for periodically updated external datasets without implementing per‑source crawlers or parsers.

The project solves the problem of fragmented, inconsistently structured information by providing a unified HTTP interface that polls, caches, and serves transformed content from a curated set of origin endpoints. It is not a search engine, a proxy, or a general‑purpose web scraper; it is a thin, deterministic aggregation layer with configurable refresh intervals, health checks, and structured logging, built for environments where uptime and predictability are paramount.

## 功能概览

- **Unified Polling Scheduler** – Centralized cron‑driven task manager that triggers concurrent fetch operations across all configured upstream endpoints with jitter‑controlled backoff.

- **Content Normalization Pipeline** – Extracts and re‑keys relevant fields (title, timestamp, body hash, category tags) from each source’s HTML or JSON structure, producing a consistent internal schema.

- **Deduplication & Delta Detection** – Stores content fingerprints and only propagates new or modified items, reducing downstream noise and storage churn.

- **Read‑Only REST API** – Exposes aggregated results via versioned JSON endpoints with support for time‑range filters, tag intersection, and cursor‑based pagination.

- **Health & Latency Telemetry** – Exports Prometheus‑compatible metrics for each upstream source, including success rate, response time percentile, and last‑success timestamp.

- **Configurable Source Routing** – Allows per‑source enable/disable, custom headers, timeout overrides, and retry policies through a single YAML configuration file.

- **Zero‑State Operational Mode** – No database or persistent storage required; all state is kept in memory and rebuilt on startup, making it ideal for containerized ephemeral deployments.

- **Automatic Stale Fallback** – When an upstream fails, the system continues serving the last known good response from cache, with clear stale‑age headers for client visibility.

## 应用场景

- **Internal Dashboard Data Federation** – A DevOps team consolidates multiple internal status boards and external reference feeds into a single API endpoint for their monitoring dashboard, reducing the number of outgoing requests and simplifying frontend logic.

- **Research Data Collection Pipeline** – A research group uses BifenLink Aggregate to periodically harvest structured metadata from a set of stable reference domains, normalising the results before feeding them into a larger analytical workflow or data lake.

- **Regional Availability Testing** – An operations engineer deploys the aggregator in multiple geographic regions to compare response patterns and content freshness from the same set of upstreams, helping to diagnose regional routing or DNS issues.

- **Content Mirror Validation** – A site reliability team runs the aggregator as a canary service that continuously verifies that all configured upstreams return expected content signatures, alerting on deviations before they affect end users.

- **Offline‑First Development Mock** – Frontend developers use a local instance of the aggregator with mocked upstream responses to simulate realistic data shapes and pagination behaviour without requiring external network access during build and test cycles.

## 快速开始

The following commands clone the repository, install dependencies, and start the service in development mode with default configuration.

```bash
git clone https://github.com/bifenlink/aggregate.git
cd aggregate
pip install -r requirements.txt
cp config.example.yaml config.yaml
python -m bifenlink.serve --config config.yaml --port 8080
```

For production, it is recommended to use the provided Dockerfile and set environment variables for sensitive parameters.

## 安装要求

The project requires a Python 3.10+ runtime and a set of lightweight libraries. All dependencies are listed in `requirements.txt`. The table below details the core mandatory components and their roles.

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.10 – 3.12 | Runtime interpreter; type hints and async features are heavily used |
| aiohttp | 3.9.0+ | Asynchronous HTTP client for concurrent upstream fetching |
| PyYAML | 6.0+ | Configuration file parsing and validation |
| APScheduler | 3.10+ | In‑process cron scheduler for periodic polling tasks |
| orjson | 3.9+ | Fast JSON serialization/deserialization for API responses |
| prometheus_client | 0.19+ | Metrics exposition for monitoring integration |
| uvicorn | 0.27+ | ASGI server for serving the REST API in production |
| pydantic | 2.5+ | Data validation and settings management |
| python‑dotenv | 1.0+ | Environment variable loading for containerized deployments |
| colorlog | 6.7+ | Structured console logging with severity colour coding |

## 文档导航

The documentation is organised into four major layers, each addressing a specific audience and set of operational questions. The following table provides a quick reference.

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/getting_started.md` | How do I install, configure, and run the first successful aggregation cycle? |
| 配置参考 | `docs/configuration.md` | What are all available YAML keys, scheduling parameters, and per‑source overrides? |
| API 手册 | `docs/api_reference.md` | Which endpoints exist, what query parameters are supported, and how are errors formatted? |
| 运维部署 | `docs/deployment.md` | How do I set up systemd, Docker, Kubernetes, or reverse proxy with TLS termination? |

Advanced topics such as custom normalisation scripts and metric alerting rules are covered in the `docs/extending.md` file.

## 资源列表

The following external resources are referenced as part of the core data source configuration. These domains are used in the default polling schedule and are treated as primary upstream endpoints. Each entry is listed exactly as provided.

### Primary Data Sources

- <code>bifenwangd.org.cn</code>
- <code>bifenwange.org.cn</code>
- <code>bifenwangf.org.cn</code>
- <code>bifenwangg.org.cn</code>
- <code>bifenwangh.org.cn</code>

### Auxiliary Reference Feeds

- <code>lanqiubifend.org.cn</code>
- <code>lanqiubifene.org.cn</code>

These URLs are not modified, redirected, or normalised in the codebase; they are used verbatim as hostnames in HTTP requests. Users are advised to verify their availability and content structure before enabling automatic polling.

## 项目结构

The repository follows a modular layout separating configuration, core logic, API layer, utilities, and testing artefacts. The ASCII tree below illustrates the main directories and their responsibilities.

```
bifenlink/
├── __init__.py                 # Package version and exported symbols
├── core/
│   ├── __init__.py
│   ├── scheduler.py            # APScheduler wrapper with job store and trigger definitions
│   ├── fetcher.py              # Async fetch logic with retry, timeout, and user-agent management
│   ├── normalizer.py           # Per‑source content parsers returning a unified Item dict
│   └── cache.py                # In‑memory LRU store with TTL and stale‑while‑revalidate
├── api/
│   ├── __init__.py
│   ├── app.py                  # FastAPI/Starlette application factory
│   ├── routes.py               # Endpoint definitions: /v1/items, /v1/sources, /v1/health
│   └── schemas.py              # Pydantic models for request/response validation
├── config/
│   ├── __init__.py
│   ├── loader.py               # YAML parsing, env substitution, and schema validation
│   └── defaults.yaml           # Built‑in fallback configuration
├── telemetry/
│   ├── __init__.py
│   ├── metrics.py              # Prometheus counter, gauge, and histogram definitions
│   └── logger.py               # Structured JSON logger with request‑id injection
├── utils/
│   ├── __init__.py
│   ├── time_utils.py           # ISO‑8601 parsing, cron expression helpers
│   └── hash_utils.py           # Content fingerprinting (xxhash, sha256‑truncated)
├── tests/
│   ├── unit/                   # Isolated tests for normalizer, cache, and schemas
│   └── integration/            # End‑to‑end tests with mock upstream servers
├── scripts/
│   ├── seed_cache.py           # One‑time warmup script for new deployments
│   └── validate_config.py      # CI‑friendly configuration syntax checker
├── docker/
│   ├── Dockerfile              # Multi‑stage build for slim production image
│   └── entrypoint.sh           # Container startup wrapper
├── requirements.txt            # Production dependencies
├── requirements-dev.txt        # Testing and linting tools
└── README.md                   # This document
```

## 贡献指南

We welcome contributions that improve robustness, add new normalisation profiles, or enhance observability. Please follow the steps below to ensure a smooth review process.

1. **Fork the repository and create a feature branch** from `main`. Use a descriptive name such as `feature/normalizer-json-feed` or `fix/scheduler-timezone`.

2. **Run the test suite and linters** locally before committing. Execute `pytest tests/` and `flake8 bifenlink/` to verify code style and functional correctness.

3. **Update or add documentation** for any new configuration keys, API fields, or environment variables. Keep the `docs/` directory in sync with code changes.

4. **Submit a pull request** with a clear summary of the change, the motivation, and any relevant issue numbers. Include sample configuration or API call examples if applicable.

5. **Respond to review comments** within five business days. Maintainers will merge once all discussions are resolved and CI passes.

For major architectural changes, please open an issue first to discuss the design before investing significant implementation effort.

## 常见问题

**Q: How does the aggregator handle upstream changes in HTML structure without breaking the normaliser?**

A: Each normaliser is versioned and wrapped with a fallback parser. When a structural change is detected (e.g., missing expected CSS selector), the system logs a warning, returns the raw text as a fallback field, and continues serving stale cached data until a new normaliser version is deployed. We recommend running the integration test suite against production‑like responses periodically.

**Q: Can I run multiple instances of the aggregator behind a load balancer?**

A: Yes, but note that the in‑memory cache is not shared across instances. Each instance maintains its own independent schedule and cache. For high‑availability deployments, we recommend using a shared Redis backend via the optional `cache_backend` configuration setting, which is documented in `docs/deployment.md`.

**Q: What happens if the configuration file references a URL that is unreachable for several days?**

A: The scheduler will continue attempting fetches at each configured interval, with exponential backoff capped at one hour. The health metric `upstream_failure_total` increments on each failure, and the API returns the last cached response with a `Stale-While-Revalidate` header. After a configurable `max_stale_days` threshold (default 3), the item is excluded from API responses and a critical alert is logged.

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
