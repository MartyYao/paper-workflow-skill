# Paper Workflow Skill — Claude Code 指令

本仓库是 8 阶段论文全流程编排器的知识库。当你被要求帮助用户完成论文写作流程时，请按以下规则操作。

## 核心文件

- `SKILL.md` — 主技能文件（669 行），包含 8 阶段完整流程、决策门规则、交互规范
- `references/` — 14 份方法论文档，按需加载

## 阶段总览

| 阶段 | 内容 | 关键文件 |
|------|------|---------|
| 0 — 选题设计 | 文献扫描 + 护栏过滤 + 可行性 | `references/edmans-guardrails.md` |
| 1 — 文献检索 | CNKI + OpenAlex 系统检索 | 直接调用工具 |
| 2 — 理论分析 | 制度背景 + 假设推演 | `references/theoretical-analysis-template.md` |
| 3 — 研究设计 | 识别策略 + 变量定义 | 按需加载 AERS 方法论 |
| 4 — 数据构建 | Stata do 文件 | `references/csmar-data-pitfalls.md`, `references/data-variable-guide.md` |
| 5 — 实证分析 | 全部回归 + 决策门 | `references/mechanism-exploration-protocol.md`, `references/mechanism-testing-methodology.md`, `references/empirical-table-format-spec.md`, `references/stata-pitfalls.md`, `references/empirical-exploration-patterns.md` |
| 6 — 论文写作 | 章节生成 + 润色 | — |
| 7 — 打磨投稿 | 5 阶段流水线 + 期刊匹配 | — |

## 交互规则

1. **先读 SKILL.md 再问** — 不要问"你想做什么阶段"，先看当前状态再推进
2. **核心文档优先** — 每个阶段的关键 reference 在 SKILL.md 中标注，优先加载
3. **决策门执行** — 阶段 5 完成后逐组件评估（主回归/平行趋势/机制/稳健性/经济后果），不是只看主回归 p 值
4. **改实证必回写** — 实证结果变化后必须同步更新研究计划和理论推演

## 执行顺序

阶段 3-5 形成快速迭代环。阶段 5 结果不满足决策门时回退到阶段 3/4/2/0。

具体流程和检查清单见 `SKILL.md` 对应章节。
