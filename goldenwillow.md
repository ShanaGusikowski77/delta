# WSNav 开源外链资源聚合平台

WSNav 是一个面向技术社区与内容创作者的轻量级外链资源导航与聚合系统。项目定位为可自部署的资源目录站，帮助个人或团队将分散于多个域名的视频流媒体、直播平台、创作者资源库统一纳入可维护的导航体系。目标用户包括开源社区文档维护者、内容聚合站运营者以及需要快速整理外部资源入口的开发人员。通过结构化数据与静态页面生成机制，WSNav 解决多源外链管理混乱、链接失效不可追踪、资源分类缺乏层级等问题，提供一套基于 Markdown 配置驱动的资源目录渲染方案。

## 功能概览

- **多级分类目录系统** 支持无限层级的资源分类与子分类，便于按主题、地区、语言或内容类型组织外链。
- **外链健康状态检查** 内置定时任务对已收录链接进行 HTTP 状态码探测，自动标记失效或重定向链接。
- **资源标签与全文检索** 为每条外链添加自定义标签，并支持标题、描述、标签组合检索，快速定位目标资源。
- **访问统计与点击排行** 记录每个外链的点击次数，按日、周、月维度生成热门资源排行榜。
- **管理员后台即时编辑** 提供 Web 管理界面，支持在线增删改资源条目、批量导入导出 CSV 格式链接库。
- **响应式前端模板** 基于 CSS Flexbox 与 Grid 布局，适配桌面端与移动端浏览器，保证不同设备下的浏览体验。
- **RSS 订阅源生成** 为每个分类目录自动生成 RSS 订阅链接，方便用户跟进特定领域资源更新。
- **数据备份与恢复接口** 提供命令行工具，支持将全部资源数据导出为 JSON 文件，并可从 JSON 文件恢复数据。

## 应用场景

- **技术文档站的外链附录** 开源项目文档站点可使用 WSNav 单独部署一个资源导航页，集中存放项目依赖的外部参考链接、视频教程地址、社区直播录播资源，避免文档正文被大量外链干扰。
- **内容创作者个人资源库** 视频创作者或直播运营者可将多个平台的个人主页、往期录播存档、合作推广链接通过 WSNav 统一归档，生成对外分享的资源门户。
- **社区维基的补充工具** 技术社区可将其 Wiki 中冗余的“相关链接”章节迁移至 WSNav，利用其分类和检索能力提升外链的可发现性，同时减轻 Wiki 页面的维护负担。
- **企业内部知识库外链管理** 企业技术团队可将常用的第三方库文档、API 参考、设计规范、培训视频等外部资源通过 WSNav 集中管理，避免员工自行收藏导致链接版本混乱。
- **活动专题页快速搭建** 针对线上技术沙龙或黑客松活动，运营人员可在数分钟内通过 WSNav 建立包含直播入口、嘉宾资料、回放视频、报名链接的专题导航页，活动结束后可保留为历史归档。

## 快速开始

以下命令适用于 Linux / macOS / Windows WSL 环境，请确保已安装 Git 与 Node.js 18.x 及以上版本。

```bash
# 克隆项目仓库
git clone https://github.com/wsnav/wsnav-core.git
cd wsnav-core

# 安装项目依赖
npm install

# 以开发模式启动本地服务
npm run dev
```

执行完毕后，访问终端输出的本地地址（默认为 http://localhost:3000）即可查看示例资源目录。如需构建生产环境静态文件，请使用 `npm run build` 命令。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | 18.x 或更高 | 运行时环境，用于执行构建脚本与开发服务器 |
| npm | 9.x 或更高 | 包管理器，用于安装项目依赖 |
| SQLite3 | 系统自带或自动安装 | 轻量级嵌入式数据库，用于存储资源条目与统计数据 |
| Git | 2.x 或更高 | 版本控制工具，用于克隆仓库及后续更新 |
| 操作系统 | Linux / macOS / Windows (WSL2) | 支持主流操作系统，Windows 下建议使用 WSL2 以获得最佳性能 |

## 文档导航

| 层面 | 目录 | 回答的问题 |
|------|------|------------|
| 入门指南 | docs/getting-started.md | 如何安装部署、首次启动、初始化示例数据？ |
| 配置说明 | docs/configuration.md | 如何修改站点名称、分类体系、页面模板？ |
| 管理手册 | docs/admin-guide.md | 如何通过后台管理界面添加、编辑、删除资源？ |
| 开发参考 | docs/development.md | 如何二次开发、扩展新功能、提交合并请求？ |
| 部署运维 | docs/deployment.md | 如何将项目部署到生产服务器、设置反向代理？ |
| API 文档 | docs/api-reference.md | 前端如何调用后端接口获取分类和资源数据？ |

## 资源列表

本平台收录的资源分为多个类别，便于用户按主题浏览。所有条目均按照原始来源原样列出，未作任何修改。

直播平台分类

- <code>wufuyewanghongzhibow.org.cn</code>
- <code>wufuyemeinvzhibow.org.cn</code>
- <code>meinvwufuyiezhibow.org.cn</code>

娱乐内容分类

- <code>shuaigefujifulizhibow.org.cn</code>

综合观看分类

- <code>oubazhibomianfeiguankanw.org.cn</code>
- <code>wanghongzhibofulizaixianw.org.cn</code>

视频资源分类

- <code>nvzhubozshipinzaixianguankanw.org.cn</code>

以上链接均以裸域名形式收录，未添加任何协议前缀。用户可根据自身网络环境选择 HTTP 或 HTTPS 访问，平台仅提供导航功能，不对第三方内容负责。

## 项目结构

```
wsnav-core/
├── src/                           # 核心源代码目录
│   ├── server/                    # 服务端逻辑（Express 路由、数据库操作）
│   │   ├── routes/                # API 路由定义（分类、资源、统计）
│   │   ├── models/                # 数据模型层（SQLite ORM 映射）
│   │   └── middleware/            # 请求中间件（日志、鉴权、错误处理）
│   ├── client/                    # 前端资源目录
│   │   ├── templates/             # EJS 模板文件（首页、分类页、详情页）
│   │   ├── static/                # 静态资源（CSS 样式、JavaScript 脚本、图片）
│   │   └── assets/                # 可复用的前端组件（搜索框、分页器、卡片）
│   ├── lib/                       # 公共工具函数（链接状态检测、RSS 生成）
│   ├── config/                    # 配置文件目录（站点设置、默认分类）
│   └── cli/                       # 命令行工具入口（数据导出导入、初始化）
├── data/                          # 数据存储目录
│   ├── database/                  # SQLite 数据库文件存放位置
│   └── backups/                   # 自动备份生成的 JSON 文件
├── docs/                          # 完整项目文档（见上文文档导航）
├── tests/                         # 单元测试与集成测试用例
├── scripts/                       # 辅助脚本（开发环境搭建、部署辅助）
├── .env.example                   # 环境变量配置示例文件
├── package.json                   # 项目依赖与脚本定义
├── README.md                      # 本文件
└── LICENSE                        # MIT 许可证文件
```

## 贡献指南

1. 阅读项目行为准则与贡献者公约，确认同意后可在 GitHub 仓库中 fork 项目并创建个人开发分支。
2. 在本地环境中运行测试用例确保现有功能完整，使用 `npm run test` 命令执行所有测试。
3. 提交代码前请运行代码格式化工具（`npm run format`）并确保新代码包含相应的单元测试。
4. 发起 Pull Request 时请清晰描述修改内容、关联 Issue 编号以及手动测试的结果截图或日志。
5. 如涉及新增依赖包或修改数据库结构，请在 PR 说明中详细解释必要性并提供回滚方案。

## 常见问题

Q: 项目启动后访问页面空白，控制台显示无法连接到数据库文件。
A: 请检查 data/database 目录是否存在且具有写入权限。若为首次启动，可尝试执行 `npm run init-db` 命令初始化数据库文件及默认分类数据。

Q: 外链健康状态检查功能报告大量链接超时，但浏览器中可正常访问。
A: 检查功能默认使用 HEAD 请求方法，部分服务器可能拒绝响应 HEAD 请求。可在配置文件中将检查方法切换为 GET，并设置较长的超时阈值（默认 5000 毫秒）。

Q: 如何将已有的大量资源链接批量导入系统？
A: 按系统要求的 CSV 格式（列：分类名称、资源标题、URL、描述、标签）准备文件，然后在管理后台的“导入”功能中上传。也可使用命令行工具 `npm run import -- --file=your_data.csv` 完成批量导入。

## 许可证

MIT License

Copyright (c) 2026 WSNav Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
