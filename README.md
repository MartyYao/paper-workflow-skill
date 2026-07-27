# Paper Workflow Skill

> 面向金融学、会计学、公司金融专业学者的实证论文全流程编排器。
> 从选题到投稿，8 阶段方法论框架。

## 8 阶段流程

| 阶段 | 内容 | 产出 |
|------|------|------|
| **0 — 选题设计** | 文献全景扫描 → Edmans 护栏过滤 → 可行性评估 | `01-选题/研究计划.md` |
| **1 — 文献检索与综述** | **中文文献**：[Chinese-Literature-Skill](https://github.com/MartyYao/Chinese-Literature-Skill)（CNKI RSS + CNKI 浏览器搜索 + NCPSSD API 三通道）/ **英文文献**：OpenAlex + Semantic Scholar → Zotero 精读 → 主题综述 | `02-文献/文献综述.md` |
| **2 — 理论分析与假设** | 制度背景 → 理论推演 → 竞争性解释 | `03-理论/理论推演.md` |
| **3 — 研究设计** | 识别策略审计 → 变量构造方案 | `04-数据/变量定义.md` |
| **4 — 数据构建** | Stata do 文件 → 清洗 → merge → 描述统计 | do 文件 + 数据报告 |
| **5 — 实证分析** | 主回归+机制+稳健性+异质性+内生性 → 决策门 | 全部实证表格 |
| **6 — 论文写作** | 章节生成 → 润色 | 初稿 |
| **7 — 打磨与投稿** | 5 阶段打磨流水线 → 期刊匹配 | 终稿 + 投稿清单 |

## 配套技能

本技能在各阶段委托了专用技能。使用时建议同时加载：

| 阶段 | 技能 | 负责内容 | GitHub |
|------|------|----------|--------|
| **1 — 文献检索** | `Chinese-Literature-Skill` | 中文文献三通道采集（CNKI RSS + 浏览器搜索 + NCPSSD API） | [链接](https://github.com/MartyYao/Chinese-Literature-Skill) |
| **4-5 — Stata 实证** | `Stata-Regression-Skill` | Do 文件模板、回归、出图、出表、计量检查 | [链接](https://github.com/MartyYao/Stata-Regression-skill) |

paper-workflow 本身只负责论文层面的逻辑决策：
- 8 阶段流程编排
- V1/V2 主次策略
- 机制检验三步法协议
- 处理强度连续得分策略
- 组件决策门规则
- Obsidian 同步协议

## v0.1.2 更新说明

- Stata 回归工作全面委托给 `Stata-Regression-skill`（v0.1.0）
- paper-workflow 不再直接包含 Stata 编码规范、出图模板、表格格式和陷阱清单
- 论文层面的逻辑（V1/V2 策略、机制检验协议、处理强度连续得分、组件决策门）保留在本技能

## 安装与使用

### Claude Code

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
claude -p "按 paper-workflow 指导我完成阶段 X"
```

### Codex

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
codex exec "加载 paper-workflow，进入阶段 X"
```

### Kimi Code

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git  
cd paper-workflow-skill
kimi -p "请按 paper-workflow skill 指导我完成阶段 X"
```

### 任意 Agent

将 `SKILL.md` 路径告知 Agent，Agent 会根据当前阶段自动选取对应方法。

## 项目结构

```
paper-workflow-skill/
├── README.md
├── AGENTS.md              ← Codex 入口
├── CLAUDE.md              ← Claude Code 入口
├── SKILL.md               ← 8 阶段方法论框架
└── references/            ← 论文层面参考文档
    ├── csmar-data-pitfalls.md
    ├── data-sourcing-province-bureaus.md
    ├── data-variable-guide.md
    ├── edmans-guardrails.md
    ├── empirical-exploration-patterns.md
    ├── empirical-table-format-spec.md
    ├── lit-review-empirical-mismatch.md
    ├── mechanism-exploration-log.md
    ├── mechanism-exploration-protocol.md
    ├── mechanism-testing-methodology.md
    ├── parallel-trends-sub-dv.md
    ├── pdf-extraction-workflow.md
    └── theoretical-analysis-template.md
```

## 依赖

- [Chinese-Literature-Skill](https://github.com/MartyYao/Chinese-Literature-Skill) — 阶段 1 中文文献采集
- [Stata-Regression-skill](https://github.com/MartyYao/Stata-Regression-skill)（v0.1.0+）— 阶段 4-5 的 Stata 技术底层
- Stata 18+（或 17，`reghdfe` 等包需安装）
- Python 3.10+（pandas, numpy, scipy, matplotlib, openpyxl）

## 致谢

本技能的方法论框架借鉴了 AERS（Applied Econometric Research Skills）生态系统的相关工作流设计。中文文献采集委托给 [Chinese-Literature-Skill](https://github.com/MartyYao/Chinese-Literature-Skill)，Stata 技术实现委托给 [Stata-Regression-skill](https://github.com/MartyYao/Stata-Regression-skill)。

## 许可证

MIT
