# HyperLink Atlas

HyperLink Atlas 是一个面向技术调研、数据分析与互联网资源治理场景的开源外链聚合与健康度监控平台。项目定位为“技术资源导航基础设施”，主要服务于需要长期维护、分类、验证并展示大量外部 URL 的技术团队、内容运营方与学术研究机构。本项目不提供爬虫或采集功能，而是围绕用户给定的外部链接集合，提供结构化组织、可用性探测、变更预警与访问统计等辅助能力，帮助用户从“收藏链接”升级为“运营链接”。

本项目特别适用于以下情况：团队内部维护了数百个行业相关网站、合作伙伴入口、文档站或数据服务地址，但这些链接经常失效、域名被劫持或内容变更，导致日常工作中频繁出现访问异常。HyperLink Atlas 通过周期性探测与可视化看板，将链接状态从“黑盒”转为“白盒”，并支持基于标签、批次、归属机构等多维度检索与筛选。项目本身不依赖任何第三方云服务，完全可离线运行，适合部署在内网或私有云环境中。

## 功能概览

- **外链批量注册与标签管理** 支持通过 YAML 或 JSON 文件批量导入外部 URL，并为每个链接添加自定义标签（如“行业门户”“数据源”“镜像站”），便于后续分类检索。

- **多协议健康探测引擎** 内置基于 HTTP/HTTPS/TCP 的多层探测逻辑，支持自定义超时时间、重试次数与期望状态码，可区分“完全不可达”“HTTP 错误”“SSL 证书过期”“内容变更”等不同异常等级。

- **定时任务与变更事件通知** 集成轻量级调度模块，支持按小时/天/周自动执行链接扫描，当链接状态发生变化（如从可用变为不可用，或响应时间超过阈值）时，可通过 Webhook 或邮件发送告警。

- **历史状态趋势看板** 提供基于 SQLite 或 PostgreSQL 存储的时序数据，支持以折线图或柱状图展示每个链接在指定时间段内的可用率、平均响应时间，辅助判断目标服务的稳定性。

- **链接关系图谱可视化** 对于带有“关联域名”或“跳转链”标签的链接，支持生成力导向关系图，直观展示域名间的跳转逻辑与依赖层次，便于排查重定向链路异常。

- **导出与分享能力** 支持将当前链接集合及其最新状态导出为 CSV、Markdown 表格或 JSON 格式，方便嵌入周报、技术文档或与其他系统对接。

- **多用户只读视图** 内置简单的基于 Token 的只读访问机制，允许将看板分享给非技术同事或外部合作方，而无需暴露底层配置与修改接口。

## 应用场景

- **行业资源门户运营** 技术社区或行业协会运营人员可使用 HyperLink Atlas 维护成员单位官网、开源镜像站、标准文档库等链接集合，每日自动检测链接有效性，提前发现网站改版或证书过期问题，避免用户访问到无效入口。

- **数据采集管道前置巡检** 在数据采集任务启动前，通过本项目的探测接口批量检查目标数据源的可达性与响应速度，若发现异常则自动暂停任务并通知运维，减少因源站故障导致的采集失败与无效重试。

- **企业内部知识库链接维护** 大型企业的内部 Wiki 或知识管理系统中常包含大量外部参考链接，管理员可定期导出所有外部 URL 并导入 HyperLink Atlas，获得一份“链接健康报告”，据此批量更新或下线失效引用，提升知识库质量。

- **安全合规审计辅助** 安全团队可利用本项目定期扫描对外公开的文档站、API 网关地址，监控 SSL 证书有效期与域名解析是否被篡改，及时发现证书过期或 DNS 劫持风险，并输出合规性报表。

- **学术研究参考文献管理** 研究人员在整理论文或综述时，可将引用的所有在线资源链接统一托管至本项目，系统自动标注哪些链接已失效，辅助判断文献的可追溯性，避免因链接失效影响论文评审结果。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，需预先安装 Git 与 Python 3.10 及以上版本。

```bash
# 1. 克隆项目仓库
git clone https://github.com/example/hyperlink-atlas.git
cd hyperlink-atlas

# 2. 创建 Python 虚拟环境并安装依赖
python3 -m venv venv
source venv/bin/activate  # Windows 下使用 venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 初始化配置与本地数据库
cp conf/example.yaml conf/local.yaml
python atlas.py init --db sqlite:///data/atlas.db

# 4. 导入示例链接数据（或替换为自定义数据）
python atlas.py import --source data/sample_links.yaml

# 5. 启动 Web 看板与探测调度器（分别在不同终端或使用 nohup）
python atlas.py web --port 8080
python atlas.py scheduler --interval 3600  # 每小时执行一次探测
```

访问 http://localhost:8080 即可查看看板界面。如需部署至生产环境，建议将 `conf/local.yaml` 中的数据库连接改为 PostgreSQL，并配置反向代理（如 Nginx）。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 ~ 3.12 | 核心运行时，低于 3.10 不支持部分类型特性 |
| SQLite | 3.35 及以上 | 默认轻量级存储引擎，用于存放链接元数据与历史探测记录 |
| PostgreSQL | 12 及以上（可选） | 生产环境推荐使用，支持并发写入与更优的时序查询性能 |
| Redis | 6.2 及以上（可选） | 用于分布式部署场景下的任务队列与缓存，单机模式可不安装 |
| Node.js | 18 及以上（仅构建前端） | 仅当需要二次开发前端看板时需要，预编译版本无需安装 |
| Nginx | 1.20 及以上（生产可选） | 推荐用于反向代理、静态资源缓存与 HTTPS 终止 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user/quickstart.md | 如何安装、配置并首次运行项目；如何导入第一批链接 |
| 运维手册 | docs/ops/deployment.md | 如何配置 HTTPS、定时任务、日志轮转与数据库备份 |
| 开发参考 | docs/dev/api.md | 如何扩展自定义探测协议、如何编写插件、API 接口规范 |
| 数据模型 | docs/dev/schema.md | 数据库表结构、字段含义与索引设计，方便进行复杂查询与报表开发 |

## 资源列表

本项目文档与示例数据中涉及或引用的外部资源链接均列于下方，按类别分组。所有链接均保持用户提供的原始格式，未做任何修改。

**机构主站**

<code>yijiabifenc.org.cn</code>

<code>fajiabifenc.org.cn</code>

**直播数据源**

<code>yingchaobifenzhibo.org.cn</code>

<code>xijiabifenzhibo.org.cn</code>

<code>dejiabifenzhibo.org.cn</code>

<code>yijiabifenzhibo.org.cn</code>

<code>fajiabifenzhibo.org.cn</code>

## 项目结构

```text
hyperlink-atlas/
├── atlas.py                 # 命令行入口，整合 web / scheduler / import / init 等子命令
├── requirements.txt         # Python 依赖列表（FastAPI、uvicorn、apscheduler、sqlalchemy 等）
├── conf/                    # 配置文件目录
│   ├── example.yaml         # 完整参数示例，含探测策略、通知渠道、标签映射
│   └── logging.conf         # 日志格式与级别配置
├── core/                    # 核心逻辑模块
│   ├── engine.py            # 探测引擎，管理并发请求、超时与重试
│   ├── scheduler.py         # 定时调度封装，基于 APScheduler 实现
│   ├── notifier.py          # 通知模块，支持 Webhook 与 SMTP
│   └── storage.py           # 数据库抽象层，统一 SQLite / PostgreSQL 操作接口
├── web/                     # Web 看板后端与前端静态资源
│   ├── app.py               # FastAPI 应用主文件，定义 RESTful 接口
│   ├── dashboard/           # 前端静态资源（预编译 Vue 3 构建产物）
│   │   ├── index.html
│   │   └── assets/
│   └── templates/           # 用于导出报告的服务端模板（Jinja2）
├── data/                    # 数据存储目录（默认存放 SQLite 文件与导入样例）
│   ├── sample_links.yaml    # 示例链接数据，包含 20 个测试域名
│   └── atlas.db             # 默认 SQLite 数据库文件（首次初始化生成）
├── tests/                   # 单元测试与集成测试
│   ├── test_engine.py
│   ├── test_scheduler.py
│   └── fixtures/            # 测试用的模拟响应数据
├── scripts/                 # 辅助运维脚本
│   ├── backup_db.sh         # 数据库备份脚本（配合 crontab 使用）
│   └── migrate_pg.sh        # 从 SQLite 迁移至 PostgreSQL 的辅助脚本
└── docs/                    # 完整文档目录（对应文档导航章节）
    ├── user/
    ├── ops/
    └── dev/
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于提交 Issue、改进文档、增加探测协议支持、优化前端界面或完善测试用例。

1. 在 GitHub 上 Fork 本仓库，并克隆至本地开发环境。确保本地 Python 版本与安装要求一致，建议使用 pre-commit 钩子以保持代码风格统一。

2. 创建新的特性分支，分支命名建议采用 `feature/简短描述` 或 `fix/问题编号` 格式。在开发前，请阅读 `docs/dev/architecture.md` 了解模块划分与依赖方向。

3. 编写或修改代码后，请确保所有现有单元测试通过，并为新增功能补充对应的测试用例（位于 `tests/` 目录）。运行 `pytest --cov=core --cov=web` 检查测试覆盖率，新增代码覆盖率不应低于 80%。

4. 更新相关文档，包括但不限于 `README.md` 中的功能说明、`docs/user/` 下的使用指南以及 `conf/example.yaml` 中的新增配置项注释。

5. 提交 Pull Request 到主仓库的 `main` 分支，并在 PR 描述中清晰说明改动目的、测试结果以及与现有功能的兼容性。PR 中会触发 CI 流水线进行自动构建与测试，审核通过后即合并。

## 常见问题

**问：探测目标网站是否会对其造成压力？如何控制请求频率？**  
答：本项目默认采用单线程顺序探测，且每个目标之间强制间隔至少 500 毫秒。用户可在 `conf/local.yaml` 中调整 `probe.interval` 与 `probe.concurrent` 参数，但建议并发数不超过 5，以免被目标服务端限流或封禁。对于高频访问需求，建议提前与目标站点沟通或使用缓存响应。

**问：支持 IPv6 域名或非标准端口吗？**  
答：支持。在导入链接时，可以按 `http://[2001:db8::1]:8080/path` 格式填写完整 URL。探测引擎基于 Python 标准库 `urllib3`，兼容 IPv6 与自定义端口。若目标站点仅支持 HTTPS 但证书为自签名，可在配置中关闭 SSL 验证（不推荐生产环境使用）。

**问：如何将现有书签或浏览器收藏夹批量导入？**  
答：项目提供了 `scripts/import_bookmark.py` 辅助脚本，支持解析 Chrome / Firefox 导出的 HTML 书签文件，自动提取标题与 URL，并生成符合导入格式的 YAML 文件。用户也可按照 `data/sample_links.yaml` 的格式手写或使用 Excel 转换工具批量生成。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
