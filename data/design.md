# Floquet Workflow Benchmark Suite — 设计草案

来源:a curated literature workflow atlas cluster #1069(Floquet effective Hamiltonian derivation and
analysis,483 实例 / 191 篇论文)。the knowledge-graph service 可恢复 147 篇,精读分类后含数值 gold 的论文按
主结论物理量分为四条赛道,共 70 篇。每条赛道输出同一物理量 → 共用一个 harbor verifier。

Workflow 步骤覆盖矩阵(★ = 旗舰全链路赛道):

| 赛道 | S1 定义H(t) | S2 选方法 | S3 构造H_eff/U(T) | S4 准能谱 | S5 观测量 | 外层循环 |
|------|:---:|:---:|:---:|:---:|:---:|:---:|
| B1 拓扑不变量 | 给定 | ✓ | ✓ | ✓ | ✓(不变量) | — |
| B2 准能量值   | 给定 | ✓ | ✓ | ✓ | — | — |
| B3 临界点 ★   | ✓(扫参改写) | ✓ | ✓ | ✓ | ✓(序参量) | ✓ 扫描+收敛 |
| B4 有效耦合   | 给定 | ✓(解析支) | ✓ | — | — | — |

B3 是端到端指标;B1/B2/B4 是能力分解,用于诊断 agent 失败在链路的哪一段。

**两条所有者原则(2026-06-13,高于下文一切细节):**

1. **赛道契约 = 关键步骤上同一工作流,而非同一输出物理量。** 各题输入输出可
   自由异构;统一的是被考察的 workflow(这样 train 集才能蒸馏出通用 skill)。
   答案可以是数值、公式或代码,每种答案类型配对应 verifier:数值→容差比对;
   公式→数值采样判等(`formula_equivalence`,已实现);代码→隐藏输入执行。
   公式型答案解锁了"论文只给闭式结果不给参数点"的大批题源(准能量类论文
   几乎全部如此),出题人不再需要代选参数点。
2. **train/validation 随机(按 model_family 分层)切分后,不因题目"正典/
   太容易"而事后调整。** 冷解探针测得的难度(crack 与否、method、confidence)
   作为每条记录的 metadata 保留,供分析,不动 split。家族分层防泄漏属于切分
   设计本身,允许;事后按难度搬动,不允许。

设计原则:
- 每个 case = 一篇论文的 headline 结果的完整复现。题面只给 H(t) 规范(模型、驱动协议、
  参数)和目标量 id 列表,不给方法提示 → 难度对齐原论文。
- train 集(autoresearch 提炼 skill 用):附论文全文 / the knowledge-graph service 推理链 / 参考解 / gold。
- validation 集(检验 skill 泛化):只给 H(t) spec + 目标量列表,gold 由 harness 持有。
- gold 来源优先级:论文报告值(the knowledge-graph service content 核验,沿用 a sibling project 的 14 字段审计协议)
  > 参考解法器在论文校验点之外生成(需先在论文报告值上通过校验)。

---

## B1 floquet-topo-invariants — 拓扑诊断侧面

**考察**:对称性分类、规范不变量计算(workflow 第 3-5 步 + 拓扑诊断)。
**答案类型**:整数(Chern 数、绕数 W₀/W_π、Z2、角态/边缘态计数)。
**规模**:21 篇(topo_invariant 18 + mode_count 3),切 11 train / 10 validation。
**体系跨度**:光子量子行走、kicked SSH、冷原子 Raman 晶格、磁振子 Chern 绝缘体、
扭转双层石墨烯、二阶拓扑超导、合成频率维度、BBH 晶格等。

verifier(harbor):
```json
{"type": "integer_exact",
 "fields": "metadata.quantity_ids",
 "rules": ["canonical integer parse (reject '8.0', '+8')",
           "exact equality per field",
           "sign convention pinned in question (orientation/gauge stated)"]}
```

## B2 floquet-quasienergy — 核心数值机侧面(formula 赛道)

**考察**:构造 Floquet 矩阵 / 单周期演化算符并对角化(workflow 第 1-4 步主干)。
**答案类型**:无量纲准能量 ε/ω(折叠到 (-1/2, 1/2])或命名能隙/劈裂值。

**gold 路线(2026-06-12 实证修订)**:跨论文扫描证实,准能量在文献中几乎从不以
明文数值报告——只以闭式公式(不附参数点)、图谱或拓扑扇区符号标签(E=0、E=π)
出现;"论文报告值"政策下 22 篇候选 0 命中。因此本赛道 gold 原生采用
**formula_derived**:the knowledge-graph service 结论节点中逐字可查的闭式公式(论文自己的结果)+
出题人在公式适用区内固定的参数点 + 机械求值(≥6 位有效数字)。证据链:公式
本身 source_verified;求值可由独立数值传播子 U(T) 交叉验证(atlas 自带评测协议),
作为发布前 selfcheck。被测 agent 看不到公式,题面只给 H(t) 与参数,难度等同
原论文。

verifier(harbor):
```json
{"type": "quasienergy_set",
 "normalize": ["divide by omega", "fold to (-0.5, 0.5]"],
 "match": "sorted pairwise",
 "tolerance": {"mode": "rel", "default": 1e-4, "per_case_override": true}}
```

## B3 floquet-critical-points — 全链路旗舰赛道 ★

**考察**:workflow 的反复应用 + 相变/临界点定位(能隙关闭、局域化转变、PT 破缺阈值)。

**★ 本套件中唯一覆盖 workflow 全部 5 步的赛道,作为重点建设目标。**
定位一个临界点要求在参数空间的每个采样点上完整执行 Step 1→5(改驱动参数 →
选方法 → 构造 H_eff/U(T) → 算准能谱 → 算序参量),外加扫描策略与收敛判据这一
论文作者真实面对的研究循环。B1/B2/B4 各覆盖局部步骤,可视为 B3 的能力分解
(诊断 agent 失败在哪一段);B3 的通过率是"整个 workflow 复现+应用能力"的
端到端指标。难度最高,最接近"用 workflow 做研究"。
**答案类型**:临界驱动振幅/频率/耦合(论文声明单位的命名标量)。
**规模**:15 篇,切 8 train / 7 validation。

verifier(harbor):
```json
{"type": "scalar_tolerance",
 "fields": "metadata.quantity_ids",
 "tolerance": {"mode": "rel",
               "formula_derived": 1e-3,
               "figure_derived": 0.05,
               "source_tagged_in": "metadata.gold_provenance"}}
```

## B4 floquet-effective-coupling — 解析推导侧面

**考察**:高频展开 / 有效哈密顿量解析推导(Bessel 重整、光致耦合项,workflow 第 2-3 步
解析分支)。
**答案类型**:无量纲重整化因子 / 有效耦合比值(J_eff/J、D_F/J 等)。
**规模**:12 篇,切 6 train / 6 validation。

verifier(harbor):
```json
{"type": "scalar_tolerance",
 "fields": "metadata.quantity_ids",
 "tolerance": {"mode": "rel", "default": 1e-3}}
```

---

## 共用 harbor 记录格式

```json
{"id": "floquet-<track>-<paper_slug>",
 "question": "<H(t) spec(模型+驱动协议+参数,机器可读)+ 目标量定义与约定>",
 "answer": {"<quantity_id>": <value>, ...},
 "verifier": {"$ref": "<track verifier>"},
 "metadata": {"paper_id": "...", "doi": "...", "system": "...",
              "split": "train|validation",
              "quantity_ids": [...],
              "gold_provenance": "paper_reported|reference_solver",
              "source_node_id": "...", "source_excerpt": "...",
              "difficulty_note": "<原论文为得到该结果所用的方法与规模>"}}
```

评分:逐字段记录连续误差(整数赛道记 0/1),case 通过 = 全字段达标;赛道指标 =
case 通过率 + 中位相对误差(连续信号,可做 RLVR 奖励与 SOTA-gap 式聚合)。

## 已排除的队列与原因

- dynamics(24 篇):输出量异构(扩散指数、OTOC、回归时间…),无法统一答案类型。
- spectro_response(14 篇):谱特征形态各异,verifier 无法共用。
- lifetime_width(6 篇)、qualitative(25 篇):规模不足 / 无数值 target。
- 44 篇 the knowledge-graph service 空图论文未参与分类,后续图谱修复后可回捞扩容。

## 风险与待办

1. 分类是单遍模型判读,四条赛道共 70 篇在 H(t) 形式化时需逐篇人工复核(本来就要做)。
2. B1 整数 gold 最稳;B3/B4 figure-derived gold 需走 the knowledge-graph service content 端点核验
   (沿用 a sibling project `original_paper_checks.csv` 协议)。
3. validation 防泄漏:train/validation 论文不得共享同一模型家族的同一参数区
   (如两篇 kicked-SSH 变体应同侧)。切分时按"模型家族"分层。
4. 每篇的 H(t) spec 抽取是人力瓶颈,the knowledge-graph service 结论节点已含大部分参数
   (实测 PT-BBH 等条目参数完整),预计可半自动化。

中间产物:/tmp/asb_scan/cls_all.csv(147 篇逐篇分类)、graphs/(the knowledge-graph service 图缓存)、
cohorts.json(关键词粗分)。
