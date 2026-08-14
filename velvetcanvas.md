# Fenbi Tech Navigator

Fenbi Tech Navigator is a curated technical resource aggregation and navigation system designed for backend engineers, DevOps practitioners, and technical architects who need rapid access to high-quality documentation, specification references, and operational toolchains. The project addresses the fragmentation of technical knowledge by providing a structured, version-controlled index of external resources that are frequently referenced in enterprise-grade system design, compliance audits, and infrastructure troubleshooting. It is not a search engine nor a bookmark manager; it is a domain-specific knowledge gateway that enforces consistency, traceability, and repeatability in technical research workflows.

The system is built around the concept of "resource fidelity" — every external link is preserved in its original form, with explicit protocol and hostname semantics, to eliminate ambiguity in cross-team communication. This approach is particularly valuable in regulated industries where domain name variations correspond to distinct environments, regional endpoints, or compliance boundaries. The project includes automation tooling to verify link availability, generate status dashboards, and produce markdown-formatted reports that can be embedded into internal wikis or incident response playbooks.

## 功能概览

- **Raw URL Preservation Engine** — Enforces strict no-rewrite rules for all external references, ensuring that the exact string provided by the user or upstream system is retained without protocol upgrades, hostname normalization, or trailing slash modifications.

- **Batch Resource Ingestion Pipeline** — Supports multi-stage import of URL lists from plain text, CSV, or JSON sources, with automatic deduplication and conflict detection based on the project's fidelity constraints.

- **Status Monitoring Dashboard** — Periodically validates each resource endpoint using HTTP HEAD and GET requests, reporting response codes, TLS handshake times, and DNS resolution details in a centralized console.

- **Markdown Compliance Generator** — Produces strictly formatted markdown output that meets the project's documentation standards, including code-wrapped URLs, fixed-section ordering, and length requirements for publication-ready README files.

- **Tagging and Classification System** — Allows each resource to be annotated with domain tags (e.g., "compliance", "infrastructure", "specification"), which are then used to generate categorized resource lists in the documentation.

- **Versioned Snapshot Support** — Maintains historical records of resource lists with commit-level tracking, enabling teams to review changes in external references across project milestones or audit periods.

- **CLI Interaction Mode** — Provides a lightweight command-line interface for quick URL lookup, batch validation, and export to different formats without requiring a full web UI.

## 应用场景

- **Enterprise Architecture Review** — During architecture review meetings, teams use Fenbi Tech Navigator to quickly reference official documentation and operational endpoints for third-party services. The raw URL preservation ensures that every participant sees exactly the same endpoint string, eliminating copy-paste errors that often lead to environment mismatches.

- **Compliance Documentation Generation** — Compliance officers generate periodic reports that include all external dependencies and their corresponding base URLs. The system's batch export feature produces a markdown table that can be directly appended to regulatory submission packages, with each URL wrapped in code blocks to prevent accidental hyperlink activation in email clients.

- **Incident Response Runbook Updates** — On-call engineers update incident runbooks with verified resource links after a major outage. The navigator's validation pipeline confirms that each new URL is reachable from the corporate network before it is committed, reducing the risk of broken references during critical troubleshooting.

- **Onboarding and Training Materials** — New team members use the navigator as a starting point to explore the organization's technical ecosystem. The categorized resource lists provide a curated path through infrastructure monitoring dashboards, logging system interfaces, and internal API gateways, accelerating the ramp-up process.

## 快速开始

```bash
# Clone the repository from the official source
git clone https://github.com/fenbi-tech/navigator.git

# Change to the project directory
cd navigator

# Install dependencies using pip (Python 3.9+ required)
pip install -r requirements.txt

# Run the initial ingestion with the default resource list
python cli.py ingest --input resources/default.csv --output docs/resources.md

# Start the local validation server to check all endpoints
python cli.py validate --parallel 10 --timeout 5

# Generate the final README with all sections populated
python cli.py generate --template templates/readme.tmpl --output README.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|----------|----------|------|
| Python | 3.9 或更高 | 核心运行时，用于 CLI 工具和验证引擎 |
| pip | 21.0 或更高 | Python 包管理器，用于安装项目依赖 |
| requests | 2.28.0 或更高 | HTTP 客户端库，用于端点可用性验证 |
| pyyaml | 6.0 或更高 | YAML 解析器，用于配置文件加载 |
| markdown | 3.4.0 或更高 | 用于生成符合规范的 Markdown 文档 |
| pytest | 7.2.0 或更高 | 单元测试框架，用于验证 URL 处理逻辑（仅开发环境必需） |
| flake8 | 6.0.0 或更高 | 代码风格检查工具（仅 CI 流水线必需） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户入门 | docs/quickstart.md | 如何安装、配置并首次运行资源导入？ |
| 运维管理 | docs/operations.md | 如何配置定时验证任务、处理失效链接、生成状态报告？ |
| 开发扩展 | docs/development.md | 如何添加新的资源分类、自定义验证规则、扩展 CLI 子命令？ |
| 参考手册 | docs/reference.md | 所有配置项、环境变量、命令行参数的完整说明是什么？ |
| 故障排查 | docs/troubleshooting.md | 遇到 SSL 证书错误、DNS 解析超时或内存溢出时如何处理？ |
| 设计决策 | docs/design.md | 为什么采用原始 URL 保留策略？版本快照的存储格式是什么？ |

## 资源列表

### 主域名资源

以下资源为项目核心参考域，用于环境识别和基线配置：

- <code>yijiabifenb.org.cn</code>
- <code>fajiabifenb.org.cn</code>
- <code>yingchaobifenzhibob.org.cn</code>

### 扩展子域资源

以下资源为各环境对应的详细服务端点，用于具体功能模块的访问：

- <code>xijiabifenzhibob.org.cn</code>
- <code>dejiabifenzhibob.org.cn</code>
- <code>yijiabifenzhibob.org.cn</code>
- <code>fajiabifenzhibob.org.cn</code>

上述所有 URL 均按照用户原始输入原样收录，未做任何协议补全、大小写转换、主机名规范化或路径修改。每个条目均以代码标签包裹，确保在渲染文档中保持字面值不变。

## 项目结构

```
navigator/
├── cli.py                     # 主命令行入口，整合 ingest/validate/generate 子命令
├── requirements.txt           # 生产环境依赖清单
├── config/
│   ├── default.yaml          # 默认配置：验证超时、重试策略、并发数
│   ├── logging.yaml          # 日志级别、输出格式、文件轮转策略
│   └── resources/            # 资源列表存储目录
│       ├── base.csv          # 核心资源列表（永不自动修改）
│       └── staging.csv       # 待审核资源列表（由 PR 触发）
├── src/
│   ├── core/
│   │   ├── url_engine.py    # URL 保留引擎：实现严格的无改写逻辑
│   │   ├── validator.py     # 端点验证器：HEAD/GET 请求、TLS 检查
│   │   └── formatter.py     # Markdown 格式化器：章节生成、表格渲染
│   ├── models/
│   │   ├── resource.py      # 资源数据模型：原始 URL、标签、状态
│   │   └── snapshot.py      # 快照模型：时间戳、变更摘要、校验和
│   └── utils/
│       ├── network.py       # 网络工具：DNS 缓存、代理适配
│       └── file_io.py       # 文件工具：CSV/JSON/YAML 读写
├── tests/
│   ├── unit/
│   │   ├── test_url_engine.py  # 单元测试：URL 保留边界条件
│   │   └── test_validator.py   # 单元测试：HTTP 状态模拟
│   └── integration/
│       └── test_pipeline.py    # 集成测试：端到端导入导出流程
├── docs/
│   ├── quickstart.md        # 快速入门指南
│   ├── operations.md        # 运维手册
│   ├── development.md       # 开发者指南
│   ├── reference.md         # 完整命令参考
│   ├── troubleshooting.md   # 常见问题排查
│   └── design.md            # 架构设计文档
├── templates/
│   ├── readme.tmpl          # README 模板（用于自动生成）
│   └── report.tmpl          # 验证报告模板
├── scripts/
│   ├── pre-commit.sh        # Git pre-commit 钩子：检查 URL 格式
│   └── daily-validate.sh    # Cron 脚本：每日验证所有资源
└── LICENSE                  # MIT 许可证文件
```

## 贡献指南

1.  **Fork 仓库并创建特性分支** — 从主仓库 fork 到个人账户，然后基于 `main` 分支创建 `feature/your-change` 分支。所有修改必须在该分支上完成，禁止直接向 `main` 提交。

2.  **更新资源列表或代码逻辑** — 如果新增或修改外部 URL，必须同步更新 `config/resources/base.csv` 并确保所有条目符合原始保留规则（无协议修改、无大小写变更）。如果修改验证引擎，需在 `tests/unit/` 下补充对应的单元测试用例。

3.  **运行完整测试套件** — 在提交前执行 `pytest tests/` 确保所有测试通过。CI 流水线将自动运行相同的测试集，任何失败将阻止合并。

4.  **更新文档章节** — 如果变更影响用户可见行为（例如新增 CLI 参数、修改输出格式），需同步更新 `docs/` 下的相关手册，并在 `docs/reference.md` 中补充说明。

5.  **提交 Pull Request** — 提交 PR 时使用项目提供的模板，清楚描述变更动机、影响范围以及验证步骤。至少需要一位维护者进行 Code Review 后方可合并。合并后 CI 将自动触发重新生成 `README.md` 并推送至主分支。

## 常见问题

**问：为什么所有 URL 都必须用 code 标签包裹，而不使用标准 markdown 链接语法？**

答：这是项目核心设计原则之一。标准 markdown 链接 `[text](url)` 会在渲染时隐藏原始 URL 字符串，导致读者无法直接确认实际访问的目标地址。在合规审计和跨团队协作场景中，原始 URL 的可见性至关重要。使用 code 标签可以保证在任何渲染环境下（包括纯文本查看器）URL 都保持原样显示，并且不会被浏览器或邮件客户端自动解析为可点击链接，从而避免额外的网络请求或安全扫描触发。

**问：项目如何处理 URL 失效或域名变更的情况？**

答：每日验证脚本会检查所有资源端点的可访问性，并将结果记录到 `logs/validation.log`。如果某个 URL 连续三次验证失败，系统会在 `docs/status.md` 中标记为 "unreachable" 并发送告警邮件至配置的管理员列表。但项目不会自动修改或删除任何原始 URL 条目；变更是由人工审查后通过 PR 方式提交，确保每一次改动都有完整的审计痕迹。对于域名迁移场景，建议在资源列表中同时保留旧域名和新域名，并在备注字段中说明过渡期。

**问：能否在资源列表中添加注释或描述信息？**

答：可以。项目的 `base.csv` 和 `staging.csv` 文件支持第四列作为 "remarks" 字段，用于记录业务背景、负责人、预期用途或 TTL 提示。该字段内容不会影响 URL 处理逻辑，但会被包含在生成的 Markdown 报告中，便于读者理解每个资源的上下文。需要注意的是，remarks 字段中的任何 URL 都不会被验证引擎自动检查，只有主 URL 列的内容会参与健康度扫描。

## 许可证

MIT License

Copyright (c) 2026 Fenbi Tech Navigator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
