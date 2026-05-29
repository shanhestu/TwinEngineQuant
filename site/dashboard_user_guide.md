# ZENCE QUANT 6.5 看板使用说明

本文档说明 [index.html](</E:/学习/AI/TwinEngineQuant/index.html>) 中各个板块的作用、查看顺序和使用方法。目标不是解释实现细节，而是帮助你每天快速读盘、看仓、执行调仓。

## 一、页面整体结构

当前控制台分成四层：

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

4. 研究层
   - `Live Attribution`
   - `Backtest Robustness`
   - `Tech Alpha / Power Defense`

建议每天按这个顺序往下看，而不是先看候选股。

## 二、顶部与风险提示

### 1. 标题栏

- `ZENCE QUANT 6.5`：系统名称。
- 右上角时间：当前页面时钟。
- `Clear`：清空当前 Firebase 用户文档中的自定义持仓。

### 2. 黄色风险横幅

示例：

`Sector Concentration Warning: Semiconductors > 60%`

作用：

- 提示当前组合在某一行业暴露过高。
- 这是风险提醒，不是交易指令。
- 当仓位明显偏单一行业时，应结合 `Rebalance Plan` 和 `Your Holdings` 一起看。

## 三、宏观层

### 1. VIX / US 10Y / SPY 三个卡片

#### VIX

- 市场恐慌指标。
- 数值高，通常代表市场风险偏好差。
- 主要用于判断当前是否适合激进加仓。

#### US 10Y

- 美国 10 年期国债收益率。
- 利率上行通常不利于高估值成长股。
- 对科技股仓位判断尤其有参考价值。

#### SPY

- 标普 500 ETF。
- 用作大盘基准。
- 方便判断组合表现是否跑赢市场。

### 2. 左侧大图：`Real Portfolio Growth (NAV)`

作用：

- 展示组合净值走势。
- 默认显示账户总资产变化。
- 点击上方 `VIX / US10Y / SPY` 卡片后，会切换成对应宏观指标的历史走势。

用途：

- 看组合是在上行、横盘还是回撤。
- 对照宏观环境和大盘判断当前净值变化是否合理。

### 3. 右侧 `Regime` 卡片

示例：

- `BULL`
- `BEAR`

下方会有一句战术说明，例如：

- `VIX low, bullish. Tech firing. Buy on 5% pullback.`
- `VIX high, bearish. Hold 50% cash.`

作用：

- 给出当前市场状态判断。
- 这是组合级别的背景判断，不是个股买卖点。

## 四、持仓层

### 1. `Your Holdings`

这是实盘持仓监控区，也是日常最常看的模块。

字段说明：

- `Ticker`：股票代码
- `Sector`：行业分类
- `Price`：实时价格
- `ATR`：平均真实波幅，反映波动水平
- `P&L`：当前该持仓的浮盈浮亏
- `Stop`：止损参考位
- `Action`：删除当前用户持仓行

底部汇总：

- `Total`：持仓总市值
- `P&L`：组合总浮盈浮亏
- `Sector`：组合行业分布

你主要看三件事：

1. 当前哪些仓位在赚钱，哪些在拖累。
2. 当前价格和止损位距离是否太近。
3. 行业暴露是否过于集中。

### 2. `Real-time News`

作用：

- 展示当前持仓相关的实时新闻。
- 新闻按持仓 ticker 聚合。

用途：

- 判断是否有财报、诉讼、评级变化、并购、监管等事件风险。
- 如果某只持仓突然出现重大事件，应回头联动看 `Your Holdings` 和 `Rebalance Plan`。

## 五、执行层

### `Rebalance Plan`

这是本次执行清单，不是理论最优组合，而是结合当前约束后的本轮调仓方案。

顶部信息：

- `V3`：再平衡版本
- `Signal 2026-05-07`：信号日期
- `Tech 70% | Power 30%`：目标风格配置

右上汇总：

- `Sell`：本次建议卖出金额
- `Buy`：本次建议买入金额
- `Turnover`：本次换手率
- `Net Cash`：本次净腾出的现金

表格字段：

- `Ticker`：标的
- `Action`：`BUY / SELL / HOLD`
- `Shares`：本次建议交易股数
- `Price`：当前参考价格
- `Value`：本次建议交易金额
- `Reason`：动作原因

常见 `Reason` 含义：

- `staged_exit_half`
  - 本次只做阶段性减仓，不一次性清仓。

- `phase1_enter`
  - 本轮允许进入，属于本次执行计划内的买入。

- `deferred_sell_turnover_cap`
  - 原本想卖，但被单次换手上限压住，先延后。

- `deferred_buy_budget_cap`
  - 原本想买，但被本轮买入预算上限压住，先延后。

你可以把这一块理解为：

- `候选池` 告诉你“理论上该看谁”
- `Rebalance Plan` 告诉你“这次实际先动谁”

## 六、研究层

### 1. `Live Attribution`

作用：

- 解释当前实盘收益来自哪里。
- 回答“赚亏不是多少，而是来自谁、来自哪个行业、来自哪类策略”。

顶部信息：

- `As of ...`：归因时点
- `Open ...`：当前持仓数
- `Total P&L ...`：累计总盈亏

右上汇总：

- `Realized`：已实现盈亏
- `Unrealized`：未实现盈亏

视图切换：

#### `Tickers`

- 按个股查看归因。
- 适合回答：哪只股票赚了钱，哪只股票在拖累。

字段通常包括：

- `Ticker`
- `Sector`
- `Realized`
- `Unrealized`
- `Total`

#### `Sectors`

- 按行业查看归因。
- 适合回答：当前盈利主要来自半导体、能源还是软件。

字段通常包括：

- `Sector`
- `Realized`
- `Unrealized`
- `Total`
- `Weight`

#### `Strategies`

- 按策略桶查看归因。
- 适合回答：收益来自 `Tech Alpha` 还是 `Power Defense`。

字段通常包括：

- `Strategy`
- `Realized`
- `Unrealized`
- `Total`
- `Open MV`

### 2. `Backtest Robustness`

作用：

- 展示策略研究结果和稳健性，而不是实盘执行。
- 回答“这套策略在历史上有没有统计意义上的稳定性”。

顶部信息：

- 回测起止日期
- `Annual`：年化收益
- `Win`：胜率

右上汇总：

- `Sharpe`
- `Max DD`

视图切换：

#### `Base`

- 展示基础回测摘要。
- 适合快速看策略总体质量。

常见字段：

- `Total Return`
- `Annualized Return`
- `Volatility`
- `Sharpe`
- `Max Drawdown`
- `Avg Turnover`
- `Avg Period Cost`
- `Win Rate`

#### `Splits`

- 展示训练集、验证集、样本外分段表现。
- 适合判断是否过拟合。

主要用途：

- 看训练期很好、样本外是否还成立。
- 如果训练好而样本外差，需要提高警惕。

#### `Stress`

- 展示压力测试结果。
- 例如更高成本、收益折损、单次冲击等情景。

主要用途：

- 判断策略是否只在理想成本和理想行情下才成立。

### 3. `Tech Alpha / Power Defense`

这是候选信号池，也可以理解为“研究侧观察名单”。

两个标签：

- `Tech Alpha`
  - 进攻型科技池

- `Power Defense`
  - 防御型、公用事业、能源等池子

字段说明：

- `Ticker`
- `Price`
- `Score`：综合评分
- `R40/Mom`：研发效率、动量等组合指标
- `ATR`
- `Signal`：信号参考价
- `Action`：当前模型动作标签

作用：

- 告诉你当前模型偏好哪些标的。
- 这是候选层，不等于直接下单。
- 真正执行仍以 `Rebalance Plan` 为准。

## 七、推荐查看顺序

每天看盘建议按这个顺序：

1. `VIX / US10Y / SPY + Regime`
   - 先判断市场环境。

2. `Your Holdings`
   - 看当前仓位、盈亏、止损、集中度。

3. `Rebalance Plan`
   - 看今天该卖谁、买谁、哪些动作被延后。

4. `Live Attribution`
   - 看最近赚亏来自哪里。

5. `Tech Alpha / Power Defense`
   - 看后续候选池。

6. `Backtest Robustness`
   - 不需要天天盯，主要在你怀疑策略失效或要调整规则时看。

## 八、各板块一句话总结

- `宏观层`：现在市场适不适合进攻。
- `持仓层`：你现在手里拿着什么，风险大不大。
- `执行层`：这一次具体该怎么调仓。
- `归因层`：最近赚亏到底来自哪里。
- `回测层`：这套策略历史上稳不稳。
- `候选层`：模型现在更偏好哪些新标的。

## 九、使用边界

需要明确几点：

1. `Rebalance Plan` 是执行建议，不代表必须机械照做。
2. `Backtest Robustness` 是研究信息，不代表未来一定重复。
3. `Real-time News` 是辅助判断，不是自动事件决策器。
4. `Regime` 是市场背景判断，不能单独替代止损和仓位管理。

## 十、相关文件

- 看板文件：[index.html](</E:/学习/AI/TwinEngineQuant/index.html>)
- 再平衡报告：[results/rebalance_report.md](</E:/学习/AI/TwinEngineQuant/results/rebalance_report.md>)
- 归因报告：[results/performance_attribution_report.md](</E:/学习/AI/TwinEngineQuant/results/performance_attribution_report.md>)
- 回测报告：[results/backtest_report.md](</E:/学习/AI/TwinEngineQuant/results/backtest_report.md>)
- 数据契约：[firebase_data_contract.md](</E:/学习/AI/TwinEngineQuant/firebase_data_contract.md>)
