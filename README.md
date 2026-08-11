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
| **5 — 实证排查** | `Research-Media-Skill` | 遇到平行趋势失败/不显著等实证问题时，搜索经管之家等中文论坛获取实操方案 | [链接](https://github.com/MartyYao/research-media-skill) |
| **5 — 研究发现** | `Research-Discovery-Skill` | 实证结果与假设不符时的系统化处理：冻结结果→分层诊断→差距分析→机制探索→决策路由→沉淀，写入 Obsidian 研究发现/ | [链接](https://github.com/MartyYao/research-discovery-skill) |

paper-workflow 本身只负责论文层面的逻辑决策：
- 8 阶段流程编排
- 机制检验三步法协议
- 处理强度连续得分策略
- 组件决策门规则
- Obsidian 同步协议

## v0.2.1 修复说明

K3 独立审查（2026-07-31）发现 4×P1 + 7×P2，全部修复：

- agent memory 路由写读闭环：启动协议统一为 `学术/论文-<关键词>/`、`学术/_方法/`、`学术/_设计/`（research-discovery 沉淀的记忆现在能被读回）
- 反向标注规则修正：`[[F-001]]` 解析不到 `F-001-标题关键词.md`，链接必须写完整文件名；序号明确为项目内递增
- 会话启动协议与机制检验块的代码块字面 `\n` 转义清理（markdown 栅栏奇偶翻转）
- README 配套技能表补"机制探索"（五步→六步）
- 准入审查路径写全前缀（`论文写作/03-理论/` 等）；阶段 7 增加审稿质疑时加载 research-discovery 的指引

## v0.2.0 更新说明

- **Obsidian 目录重构**：母文件夹 `论文/` 更名 `研究/`，每个项目拆分为 `研究发现/`（research-discovery 空间）与 `论文写作/`（原 paper-workflow 结构整体平移），两个目录通过 wiki-link 双向索引（发现文件「触发」段链接论文侧来源，「决策与影响」段链接被修改文件；论文侧修改处追加反向标注）
- 新增配套技能 `Research-Discovery-Skill`：实证异常结果的六步处理流程（冻结结果 → 分层诊断 → 差距分析 → 机制探索 → 决策路由 → 沉淀）
- 实证问题溯源顺序调整：先加载 research-discovery 分层诊断（数据层/方法层/理论层），定位到方法层需要外部实操方案时再加载 research-media-skill 搜论坛
- 迭代记录「意外发现」字段升级：意外结果必须创建 `研究发现/01-发现/F-xxx.md`
- 阶段 5→2 回写新增触发行与检查项：假设被实证修正时，理论推演.md 对应假设处追加反向标注

## v0.1.3 更新说明

- 集成 `Research-Media-Skill`：遇到实证问题（平行趋势失败、回归不显著等）优先搜索经管之家等论坛获取实操方案，避免仅凭模型知识回答
- 决策门 B 平行趋势失败时先搜论坛再回退
- 阶段 5.1 新增实证问题溯源规则，检索结论记入仪表盘迭代记录
- 修复 5.1 标题语义错位（「执行前」→「执行规范」）
- 修复 `agent-memory` 引用为 `obsidian-memory-scan`

## v0.1.2 更新说明

- Stata 回归工作全面委托给 `Stata-Regression-skill`（v0.2.3）
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

- [Chinese-Literature-Skill](https://github.com/MartyYao/Chinese-Literature-Skill)（v0.1.1+）— 阶段 1 中文文献采集
- [Stata-Regression-skill](https://github.com/MartyYao/Stata-Regression-skill)（v0.2.3+）— 阶段 4-5 的 Stata 技术底层
- [Research-Media-Skill](https://github.com/MartyYao/research-media-skill)（v0.1.1+）— 阶段 5 实证问题排查（中文论坛搜索）
- [Research-Discovery-Skill](https://github.com/MartyYao/research-discovery-skill)（v0.1.0+）— 阶段 5 实证发现管理（异常结果诊断与沉淀）
- Stata 18+（或 17，`reghdfe` 等包需安装）
- Python 3.10+（pandas, numpy, scipy, matplotlib, openpyxl）

## 致谢

本技能的方法论框架借鉴了 AERS（Applied Econometric Research Skills）生态系统的相关工作流设计。中文文献采集委托给 [Chinese-Literature-Skill](https://github.com/MartyYao/Chinese-Literature-Skill)，Stata 技术实现委托给 [Stata-Regression-skill](https://github.com/MartyYao/Stata-Regression-skill)。

## 版本

- **v0.3.1**（2026-08-10）— 新增 §7.4 审稿意见处置流程：审稿外包建议（第三方模型交叉审查，建议非强制，意见仍需逐条核实）、P0/P1/P2 分级、逐条核实真伪（数字指控必须 log/CSV 重跑验证，驳回需附证据）、处置决策矩阵、复核闭环（grep 零残留+状态行同步）、响应信结构；沉淀三条教训（外部模型简化推理误判、重跑暴露分组口径错误与论证逻辑缺陷、批量替换作用域失控）
- **v0.2.2**（2026-08-07）— 新增 §5.3 实证版本管理协议（强制执行）：Run Tag 运行标记、CSV 命名=正文表号、do-log-CSV-正文四件套绑定、改数字五步闭环、版本切换旧值扫描、数字出处纪律、临时 do 归档、log 强制留存、MAPPING.md、一致性审计——针对实证多次重跑后新旧数据混杂的系统性问题（2026-08-07 全稿一致性审查 12×P0 修复后的定案）
- **v0.2.1**（2026-07-31）— K3 审查修复：4×P1 + 7×P2
- **v0.2.0**（2026-07-31）— Obsidian 目录重构 + Research-Discovery 配套技能
- **v0.1.x**（2026-07）— 初版与迭代：8 阶段全流程 + 14 份参考文档 + 跨 Agent 支持

## 许可证

MIT
