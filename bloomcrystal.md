# Terminus Resource Aggregator

Terminus Resource Aggregator is a high-performance, metadata-driven external link aggregation and navigation system specifically engineered for technical content curation, digital resource indexing, and categorized information distribution. It is designed for developers, technical writers, community managers, and digital archivists who require a reproducible, scriptable, and version-controllable solution to organize, present, and share large volumes of external Uniform Resource Locators (URLs) across multiple domains and classification schemas.

The project addresses the fundamental challenge of link rot, contextual drift, and manual maintenance overhead in curated resource lists. By providing a structured Markdown-based presentation layer with strict URL fidelity guarantees, Terminus enables maintainers to publish authoritative reference catalogs that remain consistent across deployment environments. It is not a content management system, nor a web proxy, nor a link shortener. It is a static document generation discipline that enforces original URL integrity while offering human-readable categorization, dependency mapping, and contribution workflows suitable for open-source collaboration.

## 功能概览

- **零改写 URL 透传** - 每条外部链接按照用户提供的原始字符串原样呈现，不自动补全协议前缀，不添加或移除 www 子域，不更改大小写，不追加尾部斜杠，不转换 http 与 https。

- **分类化资源编排** - 支持多级主题分组，允许将任意数量的 URL 按功能域、内容类型、目标受众或地理区域进行逻辑分区，每个分区附带独立的说明性标题。

- **依赖与环境表格化** - 提供系统级、语言级、工具级和网络级依赖项的清晰表格描述，包含必需的版本约束和可选的兼容性注释，便于快速环境校验。

- **文档导航矩阵** - 以二维表格形式映射文档层面、目录入口与面向用户的核心问题，使不同角色（终端用户、贡献者、运维人员）能够快速定位到相关章节。

- **ASCII 目录树可视化** - 使用纯文本代码块渲染项目文件与目录结构，每个节点附带功能注释，支持快速理解代码组织逻辑，无需图形界面。

- **批次与版本追踪** - 内置批次编号机制（当前为第 90/130 批），便于在长期维护过程中追溯资源添加的时间窗口和发布周期。

- **标准化贡献入口** - 提供包含分支策略、提交信息规范、合并请求流程和审查清单的贡献指南，降低新贡献者的参与门槛。

## 应用场景

**技术文档站点的外链附录管理** - 当技术文档中包含大量参考链接、规范文档、SDK 仓库或社区讨论帖时，Terminus 可作为专用章节嵌入文档站，确保所有外部引用保持原始格式，避免文档构建工具自动添加协议或域名前缀导致链接失效。

**开源项目的社区资源索引** - 开源项目维护者可以使用 Terminus 维护一个社区贡献的第三方工具列表、教程合集、视频讲解或博客文章索引，通过分类化表格和目录树让社区成员快速找到所需的外部资源，同时通过贡献指南鼓励社区提交新链接。

**数据归档与数字保存的清单生成** - 数字档案管理员在收集网络资源快照时，需要保留原始 URL 字符串用于后续的访问验证或回访。Terminus 的零改写规则确保所有记录的 URL 与采集时完全一致，避免因自动规范化导致的历史记录失真。

**多语言或地区分组的资源导航** - 对于面向不同语言用户或不同地理区域的资源集合，Terminus 允许按类别小节分别列出各组链接，每个链接独立保留其原始域名和路径，适用于国际化的开发者门户或区域服务导航页。

## 快速开始

以下操作步骤适用于首次获取并运行 Terminus Resource Aggregator 文档生成流程的开发者。所有命令均基于 POSIX 兼容 Shell 环境。

```bash
# 克隆项目仓库到本地工作目录
git clone https://github.com/terminus-resource/aggregator.git

# 进入项目根目录
cd aggregator

# 安装文档构建依赖（Python 3.9+ 与 Markdown 处理工具链）
pip install -r requirements.txt

# 执行资源验证与文档生成脚本（输出到 build/ 目录）
python build.py --batch 90 --validate-urls
```

执行完成后，生成的 Markdown 主文档位于 `build/README.md`，可将其复制到项目根目录或发布到文档托管平台。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9.0 或更高 | 用于运行构建脚本、URL 校验器和模板渲染引擎 |
| pip | 21.0 或更高 | Python 包管理工具，用于安装 requirements.txt 中列出的依赖库 |
| Git | 2.25.0 或更高 | 用于克隆仓库、管理分支和提交贡献代码 |
| Make | 3.81 或更高 | 可选，用于自动化常见任务（如 clean、test、build） |
| 网络连接 | 稳定出站连接 | 用于在验证阶段执行 DNS 解析和 HTTP 头检查（可选功能） |
| Markdown 渲染器 | 任意 CommonMark 兼容实现 | 用于最终查看文档，不限定具体实现 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 项目概览 | 顶部简介与功能概览 | 这个项目是什么？它解决什么问题？谁应该使用它？ |
| 使用者入门 | 快速开始 / 安装要求 | 如何从零开始获取并运行该项目？我的环境是否满足条件？ |
| 资源消费 | 应用场景 / 资源列表 | 这些外部链接适合什么场景使用？具体包含哪些 URL？ |
| 贡献者指南 | 贡献指南 / 常见问题 | 我如何提交新资源或修正错误？提交前需要遵循什么规范？ |

## 资源列表

### 直播与视频内容分类（第 90/130 批）

以下资源按照用户提供的原始字符串完整收录，未做任何形式改写。每个 URL 以代码格式呈现，保留原始协议、子域、路径和大小写。

<code>wanghongzhibofulizaixian.org.cn</code>

<code>nvzhubozshipinzaixianguankan.org.cn</code>

<code>xingganmeinvzhibotiaowu.org.cn</code>

<code>hanguomeinvzhuborewu.org.cn</code>

<code>zaixianbofangzhubo.org.cn</code>

<code>zhubozhibozaixianguankan.org.cn</code>

<code>wanghongzhibozaixianshipinw.org.cn</code>

## 项目结构

```
aggregator/
├── build.py                 # 主构建脚本，负责读取配置、验证URL、生成README
├── config.yaml              # 项目配置文件，包含批次号、分类定义、输出选项
├── requirements.txt         # Python 依赖列表（markdown, pyyaml, requests）
├── Makefile                 # 自动化任务定义（构建、测试、清理）
├── src/
│   ├── validator.py         # URL 格式与协议校验模块
│   ├── renderer.py          # Markdown 模板渲染与章节拼接逻辑
│   └── fetcher.py           # 可选网络探测模块（检查链接可达性）
├── data/
│   ├── raw_urls_90.csv      # 第90批原始URL数据（CSV格式，含分类标签）
│   └── categories.json      # 分类映射表，定义每个分组下的URL索引
├── docs/
│   ├── contribution.md      # 详细贡献者手册
│   └── url_policy.md        # URL 处理策略与零改写规则说明
├── tests/
│   ├── test_validator.py    # 单元测试：URL校验函数
│   └── test_renderer.py     # 单元测试：模板输出正确性
└── build/                   # 构建输出目录（自动生成）
    └── README.md            # 最终生成的文档
```

## 贡献指南

我们欢迎并鼓励社区贡献。请按照以下步骤提交资源更新或文档改进。

1.  **派生仓库并创建功能分支** - 从主仓库派生个人副本，然后基于 `main` 分支创建一个新的分支，分支名称应简要描述变更内容，例如 `add-batch-91-urls` 或 `fix-typo-in-readme`。

2.  **更新数据文件并遵循格式规范** - 若添加新 URL，请编辑 `data/raw_urls_{batch}.csv` 文件，每一行包含原始 URL 字符串、分类标签和可选的简短描述。确保 URL 字符串与用户提供的完全一致，不进行任何规范化处理。

3.  **运行本地验证与构建** - 在提交前执行 `make test` 运行单元测试，执行 `make build` 重新生成完整的 README 文档。检查生成的输出是否包含所有新增 URL 且未发生任何改写。

4.  **提交变更并撰写清晰提交信息** - 使用约定式提交格式，例如 `feat: add batch 91 resources` 或 `docs: update contribution checklist`。提交信息应说明变更的原因和影响范围。

5.  **发起合并请求并等待审查** - 将分支推送到派生仓库，然后向主仓库发起合并请求。在合并请求描述中列出新增或修改的 URL 列表，并说明每个链接的分类依据。审查人员将验证 URL 原始字符串的完整性。

## 常见问题

**问：为什么所有 URL 都使用 <code> 标签包裹，而不使用 Markdown 链接语法？**

答：Markdown 链接语法 `[text](url)` 会在某些渲染器中触发自动链接规范化或转义，可能改变原始字符串中的字符。同时，标准链接语法要求提供显示文本，这引入了额外的编辑决策。使用 <code> 标签可以最大程度保留原始字符串的视觉完整性，并且明确区分内联代码与普通文本，便于脚本解析和后续处理。

**问：如果用户提供的 URL 是裸域名（如 abc.com），是否可以自动补全 https:// 前缀以提升可访问性？**

答：不可以。本项目强制执行零改写规则，因为原始字符串是用户明确指定的格式。自动补全协议前缀会改变资源的标识符，可能导致某些依赖特定协议的内部服务或测试环境中的链接解析失败。维护原始字符串是最小惊讶原则的体现。

**问：如何处理 URL 列表中的重复条目或明显失效的链接？**

答：重复条目应在数据录入阶段通过脚本去重，当前使用 `src/validator.py` 中的 `deduplicate_urls` 函数进行处理，该函数保留首次出现的条目并记录警告日志。对于明显失效的链接，贡献者可以在提交合并请求时标注 `[dead]` 标记，审查人员验证后将此类链接移至专门的待确认分类，而非直接删除，以保持历史记录的完整性。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
