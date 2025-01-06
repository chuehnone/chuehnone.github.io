---
title: GitHub Repository - GitPodcast 將 GitHub Repository 轉成 Podcast
author: chuehnone
categories:
  - 工具
tags:
  - github
  - repository
  - AI
  - Tool
image:
  path: "/assets/images/2025/20250105/home.png"
  alt: GitPodcast
date: 2025-01-05 11:53 +0800
mermaid: true
---

這是一個有趣的運用，就像 NotebookLM 一樣，可以產出 podcast，不同的是這個專案是專門針對 GitHub Repository 的，只要輸入 Repository 的網址，就可以轉換成 Podcast，這樣就可以透過聽 Podcast 來了解 Repository 的內容。

- GitHub repository: [GitPodcast](https://github.com/BandarLabs/gitpodcast)
- 網站：[https://www.gitpodcast.com/](https://www.gitpodcast.com/)

## 如何使用 GitPodcast

1. 輸入 Repository 網址
    ![](/assets/images/2025/20250105/flow-1.png)
    在首頁輸入你想了解的 GitHub Repository 網址。

2. 點擊 `Podcast`
    ![](/assets/images/2025/20250105/flow-2.png)
    點擊按鈕，開始生成 Podcast。

3. 等待生成
    ![](/assets/images/2025/20250105/flow-3.png)
    系統會分析 Repository 的內容，並轉換成 Podcast。

4. 播放 Podcast
    ![](/assets/images/2025/20250105/flow-4.png)
    播放生成的 Podcast，就可以聽兩位主持人解說該專案！

5. 下載 Podcast
    ![](/assets/images/2025/20250105/flow-5.png)
    也可以下載 Podcast，隨時隨地聽。

## 背後核心技術

```mermaid
flowchart TD
    A[取得 Repository 所有檔案清單] --> B[AI 分析並選出前 10 重要檔案]
    B --> C[讀取重要檔案內容並彙整成單一檔案]
    C --> D[AI 解析彙整檔案並產出 SSML]
    D --> E[AI 將 SSML 轉換成 MP3]
    
    style A fill:#e1f5fe,stroke:#01579b,stroke-width:2px,color:#01579b
    style B fill:#e8eaf6,stroke:#1a237e,stroke-width:2px,color:#1a237e
    style C fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px,color:#1b5e20
    style D fill:#e8eaf6,stroke:#1a237e,stroke-width:2px,color:#1a237e
    style E fill:#e8eaf6,stroke:#1a237e,stroke-width:2px,color:#1a237e
```

根據專案的原始碼，製作一份流程圖，方便讓大家快速了解這個專案背後技術的運作流程。

註：SSML 是 Speech Synthesis Markup Language 的縮寫，是一種用於語音合成的標記語言。
