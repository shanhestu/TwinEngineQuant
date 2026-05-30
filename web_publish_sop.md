# Web Publish SOP

这份 SOP 记录当前网页看板的标准发布流程。当前约定是：

- 主站点：Vercel
- 备份站点：GitHub Pages
- 日常发布入口：`daily_publish.bat`

## 1. 发布目标

每次发布，实际更新的是两类内容：

1. 页面文件
   - `site/index.html`
   - `site/dashboard.config.json`
   - `site/vercel.json`
2. 数据文件
   - `site/data/last_core_payload.json`
   - 可选：`site/data/last_enrichment_payload.json`
   - 可选：`site/data/last_history_snapshot.json`

## 2. 日常最小流程

日常只需要运行：

```powershell
.\daily_publish.bat
```

它会自动完成：

1. 本地生成最新 core payload
2. 更新 `results/` 下的最新 JSON
3. 重建 `site/`
4. 提交站点更新到 Git
5. push 到 GitHub
6. 触发 Vercel 自动部署

## 3. 发布前检查

发布前至少确认：

1. `site/index.html` 默认模式是：

```js
activeMode: 'hosted'
```

2. `site/dashboard.config.json` 中是：

```json
"activeMode": "hosted"
```

3. `site/data/last_core_payload.json` 能正常生成，且不包含：
   - `NaN`
   - `Infinity`
   - `-Infinity`

## 4. 本地重建但不发布

如果只想本地更新站点包，不立即 push，可以运行：

```powershell
python bridge_to_zence.py --core-only --no-notify --local-only
python publish_dashboard.py
```

这会更新：

- `results/last_core_payload.json`
- `results/last_history_snapshot.json`
- `site/data/last_core_payload.json`
- `site/data/last_history_snapshot.json`

## 5. Vercel 发布后检查

打开 Vercel 生产地址，重点确认：

1. 右上角显示 `HOSTED` 或 `HOSTED | core`
2. `Your Holdings` 有数据
3. `Rebalance Plan` 有数据
4. `Daily Execution` 有数据
5. `Live Attribution` 有数据
6. `Backtest Robustness` 有数据

## 6. GitHub Pages 的角色

GitHub Pages 现在只作为：

1. 备份访问入口
2. 静态包验证入口

不再作为主发布平台。

备份地址：

- [GitHub Pages Backup](https://shanhestu.github.io/TwinEngineQuant/)

## 7. 异常排查顺序

### 7.1 页面右上角显示 `FIREBASE`

先查：

1. `site/index.html` 是否还是 `hosted`
2. `site/dashboard.config.json` 是否可访问
3. `site/data/last_core_payload.json` 是否可访问
4. 生成端是否又写出了非法 JSON 值

### 7.2 `Your Holdings` 为空

先查：

1. `last_core_payload.json` 是否包含 `user_portfolio`
2. 页面当前是否真正在 `HOSTED` 模式

### 7.3 本地发布脚本失败

先看失败点在哪一层：

1. payload 生成失败
2. `publish_dashboard.py` 失败
3. `git commit` 失败
4. `git push` 网络失败

如果只是 `git push` 失败，通常不需要重跑整套流程，直接补一次：

```powershell
git push
```

## 8. 当前推荐做法

当前推荐的长期使用方式是：

1. 日常只跑 `.\daily_publish.bat`
2. 主看板看 Vercel
3. Pages 只做备份
4. 不再依赖对话记录记忆发布链路
