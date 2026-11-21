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

`feat`, `fix`, and `docs` cover most commits. Add `build`, `ci`, or `style` only when they fit. A published version is a tag, not a `release:` commit. Keep the subject imperative and about one line. Use an English type prefix. Maintainers should prefer a concise, precise English description in the subject. Use Chinese or English in the body for technical context, verification, compatibility, or rollback details when useful. One commit should be one coherent change.

The English subject preference is guidance. Existing Chinese commit subjects remain valid, and no commit language checks are required.

```text
feat: add config export
fix: prevent concurrent installer launches
docs: clarify when to tag a version
```

## 5. 💬 Issues

Choose the project's maintenance communication language in this order. It guides the issue body and remains the default for maintainer pull request titles and bodies.

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

Maintainers default to the project's maintenance communication language for both the pull request title and body. Use Simplified Chinese in projects maintained in Simplified Chinese and add an English summary when it helps readers. Use English in projects maintained in English. Accept pull requests from external contributors in English or Simplified Chinese. Full translations are optional, and there are no mandatory language checks.

`.github/pull_request_template.md` prefills the description. A repository can provide its own pull request template to override this default.

### Pull request descriptions and squash merges

Use the PR description as the durable review record. Include what changed, why, and how it was verified. Add compatibility, safety boundaries, known limitations, and related issues when relevant. Keep the final commit subject concise and traceable, following the [commit conventions](#4--commits). Include a commit body when important technical context needs to stay in Git history.

For a PR that represents one logical change, prefer Squash and merge where available. Keep intermediate commits during development as needed. Choose another allowed merge method when the individual commits need to remain in the default branch history.

With GitHub's **Default message**, a one-commit PR starts with that commit's title and message. A PR with multiple commits starts with the PR title and a list of commits. Reuse an accurate single-commit message. For a multi-commit PR, check the proposed subject before merging and edit it when needed to follow the commit conventions, even when the PR title follows a different project language. The default format does not extract custom Markdown sections from the PR description. A separate `Squash Summary` section and copying the whole PR description are unnecessary. See [GitHub's squash message options](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests).

Before merging, confirm the actual diff, necessary checks, merge readiness, final commit message, and author and co-author attribution. Preserve technical details and verified attribution that need to survive the squash.

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
