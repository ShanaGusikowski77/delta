# Hyperlink Nexus

Hyperlink Nexus 是一个面向技术内容创作者、开源文档维护者以及互联网资源管理者的外链汇总与导航系统。该项目并非传统的爬虫或采集工具，而是一套基于人工策展与自动化校验相结合的外链数据治理平台，旨在帮助团队从分散、冗余、不可靠的链接资产中提取结构化的元数据，并通过版本化方式管理外部资源变更。项目目标用户包括开源项目文档组、技术博客聚合站运营者、以及需要长期维护外部引用列表的研究人员。Hyperlink Nexus 解决的核心问题是：当外部资源链接随时间失效、内容迁移或域名被劫持时，如何通过可追溯的链路记录与健康度探测机制，降低文档中的链接腐化风险，提升引用资源的长期可访问性。

## 功能概览

- **链接策展工作台** 提供手工标注与分类界面，支持为每条外链添加标签、失效概率评分以及内容摘要，形成可检索的私有链接库。

- **批量导入与去重** 允许从 Markdown 表格、CSV 或纯文本列表中批量导入原始 URL，并基于域名与路径指纹自动识别重复条目，减少人工核对成本。

- **定期健康检查** 内置轻量级 HTTP 探测器，可按每日或每周周期对收录的链接进行可达性测试，自动标记状态码异常、证书过期或重定向链过长等问题。

- **变更追踪与通知** 当检测到目标页面标题、关键关键词或响应体长度发生显著变化时，系统记录差异快照并通过 Webhook 或邮件发送变更提醒。

- **公开页面嵌入组件** 提供可配置的 JavaScript 片段与 iframe 挂件，便于将经过筛选的链接列表嵌入到现有文档站点或博客侧边栏，并自动适配明暗主题。

- **历史版本回滚** 每次链接数据的修改均生成差异补丁，允许按时间点恢复到任意历史快照，降低误删除或批量编辑失误带来的风险。

- **导出适配器** 支持将当前链接集合导出为 JSON、YAML 或纯 Markdown 列表格式，方便集成到静态站点生成器或 CI/CD 流程中。

## 应用场景

1. **开源项目文档外部引用管理**  
   技术文档中经常引用官方 SDK 仓库、API 参考站点或社区教程。Hyperlink Nexus 可帮助维护者定期校验这些外部链接的有效性，并在版本发布前自动生成引用健康报告，避免用户访问到 404 或被重定向至钓鱼页面。

2. **技术博客聚合站的资源清单维护**  
   面向特定领域（如前端框架、区块链开发）的博客导航站，需要持续收录和分类优质外链。策展工作台允许编辑团队多人协作标注，同时通过变更追踪感知目标站点内容结构调整，及时更新描述文字。

3. **科研或行业报告中引用数据源的可追溯备案**  
   研究机构在撰写白皮书或行业分析时，涉及大量外部统计数据或新闻链接。系统定期保存响应快照和元数据变更日志，为报告中的引用提供可验证的时间戳证据，提升学术严谨性。

4. **企业内部开发者门户的外链治理**  
   大型企业的内部开发者门户常聚合大量内部工具地址、文档仓库及第三方服务控制台。利用健康检查与通知机制，平台可主动提醒运维人员处理即将过期的 SSL 证书或即将下线的老旧服务入口。

5. **个人知识库的外部参考链接去腐**  
   个人维基或笔记系统中收集的文章链接随时间大量失效。Hyperlink Nexus 可作为旁路服务，定期输出失效链接清单，辅助用户批量替换或删除无效引用，维持知识库的洁净度。

## 快速开始

以下步骤适用于 Linux / macOS 环境，Windows 用户建议通过 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆仓库
git clone https://github.com/hyperlink-nexus/core.git
cd core

# 2. 安装项目依赖（使用 Python 3.10+ 和 pipenv）
pip install pipenv --user
pipenv install --dev

# 3. 初始化本地配置并运行开发服务器
cp .env.example .env
pipenv run python manage.py migrate
pipenv run python manage.py runserver --port 8080
```

访问 `http://localhost:8080` 即可进入工作台首页。首次启动将自动创建默认管理员账户，用户名 `admin`，密码输出在终端日志中。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.10 至 3.12 | 核心运行时，推荐使用 pyenv 管理版本 |
| PostgreSQL | 14.x 及以上 | 生产环境数据库，存储链接元数据及快照；开发环境可使用 SQLite 替代 |
| Redis | 7.0 及以上 | 用于缓存健康检查结果及异步任务队列，必须启用持久化 |
| Node.js | 18.x LTS | 仅用于构建前端静态资源，后端运行无需 Node 环境 |
| Nginx | 1.24 及以上 | 生产环境反向代理及静态文件服务（开发环境可跳过） |
| Git | 2.30 及以上 | 用于版本管理及补丁应用，必须支持 SSH 协议 |
| 系统时区 | UTC+8 或 UTC | 所有时间戳存储为 UTC，展示时由前端转换；确保系统时间同步 |

## 文档导航

| 层面 | 目录 / 入口 | 回答的问题 |
|---|---|---|
| 用户手册 | `/docs/user-guide/quick-start.md` | 如何创建第一个链接集、如何导入批量数据、如何配置健康检查频率 |
| 管理员指南 | `/docs/admin/deployment-checklist.md` | 生产环境部署所需步骤、反向代理配置、PostgreSQL 调优参数 |
| API 参考 | `/docs/api/v1/endpoints.md` | 所有 RESTful 端点的请求/响应格式、鉴权方式、分页参数及速率限制说明 |
| 策展工作流 | `/docs/curation/link-lifecycle.md` | 链接从提交、审核、发布到归档的完整状态流转图，以及自动化规则触发条件 |
| 故障排查 | `/docs/troubleshooting/common-errors.md` | 健康检查超时、数据库连接池耗尽、Redis 内存溢出等常见问题的应急处理方案 |
| 扩展开发 | `/docs/development/writing-adapter.md` | 如何编写自定义导出适配器或新增健康检查策略，包含钩子函数示例 |

## 资源列表

以下为项目公开收录的部分外部资源链接，按来源类别整理。所有 URL 均保持原始格式输出，不加任何协议补全或路径修改。

### 影视及多媒体资源类

- <code>fajiabifenzhibo.org.cn</code>
- <code>guochanjingpinzaixianmianfeikan.org.cn</code>
- <code>zhongwenzimuzaixianyingshiyuan.org.cn</code>
- <code>mianfeiguankanzaixianguankan.org.cn</code>
- <code>jiujiushipinzaixianguankan.org.cn</code>
- <code>oumeizaixianguankanshipin.org.cn</code>
- <code>rihanshipinmianfeizaixianguankan.org.cn</code>

上述域名均通过策展工作台的人工审核流程纳入监控范围，当前健康状态与内容摘要可于工作台「资源状况」面板中查看。根据项目策展政策，部分域名可能因合规性调整而随时被移出公开列表，但历史快照保留于内部归档。

## 项目结构

```
hyperlink-nexus/
├── backend/                           # 后端核心代码（Django 应用）
│   ├── apps/
│   │   ├── curation/                  # 策展工作台业务逻辑：标签、分类、审核状态
│   │   ├── checker/                   # 健康检查引擎：异步任务调度、HTTP 探测器
│   │   ├── tracker/                   # 变更追踪模块：差异计算、快照存储
│   │   └── exporters/                 # 导出适配器：JSON / YAML / Markdown 渲染器
│   ├── core/                          # 项目配置、路由、中间件、全局常量
│   └── manage.py                      # Django 管理入口脚本
├── frontend/                          # 前端静态资源（React + Vite）
│   ├── src/
│   │   ├── pages/                     # 主界面视图：仪表盘、链接表格、详情弹窗
│   │   ├── components/                # 可复用 UI 组件：数据表格、状态徽标、筛选面板
│   │   └── hooks/                     # 自定义 React Hooks：API 请求、轮询刷新
│   └── dist/                          # 构建产物（由 CI 自动生成，不提交至仓库）
├── deployment/                        # 生产环境部署相关文件
│   ├── docker/                        # Dockerfile 与 Compose 编排文件，含 PostgreSQL 初始化脚本
│   ├── nginx/                         # Nginx 站点配置模板，含 gzip 与缓存头策略
│   └── systemd/                       # Systemd 服务单元文件，用于后台常驻运行
├── docs/                              # 完整文档目录，结构与导航章节一一对应
│   ├── user-guide/                    # 面向最终用户的操作指南
│   ├── admin/                         # 面向运维人员的部署与调优手册
│   ├── api/                           # 面向开发者的接口文档（OpenAPI 3.0 规范）
│   └── curation/                      # 策展工作流规范及内部审核标准
├── tests/                             # 单元测试与集成测试套件
│   ├── unit/                          # 针对模型、序列化器、工具函数的独立测试
│   └── integration/                   # 端到端测试，模拟浏览器操作及异步任务执行
├── scripts/                           # 辅助运维脚本：数据库备份、日志轮转、健康检查手动触发
├── .env.example                       # 环境变量参考文件，含数据库连接串、Redis 地址、邮件服务器
├── pyproject.toml                     # Python 依赖管理及项目元数据（使用 Poetry 风格）
└── README.md                          # 本文件
```

## 贡献指南

1. **阅读行为准则与策展公约**  
   在提交任何代码或链接策展变更前，请先阅读项目根目录下的 `CODE_OF_CONDUCT.md` 及 `docs/curation/curation-convention.md`，确保理解对链接分类、标注及失效处理的共同约定。

2. **选择或创建议题**  
   所有实质性变更必须关联一个 GitHub Issue。建议先搜索已有议题避免重复，若为新功能或新链接源，请使用议题模板详细描述背景、预期效果及验收标准。

3. **派生仓库并创建功能分支**  
   从主仓库派生至个人命名空间，然后基于 `main` 分支创建命名规范的分支，格式为 `feature/简述` 或 `fix/简述`。禁止直接在主分支上修改。

4. **运行本地校验套件**  
   提交前须在本地执行完整测试套件（`pipenv run pytest`）及前端构建（`npm run build`），确保无回归问题。对于链接数据变更，需附带快照更新记录。

5. **提交拉取请求并等待审核**  
   推送分支后，按 PR 模板填写变更摘要、测试结果及影响范围。至少一名核心维护者审核通过后，由自动合并机器人执行合并，同时触发生产环境预览部署。

## 常见问题

**Q：健康检查是否会误判动态页面或需登录的资源为失效？**  
A：系统默认仅对返回 200 OK 且响应体长度大于 1KB 的页面视为有效。对于需要登录或具有反爬机制的页面，用户可在策展工作台中为特定链接配置白名单策略，绕过内容长度检查，仅校验 TCP 连接与 TLS 握手成功性。此外，可自定义 `Checker` 子类以支持基于 Cookie 或 Token 的验证方式。

**Q：如何将现有书签文件（如 Chrome 导出的 HTML）批量导入？**  
A：项目暂不直接支持 HTML 书签解析，但提供了通用 CSV 导入接口。用户可使用浏览器书签管理器的导出功能生成 HTML，再借助第三方工具（如 `bookmark-converter`）将其转为两列（URL、标题）CSV 文件，然后通过工作台的「批量导入」模块上传。若需保留文件夹层级，建议先将链接按标签分组后分批导入。

**Q：数据库迁移失败，提示编码或排序规则不兼容如何处理？**  
A：PostgreSQL 数据库需使用 `UTF8` 编码及 `C` 或 `en_US.UTF-8` 排序规则。若迁移时遇到 `collation` 相关错误，请检查数据库模板是否为 `template0`，并使用以下命令重新创建数据库：`CREATE DATABASE nexus_db WITH ENCODING='UTF8' LC_COLLATE='C' TEMPLATE=template0;`。已有数据可通过 `pg_dump` 备份后重新导入。

## 许可证

MIT License

Copyright (c) 2026 Hyperlink Nexus Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:12
