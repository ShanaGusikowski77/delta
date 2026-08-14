# LinkPulse Resource Aggregator

LinkPulse 是一个面向技术内容创作者与数字媒体研究者的外链资源汇总与状态监控工具。该项目定位于解决分散在网络各处的视频直播、主播内容及多媒体资源链接的收集、有效性校验与分类管理问题，尤其适用于需要定期追踪大量外部内容链接可用性的场景。通过提供结构化的链接入库、批量状态检查与基础访问统计能力，LinkPulse 帮助用户从繁杂的链接维护工作中解脱出来，将精力聚焦于内容本身的分析与再创作。

项目当前处于活跃维护状态，核心功能围绕链接资源的全生命周期管理展开，涵盖从原始 URL 导入、自动分类打标、周期性可用性探测到访问日志记录等环节。它不直接存储或代理任何外部内容，仅作为链接元数据的索引层与状态观测层，因此可安全部署于各类内网或公网环境中，作为数据中台的一个轻量化外围组件。

## 功能概览

- **批量链接导入与解析**：支持通过文本文件、CSV 或直接粘贴方式批量导入 URL，自动解析协议头、域名及路径层级，提取有效域名与顶级后缀。

- **自动分类与标签体系**：基于域名关键词及路径模式，对导入链接自动划分至预设类别（如视频平台、直播站点、短链服务等），并允许用户自定义标签规则。

- **周期可用性探测**：内置异步 HTTP/HTTPS 探测引擎，可配置探测间隔（分钟/小时/天级），记录每次探测的响应码、响应时间及返回内容哈希，用于判断链接是否存活及内容是否变更。

- **状态变更告警**：当链接从可达变为不可达，或响应时间超出设定阈值时，通过 Webhook 或邮件方式发送通知，便于及时跟进处理失效资源。

- **访问统计与趋势视图**：以日历热力图和折线图方式展示链接的整体可用率变化趋势，支持按标签、域名或时间段筛选，辅助判断外部资源稳定性。

- **数据导出与快照**：支持将链接清单及最近一次探测结果导出为 JSON、CSV 或 Markdown 表格格式，便于离线归档或嵌入其他文档系统。

## 应用场景

- **内容聚合站点运维**：对于运营技术资讯聚合站或导航站的团队，可使用 LinkPulse 定时校验站内引用的所有外部链接，自动生成失效链接报告，避免用户点击后遇到 404 页面，提升站点信誉度。

- **数字媒体研究数据准备**：研究者需要长期观察一批直播或视频类域名的可访问性变化，以分析网络服务稳定性或区域访问差异。LinkPulse 可配置为每 30 分钟探测一次，持续收集时序数据，为后续分析提供原始素材。

- **内部文档系统链接治理**：企业内部 Wiki 或知识库中常包含大量历史引用链接，随着时间推移多数已失效。通过 LinkPulse 进行一次性全量扫描，可获得清晰的失效清单，指导文档维护人员进行针对性更新。

- **CDN 或域名迁移验证**：在切换 CDN 服务商或变更域名解析后，使用 LinkPulse 对迁移前后的链接集合进行对比探测，快速验证新链路的可用性与响应性能是否符合预期。

## 快速开始

以下步骤适用于 Linux/macOS 环境，Windows 用户可使用 WSL 或 Git Bash 配合执行。

```bash
# 1. 克隆代码仓库
git clone https://github.com/linkpulse/linkpulse-core.git
cd linkpulse-core

# 2. 安装 Python 依赖（建议使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. 初始化本地数据库（SQLite）
python manage.py migrate

# 4. 从示例文件导入首批链接
python manage.py import --file samples/links_initial.txt

# 5. 启动探测工作器（后台运行）
nohup python worker.py --interval 60 > logs/worker.log 2>&1 &

# 6. 启动 Web 仪表板（开发模式）
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 `http://localhost:8080/dashboard` 可查看实时汇总状态。生产环境部署建议配合 Gunicorn + Nginx。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 及以上 | 核心运行时，推荐 3.11 以获得性能优化 |
| SQLite | 3.35 及以上 | 默认元数据存储引擎，支持 JSON 字段操作 |
| Redis | 6.0 及以上 | 可选，用于分布式探测任务队列及缓存（单机模式可禁用） |
| curl | 7.68 及以上 | 用于备选探测通道（当 Python urllib 出现异常时降级） |
| tzdata | 2023c 及以上 | 时区数据包，确保探测时间戳记录准确 |
| psutil | 5.9.0 及以上 | 用于监控工作器进程资源占用，辅助自动扩缩容判断 |

若使用 PostgreSQL 作为生产数据库，需额外安装 psycopg2-binary 库，版本要求 2.9.5 及以上。Redis 非强制，但若启动多工作器实例，建议配置以共享任务锁状态。

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | docs/getting-started.md | 如何从零开始部署并添加第一批链接？首次探测策略如何设置？ |
| 配置参考 | docs/configuration.md | 所有环境变量与配置文件字段的含义、默认值及合法取值范围是什么？ |
| API 手册 | docs/api-reference.md | 提供哪些 RESTful 接口用于链接增删改查、探测结果查询及标签管理？ |
| 运维调优 | docs/operations-tuning.md | 当链接数量超过 10 万条时，如何调整数据库索引、工作器并发数与内存参数？ |

额外的高级主题文档（如自定义探测脚本编写、Prometheus 指标暴露）存放于 `docs/advanced/` 目录下，可根据实际需求选择性阅读。

## 资源列表

以下为当前项目维护或参与合作的外部资源导航，按类别分组陈列。所有链接均来自用户原始数据，未做任何格式或协议修正。

类别：视频直播与主播内容

- <code>nvzhubozshipinzaixianguankan.org.cn</code>
- <code>xingganmeinvzhibotiaowu.org.cn</code>
- <code>hanguomeinvzhuborewu.org.cn</code>
- <code>zaixianbofangzhubo.org.cn</code>
- <code>zhubozhibozaixianguankan.org.cn</code>
- <code>wanghongzhibozaixianshipinw.org.cn</code>
- <code>wanghongfulizhibow.org.cn</code>

上述资源链接由社区成员提交，LinkPulse 项目仅对其进行技术层面的可用性追踪与状态记录，不涉及任何内容审核、推荐或背书。用户在使用这些链接时，应自行遵守相关网站的服务条款及所在地区的法律法规。

## 项目结构

```
linkpulse-core/
├── app/                                # 主应用模块
│   ├── api/                            # RESTful API 路由与视图
│   │   ├── v1/                         # API v1 版本实现
│   │   │   ├── links.py                # 链接 CRUD 接口
│   │   │   └── probes.py               # 探测结果查询接口
│   │   └── middleware/                 # 认证与限流中间件
│   ├── core/                           # 核心业务逻辑
│   │   ├── classifier.py               # 自动分类引擎（基于规则与正则）
│   │   ├── probe_engine.py             # 异步探测调度与结果聚合
│   │   └── stats_calculator.py         # 可用率、响应分位数统计
│   ├── models/                         # 数据模型定义（SQLAlchemy ORM）
│   │   ├── link.py                     # 链接表（url, tags, status, last_probe_at）
│   │   ├── probe_record.py             # 探测记录表（timestamp, status_code, latency）
│   │   └── label.py                    # 标签表与链接-标签关联
│   ├── worker/                         # 后台工作器进程入口
│   │   ├── scheduler.py                # 基于 APScheduler 的定时任务编排
│   │   └── task_queue.py               # Redis RQ 任务封装（可选）
│   └── utils/                          # 通用工具函数集合
│       ├── http_client.py              # 带重试与超时控制的 HTTP 请求封装
│       ├── validators.py               # URL 格式校验与域名归一化
│       └── logger.py                   # 结构化日志配置（JSON 格式输出）
├── config/                             # 环境配置文件
│   ├── development.py                  # 开发环境参数（DEBUG=True，SQLite）
│   ├── production.py                   # 生产环境参数（PostgreSQL，Redis 启用）
│   └── staging.py                      # 预发布环境参数（镜像生产，日志级别调高）
├── docs/                               # 完整文档源文件（Markdown）
│   ├── getting-started.md
│   ├── configuration.md
│   ├── api-reference.md
│   └── operations-tuning.md
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # 针对 classifier、validators 的隔离测试
│   ├── integration/                    # 数据库与探测引擎的真实环境测试
│   └── fixtures/                       # 测试用样本数据（链接列表、探测响应 mock）
├── scripts/                            # 运维与部署辅助脚本
│   ├── backup_db.sh                    # 数据库定期备份（配合 crontab）
│   └── migrate_legacy.py               # 从旧版 CSV 格式导入数据的迁移工具
├── requirements.txt                    # 生产环境 Python 依赖列表（固定版本）
├── requirements-dev.txt                # 开发测试额外依赖（pytest, black, mypy）
├── manage.py                           # CLI 管理入口（import, probe, export 命令）
├── worker.py                           # 独立工作器进程启动脚本
└── README.md                           # 本文档
```

目录结构遵循分层架构原则：`app/` 存放业务逻辑与接口，`config/` 与环境解耦，`tests/` 保证质量，`scripts/` 简化运维。新增功能模块时，建议按领域放置在 `app/core/` 下的对应子文件中，并同步更新单元测试。

## 贡献指南

1. 在 GitHub 上 Fork 本仓库至个人账户，然后 clone 到本地开发环境。请确保使用 Python 3.11 及以上版本，并创建独立的虚拟环境。

2. 选择 `docs/` 目录下未完成或标注为 `[WIP]` 的文档任务，或查看 `issues` 中标记为 `help-wanted` 的开发任务。提交前需运行 `pytest tests/` 确保所有现有测试用例通过，并为新增代码编写对应测试。

3. 代码风格需遵循 PEP 8 规范，函数与方法必须包含 docstring（采用 Google 风格），类型注解需完整，通过 `mypy --strict` 静态检查。

4. 提交信息使用约定式提交格式（`feat:`、`fix:`、`docs:`、`refactor:` 等），且主体内容不超过 72 字符。发起 Pull Request 时，请清晰描述变更动机、实现方式及可能影响范围。

5. 若计划引入新的第三方依赖，需在 `requirements.txt` 中固定版本号，并在 `docs/configuration.md` 中补充相关环境变量说明。大型功能变更建议先创建 Discussion 议题与维护组沟通设计思路，避免重复劳动。

## 常见问题

**Q：探测链接时是否会被目标站点屏蔽？**

LinkPulse 默认使用 `User-Agent: LinkPulseBot/1.0 (+https://linkpulse.io/bot)`，且探测间隔默认不低于 5 分钟。但部分站点可能对频繁请求敏感，建议在 `config/production.py` 中调整 `REQUEST_DELAY` 参数（单位秒），并配置 `ROTATE_USER_AGENT` 为 True 以轮换 UA。若仍需避免干扰，可启用 `--head-only` 模式仅发送 HEAD 请求，减少带宽消耗。

**Q：如何迁移现有的大量链接数据？**

提供两种路径：第一，使用 `manage.py import --csv legacy_links.csv` 导入 CSV 文件，要求列顺序为 `url,tags,notes`；第二，编写简单的 Python 脚本调用 `app/api/v1/links.py` 中的 `batch_create` 函数，以 JSON 数组方式批量提交。迁移前建议先在 staging 环境试运行，并利用 `--dry-run` 参数预览解析结果而不实际写入数据库。

**Q：Web 仪表板加载缓慢或超时怎么办？**

通常是因为链接总数超过 5 万条且未启用分页优化。请检查 `config/development.py` 中的 `PAGE_SIZE` 默认值（建议设为 50），并在前端请求中加入 `limit` 参数。若后端数据库为 SQLite，可切换至 PostgreSQL 并创建 `idx_link_status` 与 `idx_probe_timestamp` 索引。此外，可关闭 `STATS_REALTIME` 开关，改为每小时计算缓存统计值，减少实时聚合压力。

## 许可证

MIT License

Copyright (c) 2026 LinkPulse Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
