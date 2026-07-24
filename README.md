# Paper Workflow Skill

> 🎓 **面向金融学、会计学、公司金融专业学者的实证论文全流程编排器**
> 从选题到投稿，8 阶段方法论框架，含 14 份实战参考文档。

## 适用对象

- 金融学、会计学、公司金融领域的研究人员（CSSCI 目标）
- 使用 Stata 进行实证分析的学者
- 需要系统化论文撰写流程的博士生、青年教师

**不是**零基础教程——本技能假定你已掌握基本的计量经济学和 Stata 操作，提供的是方法论文档、检查清单和决策门规则。

## 8 阶段流程

| 阶段 | 内容 | 产出 |
|------|------|------|
| **0 — 选题设计** | 文献全景扫描 → Edmans 护栏过滤 → 可行性评估 | `01-选题/研究计划.md` |
| **1 — 文献检索与综述** | CNKI + OpenAlex → Zotero 精读 → 主题综述 | `02-文献/文献综述.md` |
| **2 — 理论分析与假设** | 制度背景 → 理论推演 → 竞争性解释 | `03-理论/理论推演.md` |
| **3 — 研究设计** | 识别策略审计 → 变量构造方案 | `04-数据/变量定义.md` |
| **4 — 数据构建** | Stata do 文件 → 清洗 → merge → 描述统计 | do 文件 + 数据报告 |
| **5 — 实证分析** | 主回归+机制+稳健性+异质性+内生性 → 决策门 | 全部实证表格 |
| **6 — 论文写作** | 章节生成 → meng-skills 润色 | 初稿 `.docx` |
| **7 — 打磨与投稿** | 5 阶段打磨流水线 → 期刊匹配 | 终稿 + 投稿清单 |

其中阶段 3-5 构成**快速迭代环**，实证不通过时自动回退。

## 安装与使用

### Hermes

克隆到 `~/.hermes/skills/research/` 下：

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git ~/.hermes/skills/research/paper-workflow/
```

在 Hermes 中加载：`skill_view(name='paper-workflow')`，或直接说"写论文"触发。

### Claude Code

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
claude -p "加载 paper-workflow skill，进入阶段 X" --dangerously-skip-permissions --permission-mode bypassPermissions
```

或克隆后进入目录直接运行 `claude`（CLAUDE.md 自动加载）。

### Codex / OpenClaw

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
codex exec "加载 paper-workflow，进入阶段 X"
# 或
openclaw --context paper-workflow-skill
```

AGENTS.md 在项目根目录，会自动用于项目上下文。

### Pi

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
pi -p "请按 paper-workflow skill 指导我完成阶段 X"
```

也可将 SKILL.md 作为上下文直接粘贴给 Pi。

### Kimi Code

```bash
git clone https://github.com/MartyYao/paper-workflow-skill.git
cd paper-workflow-skill
kimi -p "请按 paper-workflow skill 指导我完成阶段 X"
```

也可将 SKILL.md 作为上下文直接粘贴给 Kimi Code。

## 依赖

本技能是**方法论框架**，不包含 Python 代码或可执行脚本。运行依赖：

| 依赖 | 用途 | 备注 |
|------|------|------|
| **Obsidian** | 项目仪表盘 + 文档管理 | 可选，可改用其他笔记系统 |
| **Stata** | 数据清洗 + 回归分析 | 核心依赖，所有实证命令为 do 文件 |
| **Zotero** | 文献管理 | 用于精读和引用 |
| **meng-skills v2** | 中文润色 + 去 AIGC | 仅 Hermes 环境 |
| **AERS** | 方法论补充 | 可选，通过 aers-index 按需加载 |

## 文件夹结构

```
paper-workflow-skill/
├── README.md                     ← 本文件（总入口）
├── SKILL.md                      ← Hermes 原生 skill 文件
├── CLAUDE.md                     ← Claude Code 项目指令
├── AGENTS.md                     ← Codex / OpenClaw 项目指令
├── references/
│   ├── edmans-guardrails.md                ← Edmans(2024) 选题质量护栏
│   ├── empirical-table-format-spec.md      ← 实证表格格式规范（12条）
│   ├── stata-pitfalls.md                   ← Stata 17条技术坑与修复
│   ├── csmar-data-pitfalls.md              ← CSMAR 数据合并陷阱
│   ├── mechanism-testing-methodology.md    ← 机制检验方法论
│   ├── mechanism-exploration-protocol.md   ← 机制探索规程（6步骤）
│   ├── mechanism-exploration-log.md        ← 机制探索日志模板
│   ├── theoretical-analysis-template.md    ← 理论分析模板
│   ├── empirical-exploration-patterns.md   ← 实证探索模式
│   ├── data-variable-guide.md              ← 变量构造指南
│   ├── data-sourcing-province-bureaus.md   ← 省级大数据局数据来源
│   ├── parallel-trends-sub-dv.md           ← 平行趋势与子 DV
│   ├── lit-review-empirical-mismatch.md    ← 文献综述与实证错配案例
│   └── pdf-extraction-workflow.md          ← PDF 表格提取工作流
```

## 项目仪表盘（Obsidian）

每个论文项目在 Obsidian vault 根目录下创建独立文件夹：

```
论文/<项目名>/
├── 00-项目仪表盘.md           ← 跨会话状态中枢（必读）
├── 01-选题/
│   └── 研究计划.md
├── 02-文献/
│   ├── 文献综述.md
│   └── 论文精读/
├── 03-理论/
│   ├── 制度背景.md
│   └── 理论推演.md
├── 04-数据/
│   ├── 数据需求清单.md
│   ├── 数据构造/
│   └── 分析命令/
├── 05-实证/
│   └── 主回归结果.md
├── 06-论文稿/
└── 07-投稿/
```

## 跨 Agent 支持矩阵

| Agent | 入口文件 | 加载方式 | 已验证 |
|-------|---------|---------|--------|
| **Hermes** | `SKILL.md` | `skill_view(name='paper-workflow')` | ✅ |
| **Claude Code** | `CLAUDE.md` | 自动加载（项目目录下） | ✅ |
| **Codex** | `AGENTS.md` | `--context` 或项目指令 | ✅ |
| **Pi** | 直接读 `SKILL.md` | `-p` 参数或上下文粘贴 | ✅ |
| **Kimi Code** | 直接读 `SKILL.md` | `kimi -p` 非交互模式 | ✅ |
| **OpenClaw** | `AGENTS.md` | 同 Codex | — |

## 方法论来源

- **Edmans (2024)** "Learnings From 1000 Rejections" — 选题质量护栏
- **江艇 (2022)** 因果推断经验研究中的中介效应与调节效应. 中国工业经济 — 机制检验方法论
- **AERS** econfin-workflow-toolkit / paper-pipeline / Stata 实证清单

## 版本

- **v0.1.0** — 初版：8 阶段全流程 + 14 份参考文档 + 跨 Agent 支持

---

*由 Marty 的 Hermes Agent 维护和导出。最后更新: 2026-07-24*
