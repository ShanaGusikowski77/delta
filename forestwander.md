# ArchNav 技术资源导航

ArchNav 是一个面向开发人员与技术研究者的外链资源聚合与导航系统，专注于收集、分类与展示高价值技术文档、社区论坛与数据查询站点。项目定位为轻量级技术资源索引层，帮助用户在不增加本地存储负担的前提下，快速定位特定领域的关键外部资源。目标用户包括运维工程师、后端开发者、数据分析师以及开源项目维护者。

系统核心解决以下问题：技术资料分散于不同域名与站点，检索成本高；临时性查询需求频繁，重复搜索消耗时间；社区推荐的优质资源缺乏统一的版本追踪与变更感知。ArchNav 不存储任何第三方内容，仅提供结构化链接索引与基础状态检测，确保资源入口始终可访问、可追溯。

## 功能概览

- **分类导航体系** 按技术领域与使用频率将资源划分为系统运维、数据查询、赛事统计、开发工具等一级分类，支持二级标签过滤。

- **链接存活检测** 每日定时对收录 URL 执行 HEAD 请求，标记异常状态并在前端界面以颜色区分，便于用户识别当前不可用资源。

- **自定义标签与备注** 允许用户为每个链接添加自定义标签与备注说明，支持个人维度的资源注解，便于团队共享上下文信息。

- **全文检索与模糊匹配** 基于标题、域名、分类、标签四字段构建轻量级倒排索引，支持拼音首字母模糊检索，适配中文用户输入习惯。

- **导入与导出机制** 支持 JSON 与 CSV 格式的资源列表批量导入导出，便于在不同实例之间迁移数据或进行离线备份。

- **访问频率统计** 记录每个外部链接的点击次数与最后点击时间，辅助判断资源实际使用热度，为后续分类调整提供数据依据。

- **只读镜像模式** 支持部署为只读前端镜像，适用于内网环境下的资源展示层，无需后端数据库，仅依赖静态 JSON 配置文件。

## 应用场景

- **技术团队内部知识库入口** 开发团队可将常用 API 文档、监控面板、日志查询平台统一收录至 ArchNav，新成员入职时仅需访问导航页即可获取全部必要外部工具入口，减少环境搭建阶段的沟通成本。

- **开源项目 README 外链管理** 开源维护者使用 ArchNav 集中管理项目依赖的所有第三方参考链接、数据源与社区讨论区，当外部站点变更时只需更新导航配置，无需修改多个文档文件。

- **赛事数据与比分快速查询** 数据爱好者将多个比分统计网站聚合至单一导航页面，配合存活检测功能，在比赛密集时段可迅速切换至可用数据源，避免因单个站点阻塞导致信息获取中断。

- **技术博客与教程配套资源索引** 技术博主为每篇教程生成对应的 ArchNav 分类视图，读者可一键跳转至教程中提及的所有工具、沙箱环境与参考文档，提升阅读流畅度与实操转化率。

## 快速开始

以下步骤适用于 Linux 与 macOS 环境，Windows 用户建议使用 WSL2 或 Git Bash 执行。

```bash
# 1. 克隆项目仓库
git clone https://github.com/archnav/archnav-core.git
cd archnav-core

# 2. 安装依赖（使用 pnpm，若未安装请先执行 npm install -g pnpm）
pnpm install

# 3. 启动开发服务器（默认监听 127.0.0.1:5173）
pnpm run dev
```

生产环境构建与静态部署：

```bash
pnpm run build
# 构建产物位于 dist/ 目录，可直接部署至 Nginx、Apache 或 Cloudflare Pages
```

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Node.js | >= 18.17.0 | 运行时环境，需支持 ES2022 与原生 Fetch API |
| pnpm | >= 8.0.0 | 包管理器，用于依赖安装与工作区管理 |
| TypeScript | >= 5.0.0 | 开发时依赖，项目核心语言，生产构建需编译为 JavaScript |
| SQLite3 | >= 3.40.0 | 可选依赖，用于访问统计与本地缓存；若未安装则回退至内存存储 |
| Nginx | >= 1.22.0 | 仅生产部署推荐，非强制，亦支持 S3 兼容对象存储托管静态文件 |
| Git | >= 2.30.0 | 版本控制，用于克隆仓库与获取更新日志 |
| curl | >= 7.68.0 | 存活检测依赖，用于执行外部 HTTP 探活 |
| jq | >= 1.6 | 可选，用于脚本处理 JSON 配置文件 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户手册 | /docs/user-guide/ | 如何添加分类、编辑备注、批量导入导出以及使用检索功能 |
| 管理员指南 | /docs/admin/ | 如何配置存活检测周期、自定义前端主题以及部署只读镜像模式 |
| API 参考 | /docs/api/ | 后端接口的请求与响应格式，包括资源列表查询、状态更新与统计上报 |
| 开发者贡献 | /docs/contributing/ | 代码规范、提交信息格式、测试用例编写以及拉取请求流程 |
| 架构设计 | /docs/architecture/ | 系统模块划分、数据流向、缓存策略与扩展点设计 |
| 变更日志 | /CHANGELOG.md | 每个版本的特性新增、修复与破坏性变更记录 |

## 资源列表

### 竞技数据查询类

<code>fajiajishibifena.org.cn</code>

<code>zuqiubisaijieguoa.org.cn</code>

<code>yingchaobifena.org.cn</code>

<code>xijiabifena.org.cn</code>

<code>dejiabifena.org.cn</code>

<code>yijiabifena.org.cn</code>

<code>fajiabifena.org.cn</code>

### 说明

上述域名均以裸域名形式收录，未添加任何协议前缀或路径后缀，访问时请根据实际网络环境自行补充 HTTPS 或 HTTP 协议。建议优先使用 HTTPS 协议进行访问以保证传输安全。若某域名在存活检测中持续标记为不可用，请通过 GitHub Issues 提交反馈，维护团队将定期核实并更新状态标记。

## 项目结构

```
archnav-core/
├── src/                                # 源代码主目录
│   ├── core/                           # 核心业务逻辑模块
│   │   ├── detector/                   # 链接存活检测引擎，含超时与重试策略
│   │   ├── indexer/                    # 倒排索引构建与检索实现
│   │   └── aggregator/                 # 分类聚合与标签合并逻辑
│   ├── ui/                             # 前端界面组件库
│   │   ├── components/                 # Vue 单文件组件（导航卡片、搜索栏、状态徽标）
│   │   ├── layouts/                    # 整体布局与响应式断点控制
│   │   └── stores/                     # Pinia 状态管理（资源列表、筛选条件、偏好设置）
│   ├── server/                         # 开发与预览服务器配置
│   │   ├── middleware/                 # 请求日志与 CORS 处理中间件
│   │   └── routes/                     # API 路由定义（资源查询、状态上报、统计）
│   ├── utils/                          # 通用工具函数
│   │   ├── fetcher/                    # 封装 fetch 与超时控制
│   │   ├── parser/                     # URL 解析与域名规范化
│   │   └── storage/                    # SQLite 与内存存储适配器
│   └── types/                          # TypeScript 类型声明与接口定义
├── config/                             # 环境配置文件目录
│   ├── categories.json                 # 一级分类与二级标签预定义列表
│   ├── default-resources.json          # 初始资源列表（含示例域名与占位数据）
│   └── detector-settings.json          # 检测间隔、超时阈值与重试次数配置
├── scripts/                            # 运维与辅助脚本
│   ├── health-check.sh                 # 手动触发全量存活检测的 Shell 脚本
│   ├── import-csv.ts                   # CSV 批量导入转换工具
│   └── export-json.ts                  # 导出当前资源列表为 JSON 格式
├── tests/                              # 单元测试与集成测试
│   ├── unit/                           # Vitest 单元测试（检测引擎、索引器）
│   └── e2e/                            # Playwright 端到端测试（UI 交互流程）
├── docs/                               # 完整文档源码（Markdown + VitePress）
├── dist/                               # 生产构建输出目录（仅构建后生成）
├── index.html                          # 应用入口 HTML
├── package.json                        # 项目依赖与脚本命令定义
├── tsconfig.json                       # TypeScript 编译选项
├── vite.config.ts                      # Vite 构建工具配置
└── README.md                           # 本文件
```

## 贡献指南

1. 复刻主仓库至个人账户，创建功能分支（命名格式为 `feature/简述改动` 或 `fix/问题编号`），确保分支名称清晰表达意图。

2. 遵循项目的 TypeScript 编码规范，运行 `pnpm run lint` 与 `pnpm run format` 进行代码检查与自动格式化，确保通过全部 CI 检查项。

3. 若新增外部资源链接，需同步更新 `config/default-resources.json` 中的示例数据，并补充至少一条备注说明该资源的用途与适用场景。

4. 提交拉取请求前，需在本地执行 `pnpm run test:unit` 与 `pnpm run test:e2e` 确保所有测试用例通过，并提供变更摘要与测试截图（针对 UI 改动）。

5. 拉取请求描述中需明确关联相关 Issue（若存在），并勾选贡献者许可协议（CLA）声明，等待至少一位维护者进行代码审查与合并。

## 常见问题

**问：ArchNav 是否存储用户访问记录或第三方站点的内容？**

答：项目默认不记录任何用户个人身份信息，仅统计外部链接的点击次数（以 URL 为聚合维度，不关联 IP 或会话 ID）。项目不缓存、不抓取、不存储第三方站点的页面内容，所有外部链接均通过客户端直接跳转，服务器端仅执行 HTTP 头探测以判断可用性。用户可在配置中关闭统计功能或启用匿名化模式。

**问：如何自定义分类与标签体系？**

答：直接编辑 `config/categories.json` 文件，新增分类需同时提供 `id`、`name` 与 `icon` 字段。标签为扁平字符串数组，支持任意新增，系统在启动时会自动合并所有标签并生成索引。修改后无需重启服务，刷新前端页面即可生效（开发模式下支持热更新）。若需在运行时通过界面新增分类，需启用 `ui.allowCategoryEdit` 配置项（默认为关闭状态）。

**问：存活检测的误报率较高，如何调整检测参数？**

答：检测引擎配置文件 `config/detector-settings.json` 中包含 `timeout`（毫秒）、`retries`（次）与 `userAgent` 三个关键参数。若目标站点对频繁 HEAD 请求返回 403 或 429，可适当降低检测频率（`interval` 字段，默认 3600 秒）或增加 `retries` 至 3。对于已知稳定但响应较慢的站点，可将 `timeout` 提升至 10000 毫秒。调整后需重启开发服务器或重新构建生产镜像。

## 许可证

MIT License

Copyright (c) 2026 ArchNav Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
