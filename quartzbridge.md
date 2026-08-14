# NovaLink 技术导航站

NovaLink 是一个面向开发者与运维工程师的高质量技术资源聚合与导航系统，定位于将分散于各处的技术文档、社区入口、监控面板、数据看板与内部工具链接进行集中管理。项目不存储任何用户数据，不提供代理或转发服务，仅作为技术团队内部的入口级导航枢纽，解决多环境、多平台、多域名下的入口分散与记忆负担问题。

目标用户包括：后端开发工程师、前端工程师、运维工程师、SRE 团队、技术管理者以及新入职的团队成员。通过 NovaLink，用户可以在统一的界面中快速抵达各类业务后台、监控系统、日志平台、配置中心与协作工具，显著降低上下文切换成本，提升日常研发与运维效率。

## 功能概览

- **多级分类导航**：支持按业务域、技术栈、环境类型（开发/测试/预发布/生产）对链接进行分组与排序，便于不同角色快速定位所需资源。

- **快速模糊搜索**：提供全局搜索框，支持对链接标题、描述、标签及目标 URL 进行实时模糊匹配，响应时间低于 200 毫秒。

- **链接可用性健康检查**：后台定时任务每 5 分钟对已注册链接发起 HTTP HEAD 请求，自动标记不可用节点并在界面中高亮告警。

- **访问频率统计与排序**：记录每个链接的点击次数与最后访问时间，支持按热度排序，帮助团队发现高频使用的关键资源。

- **自定义标签与备注系统**：允许用户为每个链接添加自定义标签（如“只读”“敏感操作”“需VPN”）和富文本备注，便于传递使用注意事项。

- **外部链接安全跳转中间页**：对于指向非内网域名的外部链接，自动经过一个警告提示页，提醒用户注意数据安全与合规要求，降低误操作风险。

- **响应式布局与移动端适配**：基于 CSS Grid 与 Flexbox 构建，在桌面、平板与手机屏幕上均能保持良好的浏览与操作体验。

- **开放 JSON API 接口**：提供 RESTful 风格的链接数据查询接口，支持第三方监控系统或 CLI 工具批量获取导航数据，便于集成到现有工作流中。

## 应用场景

- **新员工入职环境指引**：新加入团队的开发人员可通过 NovaLink 一次性获取所有必需的后台地址、代码仓库入口、CI/CD 流水线看板以及日志查询系统，无需反复向同事询问各类域名与端口。

- **故障应急响应快速切换**：当线上服务出现异常时，运维值班人员能够通过 NovaLink 在数秒内跳转到对应的监控仪表盘、链路追踪界面和错误日志聚合平台，避免因记忆错误或收藏夹失效而延误排查时机。

- **多环境配置核对与变更验证**：在版本发布前，测试人员可借助 NovaLink 快速在开发、测试、预发布环境之间切换，验证不同环境下的配置差异，确保变更在各环境中表现一致。

- **技术文档与 API 参考聚合**：团队可将内部 Wiki、接口文档、数据库 Schema 说明、架构设计提案等链接统一收录，形成团队知识库的单一入口，减少文档散落在各处造成的查找困难。

- **外部合作伙伴权限隔离访问**：对于需要向外部供应商或合作方开放的有限资源，可通过 NovaLink 的标签与分组功能单独列出可公开访问的链接，避免泄露内部敏感系统地址。

## 快速开始

以下步骤适用于 Linux / macOS / Windows WSL2 环境，前提是已安装 Git、Node.js（v18 或以上）及 npm。

```bash
# 1. 克隆代码仓库
git clone git@github.com:novalink-dev/novalink.git
cd novalink

# 2. 安装项目依赖
npm install

# 3. 启动开发服务器（默认监听 3000 端口）
npm run dev
```

启动成功后，访问控制台输出的本地地址（如 http://localhost:3000 ）即可进入导航站主页。生产环境部署请参考 `docs/deployment.md` 中的 Docker 或 PM2 部署方案。

## 安装要求

| 依赖项 | 必需版本 | 说明 |
|--------|----------|------|
| Node.js | v18.0.0 或更高 | 运行时环境，用于执行服务端与构建脚本 |
| npm | v9.0.0 或更高 | 包管理器，用于安装第三方依赖 |
| Git | v2.30.0 或更高 | 版本控制工具，用于克隆仓库与管理代码 |
| 内存 | 至少 512 MB 空闲 | 开发模式运行所需最低内存，生产模式建议 1 GB 以上 |
| 磁盘空间 | 至少 200 MB | 存放源代码、依赖包及构建产物 |
| 操作系统 | Linux / macOS / Windows（WSL2） | 官方测试通过的操作系统环境 |
| 浏览器 | 现代浏览器（Chrome 110+ / Firefox 110+ / Edge 110+） | 前端界面运行所需 |
| 网络 | 可访问外网（用于初次安装依赖） | 若使用内网镜像源，需提前配置 npm registry |

## 文档导航

| 层面 | 目录/文档 | 回答的问题 |
|------|-----------|------------|
| 用户手册 | `docs/user-guide.md` | 如何添加个人书签、如何设置默认分组、如何使用搜索与过滤功能 |
| 管理员手册 | `docs/admin-guide.md` | 如何批量导入链接、如何配置健康检查间隔、如何备份导航数据 |
| 开发指南 | `docs/development.md` | 项目目录结构说明、新增页面路由的方法、自定义主题样式流程 |
| API 参考 | `docs/api-reference.md` | 所有对外 REST 接口的请求参数、返回字段与错误码含义 |
| 部署运维 | `docs/deployment.md` | 生产环境构建优化、Nginx 反向代理配置、SSL 证书挂载方法 |
| 常见问题 | `docs/faq.md` | 搜索无结果、健康检查误报、页面加载缓慢等问题的排查步骤 |

## 资源列表

本导航项目收录的原始外部链接如下，按功能类别分组展示。所有链接均以用户提供的原始形式原样列出，未做任何协议补全或域名改写。

基础设施与监控类

- <code>xijiabifenc.org.cn</code>
- <code>dejiabifenc.org.cn</code>
- <code>yijiabifenc.org.cn</code>
- <code>fajiabifenc.org.cn</code>

业务数据看板与实时流类

- <code>yingchaobifenzhibo.org.cn</code>
- <code>xijiabifenzhibo.org.cn</code>
- <code>dejiabifenzhibo.org.cn</code>

上述链接均为示例性质的外部资源入口，实际部署时可根据团队需求替换为真实内网域名或公网服务地址。NovaLink 本身不依赖这些链接的具体内容，仅作为导航入口进行展示和跳转。

## 项目结构

```
novalink/
├── src/                          # 源代码主目录
│   ├── server/                   # 服务端代码（Node.js + Express）
│   │   ├── index.js              # 入口文件，初始化应用与中间件
│   │   ├── routes/               # 路由定义（API 与页面路由）
│   │   └── health/               # 健康检查定时任务实现
│   ├── client/                   # 前端代码（原生 JavaScript + CSS）
│   │   ├── pages/                # 页面级组件（首页、详情、管理）
│   │   ├── components/           # 可复用 UI 组件（搜索框、卡片、标签）
│   │   └── styles/               # 全局样式与主题变量
│   └── shared/                   # 前后端共享工具函数与常量
│       ├── validators/           # URL 格式与参数校验逻辑
│       └── constants/            # 默认分类、标签颜色、超时阈值
├── data/                         # 本地模拟数据（开发环境使用）
│   └── links.json                # 预置链接列表，含标题、URL、分类、标签
├── config/                       # 配置文件目录
│   ├── default.json              # 默认配置（端口、检查间隔、缓存时间）
│   └── production.json           # 生产环境覆盖配置
├── tests/                        # 单元测试与集成测试
│   ├── unit/                     # 工具函数与校验器测试
│   └── integration/              # API 接口与健康检查流程测试
├── docs/                         # 全部文档（用户手册、管理手册、API 参考等）
├── scripts/                      # 辅助脚本（数据迁移、批量导入、备份）
├── public/                       # 静态资源（favicon、robots.txt、错误页面）
├── .env.example                  # 环境变量模板（数据库连接、密钥等）
├── package.json                  # npm 项目清单与脚本定义
├── README.md                     # 项目总览与入门指南（即本文档）
└── LICENSE                       # MIT 许可证文本
```

## 贡献指南

我们欢迎并感谢任何形式的贡献，包括但不限于代码、文档、测试用例与功能建议。请遵循以下步骤提交贡献：

1. 在 GitHub 上 Fork 本仓库至您的个人账户，并将 Fork 后的仓库克隆到本地开发环境中。请确保使用 SSH 或 HTTPS 方式正确拉取。

2. 新建一个功能分支，分支名称应简要描述本次改动内容，例如 `feature/add-ldap-auth` 或 `fix/search-case-sensitivity`。请勿在主分支上直接修改。

3. 完成代码或文档改动后，请运行完整的测试套件（`npm test`）以确保未破坏现有功能。若新增功能，请同步编写对应的单元测试或集成测试。

4. 提交代码时请遵循 Conventional Commits 规范编写提交信息，格式为 `<type>(<scope>): <subject>`，例如 `feat(search): support fuzzy match for tags`。

5. 推送分支至您的 Fork 仓库，然后通过 GitHub 界面发起 Pull Request 到本仓库的 `main` 分支。PR 描述中请清晰说明改动目的、实现方式以及测试覆盖情况。

## 常见问题

**问：健康检查将某些内网地址标记为不可用，但实际这些地址在内网中是可以访问的，如何调整检查策略？**

答：默认健康检查使用 HTTP HEAD 方法且超时时间为 3 秒。对于内网中需要特殊认证或响应较慢的服务，您可以在 `config/default.json` 中调整 `healthCheck.timeout` 参数增大超时阈值，或者通过 `healthCheck.excludePatterns` 配置项排除特定域名前缀不进行检查。此外，也支持在链接编辑界面为单个链接单独禁用健康检查。

**问：搜索功能无法找到我刚刚添加的新链接，是什么原因？**

答：搜索索引在开发模式下每 10 秒重建一次，在生产模式下则依赖于数据变更事件触发重建。如果您在管理界面添加或修改链接后未能立即搜索到，请检查浏览器控制台是否有网络请求错误，或尝试手动刷新页面触发索引重建。若问题持续存在，可执行 `npm run rebuild-index` 脚本强制重建全部索引数据。

**问：是否支持多用户登录与权限区分？**

答：当前版本（v1.x）定位为轻量级团队导航工具，内置了基于简单 API 密钥的只读与读写权限区分，但未集成完整的用户认证系统。若您需要 LDAP、OAuth2 或 SSO 登录支持，请关注后续 v2.0 版本的规划路线图。目前可通过反向代理层（如 Nginx 的 basic_auth）实现基础的访问控制。

## 许可证

MIT License

Copyright (c) 2026 NovaLink Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

> 外链数量: 7 | 生成时间: 2026-08-14 22:01:34
