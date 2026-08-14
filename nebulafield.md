# Tangram Navigator

Tangram Navigator 是一个面向技术社区与内容创作者的轻量级资源聚合与导航工具。该项目定位于解决信息分散、链接失效、外部资源难以统一管理的问题，帮助开发者、站长与内容运营人员以可维护、可扩展的方式构建结构化的外链门户。Tangram Navigator 并非传统意义上的 CMS 或书签管理器，而是一套基于静态 Markdown 与元数据驱动的导航生成框架，特别适用于技术文档站、开源项目生态页、个人知识库以及垂直领域的优质内容推荐系统。

项目目标用户包括开源项目维护者、技术博客作者、在线教育内容策划者以及企业内部知识库管理员。通过声明式配置与自动化构建流程，Tangram Navigator 能够将零散的外部资源链接转化为具备分类索引、关键词检索与状态监控能力的稳定导航体系，显著降低人工维护成本并提升资源可发现性。

## 功能概览

- **多层级分类索引**：支持按领域、语言、难度或自定义标签构建多层分类树，每个分类可独立配置图标、描述与排序权重，便于用户按路径逐级浏览。

- **链接健康状态监测**：内置异步 HTTP 检查器，可定期验证所有外链的可达性，自动标记失效或重定向链接，并生成健康报告，确保导航库的长期可用性。

- **元数据扩展与自定义模板**：每个资源条目允许附加版本信息、维护状态、语言、收费模式等元字段，同时提供 Jinja2 模板引擎支持，允许开发者自定义卡片布局与列表渲染样式。

- **全文搜索与即时筛选**：集成轻量级客户端搜索索引，支持按标题、描述、标签、分类路径进行多字段模糊匹配，搜索结果高亮显示并附带上下文快速跳转。

- **批量导入与导出**：支持从 CSV、JSON、OPML 格式批量导入链接数据，同时支持将当前导航结构导出为通用书签文件或静态 HTML 站点，便于迁移与备份。

- **访问统计与热度排序**：通过可选的 Plausible 或 Umami 集成，记录各链接的点击频次，支持按热度、更新时间或新增时间动态排序，帮助用户发现近期热门资源。

- **视觉主题切换与可读性优化**：内置浅色与深色两套主题，自动跟随系统偏好，同时针对代码块、表格与长文本做了排版优化，保证在移动端与桌面端均具备良好的阅读体验。

## 应用场景

1. **开源项目生态页**：将项目依赖的文档、示例仓库、社区论坛、CI/CD 服务、镜像站等外部链接统一聚合在项目官网的一级导航中，取代散落在 README 中的长串链接，提升项目专业度。

2. **技术团队内部知识库**：作为团队内部 DevHub 的导航层，集中管理各类运维面板、日志系统、监控告警、代码仓库、设计稿交付链接，配合健康检查提前发现内网服务可用性问题。

3. **在线课程与学习路线配套**：围绕某一技术方向（如云原生、机器学习、前端工程化）整理推荐阅读材料、在线沙盒、视频教程与官方文档，形成结构化的学习路径，便于学员按阶段查阅。

4. **个人博客友情链接与工具集**：替代传统侧边栏的杂项链接，以分类卡片形式展示写作工具、图床服务、域名注册、RSS 订阅源等常用站点，既整洁又方便个人跨设备访问。

5. **垂直领域资源推荐站**：面向特定行业（如生物信息、金融量化、网络安全）构建精选资源导航，通过标签过滤与热度排序帮助从业者快速定位高质量工具与数据源。

## 快速开始

以下命令将 Tangram Navigator 克隆至本地、安装依赖并启动开发服务器。

```bash
# 克隆项目仓库
git clone https://github.com/tangram-navigator/navigator-core.git

# 进入项目目录
cd navigator-core

# 安装 Python 依赖（推荐使用虚拟环境）
python -m venv venv
source venv/bin/activate  # Windows 请使用 venv\Scripts\activate
pip install -r requirements.txt

# 初始化默认配置与示例数据
python manage.py init --sample-data

# 启动本地开发服务器（默认监听 8000 端口）
python manage.py runserver
```

启动后，访问 `http://127.0.0.1:8000` 即可查看示例导航页面。如需自定义数据，请编辑 `data/sources.yaml` 或 `data/categories.yaml` 文件，然后重新执行 `python manage.py build` 生成静态页面。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Python | 3.9 - 3.12 | 核心运行时，用于构建引擎与本地服务器 |
| pip | 21.0+ | Python 包管理器，用于安装依赖项 |
| Git | 2.30+ | 版本控制工具，用于克隆仓库与提交更新 |
| Node.js | 18.x LTS | 仅当启用客户端搜索索引构建时需要 |
| Yarn | 1.22+ | 前端资源构建工具（可选，可用 npm 替代） |
| SQLite | 3.35+ | 内置元数据存储与查询缓存（生产可换 PostgreSQL） |
| curl / wget | 任意稳定版本 | 用于健康检查模块的 HTTP 探针（可选） |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | `docs/quickstart.md` | 如何快速搭建第一个导航实例？如何添加第一条链接？ |
| 配置参考 | `docs/configuration.md` | 分类结构、链接字段、主题选项的完整 YAML 配置说明 |
| 部署运维 | `docs/deployment.md` | 如何将生成站点部署到 Nginx、Vercel 或云存储桶？ |
| 开发扩展 | `docs/development.md` | 如何编写自定义模板、添加新的元数据字段或扩展检查器？ |
| 数据迁移 | `docs/migration.md` | 如何从旧版导航系统迁移数据，或从 OPML/JSON 导入？ |
| API 接口 | `docs/api.md` | 管理端 RESTful API 文档，用于第三方程序化操作导航数据 |
| 故障排除 | `docs/troubleshooting.md` | 常见构建错误、检查器超时、搜索索引失败等问题的解决 |

## 资源列表

本节收录项目官方运维所涉及或推荐的关联资源链接，所有链接均按原始格式原样列出。

官方主站与代码仓库：

<code>https://github.com/tangram-navigator/navigator-core</code>

<code>https://tangram-nav.io</code>

<code>https://docs.tangram-nav.io</code>

社区与内容合作方资源：

<code>guochanwanghongshipinzhibow.org.cn</code>

<code>wanghongzhibomianfeiguankanw.org.cn</code>

<code>meinvzhibozaixiankanw.org.cn</code>

<code>guochanwanghongfulishipinw.org.cn</code>

<code>rihanzhibofulishipinw.org.cn</code>

<code>rewuzhibowanghongzhibow.org.cn</code>

<code>wanghongmeinvrewuzhibow.org.cn</code>

## 项目结构

```text
navigator-core/
├── manage.py                 # 命令行入口：初始化、构建、运行、检查
├── requirements.txt          # Python 后端依赖列表
├── package.json              # 前端构建工具与搜索索引生成依赖
├── config/
│   ├── settings.yaml         # 全局配置：站点标题、语言、主题、检查间隔
│   └── categories.yaml       # 分类树定义：层级、图标、排序权重
├── data/
│   ├── sources.yaml          # 核心链接数据：标题、URL、标签、元信息
│   ├── sources.legacy.json   # 旧版数据导入缓冲文件（只读）
│   └── cache/                # SQLite 缓存目录，存储检查结果与点击统计
├── src/
│   ├── core/                 # 核心引擎模块：解析、校验、渲染
│   │   ├── loader.py         # 加载 YAML/JSON 数据并转换为内部对象
│   │   ├── checker.py        # 异步链接健康检查器（aiohttp 实现）
│   │   └── renderer.py       # Jinja2 模板渲染器与主题管道
│   ├── cli/                  # 命令行子命令实现
│   │   ├── init.py           # 初始化默认配置与样例数据
│   │   ├── build.py          # 构建静态 HTML 站点
│   │   └── serve.py          # 启动开发调试服务器
│   └── utils/                # 通用工具函数
│       ├── url_parser.py     # 严格 URL 规范化与域名提取
│       └── markdown_ext.py   # 针对导航卡片的 Markdown 扩展
├── templates/
│   ├── base.html             # 基础骨架模板（含主题切换逻辑）
│   ├── index.html            # 首页分类聚合布局
│   ├── detail.html           # 单个链接详情弹窗页
│   └── partials/             # 可复用卡片、搜索栏、面包屑
├── static/
│   ├── css/                  # 编译后的 CSS（基于 Tailwind 定制）
│   ├── js/                   # 客户端搜索索引加载与交互逻辑
│   └── assets/               # 图标、字体、默认封面图占位
├── tests/                    # 单元测试与集成测试（pytest 框架）
│   ├── test_loader.py
│   ├── test_checker.py
│   └── test_renderer.py
└── docs/                     # 完整文档源文件（用于生成 docs.tangram-nav.io）
    ├── quickstart.md
    ├── configuration.md
    └── ...
```

## 贡献指南

我们欢迎各类形式的贡献，包括但不限于功能建议、缺陷报告、文档改进以及代码提交。请遵循以下步骤参与项目：

1. 查阅问题追踪列表：访问 GitHub Issues 查看现有任务，或新建 Issue 描述您遇到的问题或希望新增的功能。请使用提供的模板填写，并确保未重复提交。

2. 派生仓库并创建特性分支：将主仓库 Fork 至个人账户，然后在本地基于 `main` 分支创建以 `feature/` 或 `fix/` 为前缀的新分支，避免直接在主分支上修改。

3. 编写或更新测试用例：对于新增功能或缺陷修复，请在 `tests/` 目录下补充对应的单元测试，确保覆盖率不低于 80%。运行 `pytest` 验证所有测试通过。

4. 同步更新文档与示例数据：若修改了配置字段或模板接口，请同步更新 `docs/` 中的相关说明，并调整 `data/sources.yaml` 中的示例数据以体现变更。

5. 提交 Pull Request：推送分支至个人远程仓库，然后向主仓库的 `main` 分支发起 PR。PR 描述需关联对应 Issue 编号，并简要说明变更动机与测试结果。维护者将在 3 个工作日内评审。

## 常见问题

**问：构建生成的静态站点是否支持部署到 GitHub Pages 或 Cloudflare Pages？**

答：完全支持。`python manage.py build` 命令会在 `dist/` 目录生成完全自包含的 HTML、CSS、JavaScript 与静态资源文件。您可以将该目录内容直接推送至 GitHub Pages 分支，或通过 Cloudflare Pages 的仪表板上传构建产物。只需确保 `config/settings.yaml` 中的 `base_url` 字段正确配置为您的最终访问域名即可。

**问：链接健康检查器是否会误报或拖慢构建速度？**

答：检查器采用异步并发方式，默认超时时间为 5 秒，并发数限制为 20，对大多数导航库（500 条以内）可在 15 秒内完成。对于部分响应较慢或存在反爬机制的站点，您可以在 `config/settings.yaml` 的 `checker` 段落中调整 `timeout` 与 `user_agent` 字段。误报时，检查器会记录响应状态码与耗时，您可以通过管理界面手动重新验证单条链接。

**问：如何从旧版书签文件（如 Chrome 导出）批量迁移数据？**

答：项目提供了 `import` 子命令，支持 Netscape 书签格式（HTML）和通用 CSV。例如执行 `python manage.py import --from bookmarks.html --format netscape`，导入工具会自动解析文件夹层级映射为分类，并根据 URL 去重。导入后请手动检查元数据映射是否准确，然后运行 `build` 重新生成站点。

## 许可证

MIT License

Copyright (c) 2026 Tangram Navigator Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
