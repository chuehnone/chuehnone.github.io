---
title: 在 Chirpy 上整合 Giscus
author: chuehnone
date: 2024-09-14 11:40:00 +0800
categories: [教學]
tags: [GitHub Pages, Jekyll, Chirpy, Giscus]
render_with_liquid: false
---

為了能夠在 GitHub Pages 留言，這邊我們使用 [Giscus](https://giscus.app/zh-TW) 這個服務。

## 使用 Giscus 前置動作

在 GitHub Pages 使用 Giscus 有三個必要條件

- 這個 Repository 必須是 public
- 要安裝 [Giscus App](https://github.com/apps/giscus)
- 這個 Repository 要啟用 Discussions

這邊特別說明一下啟用 Discussions 的部分

- 到 Repository 的 Settings
- General -> Features -> Discussions 打勾就可以了，如下圖
  ![](/assets/images/2024/20240914/1.png)

## Chriry 上整合 Giscus

在 Chirpy 上整合 Giscus，只要在 _config.yml 找到 `comments` 部分，調整設定就可以

```yml
comments:
  # Global switch for the post-comment system. Keeping it empty means disabled.
  provider: giscus # 這裡要輸入 giscus
  ...
  # Giscus options › https://giscus.app
  giscus:
    repo: github_username/repo_name # 這裡要輸入你的 Repository
    repo_id: R_XXXXXXX # 這裡要輸入你的 Repository ID
    category: General # 這邊是選擇你要的分類
    category_id: DIC_kwDOMwiOps4Cib5t # 這邊是選擇你要的分類 ID
    ...
```

上面的 `...` 是指省略內容，這邊只顯示需要做調整的部分

如何取得上面資訊？也可以直接在 [Giscus](https://giscus.app/zh-TW) 頁面上，跟著指示操作，會取得 `<script>` 區塊

其中 `<script>` 區塊裡的參數，對應到 _config.yml 的設定

- **data-repo** -> **repo**
- **data-repo-id** -> **repo_id**
- **data-category** -> **category**
- **data-category-id** -> **category_id**

這樣就可以在 Chirpy 上整合 Giscus 了
