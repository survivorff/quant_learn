# 00 · 基础打底

> **这一章只讲"量化专用的结论与陷阱"，不讲数学原理的推导。**
>
> 系统的数学学习在 → [**math_learn**](https://github.com/survivorff/math_learn)（英文原版教材，长期节奏）
>
> 边界很明确：这里够用就停。宁可薄一点但会用，也不要厚一层却不会用。

---

## 与 math_learn 的分工

| 内容 | 在哪 |
|---|---|
| "为什么 crypto 夏普年化要乘 √365 而不是 √252" | ✅ 这里 |
| "√N 缩放的 IID 假设是什么，怎么证明" | → [math_learn/04-probability](https://github.com/survivorff/math_learn/tree/main/04-probability) |
| "协方差矩阵有三大陷阱，用 Ledoit-Wolf 修" | ✅ 这里 |
| "条件数、正定性、SVD 的数学" | → [math_learn/01-linear-algebra](https://github.com/survivorff/math_learn/tree/main/01-linear-algebra) |
| "测 500 组参数会出 25 个假阳性，所以要用 DSR" | ✅ 这里 |
| "多重检验的统计理论、怎么推导 DSR" | → [math_learn/05-statistics](https://github.com/survivorff/math_learn/tree/main/05-statistics) |
| "配对交易要检验协整、算半衰期" | ✅ 这里 |
| "协整的定义、OU 过程的解、ADF 检验原理" | → [math_learn/08-time-series](https://github.com/survivorff/math_learn/tree/main/08-time-series-econometrics) |

**用法：先在这里知道"有这个坑、该用哪个工具"，需要真正理解原理时再去 math_learn。**

被卡住时查 [math_learn 的"数学 → 量化对照表"](https://github.com/survivorff/math_learn/blob/main/ROADMAP.md)。

---

## 这一章解决什么问题

大多数人做量化亏钱，不是因为不会写代码，而是因为**统计直觉是错的**：

- 看到回测夏普 3.0 就兴奋，不知道试了 500 组参数之后出现夏普 3.0 是必然的
- 对价格做回归，忘了价格是非平稳序列，回归结果是伪回归
- 用正态分布算风险，然后被一次 8 倍标准差的行情打穿
- 用 Excel 拉一条相关性就说"两个币有关系"，不知道要检验协整

这一章就是修这四个洞。

---

## 章节

| 文件 | 内容 | 优先级 |
|---|---|---|
| [01-math-probability-stats.md](./01-math-probability-stats.md) | 概率、分布、假设检验、多重检验、贝叶斯直觉 | P0 |
| [02-time-series.md](./02-time-series.md) | 平稳性、自相关、协整、GARCH、状态切换 | P0 |
| [03-linear-algebra-optimization.md](./03-linear-algebra-optimization.md) | 矩阵、PCA、协方差估计、凸优化与组合求解 | P1 |
| [04-python-data-stack.md](./04-python-data-stack.md) | numpy/pandas/polars、numba、工程规范 | P0 |
| [05-financial-markets-101.md](./05-financial-markets-101.md) | 市场分类、参与者、工具、收益来源、Crypto 特殊性 | **P0（本章最该精读的一篇）** |

P0 = 必须先过；P1 = 到组合优化阶段再回来补。

> **`05-financial-markets-101.md` 是这一章唯一"不能外包给 math_learn"的内容** —— 它讲的是"钱从哪来"，这是纯市场知识，数学教材里不会有。其他四篇更多是"知道有这个坑"的索引。

---

## 出口标准（自测）

能独立回答下面这些，才算过了这一章：

1. 为什么量化里用**对数收益率**而不是简单收益率做时间聚合？什么时候必须用简单收益率？
2. 夏普比率年化为什么乘 √252（或 crypto 的 √365）？这个换算的隐含假设是什么，什么时候会失效？
3. 你测了 200 个策略，最好的那个 p 值 0.01。这个结果说明了什么？
4. 价格序列做 ADF 检验通不过，你要怎么处理才能建模？分数阶差分解决的是什么矛盾？
5. 两个币价格相关性 0.95，能不能做配对交易？还需要检验什么？
6. 用 60 天历史波动率估计的 VaR，在什么情况下会严重低估风险？
7. `pandas` 里哪些操作会静默引入未来函数？举 3 个。

---

## 动手要求

这一章配套 [`labs/lab-01-data-collector`](../labs/lab-01-data-collector/)：

- [ ] 拉取 ≥ 20 个标的、≥ 2 年的日线与小时线
- [ ] 计算简单收益率与对数收益率，验证两者在时间聚合上的差异
- [ ] 画收益率分布 vs 正态分布，算峰度与偏度，看厚尾有多厚
- [ ] 对价格与收益率分别做 ADF 检验，记录结果
- [ ] 算滚动相关性矩阵，观察相关性在极端行情下的变化（危机中相关性趋于 1）

---

## 参考资源（精选，不求全）

**这一章用的（金融向）**：
- **书**：Chan《Quantitative Trading》—— 薄，先建立全局观
- **书**：López de Prado《Advances in Financial Machine Learning》第 1-5 章 —— 金融数据为什么特殊
- **书**：Ruppert《Statistics and Data Analysis for Financial Engineering》—— 统计与金融的桥梁
- 完整清单见 [`resources/00-books.md`](../resources/00-books.md)

**数学原理去这里（英文原版，系统学）**：
- [math_learn/01-linear-algebra](https://github.com/survivorff/math_learn/tree/main/01-linear-algebra) —— Strang + MIT 18.06（免费视频）
- [math_learn/04-probability](https://github.com/survivorff/math_learn/tree/main/04-probability) —— Blitzstein + Harvard Stat 110（**免费书 + 视频 + 带答案习题**）
- [math_learn/05-statistics](https://github.com/survivorff/math_learn/tree/main/05-statistics) —— Wasserman《All of Statistics》
- [math_learn/07-optimization](https://github.com/survivorff/math_learn/tree/main/07-optimization) —— Boyd（**免费** + Stanford EE364A）
- [math_learn/08-time-series](https://github.com/survivorff/math_learn/tree/main/08-time-series-econometrics) —— Tsay《Analysis of Financial Time Series》

---

## 常见时间分配陷阱

❌ 花 3 个月系统学完数学再开始做量化 → 会忘掉 80%，而且实践进度归零
✅ 两条线并行：这里边做 lab 边查，math_learn 按月推进 → 互相喂养

原则：**先动手，被卡住，再补理论。** 理论是用来解释你已经观察到的现象的 —— 这时候的学习效率是漫无目的看书的十倍。

这也是为什么数学被单独拆成 [`math_learn`](https://github.com/survivorff/math_learn)：**它的节奏不该拖累实践的节奏。**
