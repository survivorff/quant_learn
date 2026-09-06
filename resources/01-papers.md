# 论文清单

> 只列**能改变做法**的论文。理论漂亮但不影响我怎么写代码的，不放这里。
>
> 每篇标注了"读完要做什么"。

---

## 一、必读（方法论层，直接影响研究流程）

| 论文 | 作者 | 读完要做什么 |
|---|---|---|
| **The Deflated Sharpe Ratio** | Bailey & López de Prado | 实现 DSR，接入试验次数追踪 |
| **Pseudo-Mathematics and Financial Charlatanism** | Bailey, Borwein, López de Prado & Zhu | 理解回测过拟合的数学本质 |
| **The Probability of Backtest Overfitting** | Bailey & López de Prado | 实现 PBO / CSCV |
| **A Backtesting Protocol in the Era of Machine Learning** | Arnott, Harvey & Markowitz | 拿它的清单当自查表 |
| **…and the Cross-Section of Expected Returns** | Harvey, Liu & Zhu | 理解因子研究的多重检验问题 |

**这五篇是 [`03-research-infra`](../03-research-infra/) 的理论基础。优先读这一组。**

---

## 二、微观结构与执行

| 论文 | 作者 | 读完要做什么 |
|---|---|---|
| **Optimal Execution of Portfolio Transactions** | Almgren & Chriss | 实现 A-C 基线执行算法 |
| **The Price Impact of Order Book Events** | Cont, Kukanov & Stoikov | 实现 OFI 因子，测 IC |
| **High-frequency trading in a limit order book** | Avellaneda & Stoikov | 实现 A-S 报价逻辑 |
| Empirical properties of asset returns | Cont | 验证 stylized facts |
| Universal features of price formation | Sirignano & Cont | 了解深度学习在价格形成上的应用 |

---

## 三、策略与因子

| 论文 | 作者 | 读完要做什么 |
|---|---|---|
| **Time Series Momentum** | Moskowitz, Ooi & Pedersen | 实现 TSMOM，在 crypto 上复现 |
| **Returns to Buying Winners and Selling Losers** | Jegadeesh & Titman | 实现截面动量 |
| A Century of Evidence on Trend-Following | Hurst, Ooi & Pedersen | 理解趋势策略的长期证据与水下期 |
| **Statistical Arbitrage in the US Equities Market** | Avellaneda & Lee | 实现 PCA statarb |
| Pairs Trading: Performance of a Relative-Value Arbitrage Rule | Gatev, Goetzmann & Rouwenhorst | 配对交易的实证基准 |
| **Volatility-Managed Portfolios** | Moreira & Muir | 验证 vol targeting 的效果 |
| Optimal Versus Naive Diversification | DeMiguel, Garlappi & Uppal | 理解为什么 1/N 难打败 |
| **Honey, I Shrunk the Sample Covariance Matrix** | Ledoit & Wolf | 用 Ledoit-Wolf 替代样本协方差 |

---

## 四、机器学习

| 论文 | 主题 | 读完要做什么 |
|---|---|---|
| **DeepLOB** (Zhang, Zohren & Roberts) | 订单簿深度学习 | 了解架构；**注意它不报告扣成本后的收益** |
| **An Empirical Evaluation of Generic Convolutional and Recurrent Networks** (Bai et al.) | TCN | 用 TCN 做序列基线 |
| **A Time Series is Worth 64 Words** (Nie et al.) | PatchTST | 了解 patch 化 Transformer |
| Recent Advances in RL in Finance (Hambly, Xu & Yang) | RL 综述 | 定位 RL 的实际用途 |
| **RL for Optimized Trade Execution** (Nevmyvaka, Feng & Kearns) | RL 执行 | RL 最扎实的应用 |
| Offline RL: Tutorial, Review, and Perspectives (Levine et al.) | 离线 RL | 金融场景的天然选择 |

---

## 五、LLM 与前沿（2024-2026）

| 论文/工作 | 主题 | 我的关注点 |
|---|---|---|
| **Alpha-GPT: Human-AI Interactive Alpha Mining** ([arXiv](https://arxiv.org/html/2308.00016v2)) | LLM 辅助因子挖掘 | **我的优势区**：DSL 设计 + 验证流水线 + 多重检验防护 |
| AlphaQuanter 类工作 | LLM agent 做量化 | 重点看**基线对比**部分，不看宣称的收益 |
| FinGPT 系列 | 金融领域 LLM | 文本信号提取的方法 |
| 各类 LLM 交易 agent 评测 | — | 看它们的失败案例比成功案例有价值 |

### 读这类论文的纪律

**先看三件事，再看结论**：
1. 基线是什么？（如果基线不含简单动量/均值回归，结论不可信）
2. 成本怎么建模的？（很多论文不建模成本）
3. 验证方法是什么？（有没有做 purging，有没有报试验次数）

**三项里缺一项，就把结论的可信度降一档。** 这个标准能过滤掉大量论文。

---

## 六、Crypto 特有

crypto 领域的学术论文质量参差不齐，但有几个方向值得跟：

| 主题 | 关注什么 |
|---|---|
| **Flash Boys 2.0** (Daian et al.) | MEV 概念的奠基工作 |
| 永续合约与资金费的定价 | 资金费机制的理论 |
| 清算级联的实证研究 | 级联机制的量化 |
| AMM 与无常损失 | LP 收益的建模 |
| Crypto 市场效率的实证 | 哪些低效仍然存在 |
| 交易所间价格发现 | 跨所价差的来源 |
| 永续期货的自动调参与执行约束（如 [AutoQuant](https://arxiv.org/abs/2512.22476)） | 执行约束下的参数搜索方法 |

**注意**：crypto 论文的数据往往只覆盖某一段特殊时期（如某轮牛市），外推要格外小心。

---

## 七、阅读流程

### 论文速读法（15 分钟判断是否值得深读）

```
1. 摘要 + 结论（这篇声称发现了什么）
2. 数据段（什么市场、什么时期、多长样本）
3. 基线段（跟什么比较）← 最关键
4. 成本假设（有没有建模成本）
5. 验证方法（怎么防过拟合）
6. 判断：值得深读 / 只记结论 / 跳过
```

### 深读后的产出（必须有）

在 [`notes/papers/`](../notes/) 里写：

```markdown
# 论文标题

## 一句话结论

## 核心方法（能让我复现的程度）

## 它的数据与时期（外推风险）

## 基线与验证方法（可信度评估）

## 我能直接用的部分
（具体到"我要在哪个 lab 里实现什么"）

## 我不同意的部分 / 疑问
```

**"我能直接用的部分"写不出来，说明这篇论文对我现在没用。** 记个结论就跳过，不要陷进去。

---

## 八、论文来源

| 来源 | 说明 |
|---|---|
| arXiv (q-fin) | 量化金融预印本 |
| SSRN | 金融领域的主要预印本平台 |
| Journal of Financial Data Science | 偏应用 |
| Quantitative Finance | 学术 |
| López de Prado 的个人页面 | 方法论论文集中 |
| 各量化机构的公开研究 | 偏实用 |

---

## 注

本文档中引用的外部链接内容已改写摘要以符合许可要求。论文原文请通过上述来源获取。
