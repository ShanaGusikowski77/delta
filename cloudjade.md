# CNetNav

CNetNav 是一个专注于互联网公开视频与直播资源导航的开源项目，旨在通过结构化目录与人工筛选机制，帮助技术爱好者、媒体研究者及内容运营人员快速定位高可访问性的在线视频与直播内容入口。项目不提供任何视频文件、播放流或下载服务，仅收录公开可访问的网站域名，并基于站点稳定性、内容分类清晰度与访问响应速度进行分级整理。

项目目标用户包括网络爬虫开发者、数字内容分析人员、媒体监控系统维护者以及需要批量采集公开视频源信息的工程团队。CNetNav 通过统一的数据格式与定期更新的域名列表，解决了分散查找、域名失效频繁、分类混乱等常见痛点，为上层应用提供可靠的基础数据支撑。

## 功能概览

- **域名分类索引**：根据内容主题与地区来源，将收录域名划分为国产网红直播、日韩直播、福利视频、热门推荐等多个独立分类，每个分类附带简要内容特征描述。

- **可用性健康检查**：项目内置周期性域名可达性检测脚本，可输出每个域名的 HTTP 状态码、响应时间与 SSL 证书有效期，辅助运维人员判断服务可用状态。

- **原始数据导出接口**：提供 JSON、CSV 与纯文本三种格式的域名列表导出功能，便于第三方系统批量导入或与监控报警系统对接。

- **变更日志追踪**：每次更新版本均附带 CHANGELOG 文件，明确记录新增域名、移除失效域名及分类调整操作，确保数据变更可追溯。

- **标签过滤系统**：每个域名支持多标签标注，如 高清、移动适配、弹幕、无插件 等，用户可通过标签组合快速筛选符合特定技术要求的域名。

- **外部监控集成示例**：项目仓库内提供 Prometheus Exporter 示例代码，可将域名健康检查结果暴露为监控指标，方便接入现有运维监控体系。

- **社区域名提交钩子**：通过 GitHub Issue 模板与自动化标签机器人，社区成员可提交新域名推荐或失效报告，维护者定期审核并合并。

## 应用场景

- **媒体数据采集管道初始化**：数据工程团队在搭建视频元数据采集系统时，可使用 CNetNav 提供的域名列表作为起始种子集合，配合爬虫框架批量抓取公开页面信息，大幅降低入口发现成本。

- **直播平台运营竞品分析**：市场调研人员通过分类索引快速定位同类内容来源，结合可用性检测数据评估不同平台的服务稳定性与区域覆盖差异，为运营决策提供参考依据。

- **网络监控系统健康检查配置**：运维工程师可直接引用项目导出的域名清单，配置外部 HTTP 探针任务，实现对多个直播站点的可用性集中监控，异常时触发告警通知。

- **学术研究与内容趋势分析**：传播学或计算机视觉方向的研究人员可利用域名列表构建周期性采样任务，分析不同类型视频内容的编码参数、分辨率分布或弹幕密度变化趋势。

## 快速开始

以下操作适用于 Linux / macOS 环境，需提前安装 Git 与 Python 3.9 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/cnetnav/cnetnav.git
cd cnetnav

# 安装依赖（推荐使用虚拟环境）
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 执行健康检查并导出最新域名列表
python scripts/health_check.py --output-dir ./data
python scripts/export_list.py --format json --output ./dist/domains.json
```

执行上述命令后，会在 `./data` 目录下生成带时间戳的健康检查报告，并在 `./dist` 目录中获得统一格式的域名列表文件。

## 安装要求

| 依赖组件 | 必需版本 | 说明 |
|---|---|---|
| Python | 3.9+ | 核心脚本运行环境，用于健康检查与数据导出 |
| Git | 2.25+ | 克隆仓库及版本管理 |
| aiohttp | 3.8.4+ | 异步 HTTP 客户端，用于并发域名探测 |
| cryptography | 39.0.0+ | SSL 证书信息解析依赖库 |
| pandas | 1.5.0+ | 数据表格处理与 CSV 导出支持 |
| prometheus-client | 0.16.0+ | 可选依赖，仅当启用监控集成时需安装 |

## 文档导航

| 层面 | 目录/文件 | 回答的问题 |
|---|---|---|
| 用户手册 | docs/user-guide.md | 如何安装、配置、运行导出脚本与健康检查？ |
| 开发者指南 | docs/developer-guide.md | 如何提交新域名、更新分类规则或扩展导出格式？ |
| 运维参考 | docs/operations.md | 如何部署 Prometheus 集成、设置定时任务与告警阈值？ |
| 设计说明 | docs/design.md | 域名分类原则、标签体系定义及数据模型结构是怎样的？ |

## 资源列表

以下为 CNetNav 当前收录的全部域名资源，按内容类别分组呈现。所有域名均来源于公开互联网，项目仅做索引整理，不涉及任何内容分发或存储。

**国产网红直播类别**

- <code>guochanwanghongshipinzhibo.org.cn</code>
- <code>wanghongzhibomianfeiguankan.org.cn</code>
- <code>guochanwanghongfulishipin.org.cn</code>
- <code>wanghongmeinvrewuzhibo.org.cn</code>

**美女/娱乐直播类别**

- <code>meinvzhibozaixiankan.org.cn</code>

**日韩直播类别**

- <code>rihanzhibofulishipin.org.cn</code>

**热门推荐/综合类别**

- <code>rewuzhibowanghongzhibo.org.cn</code>

## 项目结构

```
cnetnav/
├── LICENSE                          # MIT 许可协议文件
├── README.md                        # 项目总览与快速入门
├── CHANGELOG.md                     # 版本变更历史记录
├── requirements.txt                 # Python 依赖声明
├── .github/                         # GitHub 社区配置目录
│   ├── ISSUE_TEMPLATE/              # Issue 提交模板（新域名/失效报告）
│   └── workflows/                   # CI 工作流（自动健康检查）
├── docs/                            # 完整文档目录
│   ├── user-guide.md                # 用户操作手册
│   ├── developer-guide.md           # 贡献者开发指引
│   ├── operations.md                # 运维部署与监控集成
│   └── design.md                    # 数据模型与分类设计
├── scripts/                         # 可执行脚本集合
│   ├── health_check.py              # 异步域名健康检查主程序
│   ├── export_list.py               # 多格式列表导出工具
│   └── prometheus_exporter.py       # Prometheus 指标暴露示例
├── data/                            # 数据目录（自动生成）
│   ├── raw/                         # 原始域名清单（按分类）
│   └── reports/                     # 健康检查报告存档
├── dist/                            # 导出文件发布目录
│   ├── domains.json                 # JSON 格式完整列表
│   ├── domains.csv                  # CSV 表格格式
│   └── domains.txt                  # 纯文本一行一个域名
├── tests/                           # 单元测试与集成测试
│   ├── test_health_check.py
│   └── test_export.py
└── config/                          # 配置文件目录
    ├── categories.yaml              # 分类定义与标签映射
    └── probes.yaml                  # 探针超时、重试等参数
```

## 贡献指南

欢迎社区开发者提交贡献，包括但不限于新增有效域名、修复失效链接、优化检测脚本或完善文档内容。

1. 查阅现有 Issue 与 Pull Request，确认无人正在处理相同问题。建议先在 Issue 区留言说明意向，避免重复劳动。

2. 从 `main` 分支创建新的特性分支，命名规范为 `feature/简述变更内容` 或 `fix/简述修复内容`。

3. 若新增域名，请同时更新 `data/raw/` 下对应分类的清单文件，并在 `config/categories.yaml` 中补充标签定义。若为脚本变更，请确保所有单元测试通过。

4. 提交前运行 `python -m pytest tests/` 验证本地测试套件，并执行 `scripts/health_check.py` 确认新增域名可正常访问。

5. 发起 Pull Request 至 `main` 分支，描述中需包含变更原因、影响范围以及测试结果截图或日志。维护者将在 3 个工作日内完成审核。

## 常见问题

**Q：CNetNav 是否提供视频播放地址或下载链接？**

A：不提供。项目仅收录域名信息，不存储、转发或指向任何具体视频文件、播放流或下载资源。所有域名均为公开可访问的网站入口，用户访问时需遵守相应站点的服务条款。

**Q：健康检查脚本检测到部分域名不可达，我该如何处理？**

A：健康检查结果仅反映脚本执行时刻的网络状况，可能受目标站点临时维护、地域网络限制或防火墙策略影响。建议多次间隔重试，若持续不可达可通过 Issue 提交失效报告，维护者核实后将移出活跃列表。

**Q：能否在商业系统中使用 CNetNav 导出的域名数据？**

A：可以。项目采用 MIT 许可证发布，允许自由使用、修改、复制和分发，包括商业用途。但需注意，域名对应的第三方网站内容与项目无关，使用者应自行评估合规风险。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
