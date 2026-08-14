# ResourceBridge

ResourceBridge 是一个面向技术内容创作者、开源项目维护者与社区运营者的外部资源聚合与导航中间件。项目定位为“轻量级外链治理工具”，旨在解决多源异构技术资源链接分散、失效风险高、复用效率低的问题。目标用户包括开源项目文档维护者、DevRel 工程师、技术课程讲师以及需要长期管理大量外部引用链接的研发团队。

ResourceBridge 不提供内容存储，不进行爬取或缓存，仅作为结构化链接清单的管理与呈现层。项目本身以静态站点形式交付，兼容 GitHub Pages、Cloudflare Pages 及任何支持静态托管的服务。通过约定大于配置的目录结构，用户可在五分钟内完成从克隆到本地预览的全流程，并快速适配自身项目的链接资源管理需求。

## 功能概览

- **分级链接目录体系**：支持按技术领域、赛事类型、地域或任意自定义标签对链接进行一级与二级分类，内置默认分类模板可开箱即用。

- **链接状态检测占位**：提供自动化检测脚本框架，支持周期性对已收录链接进行可达性探测，输出 JSON 格式状态报告，便于及时清理或替换失效资源。

- **静态页面生成引擎**：基于单一 Markdown 源文件与链接清单，自动生成响应式导航页面，无需前端框架编译，依赖极少。

- **多格式导出支持**：支持将链接清单导出为纯文本列表、CSV 表格或 JSON API 格式，便于下游系统集成或批量迁移。

- **版本化链接台账**：每次链接增删改操作均记录于 CHANGELOG 文件，支持按时间回溯历史链接状态，适用于合规审计场景。

- **自定义元数据扩展**：每条链接可附加负责人、过期日期、访问频率、所属项目代号等自定义字段，满足团队内部管理需求。

- **零数据库依赖**：所有链接数据以 YAML 或 JSON 文件形式存储在仓库内，完全本地化，无需配置外部数据库或云服务。

- **命令行交互工具**：内置 Node.js 脚本，支持通过终端交互式添加、删除、搜索及分类迁移链接，提升日常维护效率。

## 应用场景

- **开源项目外部依赖链接管理**：开源项目 README 或文档中常引用大量第三方库官网、教程文章、API 参考等链接。使用 ResourceBridge 可集中维护这些链接，并在项目文档中统一引用生成的导航页面，避免分散维护导致的链接漂移。

- **技术培训课程资源索引**：讲师在准备系列课程时，需要为学生提供每节课的延伸阅读链接。ResourceBridge 支持按课程章节或周次分类，生成清晰的学习资源地图，且每学期可复用同一套索引结构，仅更新链接内容。

- **社区活动资料归档**：技术社区举办线上分享会或黑客松后，通常需要汇总嘉宾幻灯片、代码仓库、回放视频等链接。使用 ResourceBridge 可快速生成活动专属资源页，并支持按年份或活动编号归档。

- **个人技术写作素材库**：技术博主或文档工程师在日常阅读中积累大量待参考文章。通过 ResourceBridge 的命令行工具，可快速标记分类并添加个人备注，形成可检索的知识外链库，避免浏览器收藏夹的混乱。

- **多团队共享链接白名单**：企业内部多个团队需共用一组经过安全审核的外部资源链接（如镜像站、SDK 下载地址、官方文档）。ResourceBridge 可充当白名单台账，链接变更时通过 Pull Request 流程通知所有相关方。

## 快速开始

以下步骤适用于 macOS / Linux / Windows WSL 环境。确保已安装 Git 和 Node.js 16.x 及以上版本。

```bash
# 克隆仓库
git clone https://github.com/resourcebridge/resourcebridge.git
cd resourcebridge

# 安装依赖（仅用于本地脚本工具，运行时无需依赖）
npm install

# 复制示例链接清单并进行本地预览
cp config/links.example.yaml config/links.yaml
npm run build
npm run serve
```

执行完成后，访问控制台输出的本地地址（通常为 http://localhost:8080）即可查看生成的导航页面。修改 `config/links.yaml` 后重新执行 `npm run build` 即可更新页面。

## 安装要求

| 依赖 | 必需版本 | 说明 |
|------|----------|------|
| Node.js | 16.x 或更高 | 用于运行构建脚本与命令行工具，运行时页面本身为纯静态，但工具依赖 Node 环境 |
| npm | 8.x 或更高 | 包管理器，用于安装构建工具依赖 |
| Git | 2.30 或更高 | 版本控制，用于克隆仓库及提交链接变更记录 |
| 任意静态 Web 服务器 | 无版本要求 | 生产环境可使用 Nginx、Apache、Caddy 或托管服务自带服务器，开发环境可使用 `npm run serve` 内置的轻量服务器 |
| 磁盘空间 | 至少 50 MB | 仓库体积约 2 MB，构建产物约 15 MB，预留缓存空间 |
| 内存 | 512 MB 或更高 | 构建过程内存占用低于 256 MB，但建议留有余量 |
| 操作系统 | Linux / macOS / Windows WSL2 | 核心脚本兼容所有主流系统，但文件路径建议避免中文目录 |
| 网络 | 仅首次克隆与安装依赖需要 | 后续构建与预览完全离线，无需网络 |
| 浏览器 | 现代浏览器（Chrome / Firefox / Edge 最新两个版本） | 用于查看生成的导航页面，页面使用 HTML5 + CSS3，不兼容 IE |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `docs/guide/` | 如何初始化链接清单、如何自定义分类模板、如何生成并部署站点、如何使用命令行工具增删链接 |
| 配置参考 | `docs/config/` | 所有 YAML 配置字段的含义、数据类型、默认值及可选的元数据扩展字段说明 |
| 自动化运维 | `docs/ops/` | 如何配置链接状态检测的定时任务、如何解读检测报告、如何设置失效链接告警通知 |
| 定制化开发 | `docs/dev/` | 页面主题修改方法、新增导出格式的接口规范、构建流程各阶段钩子函数说明 |
| 迁移指南 | `docs/migration/` | 从其他书签管理工具或文档内嵌链接迁移至 ResourceBridge 的步骤及脚本辅助工具 |

## 资源列表

以下为项目预设参考资源库中收录的外部链接，按类别划分。所有链接均以用户提供的原始格式原样列出，未做任何协议、域名或路径改写。

赛事实时比分类

- <code>zuqiubifenziboc.org.cn</code>
- <code>zuqiubifenzibod.org.cn</code>
- <code>zuqiubifenziboe.org.cn</code>

联赛历史比分统计类

- <code>yingchaojishibifena.org.cn</code>
- <code>xijiajishibifena.org.cn</code>
- <code>dejiajishibifena.org.cn</code>
- <code>yijiajishibifena.org.cn</code>

## 项目结构

```
resourcebridge/
├── bin/                                 # 命令行工具入口脚本
│   ├── cli.js                           # 主 CLI 入口，注册所有子命令
│   └── commands/                        # 子命令实现目录
│       ├── add.js                       # 添加链接命令
│       ├── remove.js                    # 删除链接命令
│       ├── list.js                      # 列出所有链接命令
│       └── check.js                     # 链接可达性检测命令
│
├── config/                              # 全局配置目录
│   ├── links.example.yaml               # 链接清单示例文件，含完整注释
│   ├── categories.example.yaml          # 分类体系示例文件
│   └── settings.yaml                    # 构建与导出行为配置
│
├── src/                                 # 核心源码目录
│   ├── builder/                         # 页面构建引擎模块
│   │   ├── index.js                     # 构建流程编排主文件
│   │   ├── pageRenderer.js              # HTML 模板渲染器
│   │   └── assetProcessor.js            # 静态资源（CSS/JS）处理
│   ├── exporters/                       # 导出格式适配器
│   │   ├── jsonExporter.js              # JSON 格式导出
│   │   ├── csvExporter.js               # CSV 表格导出
│   │   └── textExporter.js              # 纯文本列表导出
│   ├── detectors/                       # 链接状态检测模块
│   │   ├── httpChecker.js               # HTTP 状态码检测器
│   │   ├── dnsResolver.js               # DNS 解析检测器
│   │   └── reporter.js                  # 检测报告生成器
│   └── utils/                           # 通用工具函数
│       ├── yamlLoader.js                # YAML 文件加载与校验
│       ├── validator.js                 # 链接格式与字段校验
│       └── logger.js                    # 命令行日志输出工具
│
├── templates/                           # 页面模板目录
│   ├── index.hbs                        # 主页面 Handlebars 模板
│   ├── partials/                        # 模板局部组件
│   │   ├── header.hbs                   # 页头组件
│   │   ├── footer.hbs                   # 页脚组件
│   │   └── linkCard.hbs                 # 单个链接卡片组件
│   └── assets/                          # 静态资源源文件
│       ├── main.css                     # 主样式表
│       └── main.js                      # 前端交互脚本（搜索/过滤）
│
├── dist/                                # 构建输出目录（git ignored）
│   ├── index.html                       # 生成的首页
│   ├── assets/                          # 压缩后的静态资源
│   └── export/                          # 导出的数据文件
│
├── docs/                                # 项目文档目录（见文档导航章节）
│   ├── guide/                           # 用户手册
│   ├── config/                          # 配置参考
│   ├── ops/                             # 运维指南
│   ├── dev/                             # 开发文档
│   └── migration/                       # 迁移指南
│
├── tests/                               # 单元测试与集成测试目录
│   ├── unit/                            # 单元测试用例
│   ├── integration/                     # 集成测试用例
│   └── fixtures/                        # 测试用固定数据
│
├── .github/                             # GitHub 配置目录
│   └── workflows/                       # CI/CD 工作流
│       ├── build.yml                    # 构建验证工作流
│       └── linkCheck.yml                # 链接状态定时检测工作流
│
├── package.json                         # Node.js 项目依赖与脚本定义
├── README.md                            # 项目说明文件（即本文档）
├── CHANGELOG.md                         # 版本变更日志，含链接台账变更记录
└── LICENSE                              # MIT 许可证文件
```

## 贡献指南

欢迎并感谢任何形式的贡献。请遵循以下步骤以确保协作流程顺畅。

1.  **查阅现有议题与项目面板**：在提交新功能或修复前，请先访问 GitHub Issues 与 Projects 面板，确认是否存在相关讨论或正在进行的工作，避免重复劳动。

2.  **Fork 仓库并创建功能分支**：从主仓库 Fork 至个人账户后，基于 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支，例如 `feature/add-export-format`。

3.  **编写或修改代码并补充测试**：所有新增功能必须包含对应的单元测试用例。修改现有功能需确保已有测试通过。测试文件放置于 `tests/` 目录下，使用 Mocha 或 Jest 框架。

4.  **更新文档与示例文件**：若变更影响配置格式、命令行用法或构建流程，请同步更新 `docs/` 目录下对应文档，并修改 `config/` 中的示例文件以反映新用法。

5.  **提交 Pull Request 并关联议题**：推送分支至个人 Fork 仓库后，向主仓库 `main` 分支发起 Pull Request。PR 描述中需清晰说明变更目的、实现方式及测试结果，并使用 `Closes #xxx` 关联相关议题编号。

## 常见问题

**Q: ResourceBridge 是否可用于内网环境，无法访问外网时能否正常使用？**

A: 可以。ResourceBridge 核心构建与导出功能完全离线运行，不依赖任何外部 API 或 CDN 资源。唯一需要外网的环节是首次 `npm install` 安装依赖，以及可选的链接状态检测功能（该功能可关闭）。若完全离线，可将 `node_modules` 目录整体打包迁移，或使用 `npm pack` 生成离线安装包。生成的静态页面可部署于任何内网 Web 服务器。

**Q: 链接清单中的自定义元数据字段是否会影响页面生成？**

A: 不会。ResourceBridge 采用“宽容解析”策略，清单文件中除 `url` 和 `category` 为必需字段外，其余字段均视为扩展元数据。页面生成时，默认模板仅渲染标题、分类和描述，扩展字段不会自动出现在页面上。但开发者可通过修改模板文件访问所有元数据，按需渲染。扩展字段主要用于命令行搜索过滤及导出格式（如 CSV）的完整列输出。

**Q: 如何迁移现有的大量浏览器书签或 Markdown 文档中的链接？**

A: ResourceBridge 提供了迁移辅助脚本，位于 `docs/migration/` 目录下。对于浏览器书签，可将书签导出为 HTML 文件后，使用 `migrate-bookmark.js` 脚本转换为 YAML 格式。对于 Markdown 文档，可使用 `migrate-md-links.js` 脚本通过正则提取所有 `[text](url)` 模式链接，并生成初始清单。迁移后仍需人工复核分类与描述字段，但可节省 80% 以上的手动录入工作量。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
