---
title: 在 GitHub Pages 上建立 Blog
author: chuehnone
date: 2024-09-13 15:59:00 +0800
categories: [教學]
tags: [GitHub Pages, Jekyll]
render_with_liquid: false
---

# 快速在 GitHub Pages 上建立 Blog

## 使用 Chirpy

Chirpy 是一個 Jekyll 主題，可以讓你快速建立一個漂亮的 Blog。

### 安裝流程

- 到 [chirpy-starter](https://github.com/cotes2020/chirpy-starter) 點選 <kbd>Use this template</kbd> 按鈕
- 選擇 <kbd>Create a new repository</kbd> 點擊，如下圖

![](/assets/images/20240913/1.png)

- 輸入 Repository name，`<name>.github.io` 其中 `<name>` 是要建立的名稱

接下來就是等待部署就可以了~

更多細節可以參考[Chirpy 安裝文件](https://chirpy.cotes.page/posts/getting-started/)

### 在本地端測試

必須先安裝好 Ruby，這邊安裝方式參考 [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/)

安裝完畢後，就可以在 local 測試

先把服務開起來
```shell
bundle exec jekyll s 
```

接著就可以開啟 `http://127.0.0.1:4000/` 進行預覽
