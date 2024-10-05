---
title: Vdosumry 新增 i18n 功能
author: chuehnone
date: 2024-10-05 23:43:00 +0800
categories: [開發]
tags: [Tool, vdosumry]
render_with_liquid: false
---

今天針對 [Vdosumry](https://github.com/chuehnone/vdosumry) 增加了 i18n 功能

原先 command 會顯示中文，現在則是會依照 local env `LANG` 顯示對應的語言

目前預設是英文，額外支援的語言是 `zh_TW`

## zh_TW 顯示樣式

![](/assets/images/20241005/zh-tw.png)

## default 顯示樣式

![](/assets/images/20241005/default.png)

## 其他調整

- 當輸出資料夾已存在時，會先清空輸出資料夾裡的資料。
- 轉錄文字部分除了支援 srt 格式外，還新增了多行文字格式，目的是嘗試純文字給 LLM 做摘要時，結果是否會更好。
