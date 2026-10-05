# Git 规范

> 用途：给提交本仓代码的人。提交身份、行尾、message 风格与发布链路的约定都在这里。

## 分支与提交策略

- 只有 `main` 分支，直接推 `main` 即发布（GitHub Pages 用户站：推上去就是线上）。
- **一批一提交**：一个提交 = 一个可回退单元；改文档与改页面不同批。

## 提交身份与行尾（有意保留的仓库级覆盖，不要"统一"掉）

- 提交邮箱是仓库级覆盖的学校邮箱（`git config user.email` = `213230392@seu.edu.cn`），
  与其余仓库的 noreply 身份不同，是有意设置。
- `core.autocrlf=true` 且本仓无 `.gitattributes`。若 `git diff` 显示 `index.html` 整文件改动，
  先怀疑 LF→CRLF 翻转，不要把它当内容改动提交。

## commit message

- 风格沿用既有历史：`<type>: 中文一句话`，type 取 `feat / fix / docs / chore`
  （复核：`git log --oneline -10`）。

## 必须入库 / 禁止上传

| 判定 | 规则 |
|---|---|
| 必须入库 | `index.html`、`assets/` 里被页面引用的图片、全部规范文档 |
| 禁止上传 | 住址、电话等比现在更敏感的个人信息；构建产物（本仓没有构建步骤） |

## CI 与 PR

- 无 CI（有意选择，见 `docs/ARCHITECTURE.md`）；门禁见 [TESTING.md](TESTING.md)。
- 个人站直接推 `main`，无 PR 流程。
