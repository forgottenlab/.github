# 📜 ForgottenLab Licensing Standard

[English](LICENSING.md) | [简体中文](LICENSING.zh-CN.md)

> This is engineering guidance, not legal advice. It does not license any other repository by itself.
> It standardizes the **decision process, declarations, provenance review, and release gates**—not one compulsory license for every project.

## 1. 🎯 Principles

1. **License each repository separately.** A reusable public project should contain a complete `LICENSE` file at its root. This `.github` handbook does not license the code of other repositories.
2. **Confirm ownership first.** Check authorship, rights to relicense, third-party contributions, and borrowed code. Exclude anything whose origin or permission cannot be established.
3. **Use defaults, not blanket rules.** Prefer evaluating MIT for small original ForgottenLab tools. Consider Apache-2.0 where express patent rights matter. Respect upstream terms for derivatives.
4. **Separate licensing from visibility and distribution.** GitHub `Private` / `Public`, npm `"private": true`, a Release, and a package `license` field serve different purposes.
5. **Preserve third-party obligations.** An original project's license never supersedes licenses on copied code, bundled software, runtime-downloaded software, or assets.
6. **Keep the process lightweight.** Per-file headers, CLAs, and automated license compliance are optional unless a real need appears.

## 2. ⚖️ Decision Guide

| Situation | Default to evaluate | Notes |
|---|---|---|
| Original CLI tools and general-purpose apps | **MIT** | Short and permissive; preserve copyright and license notices; no Apache-style express patent grant |
| Original infrastructure libraries or SDKs where explicit patent terms matter | **Apache-2.0** | Express contributor patent grant and litigation-termination rule; mark modified files; retain applicable upstream NOTICE attributions when distributing derivatives; original projects do not need a NOTICE file by default |
| A desire to require derivatives to remain open source | Discuss GPL, MPL, and similar licenses individually | This is a different licensing objective |
| Derived or copied upstream software | **Review the upstream license first** | Reuse and relicensing depend on the upstream permissions |
| Images, logos, fonts, media, third-party datasets | **Verify rights per item** | A software license is not a blanket grant for assets |
| Private work with uncertain ownership | Do not declare it open source yet | Avoid misleading metadata such as a false SPDX identifier |

Both MIT and Apache-2.0 permit commercial use. MIT does not transfer copyright to the public. Apache-2.0 does not require a separate `NOTICE` file in every original project.

Without a license, default copyright law applies. Making a GitHub repository public still lets other GitHub users view and fork it under GitHub's Terms of Service; that is not a grant to reuse the code under MIT, Apache-2.0, or any other open-source license.

## 3. 📁 Minimum Public Repository Structure

```text
project/
├── LICENSE                  # Full official license text for this repository
├── README.md                # License scope and language switch
├── README.zh-CN.md
└── package.json / ...       # SPDX metadata where the ecosystem has one
```

- Put the **full official English license text** in the repository. An external URL or a translation does not replace it. GitHub commonly detects `LICENSE`, `LICENSE.md`, or `LICENSE.txt` at the repository root; ForgottenLab uses `LICENSE`.
- GitHub cannot supply a default license from this `.github` repository. License files must live in each project so they are included when that project is cloned, packaged, or downloaded.
- In both READMEs, link to `[LICENSE](LICENSE)` and describe any separately licensed files, assets, or runtime-downloaded software.
- For Node.js / TypeScript repositories, set `"license"` to the actual SPDX identifier, such as `"MIT"` or `"Apache-2.0"`. Use `"UNLICENSED"` only when no rights are granted. `"private": true` may stay enabled so npm refuses to publish the package; it does not keep a GitHub repository private.
- Use `SPDX-License-Identifier` headers only when they help; they are not required for every small repository. MIT has no standard license header.
- Use ecosystem-specific metadata in other languages. If parts have different licenses, identify them explicitly and include the required license texts.

## 4. ©️ Copyright Ownership

- In an MIT license, replace `Copyright (c) YEAR HOLDER` with the **actual rights holder(s)** and an appropriate copyright year.
- `ForgottenLab` is a project identity and GitHub name. It is **not automatically a legal person or proof of copyright ownership**. Use it only if the rights holder determines that attribution is accurate.
- Preserve third-party and contributor notices. Do not rewrite their copyright as ForgottenLab's.
- New licensing choices generally cannot retroactively revoke permissions already granted for previously licensed copies.

## 5. 🔍 Pre-publication Review

- [ ] Establish provenance of **all** proposed source files, scripts, examples, and assets.
- [ ] Retain upstream license texts, copyrights, and applicable NOTICE information for reused materials.
- [ ] Distinguish bundled or distributed third-party software from software downloaded at runtime; each case has its own obligations.
- [ ] Check consistency among `LICENSE`, README, and metadata. Remove stale `UNLICENSED` claims once a license is actually granted.
- [ ] Inspect staged content **and the history to be pushed** for secrets, private node data, personal paths, and private configuration.
- [ ] Run relevant build and security checks; review `git diff --cached` before committing.
- [ ] Treat test success and rights verification as separate requirements.

## 6. 🤝 Contributions

Contributors should submit only material they have the right to license, disclose third-party sources, and normally contribute under the repository's stated license. Do not impose a CLA or copyright assignment by default; consider them separately if there is a real need.

## 7. 🧭 Maintenance

- Keep this policy in `forgottenlab/.github/docs/standards/` and link to it from individual projects as needed.
- **Each project owns its own `LICENSE`.** GitHub default community health files do not distribute or inherit a license.
- Before changing a published project's license, review historical grants, contributor rights, and existing obligations. Do not mass-replace licenses.
- MIT is a recommended starting point for new original software—not an automatic or compulsory license.

## 8. 📖 References

- GitHub — Licensing a repository: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
- GitHub — Default community health files: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file
- MIT License: https://choosealicense.com/licenses/mit/
- Apache License 2.0: https://www.apache.org/licenses/LICENSE-2.0
- SPDX license list: https://spdx.org/licenses/
- npm `package.json` `license` and `private`: https://docs.npmjs.com/cli/v11/configuring-npm/package-json/
