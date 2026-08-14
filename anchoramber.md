# Hyperlink Resource Aggregation Platform (HRAP)

Hyperlink Resource Aggregation Platform (HRAP) 是一个面向技术文档编写者、开源项目维护者以及网站管理员的轻量级外链资源汇总与导航系统。该项目定位为技术资源的中转枢纽，帮助用户将分散在多个域名的参考资料、分支文档、技术规范等外部链接进行集中化管理和分类展示，从而降低信息检索成本，提升项目文档的可维护性与可读性。

HRAP 并非传统意义上的爬虫或搜索引擎，而是一个基于静态配置的外链编排引擎。它通过结构化的数据配置文件，将大量原始 URL 按照业务场景、技术层级或文档阶段进行分组渲染，最终生成清晰的外链导航页面或嵌入式组件。目标用户包括需要维护大量外部引用文档的技术作者、需要管理多版本分支说明的发布协调员，以及需要对外展示技术生态图谱的开源社区运营者。HRAP 通过规则化的展示逻辑，解决了外链散落、描述缺失、分类混乱、更新滞后等常见痛点，使得外部资源引用变得规范、透明且易于审计。

## 功能概览

- **多级分类导航**：支持用户自定义分类层级，将原始 URL 按技术领域、文档类型或业务阶段进行组织，并自动生成树状或平铺式导航菜单。

- **批量链接导入**：提供基于文本列表的批量 URL 导入接口，支持裸域名、带协议完整地址、含路径深链接等多种格式自动识别与规范化存储。

- **状态监控看板**：内置轻量级链接可达性探测模块，定期检查已收录外链的响应状态码，并在管理界面中以颜色标记异常链接，辅助运维人员及时清理或更新失效资源。

- **标签与检索系统**：允许为每条链接附加多维度标签（如“稳定版”“草案”“外部依赖”），并支持基于标签组合的快速筛选和关键词模糊检索，提升资源查找效率。

- **版本历史追踪**：自动记录每次外链配置的变更操作，包括新增、删除、URL 修改及分类迁移，支持按时间轴回溯任意历史版本，便于审计和回滚。

- **嵌入组件生成**：提供可嵌入其他静态页面或动态网站的 HTML/JavaScript 片段生成能力，使得外链导航内容能够以组件形式复用，无需重复配置。

- **数据导入导出**：支持 JSON、YAML、CSV 三种格式的完整数据导入与导出，便于与其他工具链（如静态站点生成器、CMS 系统）进行数据交换。

## 应用场景

- **技术文档版本管理**：当开源项目存在多个维护分支或版本线时，每个版本对应不同的外部依赖文档链接。HRAP 可为每个版本建立独立的外链分组，并统一展示在版本发布说明页面中，帮助用户快速定位对应版本的参考资源。

- **开源社区知识库建设**：社区运营者可利用 HRAP 整理外部技术博客、官方规范、视频教程、讨论区等分散资源，按照入门、进阶、专家等层级组织，形成结构化的知识导航，降低新成员的学习曲线。

- **多语言文档对照查阅**：对于提供多语言翻译的技术文档项目，各语言版本可能引用不同语言的外部资料。HRAP 支持按语言维度建立外链集合，使得翻译维护者能够集中管理各语言对应的原始资料链接，方便交叉核对。

- **合规与审计资源归档**：企业内部的合规团队可将需要定期审阅的外部法规、标准、政策文件链接统一收录至 HRAP，并利用状态监控功能定期检查链接有效性，确保审计线索始终可访问。

## 快速开始

以下步骤假设您已具备基本的 Node.js 运行环境。HRAP 核心引擎基于 Node.js 开发，提供命令行工具和可选的 Web 管理界面。

```bash
# 1. 克隆项目仓库
git clone https://github.com/hrap-community/hrap-core.git
cd hrap-core

# 2. 安装项目依赖
npm install

# 3. 执行初始数据导入并进行本地预览
# 首先将您的 URL 列表按规则放入 ./data/import.txt，每行一个 URL
# 然后运行导入命令
npm run import -- --source ./data/import.txt --format txt

# 启动本地开发服务器，默认监听端口 3000
npm run dev
```

启动成功后，访问控制台输出的本地地址（通常为 `http://localhost:3000`）即可看到外链导航主页。如需构建生产环境静态文件，请执行 `npm run build`，生成内容位于 `./dist` 目录。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Node.js | 18.x 或 20.x LTS | 运行时环境，用于执行核心引擎及命令行工具 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖及执行脚本 |
| SQLite3 | 系统自带或通过 npm 安装 | 轻量级嵌入式数据库，用于存储链接配置及历史记录，无需独立部署 |
| Git | 2.30 或更高 | 版本控制系统，用于克隆仓库及后续更新 |
| 操作系统 | Linux (glibc 2.28+), macOS (11+), Windows (10+ 含 WSL) | 支持主流开发及服务器操作系统，Windows 用户推荐使用 WSL 2 以获得最佳性能 |
| 网络环境 | 可访问公网（用于状态监控探测） | 状态监控模块需要对外发起 HTTP 请求，若在内网使用需配置代理或白名单 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 入门指南 | `docs/getting-started/` | 如何快速安装、配置初始外链数据、启动服务并生成第一个导航页面 |
| 配置参考 | `docs/configuration/` | 数据导入格式、分类规则定义、标签体系设计、自定义渲染模板的完整参数说明 |
| 运维手册 | `docs/operations/` | 如何执行链接状态巡检、清理失效链接、备份与恢复数据、执行版本回滚操作 |
| 扩展开发 | `docs/development/` | 如何编写自定义解析器、添加新的导入导出格式、改造前端展示组件及贡献代码规范 |

## 资源列表

本部分集中收录项目内引用的全部外部资源链接，按类别分组以便查阅。所有链接均保持用户提供的原始格式，未经任何修饰或转换。

### 主要分支参考站点

<code>xijiabifenzhiboa.org.cn</code>

<code>dejiabifenzhiboa.org.cn</code>

<code>yijiabifenzhiboa.org.cn</code>

<code>fajiabifenzhiboa.org.cn</code>

### 技术指标与版本说明站点

<code>yingchaojishibifenb.org.cn</code>

<code>xijiajishibifenb.org.cn</code>

<code>dejiajishibifenb.org.cn</code>

## 项目结构

```
hrap-core/
├── bin/                                 # 命令行入口文件
│   └── hrap-cli.js                      # 主 CLI 工具，处理 import、export、check 等命令
├── config/                              # 全局配置文件目录
│   ├── default.yaml                     # 默认系统配置，含端口、数据库路径、缓存策略
│   └── schema.json                      # 数据配置文件的 JSON Schema 校验定义
├── src/                                 # 核心源代码目录
│   ├── core/                            # 核心逻辑模块
│   │   ├── importer.js                  # 批量导入处理器，支持 txt、csv、json 格式解析
│   │   ├── classifier.js                # 分类引擎，依据配置规则对链接进行自动分组
│   │   └── checker.js                   # 状态探测模块，管理并发请求与超时重试
│   ├── web/                             # Web 服务层
│   │   ├── app.js                       # Express 应用主入口，注册路由与中间件
│   │   ├── routes/                      # API 路由定义
│   │   └── views/                       # 服务端渲染模板（EJS）
│   ├── db/                              # 数据持久化层
│   │   ├── migrations/                  # 数据库迁移脚本（使用 Knex）
│   │   └── models/                      # 数据模型定义（链接、标签、历史记录）
│   └── utils/                           # 通用工具函数
│       ├── validator.js                 # URL 格式校验、协议规范化工具
│       └── logger.js                    # 结构化日志输出（基于 Winston）
├── data/                                # 用户数据存放目录（默认不纳入版本控制）
│   ├── import/                          # 存放待导入的原始数据文件
│   └── export/                          # 导出文件输出目录
├── docs/                                # 项目文档源码（Markdown 格式）
│   ├── getting-started/                 # 入门指南相关文档
│   ├── configuration/                   # 配置详解文档
│   ├── operations/                      # 运维操作文档
│   └── development/                     # 开发与贡献文档
├── test/                                # 单元测试与集成测试
│   ├── unit/                            # 各模块单元测试（使用 Mocha + Chai）
│   └── integration/                     # 端到端集成测试（使用 Supertest）
├── .env.example                         # 环境变量示例文件，含数据库路径、日志级别等
├── .gitignore                           # Git 忽略规则配置
├── package.json                         # npm 包清单，含依赖列表及脚本命令
├── README.md                            # 项目主说明文档（即本文档）
└── LICENSE                              # MIT 许可证文本
```

## 贡献指南

我们欢迎并鼓励社区贡献者参与 HRAP 项目的改进与完善。请遵循以下步骤进行协作：

1. **查阅问题列表与提案**：访问 GitHub Issues 页面，浏览当前待处理的缺陷报告、功能请求或优化提案。如您有新的想法，请先创建一个 Issue 进行讨论，避免重复劳动或设计方向偏离。

2. **派生仓库并创建特性分支**：将主仓库派生（Fork）至您的个人账户下，然后在本地克隆派生仓库。请基于 `main` 分支创建一个新的特性分支，分支命名建议采用 `feature/` 或 `fix/` 前缀，后跟简要描述，例如 `feature/add-csv-export`。

3. **遵循编码规范与测试要求**：代码提交前请运行 `npm run lint` 检查代码风格一致性，并执行 `npm test` 确保所有现有测试用例通过。新增功能或修复缺陷时，请同步编写或更新对应的单元测试与集成测试。

4. **提交变更并签署开发者原创声明**：提交信息（Commit Message）请采用语义化格式，简要说明变更内容与动机。在 Pull Request 描述中，需明确注明是否已签署项目的开发者原创声明（DCO），确保您有权贡献相关代码。

5. **发起拉取请求并参与评审**：将特性分支推送到您的派生仓库，然后向主仓库的 `main` 分支发起拉取请求（Pull Request）。项目维护者将在一周内进行评审，可能会提出修改意见，请及时响应并更新提交。

## 常见问题

**问：HRAP 是否支持私有化部署，且完全离线运行？**

答：支持。HRAP 核心功能不依赖任何外部在线服务，所有数据存储于本地 SQLite 数据库。但需注意，状态监控模块需要对外发起 HTTP 请求以检测链接可达性，该功能在完全离线环境下将无法正常使用，您可在配置中禁用该模块或设置超时时间为 0 以跳过探测。

**问：我已导入数百条 URL，但发现部分链接格式不规范（例如缺少协议头），系统如何处理？**

答：导入模块内置了智能规范化逻辑。对于缺失协议的裸域名（如 `example.org.cn`），系统会自动尝试补充 `http://` 前缀进行存贮，并在状态探测时优先尝试 HTTPS。但建议您在上游数据源头尽量提供完整格式，以提高探测准确性和页面展示一致性。您也可以使用 `npm run validate` 命令对导入前的文件进行预校验。

**问：如何将我现有的 Markdown 文档中的外链批量迁移至 HRAP 管理？**

答：您可以使用 `src/utils/markdown-extractor.js` 工具脚本，该脚本能够扫描指定目录下的所有 `.md` 文件，自动提取其中符合 URL 格式的链接，并去重后输出为 CSV 或 JSON 格式的导入文件。随后通过 `npm run import` 命令即可完成迁移。详细用法请参阅 `docs/operations/markdown-migration.md`。

## 许可证

MIT License

Copyright (c) 2026 HRAP Community

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:11
