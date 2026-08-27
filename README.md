# zagents

个人 ZCode 子智能体配置集合。

每个 `.md` 是一个独立子智能体——有专门的角色、边界、工具用法和输出格式。主智能体调度它们干专业活,自己不参与执行细节。

> 这里的子智能体走"宁缺毋滥"原则:只放实际验证过、真正能减轻重复劳动的配置。不预防性铺设。

**职责边界**:本仓库只放 agents(子智能体);skills 一律放 [zskills](https://github.com/suj1e/zskills) 仓库,别混放。

## 已有

| 子智能体 | 职责 |
|---------|------|
| [`glean`](agents/glean.md) | 感知与检索专员:多模态识图 / OCR / 图表提取 + 联网·本地·代码检索,返回结构化结论与出处 |
| [`architecter`](agents/architecter.md) | 调查与设计一体专员:证据驱动根因诊断（trace 调用链/平台专项）+ 文件级修复蓝图（影响面/备选/trade-off）。bug、故障、性能劣化、"先查清再修"场景使用 |
| [`craftsman`](agents/craftsman.md) | 执行专员:按指令编码落地;指令含测试策略时按 TDD 红→绿→重构执行,交付测试 + 实现 + 覆盖率报告 |
| [`docswriter`](agents/docswriter.md) | 文档工程专员：新写 / 优化 / 调整项目文档(README、API、changelog、迁移指南、设计转述)。收到大纲与素材直接执笔落盘;术语一致、不编造、示例必摘真实代码 |
| [`zapply-reviewer`](agents/zapply-reviewer.md) | zapply 审查专员：先做依赖决策阶梯 + 15 维清单分析，再调用内置 code-reviewer 做代码质量审查，汇总输出 blocker/suggestion 分级报告。zapply 核实门禁使用,绝不修改代码 |

## 怎么用

把需要的 `.md` 复制到你的 ZCode 子智能体目录:

```bash
# 用户级(对所有项目生效)
cp agents/glean.md ~/.zcode/agents/

# 或项目级(只对某个项目生效)
cp agents/glean.md <project>/.zcode/agents/
```

复制后按你自己的环境调整 frontmatter:
- `model` — 默认不写(继承主智能体模型)。想为子智能体指定专门的模型,就加 `model` 字段填你环境的模型 ID。
- 其他字段一般不用改。

## 子智能体配置格式

每个 `.md` 用 YAML frontmatter + Markdown 正文:

```markdown
---
name: "agent-name"
description: "何时调用 + 做什么(主智能体靠这个决定调度)"
color: pink
model: "..."            # 可选,指定专门模型
injectAgentsMd: true    # 可选,是否注入 AGENTS.md
---

# 角色
...角色定位 + 职责边界 + 明确不做什么...

# 输出格式
...结构化返回模板...
```

`description` 是关键——它决定主智能体在什么场景调度这个子智能体。要写清"何时该用、做什么、不做什么"。

## License

MIT
