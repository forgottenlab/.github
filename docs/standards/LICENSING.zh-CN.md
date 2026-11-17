# 📜 ForgottenLab 开源许可证统一规范

[English](LICENSING.md) | [简体中文](LICENSING.zh-CN.md)

> 这是工程实践建议，不是法律意见，也不会自动授予任何其他仓库使用许可。
> 目标：统一**选择流程、声明格式、第三方审查和发布门槛**，而不是强制所有项目采用同一种许可证。

## 1. 🎯 基本原则

1. **逐仓库授权**：每个需要公开复用的项目，都应在自身根目录提供完整、未经擅改的 `LICENSE`。本 `.github` 工程规范不能代替其他仓库的许可证。
2. **权利先行**：确认原创部分的著作权归属、外部贡献授权及引用代码的来源；不知道来源时先不公开或不纳入快照。
3. **默认建议而非强制**：ForgottenLab 自有小型工具与应用默认优先评估 MIT；有明确专利授权需求时考虑 Apache-2.0；基于现有开源项目衍生时遵循上游条件。特殊作品单独决策。
4. **授权不等于发布**：仓库 `Private` / `Public`、npm 的 `"private": true`、GitHub Release、`package.json` 的 `license` 字段是不同概念；`LICENSE` 与合法授权才说明对外许可范围。
5. **保留第三方义务**：不可用自有项目的 MIT 或 Apache-2.0 声明覆盖不属于自己的第三方代码、资产、随包分发的软件，或运行时下载的外部软件。
6. **简洁优先**：不强制每个源文件添加许可证头，也不强制为小项目设置 CLA、自动许可扫描或复杂合规系统；发生真实需要时再引入。

## 2. ⚖️ 许可证选择指引

| 场景 | 默认考虑 | 为什么 / 注意 |
|---|---|---|
| 原创 CLI、普通工具、个人应用 | **MIT** | 文本简短、宽松、要求保留版权与许可证声明；不附加明确的 Apache 式专利授权条款 |
| 原创基础设施库、SDK，且需要明确专利授予 | **Apache-2.0** | 明确贡献者专利授权与专利诉讼终止规则；修改文件需标明变更；分发衍生作品时保留上游 NOTICE 中适用的归属声明；原创项目不强制创建 NOTICE |
| 希望衍生版本继续开源 | 单独讨论 GPL、MPL 等 | 这是不同的授权目标，不能自动套用 MIT |
| 修改、复制上游开源软件 | **先核对上游许可证** | 是否可以再许可、必须保留哪些声明，依具体来源而定 |
| 图片、Logo、字体、音视频、第三方数据 | **逐项确认授权** | 不要默认软件 LICENSE 覆盖或取得这些素材的权利 |
| 仅私人保存、未确定权利的仓库 | 暂不发布开源许可 | 不要为了填字段写入虚假的许可证标识 |

**MIT 与 Apache-2.0 均允许商业使用**。`MIT` 不意味着放弃版权；`Apache-2.0` 也不意味着每个原创项目都必须额外提供 NOTICE 文件。

没有许可证时，适用默认著作权法。把 GitHub 仓库设为 Public，其他 GitHub 用户仍可按服务条款查看和 fork；这不等于授予 MIT、Apache-2.0 或其他开源许可证下的复用权。

## 3. 📁 每个公开软件仓库的最低结构

```text
project/
├── LICENSE                  # 该仓库完整的官方许可证文本
├── README.md                # 顶部中英切换，正文说明授权范围
├── README.zh-CN.md
└── package.json / ...       # 有相应元数据格式时使用 SPDX 标识
```

- 将许可证**官方英文全文**放在仓库内。不要仅链接到外部网站，也不要把翻译替代为有法律效力的英文原文。GitHub 通常识别仓库根目录的 `LICENSE`、`LICENSE.md` 或 `LICENSE.txt`；ForgottenLab 使用 `LICENSE`。
- GitHub **不能**通过本 `.github` 仓库提供默认许可证。许可证文件必须放进各个项目，才会随克隆、打包或下载一起提供。
- README 简洁写明 `Licensed under the MIT License. See [LICENSE](LICENSE).` 或项目实际许可证，并说明单独授权的文件、素材或运行时下载的软件；中文 README 同步。
- JavaScript / TypeScript 的 `package.json` 按实际许可证使用 SPDX 标识，例如 `"license": "MIT"` 或 `"Apache-2.0"`。只有在不授予任何使用权时才使用 `"UNLICENSED"`。**可同时保留 `"private": true"`**，它会让 npm 拒绝发布该包，并不能让 GitHub 仓库保持 Private。
- 代码文件有必要时使用 `SPDX-License-Identifier: MIT` 等标准简写；不是所有仓库的强制项。MIT 没有标准许可证头。
- 其他语言使用其生态标准许可证元数据，不一律照搬 npm 字段。
- 如果某些目录使用不同许可证，要在具体文件或目录明确标识，并携带对应完整文本。

## 4. ©️ 著作权声明

- MIT 模板中的 `Copyright (c) YEAR HOLDER` 应填写**真正有权授予许可的权利人**；按实际作品情况填写适当的版权年份。
- `ForgottenLab` 是品牌和 GitHub 标识，**不自动证明其为独立法律实体或权利所有者**。只有在权利人确认适合以此名称署名时才使用。
- 外部贡献者及复制代码的原有著作权声明不能被任意替换为 `ForgottenLab`。
- 授权以后可在条件允许时调整**未来版本**，但已向他人合法授出的旧版本许可通常不会因修改仓库文件自动撤销。

## 5. 🔍 发布前的来源与第三方检查

- [ ] 明确拟公开的**所有**源码、脚本、配置示例与资产来源。
- [ ] 保留已复制代码的上游版权、许可证、NOTICE 和必要声明；未知授权内容隔离处理。
- [ ] 分辨直接分发的依赖与运行时下载的外部软件；每种情形分别检查适用义务。
- [ ] `LICENSE` 与 README、项目元数据一致。真正授予许可后，删除过期的 `UNLICENSED` 声明。
- [ ] 检查拟提交文件和拟推送的 Git 历史，排除私钥、密码、Token、真实节点配置、个人路径和敏感数据。
- [ ] 运行适用的构建和安全测试；再核对 `git diff --cached`，最后决定提交和推送。
- [ ] 不用“测试通过”替代著作权来源确认。

## 6. 🤝 外部贡献

- 项目接收贡献时，应在贡献指南中说明：仅提交拥有相应权利的内容；说明第三方来源；通常以项目当前许可证贡献。
- 不默认要求贡献者签署 CLA 或放弃个人版权。发生实质共同开发、双重许可或商业再许可需求时再单独决定。

## 7. 🧭 变更管理

- 统一规范集中存放在 `forgottenlab/.github/docs/standards/`；各项目 README 引用本规范即可。
- **每个项目自行拥有和维护自己的 LICENSE**，不得假设 `.github` 默认社区文件能继承许可证。
- 变更已有公开项目的许可前，检查贡献者授权及历史许可承诺；避免批量替换所有仓库的 LICENSE。
- 对新的原创工具推荐 MIT，但最终选择始终是项目级决定。

## 8. 📖 参考来源

- GitHub — 为仓库选择许可证：https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
- GitHub — 默认社区健康文件：https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file
- MIT License：https://choosealicense.com/licenses/mit/
- Apache License 2.0：https://www.apache.org/licenses/LICENSE-2.0
- SPDX 许可证列表：https://spdx.org/licenses/
- npm `package.json` 的 `license` 与 `private`：https://docs.npmjs.com/cli/v11/configuring-npm/package-json/
