# LinkCatalog Core

LinkCatalog Core 是一个面向技术团队与开源项目维护者的外链资源整理与规范化发布工具。项目定位为“技术资源索引即代码”，通过结构化 Markdown 与可定制的分类体系，帮助开发者将散落在各处的文档、社区、数据源与公告页面整合为单一可维护的信息门户。目标用户包括技术文档工程师、开源社区运营者、内部平台 SRE 以及需要长期跟踪多源外部数据的爬虫开发者。LinkCatalog Core 自身不存储业务数据，仅提供资源导航骨架定义与校验能力，解决多源外链在项目文档中难以统一管理、难以版本追踪、难以自动化检查失效链接的痛点。

## 功能概览

- **资源清单标准化** 提供基于 YAML 与 Markdown 双轨制的资源声明方式，支持将裸域名、带协议 URL、带路径 URL 统一归类，并自动生成符合项目规范的资源列表章节。

- **外链状态探测接口** 内置基于 HTTP 头检查的链接存活度扫描模块，支持批量检测资源列表中各域名的可访问性，输出结构化报告。

- **多级分类与标签系统** 允许为每条资源标记类别、优先级与维护人，支持按技术领域、数据来源、公告类型等维度生成不同视图的文档页面。

- **变更审计日志** 所有资源的新增、删除、URL 变更均记录于变更日志文件，便于团队追溯外链策略调整原因，满足内部合规要求。

- **模板化文档生成器** 根据用户定义的项目元信息与资源列表，自动填充 README、资源索引页、常见问题等模板，减少手动复制粘贴错误。

- **自定义校验规则** 支持配置域名白名单、协议强制规则、路径模式匹配，可在构建时阻止不符合规范的 URL 进入正式文档。

- **命令行交互工具** 提供 cli 子命令用于添加、删除、重命名资源分组，以及批量导入来自 CSV 或现有 Markdown 的资源列表。

## 应用场景

- **开源项目外部依赖索引** 开源项目常引用多个外部数据源、公告页或姊妹项目地址。LinkCatalog Core 可作为构建流程的一部分，在每次发布前自动生成统一格式的资源附录，确保所有外部链接均经过格式校验。

- **技术社区运营公告聚合** 技术社区运营人员需要同时维护官方公告、赛事结果发布页、版本更新日志等多个外部页面入口。使用 LinkCatalog Core 可将不同来源的域名与路径按时间线分组，并生成便于社区用户查阅的导航结构。

- **内部文档中心的外链治理** 企业内部技术文档中心存在大量指向工单系统、监控面板、数据库状态页的外部链接。LinkCatalog Core 的定期探测功能可帮助发现已迁移或下线的页面，及时更新文档。

- **数据采集项目源站管理** 数据采集或爬虫项目需要长期跟踪多个数据源域名，例如比分发布站、统计信息页。LinkCatalog Core 的分类与标签系统可区分正式源、备用源与历史存档源，降低源站变更导致的采集中断风险。

## 快速开始

以下步骤帮助您在本地快速部署 LinkCatalog Core 并生成第一个资源索引页面。

```bash
# 克隆项目仓库
git clone https://github.com/linkcatalog/core.git
cd core

# 安装依赖（使用 Python 3.9+ 及 pip）
pip install -r requirements.txt

# 初始化默认资源目录与配置文件
python -m linkcatalog init --project my-resources

# 添加第一批资源条目（示例）
python -m linkcatalog add --group "official" --url "<code>xijiajishibifena.org.cn</code>"
python -m linkcatalog add --group "official" --url "<code>dejiajishibifena.org.cn</code>"
python -m linkcatalog add --group "official" --url "<code>yijiajishibifena.org.cn</code>"

# 生成最终资源文档（输出至 output/ 目录）
python -m linkcatalog build --output ./output
```

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Python | 3.9 及以上 | 核心运行环境，低于此版本将无法使用类型注解与异步特性 |
| pip | 21.0 及以上 | 用于安装项目依赖包及管理可插拔扩展 |
| Git | 2.25 及以上 | 仅开发模式需要，用于克隆仓库及提交资源变更记录 |
| 网络访问 | 出方向 80/443 开放 | 链接探测功能需要对外发起 HTTP 请求，内网环境需配置代理 |
| 文件系统权限 | 读写执行 | 项目需要创建缓存目录、日志目录及输出目录，建议 755 权限 |
| pytest | 7.0 及以上 | 仅测试环境需要，用于执行单元测试与集成测试套件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | docs/usage/ | 如何声明资源分组、如何配置探测间隔、如何自定义输出模板 |
| 运维指南 | docs/operations/ | 如何部署到生产服务器、如何对接 CI/CD 流程、如何迁移已有资源列表 |
| 设计文档 | docs/design/ | 整体架构分层、数据模型定义、扩展点设计、失效链接重试策略 |
| 贡献参考 | docs/contributing/ | 代码风格指引、提交信息格式、测试用例编写规范、评审流程 |

## 资源列表

### 官方数据源分组

<code>xijiajishibifena.org.cn</code>

<code>dejiajishibifena.org.cn</code>

<code>yijiajishibifena.org.cn</code>

<code>fajiajishibifena.org.cn</code>

### 赛事信息分组

<code>zuqiubisaijieguoa.org.cn</code>

<code>yingchaobifena.org.cn</code>

### 历史归档分组

<code>xijiabifena.org.cn</code>

## 项目结构

```
linkcatalog-core/
├── src/                           # 核心源代码目录
│   ├── linkcatalog/               # 主包
│   │   ├── __init__.py            # 版本号与公开 API 声明
│   │   ├── cli.py                 # 命令行入口与子命令路由
│   │   ├── config.py              # 配置加载、合并与校验逻辑
│   │   ├── model/                 # 数据模型层
│   │   │   ├── resource.py        # 资源条目与分组数据类
│   │   │   └── manifest.py        # 资源清单整体结构定义
│   │   ├── checker/               # 链接探测模块
│   │   │   ├── http.py            # 基于 aiohttp 的异步检查器
│   │   │   └── reporter.py        # 探测结果汇总与格式化输出
│   │   ├── generator/             # 文档生成引擎
│   │   │   ├── markdown.py        # Markdown 章节与表格渲染
│   │   │   └── template.py        # Jinja2 模板加载与上下文填充
│   │   └── utils/                 # 通用工具函数
│   │       ├── validators.py      # URL 规范化与域名白名单检查
│   │       └── logger.py          # 日志配置与敏感信息过滤
├── tests/                         # 单元测试与集成测试
│   ├── unit/                      # 单模块测试
│   └── integration/               # 端到端命令测试
├── docs/                          # 用户文档与设计文档源文件
├── samples/                       # 示例资源声明文件与输出样例
├── requirements.txt               # 生产环境依赖列表
├── requirements-dev.txt           # 开发与测试环境额外依赖
├── setup.py                       # 包安装与分发配置
├── CHANGELOG.md                   # 版本变更历史
└── README.md                      # 项目首页文档（即本文档）
```

## 贡献指南

1. 在 GitHub 或内部 Git 平台上 Fork 本项目仓库，并克隆到本地开发环境。建议在 dev 分支上进行所有改动，保持主分支与上游同步。

2. 安装开发依赖并激活预提交钩子，用于自动执行代码格式化（black、isort）与基础静态检查（flake8）。预提交配置位于 .pre-commit-config.yaml。

3. 任何新增功能或修复均需附带至少一个单元测试用例，测试文件放置于 tests/unit 对应子目录，并确保所有现有测试通过（pytest -v）。

4. 提交变更时请遵循约定式提交规范，使用 fix:、feat:、docs:、refactor: 等前缀，并在提交正文中详细说明改动原因与影响范围。

5. 发起合并请求前，请先同步上游主分支最新代码，并解决冲突。合并请求描述中需标注关联的 issue 编号以及是否包含破坏性变更。

## 常见问题

**Q：LinkCatalog Core 是否会对资源列表中的 URL 进行自动内容抓取或存储？**

A：不会。项目仅执行轻量级 HTTP HEAD 或 GET 请求以检查链接可达性与响应状态码，不会解析页面内容、不会存储任何返回的 HTML 或文本数据。所有探测结果仅包含状态码、响应时间与重定向链信息。

**Q：如果资源列表中的某个域名长期不可访问，项目会如何处理？**

A：探测模块会在每次构建时重新检查所有资源。若连续三次构建均检测到不可访问状态，项目会生成警告日志并标记该资源为“失效”，但不会自动删除条目。维护者可手动确认后移除或替换为可用地址。

**Q：项目是否支持对裸域名自动补全协议或路径？**

A：项目严格遵守用户输入的原始格式，不会对裸域名自动补充 http:// 或 https:// 前缀，也不会在域名后追加默认路径。校验模块仅检查格式合法性（如是否包含非法字符），不改变资源声明内容。用户需自行确保所声明的 URL 在浏览器或 curl 中可直接使用。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
