# ZENCE QUANT 6.5 看板使用说明

这份文档解释当前看板各模块的作用、查看顺序和使用边界。它面向日常使用，不展开实现细节。

## 1. 页面结构

当前控制台可以分成五层：

1. 宏观层
   - `VIX`
   - `US 10Y`
   - `SPY`
   - `Regime`
2. 持仓层
   - `Your Holdings`
   - `Real-time News`
3. 执行层
   - `Rebalance Plan`
   - `Daily Execution`
4. 归因层
   - `Live Attribution`
5. 研究层
   - `Backtest Robustness`
   - `Tech Alpha / Power Defense`

## 2. 顶部和宏观层

### 2.1 顶部状态

- 左上角：系统名称
- 右上角：当前时间、数据源模式、`Clear`

数据源模式常见值：

- `HOSTED`
- `HOSTED | core`
- `FIREBASE`

日常应优先看到 `HOSTED` 或 `HOSTED | core`。

### 2.2 风险横幅

黄色横幅用于提示当前组合风险集中度，例如：

- `Technology > 60%`

它不是交易指令，而是提醒你回头结合持仓和再平衡一起判断。

### 2.3 VIX / US 10Y / SPY

- `VIX`：市场风险偏好
- `US 10Y`：利率环境
- `SPY`：大盘基准

用途是先判断今天适不适合进攻，而不是直接决定买哪只股票。

### 2.4 Regime

`Regime` 给出当前市场背景判断，例如：

- `BULL`
- `BEAR`

下面那行说明是战术提醒，不是机械交易信号。

## 3. NAV 曲线

### `Real Portfolio Growth (NAV)`

这块显示组合净值曲线，主要用于：

1. 看账户是在上行、回撤还是横盘
2. 对照宏观环境和大盘判断波动是否合理

这不是回测图，而是当前组合的实盘/准实盘净值视图。

## 4. 持仓层

### 4.1 `Your Holdings`

这是最常看的模块，字段含义如下：

- `Ticker`：股票代码
- `Sector`：行业
- `Price`：当前价格
- `ATR`：波动参考
- `P&L`：当前该持仓盈亏
- `Stop`：止损参考位
- `Action`：前端手工删除按钮

底部汇总：

- `Total`：当前持仓总市值
- `P&L`：总浮盈浮亏
- `Sector`：行业暴露

### 4.2 `Real-time News`

这里显示当前持仓相关的新闻摘要，用来辅助判断：

1. 是否有财报、评级、并购、监管事件
2. 是否需要临时回看止损和减仓计划

## 5. 执行层

### 5.1 `Rebalance Plan`

这是本轮再平衡方案，不是理论最优组合，而是考虑约束后的实际调整建议。

你主要看四件事：

1. 本轮建议卖什么
2. 本轮建议买什么
3. 哪些动作被延后
4. 本轮净腾出多少现金

常见动作原因：

- `staged_exit_half`
- `phase1_enter`
- `deferred_sell_turnover_cap`
- `deferred_buy_budget_cap`

### 5.2 `Daily Execution`

这是每天最接近真实交易清单的模块。

它把当天执行拆成：

1. 先做什么
2. 后做什么
3. 哪些单子今天不动
4. 盘前检查什么

通常会包括：

- `Preflight Checks`
- `Orders`
- `Sell First`
- `Buy After`
- `Net Cash`

如果你每天只看一个执行模块，优先看这个。

## 6. 归因层

### `Live Attribution`

这块回答的是：

- 最近赚钱来自哪里
- 最近亏钱来自哪里

右上角常见汇总：

- `Realized`
- `Unrealized`

切换视图：

- `Tickers`
- `Sectors`
- `Strategies`

用法：

1. `Tickers` 看个股贡献
2. `Sectors` 看行业贡献
3. `Strategies` 看策略桶贡献

## 7. 研究层

### 7.1 `Backtest Robustness`

这是研究层，不是日内执行层。

常见指标：

- `Annualized Return`
- `Volatility`
- `Sharpe`
- `Max Drawdown`
- `Win Rate`

切换视图：

- `Base`
- `Splits`
- `Stress`

用途：

1. 判断策略历史质量
2. 判断是否过拟合
3. 看成本和压力测试下还能不能成立

### 7.2 `Tech Alpha / Power Defense`

这是候选池和观察池，不是直接下单清单。

用途：

1. 看模型当前偏好哪些标的
2. 为下一轮再平衡提供候选池

真正执行还是以：

- `Rebalance Plan`
- `Daily Execution`

为准。

## 8. 推荐查看顺序

每天建议按这个顺序看：

1. `VIX / US10Y / SPY + Regime`
2. `Your Holdings`
3. `Daily Execution`
4. `Rebalance Plan`
5. `Live Attribution`
6. `Tech Alpha / Power Defense`
7. `Backtest Robustness`

## 9. 使用边界

需要明确几件事：

1. `Rebalance Plan` 是执行建议，不是必须机械照做
2. `Daily Execution` 是当天清单，但仍需要你自己确认流动性和盘面
3. `Backtest Robustness` 是研究信息，不保证未来复制历史
4. `Real-time News` 是辅助判断，不替代风控规则

## 10. 相关文件

- 页面源码：[E:\学习\AI\TwinEngineQuant\index.html](</E:/学习/AI/TwinEngineQuant/index.html>)
- 站点入口：[E:\学习\AI\TwinEngineQuant\site\index.html](</E:/学习/AI/TwinEngineQuant/site/index.html>)
- 再平衡报告：[E:\学习\AI\TwinEngineQuant\results\rebalance_report.md](</E:/学习/AI/TwinEngineQuant/results/rebalance_report.md>)
- 执行清单报告：[E:\学习\AI\TwinEngineQuant\results\daily_execution_report.md](</E:/学习/AI/TwinEngineQuant/results/daily_execution_report.md>)
- 归因报告：[E:\学习\AI\TwinEngineQuant\results\performance_attribution_report.md](</E:/学习/AI/TwinEngineQuant/results/performance_attribution_report.md>)
- 回测报告：[E:\学习\AI\TwinEngineQuant\results\backtest_report.md](</E:/学习/AI/TwinEngineQuant/results/backtest_report.md>)
