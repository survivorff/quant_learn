# quant_learn

> 从零到前沿的量化交易学习仓库。目标不是"读完一堆书"，而是**长出一套自己能跑、能扛回撤、能持续迭代的交易系统**。
>
> 起点：10 年+ 后端工程师（Java / 高并发 / 分布式）+ Crypto 一线经验。
> 终点：能独立完成"数据 → 因子 → 回测 → 风控 → 实盘 → 复盘"闭环的系统化交易者。

---

## ⚠️ 免责声明

本仓库是**个人学习笔记与工程实践记录**，不构成任何投资建议、策略推荐或收益承诺。
金融市场交易存在本金全部损失的风险，杠杆与衍生品会放大风险。任何策略在本仓库中出现，都只代表"我在研究它"，不代表"它能赚钱"。
所有实盘决策由本人自行承担后果。

---

## 我该按什么顺序读？

量化这件事最大的坑是**顺序错了**：一上手就调参炼丹，跳过了市场结构和回测方法论，结果全是过拟合的幻觉。

```
      [1] 看懂市场            [2] 学会做研究           [3] 上前沿           [4] 活下来
  00-foundations          03-research-infra       04-ml-and-frontier   05-risk-and-portfolio
  01-market-microstructure   ↑                          ↑                06-engineering
  02-strategy-zoo  ──────────┘                          │                07-career-and-capital
        │                                               │
        └───────────── labs/（每一步都要有代码产出）──────┘
```

| 阶段 | 模块 | 预计投入 | 出口标准（做到才算过） |
|---|---|---|---|
| 1 | [`00-foundations`](./00-foundations/) | 3-4 周 | 能用 Python 拉数据、算收益率序列、做平稳性/相关性检验 |
| 1 | [`01-market-microstructure`](./01-market-microstructure/) | 2-3 周 | 能讲清限价单簿撮合、滑点来源、perp 资金费与强平机制 |
| 1 | [`02-strategy-zoo`](./02-strategy-zoo/) | 3-4 周 | 能对任一策略说出：收益来源 / 失效条件 / 容量上限 |
| 2 | [`03-research-infra`](./03-research-infra/) | 4-6 周 | 有自己的回测框架 + 因子评估流水线，能识别 6 类回测偏差 |
| 3 | [`04-ml-and-frontier`](./04-ml-and-frontier/) | 6-8 周 | 跑通一个 ML alpha（含 CPCV 验证），并能解释为什么样本外衰减 |
| 4 | [`05-risk-and-portfolio`](./05-risk-and-portfolio/) | 2-3 周 | 有明确的仓位公式、风险预算、熔断规则 |
| 4 | [`06-engineering`](./06-engineering/) | 持续 | 实盘系统可 7×24 运行，有监控/对账/降级 |
| — | [`07-career-and-capital`](./07-career-and-capital/) | 持续 | 明确走"自营/机构/资管"哪条路，有资金与止损计划 |

**核心原则：任何一章读完，`labs/` 里必须多出可运行的代码。没有代码的知识点，视为没学。**

---

## 仓库结构

```
quant_learn/
├── README.md                  # 你在这
├── ROADMAP.md                 # 12 个月路线图 + 阶段出口标准
├── TRACKING.md                # 每周追踪（学习 KPI + 实盘 KPI）
├── GLOSSARY.md                # 中英术语表（面试 & 读论文用）
│
├── 00-foundations/            # ① 基础：数学 / 统计 / 时间序列 / Python / 市场常识
├── 01-market-microstructure/ # ② 市场微观结构：订单簿 / 成本 / crypto 场内结构 / MEV
├── 02-strategy-zoo/          # ③ 策略图谱：趋势 / 统计套利 / 做市 / 套利 / 期权 / crypto native
├── 03-research-infra/        # ④ 研究基础设施：数据 / 回测 / 因子 / 评估 / 回测陷阱
├── 04-ml-and-frontier/       # ⑤ 前沿：ML / 深度学习 / RL 执行 / LLM Agent / 替代数据
├── 05-risk-and-portfolio/    # ⑥ 风控与组合：仓位 / 组合构建 / 回撤管理 / 实盘运维
├── 06-engineering/           # ⑦ 交易系统工程（我的主场）：架构 / 低延迟 / OMS / C++·Rust
├── 07-career-and-capital/    # ⑧ 转型路径：自营 vs 机构 vs 自有资金 + 面试
│
├── labs/                     # 动手实验室（6 个递进项目，代码作品）
├── resources/                # 书单 / 论文 / 开源仓库 / 数据源 / 社区
├── journal/                  # 学习日志 + 交易日志（复盘是最高杠杆的动作）
└── notes/                    # 随手笔记、论文摘读、想法暂存
```

---

## 我的差异化定位

不跟数学 PhD 拼模型，用我已有的筹码打：

| 我的存量优势 | 在量化里对应的稀缺能力 |
|---|---|
| 10 年+ Java 高并发 / 分布式 | 交易系统工程、低延迟、7×24 稳定性、对账与一致性 |
| CEX 业务与撮合侧经验 | 市场微观结构的**内部视角**：撮合、风控、强平、费率分层 |
| Crypto / 多链 / Meme 一线交易 | 链上数据、MEV、DEX 流动性、perp 结构，这块传统 quant 很多人不懂 |
| AI 工程化（Agent / LLM 落地） | LLM 辅助因子挖掘、研究流水线自动化、替代数据 NLP |

> 结论：**主攻 Crypto 量化 + 交易系统工程**，把 ML/统计当工具补齐，不当主战场。

---

## 三条铁律

1. **先假设自己是错的**。任何回测出的高夏普，默认是 bug 或过拟合，直到你排除了 [`03-research-infra/03-backtest-pitfalls.md`](./03-research-infra/03-backtest-pitfalls.md) 里的每一条。
2. **风控先于 alpha**。没写好仓位与熔断之前，不许上实盘。哪怕是 100 U。
3. **小钱先跑通全流程**，再放大资金。流程 > 单笔盈亏。

---

## 起手三件事（本周就做）

- [ ] 读完 [`ROADMAP.md`](./ROADMAP.md)，把第 1 个月的任务抄到 [`TRACKING.md`](./TRACKING.md)
- [ ] 完成 [`labs/lab-01-data-collector`](./labs/lab-01-data-collector/)：把一个交易所的 K 线 + 资金费拉到本地，落成 parquet
- [ ] 在 [`journal/progress.md`](./journal/progress.md) 开第一条打卡

---

## 更新节奏

- 每天：`journal/progress.md` 一行打卡（学了什么 / 写了什么代码）
- 每周日：更新 `TRACKING.md`，回顾本周 KPI，调整下周重点
- 每月：回看 `ROADMAP.md`，判断是否要改方向（允许改，但要写原因）
