---
title: 透過 Mochi Diffusion 在本機電腦生成出圖片
author: chuehnone
categories:
  - 教學
tags:
  - text-to-image
  - Mochi Diffusion
image:
  path: "/assets/images/2025/20250205/home.png"
  alt: Mochi Diffusion Interface
date: 2025-02-05 16:04 +0800
---

今天嘗試使用 [Diffusion Bee](https://github.com/divamgupta/diffusionbee-stable-diffusion-ui) 來進行圖片生成，但發現這個專案已經 2 年沒更新了，可能會無法支援最新的模型與技術。

所以我改用 [Mochi Diffusion](https://github.com/MochiDiffusion/MochiDiffusion)，有支援 Core ML，能夠充分利用 Apple 硬體效能。

這篇文章將介紹怎麼使用 Mochi Diffusion，從安裝到模型準備跟使用 Mochi Diffusion 生成圖片。

## 安裝 Mochi Diffusion

我們直接在 [Mochi Diffusion release](https://github.com/MochiDiffusion/MochiDiffusion/releases) 頁面，選擇最新的版本來下載 dmg 檔案，直接點擊就可以下載囉，如下圖。

![](/assets/images/2025/20250205/install-1.png)

下載後接著點擊 .dmg 檔案，將 Mochi Diffusion 的圖示直接拖曳到 Applications 就可以了！

![](/assets/images/2025/20250205/install-2.png)

打開 Mochi Diffusion 後，會發現出現 `No models found under: /Users/{username}/MochiDiffusion/models/`，表示目前沒有可用的模型

![](/assets/images/2025/20250205/install-3.png)

## 準備模型

Mochi Diffusion 需要 Core ML 版本的模型，這些模型可在 [Core ML Community](https://huggingface.co/coreml-community#models) 下載。

點擊進去後，可以看到有眾多模型可以選擇，如下圖。

![](/assets/images/2025/20250205/models-1.png)

選擇喜歡的模型，並到 `Files and versions` 可以看到有檔案與資料夾清單，接著點擊 `split_einsum` 資料夾，如下圖。

![](/assets/images/2025/20250205/models-2.png)

看到 zip 壓縮檔案，就可以直接點擊下載 zip 壓縮檔

![](/assets/images/2025/20250205/models-3.png)

接著到自己帳號的根目錄，可以看到 `/Users/{username}/MochiDiffusion`，其中 `{username}` 是你自己的名稱

這邊需要自行建立 `models` 資料夾，並將剛剛 zip 檔案解壓縮後的資料夾，移動到 `models` 底下

```shell
mkdir -p ~/MochiDiffusion/models
mv ~/Downloads/<解壓縮後的資料夾> ~/MochiDiffusion/models/
```

## 開始執行 Mochi Diffusion 生成圖片

我們接著開啟 Mochi Diffusion，可以發現那個警告訊息不見了，接著我們要來嘗試生成圖片。 

首先在左上角的 `INCLUDE IN IMAGE` 的欄位輸入你的 `prompt`，接著按 `Generate` 按鈕，就會進行生成了！

這邊附上我截圖測試用的 prompt

```
A beautiful female college student stands gracefully on a staircase, 
skillfully wielding a sword in an elegant dance. 
She wears a stylish yet practical outfit that complements her movements, 
with her long hair flowing as she moves. The setting is a grand, 
slightly misty staircase, adding a sense of mystery and drama.
The lighting highlights her confident expression and the fluid motion of her sword, 
creating a dynamic and powerful scene.
```

如果有多個模型可以選擇，則是在左邊的 Model 下拉選單可以選擇模型！

![](/assets/images/2025/20250205/generate-1.png)

## 結論

[Mochi Diffusion](https://github.com/MochiDiffusion/MochiDiffusion) 提供了一個簡單的方式，可以在 macOS 上生成圖片。

我本身也還在摸索中，如果有什麼建議或問題，也歡迎你留言討論與分享！
