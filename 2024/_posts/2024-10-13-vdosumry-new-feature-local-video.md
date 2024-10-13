---
title: Vdosumry 新增支援本機影片
author: chuehnone
date: 2024-10-13 13:58:00 +0800
categories: [開發]
tags: [Tool, vdosumry]
render_with_liquid: false
---

[Vdosumry](https://github.com/chuehnone/vdosumry) 新增支援本機影片，可以直接在網址輸入地方，輸入影片的路徑，即可開始使用 Vdosumry 進行摘要。

## 使用方式

```shell
poetry run vdosumry "./source/video.mp4"
```

上述範例是載入本機的 `video.mp4` 影片，並且會在當前目錄下生成一個 `output` 資料夾，裡面會有 `summary.txt` 檔案，就是影片的摘要。

## 其他

- 修正了部分影片會無法正常下載的問題，主因是找不到影片的格式。 
  - 修正方法是參考了 [yt-dlp Format Selection examples](https://github.com/yt-dlp/yt-dlp?tab=readme-ov-file#format-selection-examples) 方法
- 更新了套件版本
- 將部份 function 調整成 private function
