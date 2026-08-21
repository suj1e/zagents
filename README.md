# zagents

个人 ZCode 子智能体配置集合。

每个 `.md` 是一个独立子智能体——有专门的角色、边界、工具用法和输出格式。主智能体调度它们干专业活,自己不参与执行细节。

> 这里的子智能体走"宁缺毋滥"原则:只放实际验证过、真正能减轻重复劳动的配置。不预防性铺设。

## 已有

| 子智能体 / Skill | 职责 |
|---------|------|
| [`glean`](agents/glean.md) | 感知与检索专员:多模态识图 / OCR / 图表提取 + 联网·本地·代码检索,返回结构化结论与出处 |
| [`zarchitect`](skills/zarchitect/SKILL.md) | 通用方案设计 skill:需求文档/代码库/bug 分析 → 需求拆解 → 方案设计(含设计模式 + 性能优化) → 画图 → 开 openspec change → 自动触发 ztest |
| [`debugger`](agents/debugger.md) | 调试/故障排查专员:读日志、trace 调用链、定位根因、提出修复建议。遇到报错、测试失败、诡异行为、线上故障时使用。 |
| [`craftsman`](agents/craftsman.md) | 实施执行专员:接收任务后按 TDD 红→绿→重构写代码,交付测试 + 实现 + 覆盖率报告。 |

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

Skills 放在 `skills/<name>/SKILL.md`,被 ZCode 自动发现和调度。

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
