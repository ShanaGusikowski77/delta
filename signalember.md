# ResourceHub

ResourceHub 是一个面向技术内容创作者、开源项目维护者以及社区运营人员的轻量级外链资源汇总与管理平台。该项目旨在解决技术文档、项目 README、社区导航页中外部链接分散、维护成本高、分类不清晰以及链接失效难以追踪的问题。通过结构化的数据组织与简洁的展示层，ResourceHub 帮助用户快速构建一个可公开访问、可版本控制、可协作维护的技术资源导航站。

目标用户包括开源项目贡献者、技术布道师、开发者社区运营人员以及任何需要系统化管理大量外链资源的个人或团队。ResourceHub 不依赖数据库，采用纯静态 Markdown 与 YAML 数据源，支持自动化构建与部署，便于集成到现有 CI/CD 工作流中。

## 功能概览

- **结构化外链管理**：支持按类别、标签、来源等多维度对链接进行组织，并提供 Markdown 与 YAML 两种数据导入导出格式。
- **链接状态自动检测**：内置链接可用性检查模块，可定期扫描已收录资源，标记失效或重定向链接，并提供变更报告。
- **多级分类与筛选**：支持无限级分类嵌套，前端提供按分类、关键词、热度排序的交互式筛选面板。
- **资源变更历史追踪**：基于 Git 版本控制，每次增删改操作均记录提交信息，支持回溯任意历史版本。
- **自定义展示模板**：提供默认卡片式布局与列表式布局，同时允许用户通过简单的 CSS 与 HTML 模板定制页面风格。
- **开放数据 API**：提供基于 JSON 格式的只读 API 接口，便于其他系统或脚本远程获取资源列表数据。
- **批量导入与导出**：支持从 CSV、OPML 及标准书签文件批量导入链接，并支持导出为多种通用格式用于迁移或备份。

## 应用场景

1. **开源项目文档导航**：开源项目维护者可以使用 ResourceHub 整理项目相关的官方文档、社区论坛、贡献指南、API 参考、示例代码仓库等外部链接，统一放置在项目 README 的引用部分，提高文档的整洁性与可维护性。

2. **技术社区资源中心**：技术社区或线上学习平台可利用 ResourceHub 构建一个公开的优质资源汇总页，涵盖教程文章、视频课程、工具推荐、招聘信息、活动日历等，为社区成员提供一站式的信息入口。

3. **个人知识库外链管理**：技术博主或研究者可将日常阅读积累的参考文献、工具站点、数据集、论文链接等通过 ResourceHub 进行归类整理，并生成可公开分享的静态页面，替代传统的浏览器书签管理方式。

4. **企业内部技术栈索引**：中小型研发团队可使用 ResourceHub 搭建内部技术栈导航，统一收录代码仓库、CI/CD 服务、监控面板、日志系统、云服务控制台等内部链接，减少团队成员寻找关键工具的时间成本。

5. **静态网站外链聚合页**：个人静态博客或作品集网站可以利用 ResourceHub 生成一个独立的资源推荐页面，用于展示友情链接、常用开发工具、设计资源或阅读清单，提升网站的内容丰富度。

## 快速开始

以下命令适用于 Linux 与 macOS 环境，Windows 用户可使用 WSL 或 Git Bash 执行。

```bash
# 克隆项目仓库
git clone https://github.com/resourcehub/resourcehub.git
cd resourcehub

# 安装依赖（项目使用 Python 3.9+ 与 pipenv 管理）
pip install pipenv
pipenv install --dev

# 进入虚拟环境并运行本地开发服务器
pipenv shell
python manage.py runserver --host 0.0.0.0 --port 8080
```

访问 http://localhost:8080 即可查看默认资源列表页面。首次启动会自动生成示例数据，包含预置的分类与占位链接。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---------|---------|------|
| Python | 3.9 及以上 | 核心运行环境，用于后端数据处理与本地服务器 |
| pipenv | 2023.x 及以上 | 依赖管理与虚拟环境隔离工具 |
| Git | 2.30 及以上 | 用于版本控制及变更历史追踪功能 |
| Node.js | 16.x 及以上 | 仅用于前端资源构建（可选，若使用预编译样式则不需要） |
| npm 或 yarn | 最新稳定版 | 前端依赖管理（可选，仅当定制主题时需要） |
| curl 或 wget | 任意版本 | 用于链接状态检测模块的网络请求（系统自带） |
| make | 任意版本 | 用于执行自动化任务脚本（GNU make 或兼容实现） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|-----|------|-----------|
| 入门指南 | docs/getting-started.md | 如何安装、配置首次运行、生成示例数据以及部署到生产环境？ |
| 数据格式规范 | docs/data-format.md | 资源条目支持哪些字段？分类和标签如何定义？YAML 与 Markdown 格式如何转换？ |
| 定制化开发 | docs/customization.md | 如何修改页面布局、更换主题配色、添加新的页面模板或自定义 API 端点？ |
| 运维与监控 | docs/operations.md | 如何配置定时链接检测、如何查看变更日志、如何备份与恢复数据？ |

## 资源列表

以下为 ResourceHub 项目收录的示例资源链接，按类别分组展示。所有链接均保留用户提供的原始格式。

媒体资源类

<code>xingganmeinvzhibotiaowu.org.cn</code>

<code>hanguomeinvzhuborewu.org.cn</code>

<code>zaixianbofangzhubo.org.cn</code>

直播平台类

<code>zhubozhibozaixianguankan.org.cn</code>

<code>wanghongzhibozaixianshipinw.org.cn</code>

<code>wanghongfulizhibow.org.cn</code>

<code>guochanwanghongzhibozhuzaixianw.org.cn</code>

## 项目结构

```
resourcehub/
├── data/                           # 数据存储目录，包含所有资源条目与分类定义
│   ├── categories.yaml             # 分类层级定义，含显示名称与排序权重
│   ├── resources.yaml              # 核心资源条目数据，包含 URL、标题、描述、标签
│   └── history/                    # 变更历史记录，按日期归档的 JSON 差异文件
├── src/
│   ├── core/                       # 核心逻辑模块
│   │   ├── loader.py               # 数据加载与解析器，支持 YAML 与 Markdown 格式
│   │   ├── checker.py              # 链接可用性检测器，支持并发请求与超时重试
│   │   └── exporter.py             # 导出器，支持 CSV、OPML、HTML 及 JSON 格式
│   ├── web/                        # Web 服务模块
│   │   ├── app.py                  # 主应用入口，使用 Bottle 框架
│   │   ├── routes/                 # 路由处理器，按功能拆分
│   │   └── static/                 # 静态资源目录（CSS、JavaScript、图片）
│   └── cli/                        # 命令行工具模块
│       ├── main.py                 # 命令行入口，支持 add、remove、check、export 子命令
│       └── utils.py                # 通用辅助函数
├── tests/                          # 单元测试与集成测试用例
│   ├── test_loader.py
│   ├── test_checker.py
│   └── test_routes.py
├── docs/                           # 用户文档与开发文档
│   ├── getting-started.md
│   ├── data-format.md
│   ├── customization.md
│   └── operations.md
├── templates/                      # 前端模板文件（HTML 与内联样式）
│   ├── default/                    # 默认模板主题（卡片式布局）
│   └── compact/                    # 紧凑模板主题（列表式布局）
├── scripts/                        # 自动化辅助脚本
│   ├── ci-build.sh                 # CI 构建脚本，用于静态站点生成
│   └── daily-check.sh              # 每日链接检测计划任务脚本
├── Makefile                        # 常用任务快捷命令（install, test, run, build）
├── Pipfile                         # pipenv 依赖声明文件
├── Pipfile.lock                    # 依赖锁定文件
├── .gitignore
└── README.md                       # 项目说明文件（当前文档）
```

## 贡献指南

1. 在 GitHub 上 Fork 本仓库，并克隆到本地开发环境。创建新的功能分支，分支命名遵循 `feature/` 或 `fix/` 前缀加简短描述，例如 `feature/add-opml-import`。

2. 进行代码修改或文档更新时，请遵循项目现有代码风格（PEP 8 标准与 ESLint 配置）。新增功能必须包含对应的单元测试用例，测试覆盖率应不低于 80%。

3. 提交代码前，请执行本地测试套件 `make test` 确保所有用例通过。同时运行链接检测脚本 `python manage.py check --all` 确保没有引入无效的外部链接。

4. 提交 Pull Request 时，请详细描述变更目的、实现方式以及影响范围。若 PR 涉及数据格式变更，需同时更新 docs/data-format.md 中的相关说明。

5. 项目维护者会在 3 个工作日内审查 PR，并提供修改建议或合并反馈。重大功能变更建议先创建 Issue 进行讨论，以避免无效开发。

## 常见问题

**Q: 如何从现有的浏览器书签文件迁移到 ResourceHub？**

A: 您可以使用 `python manage.py import --from bookmarks.html` 命令直接导入 Netscape 格式的书签文件。系统会自动解析书签文件夹结构并转换为分类层级。导入后建议运行 `python manage.py check` 检测所有链接的有效性，并根据报告清理失效条目。

**Q: 链接状态检测模块是否会频繁访问目标站点，导致被屏蔽？**

A: 检测模块默认配置了请求间隔（500 毫秒）、单次超时时间（10 秒）以及最大重试次数（2 次）。同时支持设置 `--user-agent` 参数模拟不同浏览器标识。对于大规模检测场景，建议配置 `--rate-limit` 参数控制每秒请求数，并在非高峰时段运行计划任务。

**Q: 是否可以完全离线部署，不依赖外部 CDN 资源？**

A: 可以。ResourceHub 的默认模板使用了本地化的 CSS 与 JavaScript 文件，所有静态资源均包含在仓库的 `src/web/static/` 目录中。您只需将 `templates/default/base.html` 中的外部字体与图标库链接替换为本地路径或移除即可。同时，链接检测功能支持 `--offline` 模式，仅解析本地数据而不发起网络请求。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
