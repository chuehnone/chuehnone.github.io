---
title: 修正 Vdosumry 安裝問題：更新 README 以及修正 Python 3.13 相容性問題
author: chuehnone
categories:
  - 開發
tags:
  - vdosumry
  - Tool
date: 2025-02-03 17:09 +0800
---

今天嘗試在新環境安裝 [Vdosumry](https://github.com/chuehnone/vdosumry) 時，發現 README.md 缺少一些必要的套件安裝步驟，導致安裝失敗。
而且，在 Python 3.13 環境下，numba 無法正確安裝，因此需要更新 pyproject.toml 來修正相依性問題。

為了確保安裝流程順利，這次的更新包含：
1.	更新 README.md，補上缺少的套件的安裝指南
2.	更新 pyproject.toml，解決 Python 3.13 的相容性問題

## 更新 README.md

在 README.md 中主要加上：

- 新增 ffmpeg 安裝步驟：某些環境下 ffmpeg 可能未安裝，導致影片處理失敗。
- 新增 llvm（版本 14）安裝步驟：numba 依賴 llvmlite，需要特定版本的 llvm 才能正常運作。
- 補上 macOS 透過 brew 的安裝指令。

## 更新 pyproject.toml

由於 numba 在 Python 3.13 上無法正確安裝，這次更新了相依套件的版本：

-	numba 升級到 ^0.61.0，確保相容於 Python 3.13。
-	llvmlite 升級到 ^0.44.0，與 numba 版本同步，避免相依性問題。
-	順手更新 yt-dlp 至 ^2025.01.26 最新版本。

## 結語

這次的更新讓 Vdosumry 在安裝時更加順暢，並確保相容於最新的 Python 版本。

如果你之前遇到了安裝失敗或 numba 相關錯誤，建議更新最新的內容。

若你也在使用 Vdosumry，歡迎提供你的回饋！
