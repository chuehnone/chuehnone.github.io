---
title: Vdosumry 新功能，讓 ollama 預設自動選擇本地端可用的模型
author: chuehnone
categories:
  - 開發
tags:
  - vdosumry
  - Tool
date: 2025-02-04 13:38 +0800
---

[Vdosumry](https://github.com/chuehnone/vdosumry) 可以透過 Ollama 來處理影片字幕的摘要，其中 `--ollama-model` 參數是用來指定要使用的 Ollama 模型

## 問題

之前 `--ollama-model` 預設為一個固定的模型名稱，例如 `llama3.2`，但使用者的本地環境可能沒有下載這個模型 ，導致每次執行時都會需要加入參數指定，使用的體驗就變得有點繁瑣。

## 更新內容

今天更新的 `--ollama-model` 選擇邏輯：

- 自動偵測本地端可用的模型，優先使用已下載的模型。
- 仍然也有支援手動指定模型，如果使用者有特定需求，仍可以透過 `--ollama-model="llama3.2"` 來指定模型。

## 參考執行與結果

執行方式
```bash
poetry run vdosumry "https://www.youtube.com/watch?v=O8QIXg2l6_s"
```

執行結果
```
Using default model: deepseek-r1:14b
正在建立輸出目錄或清理現有目錄...
正在下載影片...
[youtube] Extracting URL: https://www.youtube.com/watch?v=O8QIXg2l6_s
[youtube] O8QIXg2l6_s: Downloading webpage
[youtube] O8QIXg2l6_s: Downloading tv client config
[youtube] O8QIXg2l6_s: Downloading player 0f7c1eff
[youtube] O8QIXg2l6_s: Downloading tv player API JSON
[youtube] O8QIXg2l6_s: Downloading ios player API JSON
[youtube] O8QIXg2l6_s: Downloading m3u8 information
[info] O8QIXg2l6_s: Downloading 1 format(s): 248+251
[download] Destination: ./output/video.f248.webm
[download] 100% of   14.10MiB in 00:00:01 at 10.72MiB/s
[download] Destination: ./output/video.f251.webm
[download] 100% of    1.77MiB in 00:00:00 at 5.88MiB/s
[Merger] Merging formats into "./output/video.webm"
Deleting original file ./output/video.f251.webm (pass -k to keep)
Deleting original file ./output/video.f248.webm (pass -k to keep)
影片已下載到 ./output/video.webm
正在將聲音轉錄文字...
轉錄文字已保存到 ./output/transcript.srt
正在生成摘要...
摘要已儲存到 ./output/summary.txt
正在翻譯摘要...
翻譯的摘要已儲存到 ./output/translate.txt
完成！
```

可以看到多了一行 `Using default model: deepseek-r1:14b`，這表示 Vdosumry 已經自動選擇了一個可用的 Ollama 模型 `deepseek-r1:14b`。

## 結論

這次的更新讓 `--ollama-model` 的使用更加直覺，不需要手動指定模型名稱，提高了 Vdosumry 的易用性。

如果你正在使用 [Vdosumry](https://github.com/chuehnone/vdosumry)，建議更新至最新版本，體驗更簡單的執行方式！
