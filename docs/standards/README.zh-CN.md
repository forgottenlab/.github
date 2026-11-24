# 📘 ForgottenLab 工程手册

[English](README.md) | [简体中文](README.zh-CN.md)

这是给个人维护者用的轻量 Git / GitHub 约定。以后如果有外部贡献，沿用同一套即可。Java、Python、Web 和公开仓库都用这套约定，不为每一种项目另建流程。流程保持很小：不要求独立审查者，不要求每个仓库都有 CI，也不要求每次改动都发布版本。

本手册提供实践建议，不会自动配置 CI、分支保护、发布流程或仓库权限。本仓库已经是公开的 `.github` 仓库，会为账户下缺少对应文件的仓库提供 GitHub 支持的默认社区文件，包括贡献指南和 Issue / Pull Request 模板。工程手册本身不会自动复制到其他仓库。具体规则参见 [GitHub 默认社区文件文档](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)。

## 1. 📖 术语

| 术语 | 含义 |
|---|---|
| Repository（仓库） | 项目文件及其历史 |
| Commit（提交） | 一次变更的已记录快照 |
| Branch（分支） | 一条工作线。`main` 是主线 |
| Issue | 被跟踪的问题、需求或任务 |
| Pull Request | 一份提议合并的变更，也可以用来讨论 |
| Actions | 某个仓库可选的自动化 |
| Tag（标签） | 指向一个提交的 Git 名字，通常表示版本 |
| Release（发布） | GitHub 上面向使用者展示某个已标记版本的页面 |
| Package（软件包） | 在项目确实需要分发时，再发布的库或构建产物 |

Git 记录的是项目如何演进，不只是一份最新代码的备份。

## 2. 🛠️ 日常 Git

提交前按这个顺序看一遍：

1. `git status`
2. `git diff`
3. 按路径暂存这次要包含的文件，例如 `git add path/to/file`
4. `git diff --cached`
5. `git commit`
6. 准备分享时再 `git push`

先读 diff，再提交。密钥、本机配置和与本次无关的修改留在工作区里。

维护者的低风险改动可以直接进入 `main`。典型情况：

- 文档措辞、错别字、链接修正
- 原因已经清楚的小缺陷修复
- 你愿意立刻接受、也容易回退的改动

下面的情况改用分支：

- 改动面比较大，或会跨越多天
- 还在试验，可能整段丢弃
- 希望别人先读过再合并

## 3. 🌿 分支

`main` 是主分支，允许维护者直接提交低风险改动。

名字有帮助时，可以使用这些前缀：

- `feat/…`：新行为
- `fix/…`：缺陷修复
- `docs/…`：文档
- `refactor/…`：结构调整

前缀只是提示，不是门槛。没有前缀的清楚名字同样可用。需要备份、换一台机器或打开 Pull Request 时，再推送分支。短期试验可以只留在本地。

默认不维护长期发布分支或旧版本维护分支；确有需要时，由项目自行决定。版本用标签表示。

## 4. 🧾 提交说明

提交标题使用轻量 [Conventional Commits](https://www.conventionalcommits.org/zh-hans/v1.0.0/)：

```text
type: 简短说明
```

| 类型 | 用途 |
|---|---|
| `feat` | 使用者能感知的新行为 |
| `fix` | 缺陷修复 |
| `docs` | 只改文档 |
| `refactor` | 调整结构，不打算改变行为 |
| `test` | 只改测试 |
| `chore` | 其他维护 |
| `build` | 构建或打包配置 |
| `ci` | 自动化配置 |
| `style` | 只改格式 |

日常大多只用 `feat`、`fix` 和 `docs`。`build`、`ci`、`style` 在确实匹配时再用。用标签标记发布版本，并按实际工作选择发布准备提交的类型。ForgottenLab 自有公开技术项目从第一次执行 `git commit` 起，就使用简洁、准确、祈使语气的英文 Conventional Commits 标题。每次提交记录一个连贯的变更。准确的历史提交保留原有语言。此约定同样适用于维护者和开发助手，遵循项目及上游例外，不设强制检查。

普通提交与 Squash 提交使用同一套正文判断规则。根据实际变更决定是否填写，类型前缀不决定正文长度。

- **只写标题。** 标题与差异已经说明变更，且没有需要长期保留的背景时，正文留空。常见情况包括拼写修正、小型文档或 UI 调整、常规依赖更新，以及原因明确的小修复。
- **标题加正文。** 有非显然行为或根因、设计或架构决定、兼容性、安全或权限边界、迁移、回滚或关键验证时，用一至三个短段落或少量项目符号记录。新写的正文优先简洁英文，必要时可用简体中文。准确的已有正文保留原有语言。提交正文无需固定标题或翻译。PR 模板、`English Summary`、完整测试清单和任务交接各自保留在适用的记录中。
- 保留真实且已核实的 Git trailers，包括有效的 `Co-authored-by`。只有核实了实际归属才添加归属信息。

**只写标题。** [LaunchFlow #4](https://github.com/forgottenlab/launchflow/pull/4) 的最终提交消息为 `fix: keep the Basic sidebar brand title unclipped`，Extended description 留空。

**技术正文。** [RouteQuay #13 的原始提交](https://github.com/forgottenlab/RouteQuay/commit/4a27e9dbebf90141d1330eeed203fe212d3f37f2) 采用以下结构，示例正文为转述。实际 Squash 保留了完整原消息和两条已核实的 trailers。

```text
feat: group issued clients in local metadata

Keep group membership on the operator’s machine and use it to select
members for export. Editing a group leaves remote clients unchanged.
```

## 5. 💬 Issue

按以下顺序确定项目维护交流语言。它为 Issue 正文提供参考。

1. 遵循项目明确声明的语言。项目级明确约定优先于中央默认建议。
2. 项目未声明时，由维护者参考主要用户文档和贡献指南判断。英文 README、双语 README 或编程语言本身均不足以确定维护语言。
3. 仍无法确定时，采用 ForgottenLab 全局默认语言简体中文。

这项约定由维护者在撰写时应用。GitHub 不会自动识别或切换项目语言。

公开技术项目中，维护者优先使用简洁、描述性的英文 Issue 标题。项目或上游明确声明标题语言时，遵循其约定。例如，主要面向中文用户的项目可用中文标题。标题直接描述问题或需求，省去 `bug:`、`enhancement:`、`feature:`、`docs:` 或 `[Bug]` 等分类前缀。

标题和正文可以使用不同语言。维护者可以参考项目维护交流语言，用简体中文或英文写正文。中文正文末尾附简短的 `## English Summary`，概括问题、需求、测试结果或核心结论。全文翻译可选。

接受外部贡献者用英文或简体中文提交，包括用任一语言撰写标题。外部贡献者的英文摘要可选。语言建议适用于新撰写的内容，既有 Issue 保留原有语言，不设置强制语言校验。

对外创建公开 Issue 或 Pull Request 前，按问题范围检索开放和已关闭的 Issues、Pull Requests、已启用的 Discussions，以及上游官方反馈渠道。遵循目标项目的贡献指南和模板。同一问题已有人跟踪时，优先补充有新增价值的证据，例如不同的环境或版本、日志、测试结果、更具体的原因、边界条件或已验证的修复。问题有实质差异、已修复问题再次出现，或上游指引要求另开讨论时，可以新建 Issue。

类别交给 GitHub Issue Types，优先选择可用的原生类型，例如 Bug、Task 和 Feature。

仅在类型和标题之外确有额外分类需要时使用 GitHub Labels。避免为原生 Issue Type 添加同义标签。新增或维护标签时，优先使用简洁、稳定、便于跨项目理解的英文名称。各项目可保留自己的标签集合，并为上游兼容或特殊工作流保留例外。既有标签可以保持原样，包括中文标签。中央仓库不会同步标签，中央 Issue 表单也不会添加标签。

本仓库在 `.github/ISSUE_TEMPLATE/` 提供缺陷、功能、任务和测试与验证四份短表单。表单会设置 Issue Type，并把标题留空。测试与验证使用 Task 类型。空白 Issue 仍然可以开。项目可以在专用模板中指定自己的约定。某个仓库如果在自己的 `.github/ISSUE_TEMPLATE/` 中定义了有效模板或模板配置，GitHub 就使用本地配置，不再使用整个默认模板目录。

- 缺陷证据优先附在原缺陷 Issue。
- 任务完成后的验证结果可记录在原 Task 或实现该任务的 PR 中。
- 独立测试、兼容性实验或性能评估可以使用测试与验证表单。无需为每次测试单独开 Issue。

### Issue 生命周期

- **Completed** 用于问题已解决或工作已完成，且所需验证已完成的情况。按需关联修复 Commit、PR 或测试记录，也可简述完成情况。尚未验证的结果应如实说明。
- **Duplicate** 用于确认实质相同的问题。说明重复关系并引用原 Issue，有原生重复关闭选项时使用该选项。仅标题相似不足以判定重复。[GitHub CLI 重复关闭说明](https://cli.github.com/manual/gh_issue_close)
- **Not planned** 用于记录暂缓或不实施的决定。简述原因，并与已解决区分开。
- **重新打开或报告回归** 前，核对根因、受影响版本和此前讨论。按实际情况重新打开原 Issue 或另开一项，并交叉引用相关工作。
- **Open 或结论未定** 适用于证据尚不足以确认解决的情况。按需保持开放。长时间无活动本身不足以关闭 Issue。

使用 GitHub 原生状态、关闭原因和 Issue 引用。相关时可附 PR 链接。无需新增自定义状态、生命周期标签或自动关闭规则。

### 使用 GitHub CLI 提交 Issue

GitHub 网页会将 YAML Issue Forms 渲染成带字段、验证及上传控件的表单。使用 `gh` 时，先准备 Markdown，再通过 `--body-file` 提交。`--template` 提供正文初稿。填写和验证 YAML 表单字段应使用网页表单。[GitHub CLI Issue 参考](https://cli.github.com/manual/gh_issue)

将 `OWNER/REPO` 换成目标仓库。沿用上文的标题和正文约定，维护者使用中文正文时附简短英文摘要。优先使用仓库原生 Issue Type，省去无必要的标签。先查重，公开写入前核对实际仓库、标题和完整内容。操作已有 Issue 时，还要核对编号和现有内容。查询和预览不构成写入授权。

```powershell
$repo = 'OWNER/REPO'
$title = 'Export fails when the output directory is missing'
gh issue list --repo $repo --state all --search 'export "output directory"'
Get-Content -LiteralPath .\issue.md -Raw -Encoding utf8
```

例如，`issue.md` 可以是一段简短的中文正文，末尾附英文摘要。

```markdown
导出目录不存在时，导出会失败。预期自动创建目录并完成导出。

## English Summary
Export fails when the output directory is missing. It should create the directory and complete the export.
```

获得创建授权后执行创建命令。仅在 `Bug` 这一原生类型可用且适合时传入 `--type Bug`。

```powershell
gh issue create --repo $repo --title $title --body-file .\issue.md --type Bug
```

给已有 Issue 补充证据时，先预览 `evidence.md` 并核对实际编号。以下命令会发布新评论。

```powershell
# 将 123 替换为待更新的 Issue 编号。
$issue = 123
gh issue comment $issue --repo $repo --body-file .\evidence.md
```

修改已有 Issue 时，可设置新标题，也可用 `--body-file` 提供已审阅的完整正文。只使用本次要改的选项。

```powershell
gh issue edit $issue --repo $repo --title $title
# 仅修改正文时，使用已审阅的完整替换正文。
# gh issue edit $issue --repo $repo --body-file .\issue.md
```

用 `gh issue view` 核对结果。创建 Issue 后，将 `$issue` 设为新 Issue URL 中的编号。

```powershell
gh issue view $issue --repo $repo --json url,title,body,state,issueType,labels
```

## 6. 🤝 Pull Request

日常独自开发可以不打开 Pull Request，直接在 `main` 上完成低风险提交。

这些情况适合打开：

- 改动较大，希望先看完整差异再合并
- 需要一个可暂停的检查点
- 有外部贡献

Pull Request 是提议合并的变更。审查是其中一种用法，不是必经步骤。不设独立审查者。维护者可以合并自己的 Pull Request。说明里写清改了什么、如何检查过即可。

ForgottenLab 自有公开技术项目的维护者优先用简洁、准确的英文 PR 标题，描述拟合并的变更。建议按实际改动选择 Conventional Commits 风格的前缀，例如 `feat: add read-only setup planning`、`fix: prevent concurrent installer launches` 或 `docs: clarify installation requirements`。PR 前缀是建议，项目级明确约定可优先。Issue 标题继续描述问题，由原生 Issue Type 分类。

PR 标题和正文可用不同语言。维护者通常用简体中文写技术正文，也可用英文。中文为主体的正文末尾附简短的 `## English Summary`，概括主要变更、验证结果或必要限制。英文正文可直接提交。外部贡献者可用英文或简体中文，英文摘要可选。两种语言都接受，全文翻译可选，不设强制语言校验。

`.github/pull_request_template.md` 预填 PR 说明。项目可提供自己的 Pull Request 模板以覆盖默认模板。

### 准备提交与 PR

一个 PR 对应一个连贯的逻辑变更。小型修复、独立功能或适合一次提交的工作优先形成一个完整提交。复杂开发、阶段性验证或有独立保留价值的改动可以用多个提交。执行 amend、rebase 或 force push 前须获得授权。创建 PR 前，分别核对实际提交消息、提交数量和独立撰写的 PR 正文。

PR 正文用于保留审查记录。使用[中央 PR 模板](../../.github/pull_request_template.md)或项目自己的模板。

- `## 改动 / What changed` 为固定章节。说明实际改动，按需补充原因或实现方式。
- `## 检查 / How it was checked` 为固定章节。如实记录检查和结果，未运行测试也应说明。
- `## 范围与限制 / Scope and limitations` 为可选章节。有兼容性、安全边界、未完成事项或发布限制时填写，否则删除。
- `## English Summary` 放在以中文为主的维护者 PR 正文末尾。全英文正文删除该章节，外部贡献者可按需填写。

小型 PR 可在固定章节各写一条。较大 PR 可在这些章节下使用子标题、列表、表格或证据。例如 [PathPilot #10](https://github.com/forgottenlab/pathpilot/pull/10) 用中文说明只读初始化预览及检查，记录预览的限制，末尾附简短英文摘要。

PR 面向默认分支且应关闭某个 Issue 时，把 `Fixes #N` 或 `Closes #N` 写在 PR 正文。提交正文需要给后来的读者留链接时，可以用 `Refs #N`。

### Squash 提交消息

一个逻辑变更可优先考虑 Squash and merge。需要让独立提交在默认分支可见时，保留普通 Merge 方式。每个仓库在 **Settings → General → Pull Requests** 中继续推荐将 Squash 消息设为 **Default message**。GitHub 的普通 Merge Commit 预填格式（`Merge pull request #… from …`）仍适用于普通合并。

| GitHub Squash 设置 | 预填内容 |
|---|---|
| **Default message**，单提交 | 原提交标题和正文 |
| **Default message**，多提交 | PR 标题和提交列表 |
| **Pull request title and description** | PR 标题和正文 |

从预填内容起草一条概括逻辑变更的简洁英文 Conventional Commits 标题。普通提交标题与 PR 标题不追加 `(#N)` 形式的后缀，确认 Squash 前删除预填的 `(#N)`。保留历史消息。参见 [GitHub 的 Squash 消息选项](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests)。

- **单提交。** 如果符合[提交规则](#4--提交说明)，完整复用原消息。原提交正文为空且符合留空条件时，**Extended description** 留空。保留有用技术信息及原语言。仅对不准确、重复、无关的 PR 段落或中间记录做最小调整。英文摘要中的独有信息应保留或整合，有效的 Git trailers 应保留。
- **多提交。** 用一个标题概括整个变更。按[同一套正文规则](#4--提交说明)判断是否填写 Extended description。从实际差异和原始提交提炼长期有用的信息。省去自动生成的提交列表、整份 PR 正文和独立的 Squash 或英文摘要章节。

**复用示例。** [PathPilot #11](https://github.com/forgottenlab/pathpilot/pull/11) 最终使用 `feat: add automatic Windows path discovery to setup plans`，以中文说明发现顺序、安全检查和只读边界。如果单条原始提交已准确说明这类技术背景，保留其中文正文。该 PR 的实际原始提交没有正文，这些背景由最终 Squash 补入。

确认合并前核对实际差异、验证结果、合并就绪状态、最终提交消息、作者和共同作者归属。

### 开发助手的操作指引

从首次提交起，阅读项目适用的指令及其引用的提交规范。交接时明确所准备的记录类型。准备 PR 时提供 **PR Title** 和 **PR Body**。准备 Squash 时提供 **Commit message** 和 **Extended description**。正文应留空时直接说明留空，只给一套可复制的填写内容。所有开发助手采用相同流程。

当项目缺少相应文件时，GitHub 为受支持的文件提供[中央社区默认文件](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)。这些默认文件由 GitHub 提供，不会出现在项目克隆中。要让开发助手找到规则，可在所用助手实际读取的项目指令中链接本手册的提交与 PR 章节，或在任务中明确附链接并要求提交前阅读。

### 向外部项目贡献

向其他人维护的仓库提交 Issue 或 PR 时，按以下顺序参考目标项目的规则。

1. 遵循目标项目明确的贡献指南、Issue 或 PR 模板、维护者要求、仓库开发规则和相关官方说明。
2. 若没有明确要求，查看近期多个有代表性的开放与已合并 PR。结合标题、正文、提交标题、合并方式、语言和维护者反馈判断是否形成稳定惯例。
3. 如果仍无明确惯例，使用清晰的英文标题和目标社区易于理解的正文，准确说明实际工作与验证情况。

由目标项目决定是否采用标题前缀、英文摘要、模板或 Squash 合并。遇到要求冲突或不明确时，说明不确定之处，由上游维护者决定其规范。

## 7. 🧪 检查与自动化

某个仓库会反复受益于同一组检查时，再添加 GitHub Actions。小型或早期仓库可以没有 CI。准备发布有意义的版本时，先运行项目已有的检查；没有 Actions 时也一样。

检查通过只说明这次运行里的命令成功了。打标签、创建 Release 和部署仍然分别决定。如果工作流会发布产物，从标签或手动运行启动它，而不是挂在每一次推送上。

从一个有用的作业开始。出现真实需要后再增加作业。

CI 原始日志和大体积构建产物优先放在 Actions Artifacts 或合适的报告位置。在 Issue 中简述结论并附证据链接。上传公开附件前，先移除密钥、令牌、隐私数据和未脱敏的内部配置。Issue 表单仅接受指定格式，单张图片上限为 10 MB，支持的文档、文本文件和压缩包每个上限为 25 MB。参见 [GitHub Issue 表单上传限制](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema#supported-file-types-and-size-limits)。

## 8. 📦 版本与发布

版本对你或对使用者有意义时再打标签。错别字、私人笔记和未完成的试验不必发版。

使用语义化版本 `MAJOR.MINOR.PATCH`：

| 部分 | 何时增加 |
|---|---|
| MAJOR | 不兼容的变化 |
| MINOR | 向后兼容的新行为 |
| PATCH | 向后兼容的修复 |

例如，`v0.2.0` 增加了兼容的新能力；随后的小修复是 `v0.2.1`。

```bash
git tag -a v0.1.0 -m "First usable version"
git push origin v0.1.0
```

值得发布时，按这个顺序：运行相关检查，若项目维护 CHANGELOG 就先更新它，然后打标签，再创建 Release。

使用者需要说明或可下载文件时，再创建 GitHub Release。标签可以单独存在。早期版本可以只发布源码。对外提供的二进制放在 Release 上，生成的构建目录留在源码历史之外。

有人会追随版本时，再维护 CHANGELOG。早期的私人项目用 Git 历史和 Release 说明就够。

Package 同样按需使用。没有分发库或安装包的项目，不必配置软件包发布。

## 9. 📝 文档

公开项目的 README 说明：它解决什么问题、不做什么、如何使用、使用什么许可证。功能、安装、配置、示例、测试和路线图在有帮助时再写。给出命令之前，先说明这条命令会做什么。

两种读者都重要时，提供 `README.md` 和 `README.zh-CN.md`，并在顶部互相链接。详细笔记可以先保持一种语言，值得持续维护时再翻译。

开始接收他人的改动时，再添加 `CONTRIBUTING`，并让它指向本手册，而不是在每个仓库复制一份。

打算让别人复用的公开仓库，放一个许可证文件。选择、声明和审查流程见[开源许可证统一规范](LICENSING.zh-CN.md)。本 `.github` 仓库不会为其他项目授予许可证。

## 10. 🔐 安全

- 令牌、密码、私钥和本机私有配置不进入提交，也不写进 Issue。
- `.env`、`secrets/` 和本地凭据文件保持未跟踪。
- 每次提交前阅读 `git diff`。
- 难以撤销的修改之前先备份；能提供恢复步骤时就写上。
- 破坏性操作要写清楚。使用者没有要求时，不停止或替换已有服务。
- 会写入配置或重启服务的工具，应能在不触碰真实环境的情况下测试。
- 推送到公开远程、force-push、改写历史、删除共享工作，都单独决定后再做。
- 保留与当前任务无关的现有改动。
- 测试通过、创建标签和部署是三件不同的事。

不要在公开 Issue 中披露未修复的漏洞或已暴露的密钥。目前尚未配置专门的私密报告渠道。

## 11. 🧭 默认约定

- 主分支是 `main`。
- 维护者的低风险改动可以直接提交到 `main`。
- 改动较大或需要别人阅读时，使用分支和 Pull Request。
- 不要求独立审查者。
- CI 只加在值得自动检查的仓库上。
- 版本在有意义时发布。
- Issue 使用描述性标题和原生 Issue Types，标签保持很少。

真实问题优先，默认更安全，先解释再执行，先备份再修改，先测试再发布。写文档给未来的自己，通过真实反馈持续改进。

### 优先复用已有实现

开始重大功能或建立独立项目之前，先核对当前项目、ForgottenLab 其他仓库和相关开源生态已有的能力。查阅官方文档和上游组件，核对适用性与许可证。优先直接使用现成方案，再考虑扩展或修复已有项目、参与上游贡献、整合项目或复用模块，最后评估是否需要单独建仓。

学习实验、不同架构、安全边界、兼容目标或明确的创新方向，都可以让新项目具有独立价值。检索范围随决策规模调整，日常小修只需有针对性地检查。
