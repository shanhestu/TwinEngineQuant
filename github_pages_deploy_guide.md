# GitHub Pages Deploy Guide

GitHub Pages 现在保留为**备份站点**，不再是主发布平台。

当前角色：

- 主站点：Vercel
- 备份站点：[GitHub Pages Backup](https://shanhestu.github.io/TwinEngineQuant/)

## 1. 什么时候用 GitHub Pages

GitHub Pages 现在主要用于：

1. 作为 Vercel 的备份访问入口
2. 快速验证 `site/` 静态包是否正常
3. 在 Vercel 暂时异常时做兜底

## 2. Pages 站点依赖什么

当前 Pages 读取的是：

- `site/index.html`
- `site/dashboard.config.json`
- `site/data/last_core_payload.json`

可选增强数据：

- `site/data/last_enrichment_payload.json`
- `site/data/last_history_snapshot.json`

## 3. 当前生效方式

仓库中保留的正确 workflow 是：

- `.github/workflows/deploy-pages.yml`

Pages Source 应保持为：

- `GitHub Actions`

## 4. 当前推荐关系

访问优先级：

1. Vercel 生产域名
2. GitHub Pages 备份站点

## 5. 当前建议

Pages 现在不要承担主发布职责。  
它更适合作为：

1. 静态包备份
2. 简单校验入口
3. 公网兜底入口
