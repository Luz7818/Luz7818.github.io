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
