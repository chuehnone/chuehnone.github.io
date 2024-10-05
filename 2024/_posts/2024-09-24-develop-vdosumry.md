---
title: 開發了 Vdosumry 來取得影片摘要
author: chuehnone
date: 2024-09-24 16:20:00 +0800
categories: [開發]
tags: [Tool, vdosumry]
render_with_liquid: false
---

為了能夠快速取得影片摘要，所以開發了一個小工具 [Vdosumry](https://github.com/chuehnone/vdosumry)。

## Vdosumry 簡單介紹

Vdosumry 主要由三個功能組成

- yt-dlp: 下載影片
- whispr: 聲音轉文字
- ollama: 將文字轉成摘要

將這三個組合起來，就可以將線上影片轉成文字摘要。前提這個線上影片有語音，不然也是無法輸出文字。

## 安裝

可以參考 [Vdosumry README](https://github.com/chuehnone/vdosumry/blob/master/README.md)

## 使用方式

目前是透過 poetry 執行，可能之後會放上 homebrew 上，就可以有個簡單 command 使用

````shell
poetry run vdosumry "https://www.youtube.com/watch?v={youtube_youtube_id}"
````

執行完畢後，會在當前目錄下生成一個 `output` 資料夾，裡面會有 `summary.txt` 檔案，就是影片的摘要。
