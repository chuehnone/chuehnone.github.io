---
title: 如何清除 Ollama 下載失敗的模型檔案
author: chuehnone
categories:
  - 教學
tags:
  - Ollama
image:
  path: "/assets/images/2025/20250126/home.png"
  alt: Ollama partial files
date: 2025-01-26 16:39 +0800
---

在使用 Ollama 下載模型檔案時，下載過程可能會因網路問題、意外中斷等原因導致失敗。此時，系統可能會留下部分未完成的檔案，這些檔案既佔用空間，又無法使用。
本文將介紹如何清除這些失敗的檔案，並提供解決過程中的一些方法。

## 嘗試方法

### 使用 Ollama 指令

首先嘗試透過 Ollama 提供的指令刪除特定模型檔案。
例如，想刪除 `gemma2:2b` 模型，可以執行以下指令：

```shell
ollama rm gemma2:2b
```

但執行後結果會出現錯誤訊息

```
Error: model 'gemma2:2b' not found
```

這表示這個方法行不通。

### 手動刪除

接著檢查存放模型的資料夾 `~/.ollama/models/blobs`。
執行指令如下：

```shell
ls -al ~/.ollama/models/blobs
```

可以發現多個檔案，其中結尾包含 partial 文字的檔案應該就是未完成下載的模型資料

```
drwxr-xr-x@ 29 chinsheng  staff         928  1 26 16:58 .
drwxr-xr-x@  4 chinsheng  staff         128  1 11 11:49 ..
-rw-r--r--@  1 chinsheng  staff         275  1 11 12:01 sha256-32695b892af87ef8fca6e13a1a31c67c1441d7398be037e366e2fc763857c06a
-rw-r--r--@  1 chinsheng  staff         387  1 25 11:36 sha256-369ca498f347f710d068cbb38bf0b8692dd3fa30f30ca2ff755e211c94768150
-rw-r--r--@  1 chinsheng  staff         488  1 25 11:37 sha256-3c24b0c80794f0eb6e0de0033f8e3203075db1c4640e837e097712a4b88d393b
-rw-r--r--@  1 chinsheng  staff          82  1 11 12:01 sha256-45a1c652dddc9efdcefa977ab81cfbe26b6e52bc8e78f2f4c698538783e0ac80
-rw-r--r--@  1 chinsheng  staff        1065  1 25 11:36 sha256-6e4c38e1172f42fdbff13edf9a7a017679fb82b0fde415a3e8b3c31c6ed4a4e4
-rw-r--r--@  1 chinsheng  staff  8988109952  1 25 11:36 sha256-6e9f90f02bb3b39b59e81916e8cfce9deb45aeaeb9a54a5be4414486b907dc1e
-rw-r--r--@  1 chinsheng  staff  1629509152  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial
-rw-r--r--@  1 chinsheng  staff          55  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-0
-rw-r--r--@  1 chinsheng  staff          64  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-1
-rw-r--r--@  1 chinsheng  staff          65  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-10
-rw-r--r--@  1 chinsheng  staff          65  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-11
-rw-r--r--@  1 chinsheng  staff          66  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-12
-rw-r--r--@  1 chinsheng  staff          65  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-13
-rw-r--r--@  1 chinsheng  staff          65  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-14
-rw-r--r--@  1 chinsheng  staff          65  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-15
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-2
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-3
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-4
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-5
-rw-r--r--@  1 chinsheng  staff          64  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-6
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-7
-rw-r--r--@  1 chinsheng  staff          63  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-8
-rw-r--r--@  1 chinsheng  staff          64  1 26 16:58 sha256-7462734796d67c40ecec2ca98eddf970e171dbb6b370e43fd633ee75b69abe1b-partial-9
-rw-r--r--@  1 chinsheng  staff         148  1 25 11:36 sha256-f4d24e9138dd4603380add165d2b0d970bef471fac194b436ebd50e6147c6588
-rw-r--r--@  1 chinsheng  staff         486  1 11 12:01 sha256-f5d6f49c64775df1536e9d747c6b6b4c101f6a8658108fbd18a15d046575c68b
-rw-r--r--@  1 chinsheng  staff        1084  1 11 12:01 sha256-fa8235e5b48faca34e3ca98cf4f694ef08bd216d28b58071a1f85b1d50cb814d
-rw-r--r--@  1 chinsheng  staff  9053114464  1 11 12:01 sha256-fd7b6731c33c57f61767612f56517460ec2d1e2e5a3f0163e0eb3d8d8cb5df20
```

雖然可以手動刪除這些檔案，但應該有更好的方式可以處理？

## 解決方案

最後在 [Ollama 的 Issues](https://github.com/ollama/ollama/issues/1599) 發現簡單有效的答案。

只要重啟 Ollama，它會自動檢查並刪除失敗的 model 檔案，步驟如下：

1. 透過介面關閉 Ollama
2. 重新啟動 Ollama
3. 確認檔案是否有被清除

```shell
ls -al ~/.ollama/models/blobs
```

檢查結果看起來 partial 相關檔案已經被刪除。

```
drwxr-xr-x@ 12 chinsheng  staff         384  1 26 17:04 .
drwxr-xr-x@  4 chinsheng  staff         128  1 11 11:49 ..
-rw-r--r--@  1 chinsheng  staff         275  1 11 12:01 sha256-32695b892af87ef8fca6e13a1a31c67c1441d7398be037e366e2fc763857c06a
-rw-r--r--@  1 chinsheng  staff         387  1 25 11:36 sha256-369ca498f347f710d068cbb38bf0b8692dd3fa30f30ca2ff755e211c94768150
-rw-r--r--@  1 chinsheng  staff         488  1 25 11:37 sha256-3c24b0c80794f0eb6e0de0033f8e3203075db1c4640e837e097712a4b88d393b
-rw-r--r--@  1 chinsheng  staff          82  1 11 12:01 sha256-45a1c652dddc9efdcefa977ab81cfbe26b6e52bc8e78f2f4c698538783e0ac80
-rw-r--r--@  1 chinsheng  staff        1065  1 25 11:36 sha256-6e4c38e1172f42fdbff13edf9a7a017679fb82b0fde415a3e8b3c31c6ed4a4e4
-rw-r--r--@  1 chinsheng  staff  8988109952  1 25 11:36 sha256-6e9f90f02bb3b39b59e81916e8cfce9deb45aeaeb9a54a5be4414486b907dc1e
-rw-r--r--@  1 chinsheng  staff         148  1 25 11:36 sha256-f4d24e9138dd4603380add165d2b0d970bef471fac194b436ebd50e6147c6588
-rw-r--r--@  1 chinsheng  staff         486  1 11 12:01 sha256-f5d6f49c64775df1536e9d747c6b6b4c101f6a8658108fbd18a15d046575c68b
-rw-r--r--@  1 chinsheng  staff        1084  1 11 12:01 sha256-fa8235e5b48faca34e3ca98cf4f694ef08bd216d28b58071a1f85b1d50cb814d
-rw-r--r--@  1 chinsheng  staff  9053114464  1 11 12:01 sha256-fd7b6731c33c57f61767612f56517460ec2d1e2e5a3f0163e0eb3d8d8cb5df20
```

## 結論

在 Ollama 中處理下載失敗的模型檔案，只要重啟 Ollama 就可以刪除失敗的模型檔案，如果需要馬上清空資料，就可以透過這個方式來處裡。
