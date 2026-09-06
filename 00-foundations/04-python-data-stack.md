# 04 · Python 数据栈与工程规范

> 我的 Java 工程习惯在这里是优势，但 Python 数据栈有它自己的坑，尤其是**静默引入未来函数**这一类。
>
> 这一章的目标：建立一套自己的研究代码规范，让"回测结果可复现"成为默认状态。

---

## 一、工具选型（2026 年的实际情况）

### 核心库

| 层 | 选择 | 说明 |
|---|---|---|
| 数值 | `numpy` | 基础，不可替代 |
| 数据框 | `pandas` + `polars` | pandas 生态最全；polars 在大数据量下快一个数量级，且 API 更严格（不容易写出隐式对齐 bug） |
| 存储 | `parquet`（Arrow）+ `duckdb` | parquet 列存压缩率高；duckdb 直接对 parquet 跑 SQL，本地分析神器 |
| 时序库 | `duckdb` / `clickhouse` / `timescaledb` | 逐笔数据量大时需要真正的时序存储 |
| 加速 | `numba` | JIT 编译热路径循环，事件驱动回测的性能救星 |
| 统计 | `statsmodels`、`arch`、`scipy.stats` | ADF、GARCH、检验 |
| ML | `scikit-learn`、`lightgbm`、`xgboost` | 表格因子的主力仍是梯度提升树 |
| 深度学习 | `pytorch` | 需要时再上 |
| 绘图 | `matplotlib` + `plotly` | 静态分析用前者，交互看 K 线用后者 |
| 环境 | `uv` | 比 pip/poetry 快得多，2026 年的默认选择 |
| 质量 | `ruff`（lint+format）、`mypy`、`pytest` | 从第一天就上，别等代码烂了再补 |

### 量化专用库

| 库 | 定位 | 我的判断 |
|---|---|---|
| `nautilus_trader` | 事件驱动、研究到实盘同一套代码 | **重点关注**。Rust 内核 + Python API，回测/实盘一致性是它的核心卖点，最接近生产级 |
| `vectorbt` | 向量化，参数扫描极快 | 适合大规模参数搜索与快速筛选，但向量化范式容易掩盖执行细节 |
| `qlib`（微软） | AI 量化研究平台，偏 A 股/股票因子 | 学习因子研究工作流的好参考 |
| `backtesting.py` | 极简回测 | 学习用，别用于严肃研究 |
| `backtrader` | 老牌事件驱动 | 生态成熟但维护放缓 |
| `zipline-reloaded` | 老牌，日频股票 | 偏美股，crypto 用不上 |
| `hummingbot` | 现成的做市/套利机器人 | 读它的执行层代码，学 crypto 做市工程 |
| `ccxt` | 统一多交易所 API | 数据采集和下单的事实标准；**但延迟敏感场景要用原生 API** |
| `skfolio` / `riskfolio-lib` | 组合优化 | 组合层直接用 |
| `mlfinpy` / `mlfinlab` 类库 | AFML 方法实现（三重障碍、CPCV、HRP） | 省很多重复劳动 |

**我的路线**：先手写回测器（`lab-02`）搞懂原理 → 再用 `nautilus_trader` 做严肃研究和实盘 → 用 `vectorbt` 做粗筛。

> 不要一开始就用现成框架。手写一遍事件驱动回测器，是理解"回测为什么会骗你"的最快方式。

---

## 二、pandas 的未来函数陷阱（重点）

这是量化 Python 代码里最常见的致命 bug。列几个必须警惕的：

### 1. `shift` 方向搞反

```python
# 错：用了未来的收益
df['signal'] = df['feature']
df['pnl'] = df['signal'] * df['return']     # return 是当期，signal 也是当期 → 未来函数

# 对：信号只能用于下一期
df['pnl'] = df['signal'].shift(1) * df['return']
```

**规则**：任何"信号 × 收益"的乘法，都要问一遍"这个信号在收益发生之前真的可得吗"。

### 2. 全样本统计量泄漏

```python
# 错：用了全样本均值和标准差做标准化
df['z'] = (df['x'] - df['x'].mean()) / df['x'].std()

# 对：用滚动窗口
r = df['x'].rolling(252)
df['z'] = (df['x'] - r.mean()) / r.std()
```

同类问题：全样本分位数、全样本 min-max 归一化、在整个数据集上 `fit` scaler 再切分训练测试。

### 3. `fillna` / `interpolate` 引入未来信息

```python
df.fillna(method='bfill')       # 用后面的值填前面 → 直接的未来函数
df.interpolate()                # 线性插值同样使用了后续点
```

只能用 `ffill`，且要限制填充长度（`limit=`），并**记录填充了多少**。

### 4. `resample` 的区间标签

`resample('1h')` 默认标签是区间**左端**，但聚合值包含整个小时的数据。用 `label='right', closed='right'` 明确语义，否则会用"这一小时的收盘"当作"这一小时开始时的信息"。

### 5. 索引隐式对齐

pandas 的算术运算会按索引自动对齐，两个不同索引的 Series 相乘会静默产生 NaN 或错位。polars 不做隐式对齐，这是它更安全的原因。

### 6. 数据修订（restatement）

链上数据重组、交易所修正历史 K 线、指数成分回溯调整 —— 你今天下载的历史数据，和当时能看到的数据不一样。这叫缺少 **point-in-time** 正确性。

对策：**数据入库时打上采集时间戳，永不覆盖，只追加版本。**

### 防御性做法

- 写一个 `assert_no_lookahead(df, signal_col, return_col)` 工具函数，每次回测前跑
- 回测器设计成**只能按时间顺序推进**的事件循环，物理上无法访问未来数据（这是事件驱动优于向量化的核心原因）
- 单元测试：给一段人造数据，未来某个点放一个巨大异常值，如果策略在异常值之前就"预知"了，说明有泄漏

---

## 三、研究代码规范

### 目录约定

```
labs/lab-xx-name/
├── README.md          # 目标、结论、怎么跑
├── pyproject.toml     # 依赖（用 uv 管理）
├── config/            # 参数配置（yaml），不硬编码
├── src/               # 可复用模块
│   ├── data/          # 数据加载
│   ├── features/      # 因子计算
│   ├── strategy/      # 策略逻辑
│   ├── backtest/      # 回测引擎
│   └── report/        # 报告生成
├── notebooks/         # 探索性分析（不放核心逻辑）
├── tests/             # 关键逻辑必须有测试
└── results/           # 输出（.gitignore，只提交 md 报告）
```

### 硬性规则

1. **Notebook 里不放核心逻辑**。Notebook 只用来看图和探索，逻辑都在 `src/`，Notebook 里 import。理由：Notebook 的执行顺序不可靠，是不可复现的头号来源。
2. **参数全部外置到 config**。硬编码的魔法数字是回测无法复现的第二大来源。
3. **每次回测输出一个 run 记录**：配置快照 + git commit hash + 数据版本 + 结果。没有这个，三个月后你无法解释自己的结果。
4. **固定随机种子**，并记录在 run 记录里。
5. **测试覆盖关键路径**：手续费计算、仓位计算、PnL 累加、信号对齐。这几处出 bug 最贵。
6. **金额用整数最小单位或 Decimal**，不用 float 累加。
7. **时间统一用 UTC，带时区的 datetime**。crypto 是 24/7 全球市场，本地时区会害死你。

### 让研究可复现的最小工程

```python
# 每次 run 都记录
run_meta = {
    "run_id": uuid,
    "timestamp": utcnow(),
    "git_commit": subprocess("git rev-parse HEAD"),
    "git_dirty": bool,               # 有未提交改动就标记，结果不可信
    "config": config_dict,
    "data_version": data_manifest_hash,
    "random_seed": seed,
    "lib_versions": {...},
}
```

这套东西对我来说是本能（后端做发布追溯的习惯），但在量化研究里恰恰是绝大多数人缺的。**这是我的工程背景能直接变现的地方。**

---

## 四、性能：什么时候该优化

顺序不要搞错：

1. **先向量化**（numpy/polars），通常能带来 10-100x
2. **减少数据量**：先在小样本上验证逻辑，再上全量
3. **用 duckdb 做重聚合**，别用 pandas 硬扛
4. **numba JIT** 热路径循环（事件驱动回测的主循环）
5. **并行**：参数扫描用 `joblib` / `multiprocessing`，天然可并行
6. **最后才考虑 Rust / C++**（见 `06-engineering`）

反面教训：不要在策略逻辑都还没验证对的时候花两周优化性能。**先对，再快。**

---

## 五、动手清单

- [ ] 用 `uv` 建一个项目环境，配好 `ruff` + `pytest` + `mypy`
- [ ] 写数据加载模块：parquet 分区（按标的/月份）、增量更新、完整性校验（缺失 K 线检测）
- [ ] 写 `assert_no_lookahead` 工具函数并加进测试
- [ ] 故意写一段有未来函数的回测，看夏普能虚高到多少 —— **这个实验价值极高，做一次记一辈子**
- [ ] 对比 pandas vs polars 在 1 亿行逐笔数据上的聚合性能
- [ ] 用 duckdb 直接对 parquet 做 SQL 聚合，感受一下不用加载到内存的爽快
- [ ] 实现 run 记录机制（含 git hash 和 dirty 检查）
- [ ] 用 numba 加速事件循环，测量提速倍数

---

## 参考

- `polars` 官方文档（迁移指南对 pandas 用户友好）
- `duckdb` 文档（重点看对 parquet 的直接查询）
- `nautilus_trader` 文档与源码（学生产级架构设计）
- López de Prado, *AFML*（书里的代码质量一般，但方法论必读）
- 完整仓库清单见 [`resources/02-github-repos.md`](../resources/02-github-repos.md)
