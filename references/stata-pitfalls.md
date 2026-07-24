# Stata 技术陷阱速查

paper-workflow 阶段 4-5 常见错误与修复方案。

## 数据与回归陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 1 | `corr` 多变量缺失值不同 | 「no observations」r(2000) | 改用 `pwcorr ..., obs` 做 pairwise |
| 2 | `preserve/restore` 在循环内溢出 | 「already preserved」r(621) | 循环内不用 preserve；每次 reload 数据或 gen/drop |
| 3 | 安慰剂检验 500 轮 `reghdfe` | 耗时数小时 | ≤100 轮；或降至省年面板 |
| 4 | 大额绝对量变量未取对数 | 系数极小（如 5e-06） | `fiscal_ratio`、GDP、wage 等 → `gen ln_x = ln(x)` |
| 5 | 描述统计缺少省级控制变量 | Table 1 不完整 | 描述统计必须包含全部控制变量 |
| 6 | 回归表用 ✓ 省略控制变量 | 投稿退回 | 逐行列出所有系数和 SE；仅 FE 可用 ✓ |
| 7 | `use data, clear` 后丢失临时变量 | `ln_fiscal_ratio not found` r(111) | 重载后立即 regenerate 所有临时变量 |

## Stata 语法陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 8 | 因子变量不接受负值 | `i.rel_time` → r(452) | `gen rel_pos = rel_time + 5`，`ib4.rel_pos` |
| 9 | `esttab keep()` 不匹配因子名 | `keep(*.rel_time)` 找不到 | 改 `keep(*.rel_time_pos)` |
| 10 | `esttab` 首次输出 CSV | 「file not found」 | 忽略（首次创建的正常提示） |
| 11 | `ib(-1).rel_time` 被 reghdfe 拒绝 | `variable ib not found` r(111) | 用偏移方法（见 #8） |

## 工作流陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 12 | **`read_file` + `write_file` 污染 do 文件** | 行号前缀 `123|456|` 被写入 | **永远不**用 `read_file` 返值直接 `write_file`。改 do 文件只用 `skill_manage(action='patch')` 或干净 `write_file` |
| 13 | zsh glob 与 `rm -f` 冲突 | `rm -f *.csv` → 「no matches found」阻断命令 | 不批量清理旧 CSV；或 `2>/dev/null; true` |

## CSMAR 数据融合陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 19 | **CSMAR 财务数据库无 `year` 变量** | `variable year not found` r(111) | 从 `Accper`（字符串 "YYYY-MM-DD"）生成：`gen year = year(date(Accper, "YMD"))` |
| 20 | **CSMAR 现金流量表科目不可做寻租代理** | `C001022000`（支付其他与经营活动有关的现金）含差旅费、R&D、排污费等几十项，用它做寻租代理得到的方向可能反向且不可解释 | 真正的业务招待费在财务报表附注明细中（如"管理费用—业务招待费"），需要 CSMAR 财务报表附注子库单独提取。现金流量表汇总科目噪音太大 |

## 机制检验陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 14 | **三步法 Step2 用固定特征做 M** | X→M 永远不显著（M 时不变，企业 FE 已吸收） | 机制变量必须有时序变异。pc_any/SOE/srdi_any 等企业固定特征只能用交互项（调节效应），不能做三步法被解释变量 |
| 15 | **经济后果变量全不显著** | 跑一堆 t+1 变量只有 1 项显著 | 从通过的那一条倒退逻辑：为什么只有它显著？故事围绕唯一通过的结果展开，不强凑不显著项 |

## 多期 DID 平行趋势三陷阱

**陷阱 A**：`if !missing(rel_time)` 会删除从未处理省份（3066 obs 对照组全丢）。正确：`replace rel_time = -5 if missing(rel_time)` 保留为基期。

**陷阱 B**：基期选 `ib4.rel_time_pos`（即 rel_time=-1），不选 `ib0.rel_time_pos`（边界可能混入真实处理）。

**陷阱 C**：传统 TWFE 中早期处理组成为后期处理组对照（forbidden comparisons）。可用 csdid 或 eventstudyinteract。

**子样本平行趋势**：如果 DV 是条件子样本（如 over 仅 ε>0），ε 符号切换会导致选择偏误。用「符号一致子样本」。

## 处理强度异质性陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 16 | **二元组间比较限定 ever-treated 子样本** | 聚类数从 31→15-20 省，统计功效骤降；控制组定义松（混入正处/挂牌）导致效应稀释 | 用连续剂量-反应变量（如 `treat_score1` 0-5）在全样本上回归，不丢弃从未处理省份 |
| 17 | **精确控制组定义被宽泛化** | 用户要求「正厅 vs 副厅」但控制组混入了正处/挂牌 | 用户指定控制组时，用 `level_yr` / `nature_yr` 精确限定（如 `keep if inlist(level_yr, 2, 3)`），不用 `d_zhengting` 的模糊 0 值 |

**案例（2026-07）**：连续得分 `treat_score1` 全样本回归的 p 值系统性优于所有二元比较——over_v2 p=0.001（全样本连续） vs p=0.037（ever-treated 二元 d_zhengting） vs p=0.099（精确限定副厅控制组）。连续得分同时捕获"从无到有"和"级别提升"两个维度的变异。

## 经济后果/进一步分析陷阱

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 18 | **机制或经济后果用二元分组建模** | 用虚拟变量分组回归（如 suspect_rd=0/1），两组 post 系数一显著一不显著，但无正式组间差异检验，审稿人会质疑 | ①优先用连续 DV 直接回归（如 `RDIN ~ post` 而非分 suspect_rd 组）；②若必须分组，加交互项 `post×suspect_rd` 做全样本检验；③分组结果仅作为稳健性补充，不作为主发现 |

**案例（2026-07）**：用户拒绝了 `patent ~ post` 按 `suspect_rd` 二元分组的方法——"这种分组应该属于组间系数差异而非进一步研究……我从未在论文中见过这么做的"。正确做法：`RDIN ~ dev×post`（连续研发操纵强度做被解释变量，单条回归）。分组发现可保留为辅助证据但不作为主表。

## CSMAR 子库陷阱（2026-07 新增）

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 21 | **CSMAR 变量类型不一致** | `AnanmID`/`Brokern` 等 ID 字段是 string，`Audittyp` 是 string 编码的数字 | string 变量不能用 `collapse (count)` 或数值比较。解决：计数去重用 `egen tag = tag(Stkcd year stringvar)` + `egen total = total(tag)`；类型转换用 `destring Audittyp, replace force` |
| 22 | **`winsor2` 可能未安装** | `command winsor2 not found` | 写临时 do 文件避免依赖外部包：`qui sum v, d` → `replace v = r(p1) if v < r(p1)` → `replace v = r(p99) if v > r(p99)` |
| 23 | **审计意见全样本无变异** | `reghdfe NonStdAudit post ...` → `insufficient observations r(2001)` | A股上市公司非标审计意见占比极低（<5%），全样本回归几乎不可行。改为分样本描述统计或放弃该机制 |

## 研究设计陷阱（2026-07 新增）

| # | 陷阱 | 表现 | 修复 |
|---|------|------|------|
| 24 | **研发投入强度做机制变量的内生性** | Step2 post→RDSpendSumRatio 显著（p=0.046），但 Step3 RDSpendSumRatio→dev 不显著。用户指出可能存在反向因果——企业为获取补贴故意提高研发投入 | 研发投入与补贴获取存在双向因果关系。机制检验中应避免用研发投入类变量作为中介 M，或使用滞后项/工具变量处理内生性 |
| 25 | **大数据局分类数据需定期核查** | 多省同时存在行政机构（大数据局/数据局）和事业单位（大数据中心），只找到事业而漏掉行政会导致 DV 编码错误 | 31 省逐省核查：①是否有多个数据管理机构并存；②机构性质是行政还是事业；③是否有 2024 年级别升格或性质转换。优先查省政府官网→机构设置，而非百度百科 |
| 26 | **CSMAR 多表 merge 的 Stkcd 通用方案** | working_data 的 Stkcd 是 str6，CSMAR 某些表是 long 或 string | 统一方案：①遇到 long→`gen Stkcd_str = string(Stkcd, "%06.0f")`；②遇到 string 且 `%06.0f` 报 type mismatch→Stkcd 已是 string，直接 merge；③去重只用一个载体：在 merge 前统一 `tostring Stkcd, replace` 或 `destring Stkcd, replace force` |

## 大数据局数据核查清单

> 来源：2026-07-11 会话，用户反馈甘肃省大数据局已从事业转为政府部门，触发全 31 省复查。

**背景**：多省同时存在「大数据局/数据局」（行政）和「大数据管理中心」（事业），两项职能可能分拆或合署。仅检索到事业机构不等于该省无行政机构。

**核查流程**：
1. 查省政府官网→政府信息公开→机构设置→找到数据管理机构名称和性质
2. 确认是否有一个以上的数据管理机构（行政+事业并存）
3. 记录成立年份、级别、机构性质、变动年份
4. 用 `.gov.cn` 域名的 URL 作为来源记录

**已知 2024 变动（需确认）**：
- 上海：事业→行政
- 四川：事业→行政  
- 江苏：事业→行政，副厅→正厅
- 浙江：副厅→正厅
- 江西/黑龙江/云南/青海/山西/湖南：2024 新设行政机构（替代旧事业机构）
- 湖北/陕西/河北/西藏：2024 新设行政机构

**对 working_data 的影响**：样本期 2015-2023 内，2024 变动不影响 post 编码，但影响 treat_score1 的 nature_yr 和 level_yr 字段。
