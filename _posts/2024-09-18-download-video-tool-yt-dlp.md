---
title: 從線上平台下載影音到電腦本機端的工具 - yt-dlp
author: chuehnone
date: 2024-09-18 17:00:00 +0800
categories: [工具]
tags: [yt-dlp, Tool]
render_with_liquid: false
---

# 從線上平台下載影音到電腦本機端的工具 - yt-dlp

這篇文章純粹是記錄一下工具，方便之後找尋。

## 簡單介紹

是由 Python 寫成的工具，可以下載線上平台的影音，[支援的影音平台清單](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md)。

補上 [GitHub 連結](https://github.com/yt-dlp/yt-dlp)


## 安裝

安裝方式可以參考 [yt-dlp Wiki](https://github.com/yt-dlp/yt-dlp/wiki/Installation)

這邊用 homebrew 來安裝

```shell
brew install yt-dlp
```

## 使用

這邊以 YouTube 為例

第一種方法，用 `"` 包住網址
```shell
yt-dlp "https://www.youtube.com/watch?v=bpp6Dz8N2zY"
```

第二種方法，因為有 `?` 所以要用 `\` 跳脫
```shell
yt-dlp https://www.youtube.com/watch\?v=bpp6Dz8N2zY
```

檔案就會在執行的路徑生成
