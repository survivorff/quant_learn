# 术语表（中英对照）

> 用途：读英文论文/文档不卡壳；面试时能用对方的词说话。
> 按主题分组，不按字母。遇到新词就往对应组里加。

---

## 一、收益与风险

| 英文 | 中文 | 一句话说清 |
|---|---|---|
| Return / Log return | 收益率 / 对数收益率 | 对数收益可加，做时间聚合时用它 |
| Excess return | 超额收益 | 减掉无风险利率或基准之后的收益 |
| Alpha | 阿尔法 | 无法被已知风险因子解释的那部分收益 |
| Beta | 贝塔 | 对某个风险因子（常指市场）的暴露 |
| Sharpe ratio | 夏普比率 | 超额收益 / 波动率，年化时要乘 √周期数 |
| Sortino ratio | 索提诺比率 | 只用下行波动做分母的夏普 |
| Calmar ratio | 卡玛比率 | 年化收益 / 最大回撤，对回撤更敏感 |
| Max drawdown (MDD) | 最大回撤 | 峰值到谷值的最大跌幅，决定你能不能活到策略生效 |
| Underwater period | 水下时长 | 从回撤开始到回到新高的时间，心理上比 MDD 更难熬 |
| Volatility drag | 波动率损耗 | 波动本身会侵蚀复合收益，几何 < 算术 |
| Tail risk | 尾部风险 | 极端事件风险，正态假设最容易在这里出事 |
| VaR / CVaR (ES) | 风险价值 / 条件风险价值 | VaR 是分位数损失，CVaR 是超过 VaR 的期望损失 |
| Kelly criterion | 凯利公式 | 最大化长期对数财富的仓位；实务用分数 Kelly |
| Risk parity | 风险平价 | 按风险贡献而非资金等权分配 |
| Turnover | 换手率 | 决定成本；高换手策略对成本估计极其敏感 |
| Capacity | 容量 | 策略能承载多少资金而不显著衰减 |

---

## 二、市场微观结构

| 英文 | 中文 | 一句话说清 |
|---|---|---|
| Limit order book (LOB) | 限价单簿 | 买卖挂单的价格-数量集合 |
| Best bid / offer (BBO) | 最优买价 / 卖价 | 盘口一档 |
| Bid-ask spread | 买卖价差 | 做市商的基础收入，也是你的基础成本 |
| Mid price / Microprice | 中间价 / 微观价格 | 微观价格用两侧量加权，比中间价更能预测短期方向 |
| Depth | 深度 | 各档挂单量，决定大单冲击 |
| Market order / Limit order | 市价单 / 限价单 | 前者吃流动性付 taker 费，后者提供流动性收 maker 费 |
| Maker / Taker | 挂单方 / 吃单方 | 费率不同，很多策略的生死线 |
| Price-time priority | 价格-时间优先 | 主流撮合规则，队列位置有价值 |
| Queue position | 队列位置 | 同价位排在前面成交概率更高 |
| Market impact | 市场冲击 | 你的成交本身推动价格，常用平方根律建模 |
| Slippage | 滑点 | 预期成交价与实际成交价之差 |
| Implementation shortfall | 执行落差 | 决策价到最终成交的总成本 |
| Adverse selection | 逆向选择 | 做市商被"知情交易者"打穿的风险 |
| Inventory risk | 库存风险 | 做市商持仓被动暴露的方向风险 |
| Order flow imbalance (OFI) | 订单流失衡 | 短期价格预测中最有效的微观特征之一 |
| Tick size | 最小价格变动单位 | 影响价差下限与队列价值 |
| Latency | 延迟 | 从行情到下单的时间；HFT 的核心战场 |
| Colocation | 同机房托管 | 把服务器放在撮合引擎旁边 |
| Iceberg / Hidden order | 冰山单 / 隐藏单 | 只显示部分数量 |
| TWAP / VWAP / POV | 时间加权 / 成交量加权 / 参与率 | 三种基础执行算法 |

---

## 三、Crypto 特有

| 英文 | 中文 | 一句话说清 |
|---|---|---|
| Perpetual swap (perp) | 永续合约 | 无到期日的合约，用资金费锚定现货 |
| Funding rate | 资金费率 | 多空之间周期性支付，是一个可交易的收益来源 |
| Basis | 基差 | 期货/永续价格与现货之差 |
| Cash and carry | 期现套利 | 现货多 + 合约空，赚基差/资金费 |
| Mark price | 标记价格 | 用于计算未实现盈亏与强平，通常用指数+基差平滑 |
| Liquidation | 强制平仓 | 保证金不足被强平；级联强平是重要的价格事件 |
| ADL (auto-deleveraging) | 自动减仓 | 保险基金不足时对盈利方强制减仓 |
| Insurance fund | 保险基金 | 吸收穿仓损失 |
| Cross / Isolated margin | 全仓 / 逐仓保证金 | 风险隔离方式不同 |
| Open interest (OI) | 未平仓量 | 合约持仓总量，配合资金费判断拥挤度 |
| AMM | 自动做市商 | 用公式（如 x·y=k）定价的链上做市机制 |
| Impermanent loss | 无常损失 | LP 相对持币的相对损失 |
| Concentrated liquidity | 集中流动性 | Uniswap v3 式在价格区间内提供流动性 |
| Slippage tolerance | 滑点容忍度 | 链上交易的保护参数，设太宽会被夹 |
| MEV | 最大可提取价值 | 通过重排/插入交易获取的价值 |
| Sandwich attack | 三明治攻击 | 在你的交易前后各插一笔 |
| Priority fee / Tip | 优先费 / 小费 | 争夺区块内排序 |
| Private mempool / Order flow auction | 私有内存池 / 订单流拍卖 | 避免被夹的执行通道 |
| CEX / DEX | 中心化 / 去中心化交易所 | 结算与托管模型不同 |
| Onchain data | 链上数据 | 地址行为、资金流、合约事件，属于替代数据 |

---

## 四、统计与时间序列

| 英文 | 中文 | 一句话说清 |
|---|---|---|
| Stationarity | 平稳性 | 统计性质不随时间变化；价格通常非平稳，收益率近似平稳 |
| Unit root / ADF test | 单位根 / ADF 检验 | 检验是否非平稳 |
| Cointegration | 协整 | 两个非平稳序列的线性组合平稳，配对交易的理论基础 |
| Autocorrelation (ACF/PACF) | 自相关 / 偏自相关 | 序列依赖结构 |
| ARIMA / GARCH | 自回归积分滑动平均 / 广义自回归条件异方差 | GARCH 建波动率聚集 |
| Heteroskedasticity | 异方差 | 波动率随时间变化，金融数据的常态 |
| Fat tails / Kurtosis | 厚尾 / 峰度 | 极端值比正态多得多 |
| Regime switching | 状态切换 | 市场在不同状态间跳转（如高波动/低波动） |
| Hurst exponent | 赫斯特指数 | 判断趋势性还是均值回归性 |
| Half-life | 半衰期 | 均值回归速度，用 OU 过程估计 |
| Ornstein-Uhlenbeck (OU) | OU 过程 | 均值回归的连续时间模型 |
| Multiple testing / p-hacking | 多重检验 / p 值操纵 | 试 1000 个策略必然出现"显著"的假发现 |
| Deflated Sharpe ratio | 收缩夏普比率 | 对多重检验做惩罚后的夏普 |
| PBO | 过拟合概率 | 回测过拟合的概率估计 |

---

## 五、机器学习与研究方法

| 英文 | 中文 | 一句话说清 |
|---|---|---|
| Feature / Factor | 特征 / 因子 | 量化里两者常混用；因子更强调经济含义 |
| IC / Rank IC | 信息系数 / 秩信息系数 | 因子值与未来收益的相关性 |
| IR (Information Ratio) | 信息比率 | IC 均值 / IC 标准差，衡量因子稳定性 |
| Triple-barrier method | 三重障碍法 | 用止盈/止损/时间三个边界构造标签（López de Prado） |
| Meta-labeling | 元标注 | 主模型定方向，二级模型定是否下注与下多少 |
| Purging / Embargo | 清除 / 禁运 | 交叉验证时切除信息重叠的样本，防泄漏 |
| CPCV | 组合purged交叉验证 | 金融时序上更可靠的验证方式 |
| Walk-forward | 滚动前推验证 | 模拟真实的"用过去训练、对未来预测" |
| Look-ahead bias | 未来函数 / 前视偏差 | 用到了当时不可得的信息，最常见的致命 bug |
| Survivorship bias | 幸存者偏差 | 只用还活着的标的，高估收益 |
| Point-in-time (PIT) data | 时点数据 | 保留"当时看到的版本"，避免被修订后的数据污染 |
| Overfitting | 过拟合 | 在样本内学到噪声 |
| Feature importance (MDI/MDA/SHAP) | 特征重要性 | MDA 和 SHAP 比 MDI 更可靠 |
| Fractional differentiation | 分数阶差分 | 在保留记忆的同时获得平稳性 |
| Sample weights / Uniqueness | 样本权重 / 唯一性 | 重叠标签需要降权 |
| Ensemble / Bagging / Boosting | 集成 / 装袋 / 提升 | LightGBM/XGBoost 属于 boosting |
| Reinforcement learning (RL) | 强化学习 | 在量化中最扎实的应用是执行优化 |
| Backtest overfitting | 回测过拟合 | 参数扫描出来的"最优"通常不可复现 |

---

## 六、组织与职业

| 英文 | 中文 | 说明 |
|---|---|---|
| Quantitative researcher (QR) | 量化研究员 | 做 alpha 研究，数学/统计要求最高 |
| Quantitative developer (QD) | 量化开发 | 建系统、回测框架、执行链路，工程要求最高 |
| Quantitative trader (QT) | 量化交易员 | 盯策略运行、参数与风险，偏实时决策 |
| Prop trading firm | 自营交易公司 | 用自有资金交易 |
| Market maker | 做市商 | 提供双边流动性赚价差与返佣 |
| Track record | 历史业绩记录 | 管外部资金的硬门槛 |
| AUM | 管理资产规模 | |
| Carry / Performance fee | 业绩分成 | |
| Drawdown limit | 回撤限额 | 机构里超限直接停策略 |
