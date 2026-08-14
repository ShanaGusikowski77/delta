# HyperLink Navigator

HyperLink Navigator 是一个面向技术内容聚合与资源导航的开源项目，旨在为开发者、技术研究者及信息整理人员提供高效、结构化、可审计的外部链接管理与展示方案。该项目定位为轻量级技术资源外链汇总站，通过静态 Markdown 文档体系组织 URL 资源，解决个人或团队在信息收集、分类归档、共享分发过程中面临的链接散乱、缺乏版本控制、难以协作等问题。HyperLink Navigator 不依赖动态数据库或后端服务，所有资源条目以纯文本形式存储于仓库中，支持标准 Git 工作流，便于复刻、分支管理与变更追溯。

## 功能概览

- **链接分类归档**：支持按技术领域、内容类型、来源机构等多维度对 URL 进行分组标记，每个链接条目可附加简短说明与标签。
- **结构化文档生成**：基于预定义 Markdown 模板自动生成资源列表、场景说明、快速开始指南等章节，确保文档风格一致且机器可读。
- **依赖环境检测**：内置基础脚本用于检查运行环境中的必需工具版本，并输出兼容性报告，降低部署失败概率。
- **静态树形目录输出**：通过命令行工具生成当前仓库的 ASCII 目录树，并附带每个子目录的功能注释，便于项目结构可视化。
- **链接可用性预检**：提供可选的离线正则校验与 DNS 解析预检功能（需网络权限），帮助维护者及时发现失效域名。
- **多格式导出支持**：除标准 Markdown 外，支持将资源列表导出为 CSV 或 JSON 格式，便于与其他数据处理工具集成。
- **变更日志自动追加**：在指定资源文件发生修改时，自动在 CHANGELOG 中记录变更时间、操作类型与影响范围，增强审计能力。

## 应用场景

- **技术团队内部知识库构建**：研发团队可使用 HyperLink Navigator 整理常用开发文档、API 参考、设计规范等外链，统一存放于项目仓库中，新成员可通过快速开始步骤一键克隆并浏览全部资源。
- **开源项目外部依赖索引**：开源维护者可将项目依赖的第三方库、工具官网、社区论坛等链接集中管理，并在 README 中嵌入资源列表章节，方便用户直接访问原始出处。
- **学术研究文献参考汇集**：研究人员可利用本项目的分类与注释功能，按课题、期刊、作者等维度组织大量在线论文及数据集的 URL，配合 Git 历史记录追踪引用变化。
- **个人书签同步与版本化管理**：个人开发者可将浏览器书签导出为 Markdown 列表并纳入本项目管理，通过分支实现工作与个人环境隔离，同时利用合并请求同步多设备修改。

## 快速开始

以下命令演示如何从 GitHub 克隆 HyperLink Navigator 仓库、安装基础依赖并运行首个资源列表生成任务。请确保系统已安装 Git 与 Python 3.8 及以上版本。

```bash
# 克隆仓库到本地
git clone https://github.com/example/hyperlink-navigator.git
cd hyperlink-navigator

# 安装 Python 依赖（使用虚拟环境推荐）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 执行资源列表生成脚本，输出整合后的 README 资源章节
python scripts/generate_links.py --input data/links.yaml --output README.md
```

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Git | 2.20 或更高 | 用于克隆仓库及提交变更记录 |
| Python | 3.8 - 3.11 | 运行核心脚本与依赖解析 |
| pip | 21.0 或更高 | 安装 requirements.txt 中列出的第三方库 |
| PyYAML | 5.4.1 或更高 | 解析 links.yaml 配置文件 |
| Markdown | 3.3.6 或更高 | 用于生成结构化文档内容 |
| pytest | 7.0 或更高 | 仅开发测试阶段需要，生产环境可忽略 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户入门 | README.md | 项目定位、功能、快速开始与资源列表 |
| 配置参考 | docs/configuration.md | 如何编写 links.yaml 条目、支持哪些字段与校验规则 |
| 脚本工具 | docs/scripts_usage.md | 各个 Python 脚本的参数说明与执行范例 |
| 贡献规范 | CONTRIBUTING.md | 提交 PR 的流程、代码风格要求与测试标准 |
| 变更历史 | CHANGELOG.md | 每个版本的新增功能、修复项与破坏性变更 |
| 常见问题 | docs/faq.md | 网络超时、编码错误、目录权限等典型问题解决方案 |

## 资源列表

本列表按照类别组织用户提供的全部原始链接资源，所有 URL 严格保持原始格式输出，不添加协议前缀或修改域名大小写，结尾不附加斜杠。

外部视频与直播类资源

<code>oubazhibomianfeiguankan.org.cn</code>

<code>wanghongzhibofulizaixian.org.cn</code>

<code>nvzhubozshipinzaixianguankan.org.cn</code>

<code>xingganmeinvzhibotiaowu.org.cn</code>

<code>hanguomeinvzhuborewu.org.cn</code>

<code>zaixianbofangzhubo.org.cn</code>

<code>zhubozhibozaixianguankan.org.cn</code>

## 项目结构

```
hyperlink-navigator/
├── README.md                       # 项目主说明文档（含功能、场景、快速开始）
├── CONTRIBUTING.md                 # 贡献指南与代码提交规范
├── CHANGELOG.md                    # 版本迭代变更记录
├── LICENSE                         # MIT 许可证全文
├── requirements.txt                # Python 运行时依赖列表
├── .gitignore                      # Git 忽略规则（含 venv、pycache 等）
├── data/
│   ├── links.yaml                  # 主链接资源配置文件（YAML 格式）
│   └── categories.yaml             # 分类映射与标签定义
├── scripts/                        # 可执行脚本目录
│   ├── generate_links.py           # 根据 YAML 生成 Markdown 资源列表
│   ├── check_env.py                # 检测运行环境依赖版本
│   ├── tree_printer.py             # 输出带注释的 ASCII 目录树
│   └── validate_urls.py            # 执行基本 URL 格式与 DNS 预检
├── tests/                          # 单元测试目录
│   ├── test_generate.py            # generate_links 功能测试用例
│   └── test_validate.py            # validate_urls 边界条件测试
├── docs/                           # 扩展文档目录
│   ├── configuration.md            # links.yaml 配置项详细说明
│   ├── scripts_usage.md            # 各脚本使用示例与参数表格
│   └── faq.md                      # 常见问题汇编
└── output/                         # 导出文件默认存放目录（运行时生成）
    ├── links_export.csv
    └── links_export.json
```

## 贡献指南

1. 复刻本项目仓库至个人账户，并在本地克隆复刻版本，建议创建新分支用于开发，分支命名格式为 `feature/简述改动` 或 `fix/问题编号`。
2. 在 `data/links.yaml` 中添加或修改链接条目时，需遵循既有的缩进与字段规范（参见 `docs/configuration.md`），并同步更新 `data/categories.yaml` 中的分类定义（若引入新类别）。
3. 所有脚本改动需编写相应的单元测试，放置于 `tests/` 目录下，并确保在提交前通过全部测试用例（执行 `pytest tests/` 无报错）。
4. 提交代码前运行 `scripts/check_env.py` 确认本地环境通过所有依赖检查，并执行 `scripts/tree_printer.py` 更新项目结构注释（如有目录变更）。
5. 发起 Pull Request 至主仓库的 `main` 分支，在 PR 描述中清晰说明改动目的、影响范围及测试结果，等待维护者审核。

## 常见问题

**问：运行 generate_links.py 时提示 YAML 解析错误，如何定位？**
答：该错误通常由 `data/links.yaml` 中的缩进不一致或非法字符引起。可使用 `python -c "import yaml; yaml.safe_load(open('data/links.yaml'))"` 快速校验语法，并检查是否混用了 Tab 与空格。建议使用支持 YAML 的编辑器（如 VS Code 搭配 YAML 插件）开启格式化校验。

**问：预检脚本 validate_urls.py 报告部分域名无法解析，是否影响正常使用？**
答：该预检仅作辅助参考，用于提醒维护者注意可能失效的链接。若域名确实有效但解析受本地网络限制（如防火墙或 DNS 污染），可在脚本参数中添加 `--skip-dns` 跳过解析检查，仅执行正则格式校验。资源列表本身为静态记录，不会因预检失败而删除条目。

**问：如何将现有浏览器书签批量导入本项目？**
答：目前项目未提供直接浏览器导入功能，但可手动将书签导出为 HTML 格式，再使用 Python 的 `BeautifulSoup` 解析提取 URL 与标题，按 `links.yaml` 的格式写入。建议编写一次性转换脚本并放置于 `scripts/contrib/` 目录下，未来版本可能集成该辅助工具。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:02:13
