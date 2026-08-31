# AGENTS.md

个人 ZCode 子智能体配置集合。纯内容仓库——只有 markdown，没有构建 / lint / 测试命令，改完用 `git diff` 自查即可。

## 仓库结构

- `agents/*.md` — 每个文件一个独立子智能体（当前 5 个：glean / doctor / craftsman / docswriter / zapply-reviewer）
- `README.md` — 对外说明，「已有」表格必须与 `agents/` 目录实际文件保持一致
- `LICENSE` — MIT

## 硬性边界

**本仓库只放 agents（子智能体）；skills 一律放 [zskills](https://github.com/suj1e/zskills) 仓库，别混放。**

## 新增 / 修改 agent 的约定

- 文件格式：YAML frontmatter（`name` / `description` / `color` / 可选 `model` / `injectAgentsMd`）+ Markdown 正文（角色定位 + 职责边界 + 明确不做什么 + 输出格式）
- `description` 是调度关键，必须写清「何时该用、做什么、不做什么」
- `name` 不要与 ZCode 内置 agent 重名（例：审查 agent 叫 `zapply-reviewer` 而非 `code-reviewer`，因为内置已有 code-reviewer；它内部分层调用内置 code-reviewer）
- 新增 agent 走「宁缺毋滥」原则：只放实际验证过、真正减轻重复劳动的配置，不预防性铺设
- 内容用中文书写

## 镜像维护（容易踩的坑）

以下条款在 zskills 仓库有详细版，**改任一侧必须双向同步**：

- `agents/zapply-reviewer.md` 的 15 维清单 ↔ zskills `skills/zapply/references/code-reviewer-prompt.md`
- `agents/craftsman.md` 的 TDD / DESIGN 条款 ↔ zskills `skills/zapply/references/craftsman-prompt.md`

改这些文件时先检查另一侧是否需要同步，同步后两边各自提交。

## 历史改名记录（避免引用失效）

- `architecter` → `doctor`（调查与设计一体专员）
- `docwriter` → `docswriter`（与内置工具名拉开距离）
- `code-reviewer` → `zapply-reviewer`
