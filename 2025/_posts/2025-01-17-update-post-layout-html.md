---
title: 調整 Chirpy 主題的 post layout
categories:
  - 教學
tags:
  - Chirpy
  - Substack
date: 2025-01-17 15:14 +0800
---

今天嘗試增加電子報服務，主要是提供訂閱功能，這樣就可以實現透過 Email 通知新文章。

用的服務是 [Substack](https://substack.com/)，這個服務提供了訂閱功能，只要填寫 Email 就可以訂閱以及還有付費訂閱功能。

不過比較麻煩的是文章分散在比較多地方，還在研究能不能偷懶自動化更新。

回到主題，主要是想在文章頁面加上 Substack 的訂閱 iframe，這樣就可以在每篇文章頁面提供訂閱。

## 修改 post layout

因為這個 Blog，我是透過 [Chirpy 在 GitHub Pages 上建立 Blog](/posts/use-github-page/)。

所以檔案結構比較精簡，原先的檔案結構裡並沒有 `_layouts` 資料夾，需要自己新增。

### 操作步驟

#### 1. 新增 `_layouts` 資料夾與 `post.html`

首先，確認目前檔案結構：

```markdown
.
├── 2024
├── 2025
├── CNAME
├── Gemfile
├── Gemfile.lock
├── LICENSE
├── README.md
├── _config.yml
├── _data
├── _plugins
├── _site
├── _tabs
├── assets
├── index.html
└── tools
```

新增了 `_layouts` 資料夾，並從 [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/_layouts/post.html) 複製了 `post.html` 進來。

```markdown
.
├── 2024
├── 2025
├── CNAME
├── Gemfile
├── Gemfile.lock
├── LICENSE
├── README.md
├── _config.yml
├── _data
├── _layouts
│   └── post.html
├── _plugins
├── _site
├── _tabs
├── assets
├── index.html
└── tools
```

#### 2. 修改 `post.html`

在 `post.html` 中的選擇希望放置的位置加入 Substack iframe：

```html
  <iframe src="{your substack link}" width="100%" height="200"></iframe>
```

`iframe` 程式可以在 Substack 的 Settings > Detail > Embeddable subscribe button 取得。
![](/assets/images/2025/20250117/embed.png)


這樣就可以在每篇文章頁面加上 Substack 的訂閱功能！
