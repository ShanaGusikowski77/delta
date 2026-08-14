# OpenResource Hub

OpenResource Hub 是一个面向技术开发者与内容研究者的高质量外链资源聚合平台，专注于对中文网络环境中可公开访问的视频素材库、字幕资源站与在线影音资料源进行系统化编目与导航。项目定位为技术型资源索引工具，而非内容托管平台，其核心目标用户包括自然语言处理研究人员、多媒体内容分析工程师、数据标注团队负责人以及开源社区文档贡献者。通过构建结构化的资源分类框架与可复用的链接校验逻辑，OpenResource Hub 有效解决了分散资源难以定位、链接可用性不可知、站点归属关系不清晰等实际问题，为技术工作流中的资料采集环节提供确定性支持。

项目本身不存储、不修改、不转发任何第三方内容，仅提供公开 URL 的元信息整理与可访问性标注，所有资源链接均保持原始出处，用户通过本项目获取的链接访问行为均受目标站点自身服务条款约束。OpenResource Hub 遵循最小化信息处理原则，不收集用户访问记录，不嵌入追踪脚本，不设置用户行为分析模块，以确保资源导航行为的中立性与合规性。

## 功能概览

- **多源链接统一编目** 对输入的原始 URL 进行标准化识别与分类标注，自动区分视频内容站、字幕资源站、在线播放站等不同类型，并生成对应的分类标签与简要说明，便于用户按需筛选。

- **可访问性状态标记** 集成轻量级链接存活检测机制，定期对收录资源进行 HTTP 状态码检查，并在索引中标注可访问状态与最近检测时间，帮助用户规避失效链接。

- **站点归属关系追踪** 针对域名结构相似的资源站，自动提取域名核心字段并生成关联图谱，提示可能存在的站点集群或镜像关系，为批量采集策略提供参考依据。

- **结构化元数据导出** 支持将资源列表以 JSON、CSV、Markdown Table 三种格式导出，方便用户导入数据采集流水线、标注工具配置或文档自动化生成流程。

- **自定义标签与备注系统** 允许用户对每个资源链接添加自定义标签（如"需代理访问""非中文界面""高码率源"）和备注文本，并支持本地持久化存储，满足个性化整理需求。

- **链接变更历史记录** 对每个收录 URL 保留最近三次的可用性变化记录（包括首次收录时间、状态变更时间、变更前后状态），为资源稳定性分析提供基础数据。

- **关键词全文检索** 基于标题、域名、分类标签、用户备注等字段构建简单倒排索引，支持多关键词组合查询，响应时间控制在 200 毫秒以内，适用于百级数量资源库的快速定位。

## 应用场景

- **NLP 语料采集前的资源盘点** 研究团队在启动中文视频字幕语料采集项目前，可使用 OpenResource Hub 快速浏览已收录的字幕资源站点分布情况，结合可访问性标记筛选出高可用性来源，减少人工逐个验证的重复劳动。

- **多媒体内容分析任务的样本来源规划** 从事视频内容分类、场景识别或文字检测算法研发的工程师，可通过本项目的分类标签快速定位视频素材类资源站，并根据站点归属关系信息评估来源多样性，为训练集构建提供可靠的数据来源清单。

- **数据标注外包团队的标准化交接** 标注项目管理人员可将 OpenResource Hub 导出的资源清单直接作为交付物附件提供给外包团队，附带可访问性状态与备注说明，确保标注人员使用的资料源一致且有效，降低因链接差异导致的标注偏差风险。

- **开源文档与教程的参考资料维护** 技术博客作者或开源项目维护者在编写涉及中文在线资源引用的文档时，可引用 OpenResource Hub 中持续更新的资源列表作为附录，避免文档中直接嵌入大量不易维护的裸链接，提升文档的长期可读性与可信度。

- **个人技术笔记的知识沉淀辅助** 开发者在日常浏览过程中积累的视频源或字幕站链接，可通过本项目的自定义标签与备注系统进行统一收纳，并结合链接变更历史记录及时感知资源变动，构建个人化的高质量外链知识库。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，确保系统已安装 Git 与 Python 3.9 及以上版本。

```bash
# 1. 克隆项目仓库
git clone https://github.com/open-resource-hub/openhub.git
cd openhub

# 2. 安装依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate     # Windows 下使用 venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt

# 3. 运行本地索引服务（默认监听 127.0.0.1:8080）
python app.py --port 8080 --no-browser
```

启动成功后，在浏览器中访问 `http://127.0.0.1:8080` 即可查看本地资源索引面板。首次启动将自动载入内置的资源清单，完整列表同步生成于 `data/resources.json` 文件中，用户可直接编辑该文件进行增删改操作，服务会自动热加载变更内容。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9 - 3.12 | 核心运行环境，低于 3.9 版本将不兼容类型注解语法 |
| Git | 2.25 及以上 | 用于克隆仓库和后续版本更新拉取 |
| pip | 21.0 及以上 | Python 包管理器，用于安装 requirements 中声明的依赖 |
| Flask | 2.2.5 | 轻量级 Web 框架，提供索引面板与 API 端点 |
| requests | 2.28.0 | 用于链接可访问性检测的 HTTP 请求库 |
| pytest | 7.2.0（可选） | 仅运行单元测试时需要，生产环境可不安装 |
| 磁盘空间 | 至少 50 MB | 用于存储资源索引 JSON 文件与日志记录，不含任何视频或字幕实体文件 |
| 内存 | 最低 256 MB | 服务运行内存占用约为 80 - 120 MB，视资源条目数量略有浮动 |
| 网络 | 出站可访问公网 | 仅可访问性检测功能需要外网权限，纯本地索引浏览无需网络 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|---|---|---|
| 用户指南 | docs/user-guide.md | 如何使用索引面板进行分类筛选、关键词检索和自定义标签添加；如何导出不同格式的资源清单 |
| 运维手册 | docs/operation.md | 如何部署到生产服务器；如何配置定期链接检测任务；如何备份和恢复用户自定义数据 |
| 开发者文档 | docs/developer.md | 项目代码结构说明；新增资源分类的扩展方法；API 端点定义与单元测试编写规范 |
| 资源编目规范 | docs/catalog-spec.md | 链接分类的判定标准；域名归属关系的识别逻辑；备注字段的推荐用语与缩写规则 |
| 常见问题汇总 | docs/faq.md | 链接状态检测的误报处理；自定义标签的导入导出方式；索引服务启动失败的可能原因排查 |
| 版本更新记录 | CHANGELOG.md | 每个版本新增的资源条目、修复的链接检测逻辑、以及界面交互优化明细 |

## 资源列表

以下为项目当前收录的全部外链资源，按站点类型分为三个子类别。所有 URL 均严格保持用户原始输入格式，未作任何协议补全、域名改写或路径调整。

视频素材与在线观看类

- <code>guochanjingpinzaixianmianfeikanb.org.cn</code>
- <code>mianfeiguankanzaixianguankanb.org.cn</code>
- <code>jiujiushipinzaixianguankanb.org.cn</code>

中文字幕资源类

- <code>renqixiliezhongwenzimuw.org.cn</code>
- <code>rihanmeinvzhongwenzimu.org.cn</code>
- <code>qingqingcaoyuanzhongwenzimu.org.cn</code>
- <code>zhongwenzimuzaixianyingshiyuanb.org.cn</code>

以上资源链接均源自公开可访问的域名，OpenResource Hub 不对链接指向内容的合法性、时效性及可用性作任何明示或暗示的保证，用户访问相关链接时应自行查阅对应站点的服务协议与免责声明。

## 项目结构

```bash
openhub/
├── app.py                      # Flask 应用主入口，注册路由与启动服务
├── requirements.txt            # 生产环境 Python 依赖清单
├── config/
│   ├── settings.py             # 应用配置项（端口、检测间隔、日志级别）
│   └── resource_schema.json    # 资源条目的 JSON Schema 校验规则
├── data/
│   ├── resources.json          # 核心资源索引存储文件，可手动编辑
│   └── history/                # 链接变更历史归档目录，按月份分文件
│       └── 2026-08.json
├── core/
│   ├── __init__.py
│   ├── checker.py              # 链接可访问性检测模块，封装 requests 超时与重试逻辑
│   ├── parser.py               # URL 分类解析与域名特征提取函数
│   └── exporter.py             # JSON / CSV / Markdown 导出格式转换器
├── web/
│   ├── static/                 # 前端静态资源（CSS 样式、JavaScript 交互脚本）
│   │   ├── style.css
│   │   └── dashboard.js
│   └── templates/
│       └── index.html          # 资源索引面板主页面模板
├── tests/
│   ├── test_checker.py         # 可访问性检测功能的单元测试用例
│   ├── test_parser.py          # URL 解析功能的边界条件测试
│   └── test_exporter.py        # 导出格式正确性与完整性测试
├── docs/                       # 完整文档目录，内容参见上方文档导航表格
│   ├── user-guide.md
│   ├── operation.md
│   ├── developer.md
│   └── catalog-spec.md
└── scripts/
    ├── bootstrap.sh            # 首次部署时的环境初始化脚本（创建虚拟环境、安装依赖）
    └── cron_daily_check.py     # 每日定时检测脚本，可由 crontab 调用执行
```

## 贡献指南

欢迎社区开发者参与 OpenResource Hub 的改进与维护，所有贡献需遵守以下流程，以确保索引数据的准确性与代码的稳定性。

1. **提交资源新增或变更请求**：若需新增或修改资源链接，请通过 GitHub Issues 提交申请，并附上资源站点的简要说明、分类建议以及至少两次不同时间点的可访问性测试结果，便于维护团队评估其纳入索引的合理性。

2. **代码贡献分支流程**：修复 Bug 或新增功能时，请先 fork 主仓库至个人账户，在 dev 分支上进行开发，所有提交信息需遵循 Conventional Commits 规范（如 `fix: 修复 parser 模块对裸域名处理异常`），开发完成后向主仓库的 main 分支发起 Pull Request。

3. **单元测试覆盖要求**：所有针对 `core/` 目录下核心模块的代码变更，必须同步编写或更新对应的单元测试用例，并确保 `pytest` 执行后全部测试通过，测试覆盖率不得低于 85%。

4. **文档同步更新**：新增功能或修改用户可见行为后，需同步更新 `docs/` 目录下的对应文档以及 `CHANGELOG.md` 中的版本记录，避免文档与实现脱节。

5. **资源列表维护规则**：直接编辑 `data/resources.json` 的 Pull Request 需额外说明每个 URL 的收录理由及验证方式，维护人员将进行人工复核，确认无误后方可合并。

## 常见问题

**问：项目内置的资源链接检测状态显示为不可达，但我在浏览器中可以正常访问，是什么原因？**

答：可访问性检测模块默认使用无状态的 HTTP GET 请求，且设置了 5 秒超时限制，不携带任何 Cookie 或 Referer 头，也不执行 JavaScript 重定向逻辑。若目标站点依赖特定的浏览器环境、用户代理字符串或交互式验证码，则检测结果可能为假阴性。您可在 `config/settings.py` 中调整 `USER_AGENT` 和 `TIMEOUT` 参数，或直接在 `data/resources.json` 中手动修改对应条目的 `status` 字段为 `"reachable"`，系统将在下次检测周期保留该手动覆盖值。

**问：我添加的自定义标签和备注信息存储在何处？更换设备后如何迁移？**

答：所有用户自定义数据（标签、备注、手动状态覆盖）均保存在 `data/resources.json` 文件中的 `custom` 字段下，与核心资源列表同文件存储。迁移时只需将整个 `data/` 目录复制至新设备的项目根目录下即可。若使用 Docker 部署，建议将 `data/` 目录挂载为外部卷以便持久化。

**问：项目能否支持新增的资源链接自动抓取网站标题和描述信息？**

答：当前版本不提供自动抓取功能，因为自动抓取涉及对第三方网站内容的主动请求，存在法律合规风险且可能增加目标站点的服务器负担。用户可通过自定义备注字段手动记录站点的标题和简要描述，项目提供的 `parser.py` 模块仅对域名结构进行本地字符分析，不发出任何外网请求。若您有批量导入需求，建议先通过外部工具获取站点信息，再按 `resource_schema.json` 定义的格式批量写入 `resources.json`。

## 许可证

MIT License

Copyright (c) 2026 OpenResource Hub Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
