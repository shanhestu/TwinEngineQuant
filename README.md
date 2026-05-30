# TwinEngineQuant

个人量化交易策略项目，当前已经形成一套可持续使用的工作流：

- 交易账本
- 目标仓位与再平衡
- 组合约束
- 实盘绩效归因
- 回测稳健性
- 网页控制台
- 一键日常发布

## 当前主发布结构

- 主站点：Vercel
- 备份站点：GitHub Pages
- 日常发布入口：`daily_publish.bat`

## 关键入口文档

- 看板使用说明：[dashboard_user_guide.md](</E:/学习/AI/TwinEngineQuant/dashboard_user_guide.md>)
- 网页发布 SOP：[web_publish_sop.md](</E:/学习/AI/TwinEngineQuant/web_publish_sop.md>)
- Vercel 部署说明：[vercel_deploy_guide.md](</E:/学习/AI/TwinEngineQuant/vercel_deploy_guide.md>)
- GitHub Pages 备份说明：[github_pages_deploy_guide.md](</E:/学习/AI/TwinEngineQuant/github_pages_deploy_guide.md>)

## 日常最小动作

```powershell
.\daily_publish.bat
```

这会自动：

1. 生成最新 payload
2. 重建 `site/`
3. 提交并 push 站点更新
4. 触发 Vercel 自动部署

## 当前项目状态

如果后面我们继续开发，优先不要再依赖聊天记录回忆上下文。  
建议先看仓库文档，再看以下结果文件：

- `results/rebalance_report.md`
- `results/daily_execution_report.md`
- `results/performance_attribution_report.md`
- `results/backtest_report.md`

## 下一步建议方向

当前发布链路已经可用，后续更值得投入的方向是：

1. 交易执行体验细化
2. 自动化计划任务
3. 策略本身的持续优化
