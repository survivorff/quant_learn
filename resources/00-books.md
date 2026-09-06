# 书单

> **不求全，求精读。** 下面标注了优先级和"该读哪几章"，避免为了读完而读。
>
> 原则：一本书精读并动手实现 > 十本书泛读。

---

## 第一梯队（必读，按顺序）

| 书 | 作者 | 为什么读 | 读哪部分 |
|---|---|---|---|
| **Quantitative Trading** | Chan | 最薄，一周读完，先建立全局观 | 全书 |
| **Systematic Trading** | Carver | **最实用的实操书**：仓位、波动率目标、多周期、组合 | 全书 |
| **Advances in Financial Machine Learning** | López de Prado | **方法论圣经**：标签、样本权重、CPCV、回测陷阱 | Ch.2-8, 10-16 |
| **Trades, Quotes and Prices** | Bouchaud et al. | 现代实证微观结构，最贴近真实交易 | Ch.1-8 |

**这四本 + 交易所 API 文档，覆盖了 80% 的实用知识。**

---

## 按主题分类

### 统计与时间序列

| 书 | 优先级 | 说明 |
|---|---|---|
| Statistics and Data Analysis for Financial Engineering (Ruppert) | P0 | 统计 + 金融结合得最好 |
| Analysis of Financial Time Series (Tsay) | P1 | 时间序列标准教材，作参考书查 |
| Time Series Analysis (Hamilton) | P2 | 理论深度，只查不读 |

### 市场微观结构

| 书 | 优先级 | 说明 |
|---|---|---|
| **Trades, Quotes and Prices** (Bouchaud et al.) | **P0** | 实证微观结构，最推荐 |
| Trading and Exchanges (Harris) | P1 | 制度与参与者，概念框架 |
| Algorithmic and High-Frequency Trading (Cartea et al.) | P1 | 数学化的做市与执行模型 |
| Market Microstructure Theory (O'Hara) | P2 | 理论 |

### 策略

| 书 | 优先级 | 说明 |
|---|---|---|
| **Systematic Trading** (Carver) | **P0** | 实操最佳 |
| Advanced Futures Trading Strategies (Carver) | P0 | 上一本的进阶，策略更具体 |
| Algorithmic Trading (Chan) | P1 | 配对交易、均值回归的实操细节 |
| Following the Trend (Clenow) | P1 | **趋势跟踪的真实体验**，讲清水下期的痛苦 |
| Inside the Black Box (Narang) | P1 | 量化机构怎么运作 |
| Pairs Trading (Vidyamurthy) | P2 | 协整方法系统论述 |

### 机器学习

| 书 | 优先级 | 说明 |
|---|---|---|
| **Advances in Financial Machine Learning** (López de Prado) | **P0** | 方法论核心 |
| Machine Learning for Asset Managers (López de Prado) | P0 | 精简版，可以先读这本 |
| Machine Learning for Algorithmic Trading (Jansen) | P1 | 代码实现丰富 |
| Machine Learning in Finance (Dixon et al.) | P2 | 理论更系统 |
| Reinforcement Learning: An Introduction (Sutton & Barto) | P2 | RL 基础，按需 |

### 期权与波动率

| 书 | 优先级 | 说明 |
|---|---|---|
| **Option Volatility and Pricing** (Natenberg) | **P0**（做期权时） | **交易员视角，比 Hull 实用** |
| Volatility Trading (Sinclair) | P1 | 波动率交易实操、VRP 实证 |
| Options, Futures, and Other Derivatives (Hull) | P1 | 标准教材，查阅用 |
| Dynamic Hedging (Taleb) | P2 | 尾部风险的实战视角 |
| The Volatility Surface (Gatheral) | P2 | 曲面建模深入 |

### 风险与组合

| 书 | 优先级 | 说明 |
|---|---|---|
| Active Portfolio Management (Grinold & Kahn) | P1 | IR、信息法则、容量的理论基础 |
| Introduction to Risk Parity and Budgeting (Roncalli) | P2 | 风险平价系统论述 |
| The Kelly Capital Growth Investment Criterion (MacLean et al.) | P2 | Kelly 的完整论述与批评 |
| Convex Optimization (Boyd & Vandenberghe) | P2 | 只读前 5 章 |

### 工程

| 书 | 优先级 | 说明 |
|---|---|---|
| **Designing Data-Intensive Applications** (Kleppmann) | P0 | 状态、一致性、幂等 —— 交易系统的基础 |
| Site Reliability Engineering (Google) | P1 | 可靠性工程 |
| The Rust Programming Language | P1（阶段四） | 官方书，免费 |
| C++ Concurrency in Action (Williams) | P2 | 如走 C++ 路线 |

### 心理与思维

| 书 | 优先级 | 说明 |
|---|---|---|
| **Trading in the Zone** (Douglas) | P0（上实盘前） | 纪律与概率思维 |
| Fooled by Randomness (Taleb) | P1 | 区分运气与技能 |
| Thinking, Fast and Slow (Kahneman) | P1 | 认知偏差 |
| Antifragile (Taleb) | P2 | 尾部风险的思维方式 |

### 面试

| 书 | 优先级 | 说明 |
|---|---|---|
| Quant Job Interview Questions and Answers (Joshi) | P1（求职时） | 题库经典 |
| Heard on the Street (Crack) | P1（求职时） | 概率与思维题 |

### 行业与历史

| 书 | 优先级 | 说明 |
|---|---|---|
| The Quants (Patterson) | P2 | 行业历史与人物 |
| The Man Who Solved the Market (Zuckerman) | P2 | 文艺复兴的故事 |

---

## 阅读计划（与 ROADMAP 对齐）

| 阶段 | 读什么 |
|---|---|
| 月 1 | Chan《Quantitative Trading》全书 + Ruppert 相关章节 |
| 月 1-2 | Bouchaud《Trades, Quotes and Prices》Ch.1-8 |
| 月 2 | Carver《Systematic Trading》全书 |
| 月 3-4 | López de Prado《AFML》Ch.2-8, 11-16 |
| 月 3-4 | Kleppmann《DDIA》相关章节 |
| 月 5-6 | Jansen《ML for Algorithmic Trading》选读 |
| 上实盘前 | Douglas《Trading in the Zone》 |
| 阶段四 | Natenberg（如做期权）/ Rust 官方书（如走 QD） |

---

## 一条阅读纪律

> **每读完一章，必须在 labs 里产出对应的代码，或在 notes 里写下 3 条可操作的结论。**
>
> 做不到就说明这一章没读懂，或者这一章对我没用（也是有效信息）。

读书笔记放在 [`notes/`](../notes/)。
