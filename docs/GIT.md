# Git 规范

> 用途：给提交本仓代码的人。提交身份、行尾、message 风格与发布链路的约定都在这里。

## 分支与提交策略

- 只有 `main` 分支，直接推 `main` 即发布（GitHub Pages 用户站：推上去就是线上）。
- **一批一提交**：一个提交 = 一个可回退单元；改文档与改页面不同批。

## 提交身份与行尾（有意保留的仓库级覆盖，不要"统一"掉）

- 提交邮箱是仓库级覆盖的学校邮箱（`git config user.email` = `213230392@seu.edu.cn`），
  与其余仓库的 noreply 身份不同，是有意设置。
- `core.autocrlf=true`；仓根 `.gitattributes` 已锁 `*.html -text`（页面文件不做行尾转换，
  `index.html` 不再出现整文件翻转），其余文本文件 `* text=auto` 入库归一 LF。若 `git diff`
  仍显示整文件改动，先查 `.gitattributes` 与行尾，不要把它当内容改动提交。

## commit message

- 风格沿用既有历史：`<type>: 中文一句话`，type 取 `feat / fix / docs / chore`
  （复核：`git log --oneline -10`）。

## 必须入库 / 禁止上传

| 判定 | 规则 |
|---|---|
| 必须入库 | `index.html`、`assets/` 里被页面引用的图片、全部规范文档 |
| 禁止上传 | 住址、电话等比现在更敏感的个人信息；构建产物（本仓没有构建步骤） |

## CI 与 PR

- CI 只有一条最小工作流 `.github/workflows/check.yml`（跑 `AGENTS.md` 的两条核对，任一有
  输出即失败，2026-10-07 起）；无构建、无 lint。门禁见 [TESTING.md](TESTING.md)。
- 个人站直接推 `main`，无 PR 流程。
