# HISTORY —— 版本更新记录

> 用途：记录每次版本与规范变更的内容和缘由。只追加，禁止删除或改写既有条目；写错了就追加一条
> 更正。新条目写在文件末尾。

## 2026-10-05 · 文档规范体系落位

- 文档从"五件套"迁到九件体系：新增 `docs/ARCHITECTURE.md`、`docs/CODE-STYLE.md`、
  `docs/TESTING.md`、`docs/GIT.md`、`HISTORY.md`、`TODO.md`；`docs/getting-started.md`
  更名 `docs/GET-START.md`；`AGENTS.md` 重写为规范入口（原「当前真实状态」「已知坑」的事实
  原样保留，原「仓库地图」移入 ARCHITECTURE，原「改动后的验证」移入 TESTING）。
- 变更缘由：落位《项目整体规范.md》的九件必建。本仓此前无版本记录文件，更早历史未在此建档，
  可由 `git log --oneline` 追溯（复核：`git log --oneline | wc -l`）。

## 2026-10-06 · 文档核查修复（章节改名残引清理）

- **章节改名残引**：assets/README 两处指向 AGENTS 旧章节名——「改动后的验证」实际在
  `docs/TESTING.md`（九件迁移时移入），「当前真实状态」已更名「当前状态」，均回改。
- **杂项**：GET-START 加卡片示例的 `<仓库名>` 占位改真实示例 `zhishuxing` 并加注；
  目录说明树补 `.gitignore`（入库文件此前未画进树）、删去与 ARCHITECTURE 重复的
  规模数字职责短语；TODO「正在做」随迁移完成更新。

## 2026-10-07 · 分享元数据与首屏外图片懒加载

- `<head>` 补齐社交分享元数据：`og:title` / `og:description` / `og:image` / `og:url` /
  `og:type`、`twitter:card`（summary，头像 278×278 方图）与 `rel="canonical"`。og 文案逐字
  取自既有 `<title>` 与 `meta description`，不新造宣传语；`og:image` 用 Pages 根路径绝对
  URL `https://luz7818.github.io/assets/portrait.jpg`。核查报告连续三轮挂账的 P2 项，本轮清账。
- 首屏之外的 5 处 `<img>`（campus-band 连续剪影、#about 校徽与礼堂线稿、contact-lockup、
  footer-mark）加 `loading="lazy"`；侧边栏 5 处、顶栏 1 处与 hero 区 3 处首屏图保持即时
  加载，首屏渲染不变。CSS `::before` / `::after` 背景水印不受该属性作用，未动。
- AGENTS.md「当前状态」同步：行数 2105→2112、本地字节数；远程资源复核命令排除
  `rel="canonical"`（它是 `<link>` 声明，页面不加载它，不违反零远程资源约定）；新增
  分享元数据与图片懒加载两行及其复核命令。
