# Project Status 2026-05-30

这份文档用于在对话上下文很长时，快速恢复项目状态。

## 1. 当前整体状态

项目当前已经完成并打通：

1. 交易账本
2. 目标仓位和再平衡建议
3. 组合约束
4. 实盘绩效归因
5. 回测防过拟合与压力测试
6. 统一网页控制台
7. Vercel 主站点发布
8. 每日交易执行清单
9. 一键日常发布

## 2. 当前主站点与备份站点

- 主站点：Vercel
- 备份站点：GitHub Pages

页面右上角正常应显示：

- `HOSTED`
- 或 `HOSTED | core`

## 3. 当前日常发布入口

标准入口：

```powershell
.\daily_publish.bat
```

它负责：

1. 本地生成最新 core payload
2. 更新 `site/data/*.json`
3. 保持 `site/index.html` 同步
4. Git 提交并 push
5. 触发 Vercel 自动部署

## 4. 当前看板主要模块

1. 宏观层
   - VIX
   - US 10Y
   - SPY
   - Regime
2. 持仓层
   - Your Holdings
   - Real-time News
3. 执行层
   - Rebalance Plan
   - Daily Execution
4. 归因层
   - Live Attribution
5. 研究层
   - Backtest Robustness
   - Tech Alpha / Power Defense

## 5. 当前重要文件

核心页面：

- `index.html`
- `site/index.html`

发布相关：

- `daily_publish.bat`
- `publish_dashboard.py`
- `site/vercel.json`

文档：

- `dashboard_user_guide.md`
- `web_publish_sop.md`
- `vercel_deploy_guide.md`
- `github_pages_deploy_guide.md`

结果文件：

- `results/rebalance_report.md`
- `results/daily_execution_report.md`
- `results/performance_attribution_report.md`
- `results/backtest_report.md`

## 6. 当前已知约定

1. 主站点以 Vercel 为准
2. GitHub Pages 只做备份
3. hosted 模式优先读取 `site/data/*.json`
4. Firebase 不再是主公开站点的数据来源

## 7. 当前更适合继续投入的方向

1. 交易台交互细化
2. Windows 计划任务自动运行发布
3. 策略本体优化
4. 风险控制规则继续结构化
