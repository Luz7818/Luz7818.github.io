# 个人主页 架构

> 用途：给要理解或改动本站结构的人。架构总览、目录结构（含根目录所有文件用途）、发布链路都在这里。
> 操作步骤在 `docs/GET-START.md`；数字口径在根目录 `AGENTS.md` 的「当前状态」。

## 架构总览

单文件静态页：`index.html` 一个文件承载结构（8 个 `<section id="…">` 小节）、样式（内联
`<style>`，`:root` 下 14 个自定义属性）、脚本（内联 `<script>`，仅做锚点平滑滚动）与全部文案。
GitHub Pages 把本仓当作用户站，从 `main` 分支根目录直接发布，无构建、无依赖、无后端。

## 目录结构

```
Luz7818.github.io/
├── index.html          页面全部内容：结构、样式、脚本、文案
├── assets/             图片资源，13 个文件全部被页面引用
├── docs/               手册与专项规范（GET-START / ARCHITECTURE / CODE-STYLE / TESTING / GIT）
├── README.md           展示用入口
├── AGENTS.md           规范入口；数字与门禁命令的单一来源
├── 目录说明.md          纯导航
├── HISTORY.md          版本更新记录
└── TODO.md             开发计划与当前进度
```

| 文件 | 用途 |
|---|---|
| `index.html` | 页面全部内容，唯一源文件 |
| `README.md` | 给访客的入口：是什么、怎么跑、往哪走 |
| `AGENTS.md` | 规范入口与索引；行数、字节数、图片数等事实以它的「当前状态」为准 |
| `目录说明.md` | 纯导航，只回答"东西在哪" |
| `docs/GET-START.md` | 上手手册：改文案、加卡片、换图、发布的步骤 |
| `docs/ARCHITECTURE.md` | 本文件 |
| `docs/CODE-STYLE.md` | HTML/CSS 约定（配色单源、锚点成对、外链规范） |
| `docs/TESTING.md` | 门禁：资源核对、锚点核对两条命令与目检清单 |
| `docs/GIT.md` | 提交身份、行尾、message 风格 |
| `HISTORY.md` / `TODO.md` | 版本记录 / 开发计划 |

## 数据组织方式

无数据层与后端。图片资源在 `assets/`：13 个文件全部被页面引用、0 个多余，且
`assets/README.md` 是目录说明页、不上页面（复核命令见 `AGENTS.md`「当前状态」的资源核对）。

## 发布与依赖关系

| 路径 | 由谁发布 |
|---|---|
| `https://luz7818.github.io/` | 本仓的 `index.html` |
| `https://luz7818.github.io/marx-cloud/` | **另一个仓库** `marx-cloud` 的 Pages |

因此本仓**不得**新建 `marx-cloud/` 等同名子目录——用户站占根路径，同名目录会与项目页抢
URL。页面与 `luzzz.me` 是两个独立站点，内容各自维护，不大段互相复制。

## 子目录说明索引

| 子目录 | 说明 |
|---|---|
| `assets/` | [`assets/README.md`](../assets/README.md)（逐张图片的用途与可删性） |
| `docs/` | 无（文档目录本身，内容见上表） |

## 已知架构问题

- 零依赖单文件是**有意约束**（离线双击可看），不是技术债：不引入构建工具、CDN、远程字体。
- 无测试、无 CI 是有意选择：门禁就是 [docs/TESTING.md](TESTING.md) 的两条核对命令。
- 移动端 3 个断点（1100 / 920 / 640 px）未在真机逐一验证过，见 `TODO.md` 任务 3。
