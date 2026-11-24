# 📘 ForgottenLab Engineering Handbook

[English](README.md) | [简体中文](README.zh-CN.md)

Lightweight Git and GitHub defaults for a solo maintainer. External contributors can use the same rules later. The same defaults fit Java, Python, web, and public repositories. The process stays small: no required reviewer, no required CI, and no release for every change.

This handbook is guidance, not automatic configuration of CI, branch protection, releases, or repository permissions. This public `.github` repository supplies supported default community health files, including contribution guidelines and Issue / Pull Request templates, to repositories owned by the account that lack their own corresponding files. The handbook itself is not automatically copied into other repositories. See [GitHub default community health file rules](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

## 1. 📖 Terms

| Term | Meaning |
|---|---|
| Repository | The project files and their history |
| Commit | A recorded snapshot of a change |
| Branch | A line of work. `main` is the primary line |
| Issue | A tracked problem, request, or task |
| Pull request | A proposed change, ready to merge or discuss |
| Actions | Optional automation for one repository |
| Tag | A Git name for one commit, usually a version |
| Release | A GitHub page that presents a tagged version |
| Package | A published library or build, only when a project needs one |

## 2. 🛠️ Everyday Git

1. `git status`
2. `git diff`
3. Stage the intended files by path, for example `git add path/to/file`
4. `git diff --cached`
5. `git commit`
6. `git push` when that work is ready to share

Read the diff before committing. Secrets, local configuration, and unrelated edits stay out of the commit.

Low-risk owner work can go straight to `main`: documentation, a typo, or a small fix whose cause is already understood.

Use a branch for work that is large, experimental, easy to discard, or meant for someone else to read first.

## 3. 🌿 Branches

`main` is the primary branch and can receive direct low-risk commits.

Optional prefixes when a name helps:

- `feat/…`
- `fix/…`
- `docs/…`
- `refactor/…`

A clear name without a prefix is fine. Push a branch when you want a backup, another machine, or a pull request. A short experiment can stay local.

Versions are marked with tags. Long-lived release branches are not needed by default; individual projects may add them when necessary.

## 4. 🧾 Commits

Use a lightweight [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) subject:

```text
type: short description
```

| Type | Use |
|---|---|
| `feat` | User-visible behavior |
| `fix` | A defect fix |
| `docs` | Documentation only |
| `refactor` | Restructuring without an intended behavior change |
| `test` | Tests only |
| `chore` | Other maintenance |
| `build` | Build or packaging setup |
| `ci` | Automation setup |
| `style` | Formatting only |

`feat`, `fix`, and `docs` cover most commits. Add `build`, `ci`, or `style` only when they fit. Mark published versions with tags and keep release preparation under the type that describes the work. For new commits in ForgottenLab’s public technical projects, use a short, imperative English Conventional Commits subject from the first `git commit`. Each commit should capture one coherent change. Keep accurate historical messages in their original language. This guidance applies to maintainers and development assistants, with project and upstream exceptions and no mandatory linting.

Ordinary commits and squash commits use the same body rules. Decide from the actual change, regardless of the type prefix.

- **Subject only.** Leave the body empty when the subject and diff explain the change and there is no lasting context to record. Common examples include typos, small documentation or UI changes, routine dependency updates, and fixes with an obvious cause.
- **Subject and body.** Add one to three short paragraphs, or a few bullets, for non-obvious behavior or root causes, design or architecture decisions, compatibility, security or permissions, migration, rollback, or essential verification. Prefer concise English for new text and use Simplified Chinese when useful. Keep accurate existing text in its original language. Commit bodies have no fixed headings or translation requirement. Keep the PR template, `English Summary`, full test checklist, and handoff in their own records.
- Preserve real, verified Git trailers, including existing valid `Co-authored-by` entries. Add attribution only when it is verified.

**Subject only.** `fix: keep the Basic sidebar brand title unclipped` was the final [LaunchFlow #4](https://github.com/forgottenlab/launchflow/pull/4) message. Its Extended description was empty.

**Technical body.** [RouteQuay #13’s original commit](https://github.com/forgottenlab/RouteQuay/commit/4a27e9dbebf90141d1330eeed203fe212d3f37f2) used this structure. The example paraphrases its body. The actual squash preserved the full original message and both verified trailers.

```text
feat: group issued clients in local metadata

Keep group membership on the operator’s machine and use it to select
members for export. Editing a group leaves remote clients unchanged.
```

## 5. 💬 Issues

Choose the project's maintenance communication language in this order. It guides the issue body.

1. Follow the language explicitly declared by the project. Project-specific conventions take precedence over the central defaults.
2. If there is no declaration, maintainers can use the project's main user documentation and contribution guide to make a judgment. An English README, bilingual READMEs, or the programming language alone cannot determine the maintenance language.
3. If the language is still unclear, use ForgottenLab's default of Simplified Chinese.

Maintainers apply this guidance when writing. GitHub does not automatically detect or switch the language for a project.

For maintainer issues in public technical projects, prefer a concise, descriptive English title. Follow any explicit project or upstream title policy. For example, a project primarily serving Chinese-speaking users can use Chinese titles. Describe the problem or request directly and omit category prefixes such as `bug:`, `enhancement:`, `feature:`, `docs:`, or `[Bug]`.

The title and body can use different languages. Maintainers can write the issue body in Simplified Chinese or English, using the project's maintenance language as a guide. End a Chinese body with a brief `## English Summary` of the problem, request, test results, or main conclusion. Full translations are optional.

Accept external contributions in English or Simplified Chinese, including titles in either language. An English summary is optional for external contributors. Apply this guidance to new writing and retain existing issues in their original language. The preference adds no language checks.

Before opening a public issue or pull request, search the relevant open and closed issues, pull requests, enabled Discussions, and the upstream project's official feedback channels. Follow the target project's contribution guide and templates. When the same problem is already tracked, add evidence that changes what is known, such as another affected environment or version, logs, test results, a narrower cause, a boundary case, or a verified fix. Open a separate issue for a materially different problem, a regression after a fix, or when upstream guidance calls for a new thread.

Record the category with GitHub Issue Types. Prefer available native types such as Bug, Task, and Feature.

Use labels only for extra classification beyond the type and title. Avoid labels that duplicate native Issue Types. Prefer short, stable English names that are easy to understand across projects when adding or maintaining labels. Each project can keep its own label set, with exceptions for upstream compatibility or special workflows. Existing labels, including Chinese labels, can stay as they are. The central repository does not synchronize labels, and its issue forms do not assign them.

This repository includes short Bug, Feature, Task, and Test & Validation forms in `.github/ISSUE_TEMPLATE/`. Each form sets the issue type and leaves the title empty. Test & Validation uses the Task issue type. A blank issue stays available. Projects can specify their own conventions in dedicated templates. If a repository defines valid issue templates or template configuration in its own `.github/ISSUE_TEMPLATE/`, GitHub uses that local configuration instead of the entire default template folder.

- Attach bug evidence to the original Bug issue.
- Record task verification results in the original Task or in the PR that implements it.
- Use Test & Validation for standalone tests, compatibility experiments, or performance evaluations. A separate issue is optional for each test.

### Issue lifecycle

- **Completed** applies when the issue is resolved or the work is finished and the necessary verification is complete. Link a fix commit, PR, or test record, or summarize what was done when useful. Report unverified results as such.
- **Duplicate** applies when the issues are materially the same. Explain the relationship and reference the original issue. Use GitHub's native duplicate closure where available. A similar title alone is insufficient. [GitHub CLI duplicate closure](https://cli.github.com/manual/gh_issue_close)
- **Not planned** records a decision to defer or decline work. Briefly explain the reason and keep it distinct from a resolution.
- **Reopen or report a regression** after checking the root cause, affected version, and earlier discussion. Decide whether to reopen the existing issue or file a new one, and cross-reference related work.
- **Open or inconclusive** is appropriate when the evidence does not establish a resolution. Leave it open as needed. Inactivity alone is insufficient grounds to close it.

Use GitHub's native state, close reasons, and issue references. Add a PR link when relevant. A custom status, lifecycle label, or automatic closure rule is unnecessary.

### Filing issues with GitHub CLI

The GitHub web interface renders YAML Issue Forms with fields, validation, and upload controls. With `gh`, prepare Markdown and pass it with `--body-file`. The `--template` flag supplies starting body text. To fill and validate YAML form fields, use the web form. [GitHub CLI issue reference](https://cli.github.com/manual/gh_issue)

Replace `OWNER/REPO` with the intended repository. Use the title and body conventions above, including a short English summary for a maintainer's Chinese body. Prefer the repository's native Issue Type and omit unnecessary labels. Search first, then review the actual repository, title, and complete text before any public write. For existing issues, verify the issue number and current contents. A search or preview grants no write authorization.

```powershell
$repo = 'OWNER/REPO'
$title = 'Export fails when the output directory is missing'
gh issue list --repo $repo --state all --search 'export "output directory"'
Get-Content -LiteralPath .\issue.md -Raw -Encoding utf8
```

For example, `issue.md` could be a short Chinese body with an English summary.

```markdown
导出目录不存在时，导出会失败。预期自动创建目录并完成导出。

## English Summary
Export fails when the output directory is missing. It should create the directory and complete the export.
```

Once authorized to create the issue, run the create command. Use `--type Bug` only when that native type is available and appropriate.

```powershell
gh issue create --repo $repo --title $title --body-file .\issue.md --type Bug
```

To add evidence to an existing issue, preview `evidence.md` first and use the actual issue number. The following command posts a new comment.

```powershell
# Replace 123 with the issue number to update.
$issue = 123
gh issue comment $issue --repo $repo --body-file .\evidence.md
```

To edit an existing issue, set the revised title or use `--body-file` with the complete reviewed body. Use only the option you intend to change.

```powershell
gh issue edit $issue --repo $repo --title $title
# Body-only edit, using the complete reviewed replacement body
# gh issue edit $issue --repo $repo --body-file .\issue.md
```

Check the result with `gh issue view`. After creation, set `$issue` to the number shown in the new issue URL.

```powershell
gh issue view $issue --repo $repo --json url,title,body,state,issueType,labels
```

## 6. 🤝 Pull requests

A pull request is optional for ordinary solo work.

Open one for a substantial change, a checkpoint before merging, or an external contribution. No independent reviewer is required. The author may merge their own pull request. Describe what changed and how it was checked.

In ForgottenLab's own public technical projects, maintainers should prefer a concise, accurate English PR title that describes the change that would be merged. Prefer a Conventional Commits prefix that fits the actual work, such as `feat: add read-only setup planning`, `fix: prevent concurrent installer launches`, or `docs: clarify installation requirements`. PR prefixes are recommended, and project-specific rules can take precedence. Use the Issue title to describe the problem and the native Issue Type to classify it.

The PR title and body can use different languages. Maintainers usually write technical details in Simplified Chinese and can also write in English. End a primarily Chinese body with a brief `## English Summary` covering the main changes, verification results, or relevant limits. An English body can stand on its own. External contributors can use either English or Simplified Chinese, and their English summary is optional. Accept both languages without mandatory language checks or full translations.

`.github/pull_request_template.md` prefills the description. A repository can provide its own pull request template to override this default.

### Preparing the commit and pull request

Keep each PR to one coherent change. Prefer one complete commit for a small fix, self-contained feature, or work that fits one commit. Multiple commits are fine for complex work, staged verification, or independently useful changes. Get authorization before amending, rebasing, or force-pushing. Before opening a PR, check the actual commit messages, commit count, and standalone PR body against their respective rules.

Use the PR body as the durable review record. Follow the [default PR template](../../.github/pull_request_template.md) or the project’s local template.

- `## 改动 / What changed` is required. Describe the actual change and explain its reason or implementation when useful.
- `## 检查 / How it was checked` is required. Report actual checks and results, including when tests were not run.
- `## 范围与限制 / Scope and limitations` is optional. Keep it for compatibility, safety, unfinished work, or release boundaries. Remove it when irrelevant.
- `## English Summary` comes last for primarily Chinese maintainer PRs. Remove it for English bodies. It is optional for external contributors.

Small PRs can use one line per required section. Larger ones can add subheadings, lists, tables, or evidence under those sections. For example, [PathPilot #10](https://github.com/forgottenlab/pathpilot/pull/10) uses Chinese to explain the read-only setup preview and checks, states the limits of that preview, and closes with a short English summary.

When a PR targets the default branch and should close an Issue, put `Fixes #N` or `Closes #N` in its body. Use `Refs #N` in a commit body when the link helps future readers.

### Squash messages

For one logical change, consider Squash and merge. Keep the native merge option for changes whose commits should remain independently visible. Keep **Default message** as the per-repository squash setting under **Settings → General → Pull Requests**. GitHub’s native merge-commit prefill (`Merge pull request #… from …`) remains valid for a regular merge.

| GitHub squash setting | Prefill |
|---|---|
| **Default message**, one commit | Original commit subject and body |
| **Default message**, multiple commits | PR title and commit list |
| **Pull request title and description** | PR title and body |

Treat the prefill as a starting point. Use one concise English Conventional Commits subject for the logical change. Leave `(#N)` off new ordinary commit subjects and PR titles, and remove a prefilled suffix before confirming a squash. Keep existing history intact. See [GitHub’s squash message options](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests).

- **One commit.** Reuse the complete message when it follows the [commit rules](#4--commits). An empty original body can leave **Extended description** blank. Keep useful technical context in its existing language. Make minimal edits for inaccuracy, duplication, stray PR headings, or irrelevant intermediate notes. Retain any unique details from an English summary and preserve valid Git trailers.
- **Multiple commits.** Write one subject for the whole change. Add an Extended description only when the [same body rules](#4--commits) call for it. Synthesize durable facts from the diff and commits. Leave out the generated commit list, the full PR body, and standalone Squash or English summary sections.

**Reuse example.** [PathPilot #11](https://github.com/forgottenlab/pathpilot/pull/11) landed with `feat: add automatic Windows path discovery to setup plans` and a Chinese body covering discovery priority, safety checks, and the read-only boundary. If a single original commit already contains accurate technical context like this, reuse it in Chinese. In the actual PR the original commit had no body, and the final squash added that context.

Before confirming, check the diff, verification, merge readiness, final message, and author and co-author attribution.

### Guidance for development assistants

Before the first commit, read the project’s applicable instructions and its referenced commit rules. In a handoff, identify the record you are preparing. For a PR, provide **PR Title** and **PR Body**. For a squash, provide **Commit message** and **Extended description**, explicitly say to leave the description blank when appropriate, and supply one copy-ready version. Apply the same workflow across assistants.

GitHub uses the [central community defaults](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) for supported files when a project does not supply its own. Those defaults are served by GitHub and are absent from the project clone. For assistant discovery, link this handbook’s commit and PR sections from instructions the chosen assistant actually loads, or include the links in the task and ask it to read them before committing.

### Contributing to other projects

When opening an issue or PR in a repository maintained by someone else, use this order.

1. Follow the target project's explicit contribution guide, issue or PR template, maintainer instructions, repository development rules, and applicable official guidance.
2. If the project is silent, look at several representative recent open and merged PRs. Compare titles, bodies, commit subjects, merge practices, language, and maintainer feedback before treating a pattern as an established convention.
3. If there is no clear pattern, use a clear English title and a body the target community can understand. Describe the work and its verification accurately.

The target project decides whether to use a title prefix, English summary, template, or squash merge. If its guidance conflicts or is unclear, flag the uncertainty and leave upstream rules to its maintainers.

## 7. 🧪 Checks and automation

Add GitHub Actions when a repository benefits from a repeatable check. A small or early repository can stay without CI. Before a meaningful release, run the checks the project already has, even when there is no Actions workflow.

A green check means those commands passed in that run. Tagging, publishing a Release, and deploying remain separate decisions. If a workflow publishes anything, start it from a tag or a manual run.

Start with one useful job. Add more only for a real need.

Keep raw CI logs and large build outputs in Actions artifacts or an appropriate report location. In the issue, summarize the outcome and link to the evidence. Remove secrets, tokens, private data, and sensitive internal configuration before uploading public attachments. Issue forms accept specific file formats and allow up to 10 MB per image and 25 MB per accepted document, text file, or archive. See [GitHub's issue form upload limits](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-form-schema#supported-file-types-and-size-limits).

## 8. 📦 Versions and releases

Tag a version when it is meaningful to you or to a user. Skip tags for typos, private notes, and unfinished work.

Use semantic versions, `MAJOR.MINOR.PATCH`:

| Part | Change |
|---|---|
| MAJOR | A breaking change |
| MINOR | Compatible new behavior |
| PATCH | A compatible fix |

```bash
git tag -a v0.1.0 -m "First usable version"
git push origin v0.1.0
```

When a version is worth publishing, run the relevant checks, update the CHANGELOG if the project keeps one, create the tag, then create the Release.

Create a GitHub Release when users need notes or downloadable files. A tag can exist without a Release. Early versions can ship source first. Put published binaries on the Release, and keep generated build output out of source history.

Keep a CHANGELOG once people follow versions. Early private work can rely on Git history and Release notes.

Use GitHub Packages only when the project publishes a library or an installable build.

## 9. 📝 Documentation

A public README should say what problem the project solves, what it does not do, how to use it, and which license applies. Add features, install steps, configuration, examples, tests, and a roadmap when they help. Explain a command before asking someone to run it.

Use `README.md` and `README.zh-CN.md`, linked at the top, when both languages are useful. Detailed notes can stay in one language.

Add `CONTRIBUTING` when other people send changes. It can point to this handbook.

A public repository should include a license file when the work is meant to be reused. See the [Licensing Standard](LICENSING.md) for how ForgottenLab chooses, declares, and reviews licenses. This `.github` repository does not license other projects.

## 10. 🔐 Security

- Keep tokens, passwords, private keys, and private machine configuration out of commits and issues.
- Leave `.env`, `secrets/`, and local credential files untracked.
- Read `git diff` before every commit.
- Back up before a change that is hard to undo, and give a restore step when you can.
- State a destructive action plainly. Do not stop or replace an existing service unless the user asks.
- A tool that writes configuration or restarts a service should be testable without touching the real environment.
- Treat publishing, force-push, history rewrite, and deletion of shared work as their own decisions.
- Leave unrelated work untouched.
- Passing tests, creating a tag, and deploying are three separate steps.

Do not disclose unpatched vulnerabilities or exposed secrets in public issues. A dedicated private reporting channel has not been configured.

## 11. 🧭 Defaults

- Primary branch: `main`, including direct low-risk commits
- Branches and pull requests for large or shared work
- No required reviewer
- CI only where a repeated check helps
- Versions when they mean something
- Descriptive issue titles, native issue types, few labels

Start from a real problem. Prefer the safer default. Explain a command before running it, back up before changing something hard to undo, and test before you publish. Document for your future self and improve through real feedback.

### Reuse-first development

Before starting a substantial feature or a standalone project, check what the current project, other ForgottenLab repositories, and the relevant open-source ecosystem already provide. Use official documentation and upstream components to verify fit and licensing. Start with what can be used directly. Consider extending or fixing an existing project, contributing upstream, or combining projects or reusing a module before starting a new repository.

A new project can have independent value as a learning experiment or because it needs a different architecture, safety boundary, compatibility target, or clear innovation. Keep the research proportional to the decision. A routine fix needs only a focused check.
