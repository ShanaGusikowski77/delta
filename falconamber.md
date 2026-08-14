# Terminus Tech Resource Hub

Terminus Tech Resource Hub 是一个面向技术内容创作者、流媒体运维工程师及实时数据服务开发者的外链资源导航与聚合系统。该项目不直接存储或托管任何视频流、比赛数据或用户生成内容，而是提供一套结构化的外链分类框架、访问合规性检查工具与资源可用性探测模块，帮助用户从海量公开网络资源中快速定位可用服务端点。

项目目标用户为需要频繁切换流媒体源地址的运维人员、搭建体育数据看板的开发者，以及研究网络资源生命周期管理的技术爱好者。通过本系统，用户可降低重复检索成本，规避因源地址变更导致的业务中断，同时获得一套可私有化部署的资源索引管理方案。

## 功能概览

- 外链分类引擎：系统内置多级分类标签，支持按内容类型、服务商、可用区域与协议版本对原始 URL 进行标记与分组，便于后续自动化处理。

- 可用性探测看板：集成轻量级 HTTP/HTTPS 探活模块，定时检测已收录资源路径的响应状态码与首字节时间，并在 Web 界面中以红黄绿灯形式可视化呈现。

- 黑名单与冗余过滤：支持自定义正则规则，自动剔除已失效、频繁超时或返回非预期 Content-Type 的链接，降低用户人工筛选负担。

- 一键导出结构化清单：提供 JSON、CSV 与纯文本三种格式的导出接口，方便用户将筛选后的资源列表导入其他监控系统或播放器配置文件。

- 私有化部署支持：项目完全基于静态文件与浏览器端 JavaScript 构建，无外部数据库依赖，用户可下载源码后在内网环境一键运行。

- 变更历史追溯：每次外链库更新均生成差异报告，记录新增、移除与状态变化的条目，便于审计与回滚。

- 响应式管理界面：适配桌面与平板设备，提供搜索、筛选、排序与批量标签编辑能力，提升日常维护效率。

## 应用场景

- 流媒体源地址日常巡检：运维人员每日通过看板检查收录的外链响应情况，及时发现不可用节点并手动替换或标记下线，保障内部播放服务稳定性。

- 体育数据看板快速原型开发：前端开发者在构建比分展示页面时，使用本项目导出的 JSON 清单作为临时数据源，无需自行爬取或维护测试端点，加速原型验证。

- 网络资源生命周期研究：学术研究人员利用本系统积累的变更历史与可用性日志，分析公共流媒体或数据服务域名的存活周期、迁移规律与常见故障模式。

- 内网资源索引建设：企业或学校内部团队下载本项目后，将原有内部服务地址按相同分类结构录入，快速搭建部门级资源导航页，替代混乱的共享文档。

- 自动化运维脚本集成：DevOps 工程师通过命令行调用导出接口，将可用外链列表注入容器环境变量或配置中心，实现服务发现配置的自动更新。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL 环境，需提前安装 Git 与 Node.js 16+。

```bash
# 克隆项目仓库
git clone https://github.com/terminus-tech/resource-hub.git
cd resource-hub

# 安装依赖（仅用于本地开发服务器与构建工具）
npm install

# 启动开发模式，默认监听 8080 端口
npm run dev
```

启动后，在浏览器中访问 `http://127.0.0.1:8080` 即可看到资源管理界面。若仅需使用静态资源索引功能，可直接将 `public` 目录下的所有文件复制到任意 HTTP 服务器根目录。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 16.x 或 18.x LTS | 用于运行开发服务器、执行构建脚本与单元测试 |
| npm | 8.x 或 9.x | 依赖包管理工具，随 Node.js 一同安装 |
| Git | 2.30+ | 用于克隆仓库及版本管理，非运行时强制依赖 |
| 现代浏览器 | Chrome 90+ / Firefox 88+ / Edge 90+ | 管理界面基于 ES2020 与 CSS Grid 构建 |
| 网络连通性 | 可变 | 探活功能需目标外链可达，但系统本身离线可用 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 用户手册 | `/docs/user-guide.md` | 如何添加新链接、批量编辑标签、导出清单及解读可用性看板 |
| 运维参考 | `/docs/operations.md` | 如何调整探测超时阈值、配置黑名单规则、备份变更历史 |
| 开发者指南 | `/docs/developer.md` | 项目目录结构说明、核心 API 设计、如何扩展分类引擎与探测模块 |
| 部署手册 | `/docs/deployment.md` | 如何将项目部署到 Nginx、Caddy 或云存储桶，以及 HTTPS 配置建议 |

## 资源列表

### 流媒体与直播类

- <code>zaixianbofangzhubow.org.cn</code>
- <code>zhubozhibozaixianguankanw.org.cn</code>

### 实时比分数据类

- <code>zuqiujishibifend.org.cn</code>
- <code>zuqiujishibifene.org.cn</code>
- <code>zuqiujishibifenf.org.cn</code>
- <code>zuqiujishibifeng.org.cn</code>
- <code>zuqiujishibifenh.org.cn</code>

## 项目结构

```
resource-hub/
├── public/                         # 静态资源根目录，可直接部署
│   ├── index.html                  # 主管理界面 HTML 入口
│   ├── css/
│   │   ├── base.css                # 全局基础样式与 CSS 变量
│   │   └── dashboard.css           # 看板专用布局与卡片样式
│   ├── js/
│   │   ├── app.js                  # 前端主控制器，负责路由与状态管理
│   │   ├── probe-worker.js         # 探活模块的 Web Worker 实现
│   │   └── export-handler.js       # 导出 JSON/CSV/TXT 的逻辑
│   └── assets/
│       └── default-avatar.svg      # 未分类链接的占位图标
├── src/                            # 源代码目录，含构建与测试脚本
│   ├── core/
│   │   ├── classifier.js           # 外链接收与标签分类引擎
│   │   ├── validator.js            # URL 格式校验与协议规范化
│   │   └── history.js              # 变更记录生成与差异对比工具
│   ├── probes/
│   │   ├── http-probe.js           # 基于 fetch 的 HTTP 探测实现
│   │   └── probe-scheduler.js      # 定时任务调度与并发控制
│   └── utils/
│       ├── storage.js              # LocalStorage 读写与数据迁移
│       └── logger.js               # 分级日志输出（debug/info/error）
├── tests/                          # 单元测试与集成测试
│   ├── classifier.test.js
│   ├── probe.test.js
│   └── fixtures/
│       └── sample-links.json       # 测试用固定外链样本集
├── scripts/                        # 构建与运维辅助脚本
│   ├── build-static.js             # 打包 public 目录用于生产
│   └── seed-data.js                # 初次运行时注入初始外链样本
├── docs/                           # 完整文档（参见文档导航章节）
├── .github/
│   └── workflows/
│       └── ci.yml                  # GitHub Actions 持续集成配置
├── package.json                    # npm 依赖与脚本定义
├── README.md                       # 本文件
└── LICENSE                         # MIT 许可证文本
```

## 贡献指南

1. 查阅 issue 列表或创建新 issue 描述您希望改进的功能或修复的问题，等待维护者确认需求合理性。

2. Fork 本仓库，在您的个人分支上进行代码修改。提交前请运行 `npm run lint` 与 `npm run test` 确保代码风格与现有逻辑兼容。

3. 若涉及新增外链分类规则或探活参数，需同步更新 `/docs` 下对应的用户手册或运维文档，并补充至少一条单元测试用例。

4. 提交 Pull Request 时请引用相关 issue 编号，并在描述中清晰说明变更内容、测试覆盖情况以及对外链处理逻辑的影响范围。

5. 维护者将在 3 个工作日内进行 Code Review，必要时会提出修改意见。合并后您的贡献将出现在下一版本的变更日志中。

## 常见问题

Q: 项目是否存储或缓存外链指向的实际内容，例如视频流或比赛数据？

A: 不存储。本项目仅记录 URL 字符串及其元数据（标签、添加时间、最近探测状态）。所有探测行为仅发送 HTTP HEAD 或 GET 请求并记录响应头与状态码，不下载响应体。用户需遵守相关外链服务商的使用条款。

Q: 如何批量导入已有的大量外链地址？

A: 在管理界面中点击“批量导入”按钮，上传符合格式要求的 CSV 文件（列标题为 url, category, tags）。您也可以直接编辑浏览器开发者工具中的 LocalStorage 数据，但推荐使用导入功能以避免格式错误。

Q: 探活结果出现大量超时或误报，如何调整？

A: 您可在 `src/probes/probe-scheduler.js` 中调整 `TIMEOUT_MS`（默认 5000 毫秒）与 `RETRY_TIMES`（默认 2 次）变量，或通过运维文档中说明的环境变量 `PROBE_TIMEOUT` 与 `PROBE_RETRY` 在启动时覆盖。对于频繁变动的域名，建议将探测间隔从默认 10 分钟延长至 30 分钟以上。

## 许可证

MIT

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
