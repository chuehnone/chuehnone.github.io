---
title: 什麼是 Prompt Engineering
author: chuehnone
categories:
  - 學習
tags:
  - prompt engineering
render_with_liquid: false
image:
  path: "/assets/images/2024/20241210/prompt-engineering.png"
  alt: Prompt engineering
date: 2024-12-10 14:19 +0800
---

昨天在公司分享了一場關於 prompt engineering 的活動，內容持續了一個小時。

主要討論了如何撰寫清晰明確的指示，並提供了一些 prompt 讓大家練習。這裡簡單整理一下分享的內容。

## 什麼是 Prompt Engineering
在前一篇文章，解析 OpenAI 的 Prompt Engineering 有提到六大策略。

而我個人的整理為四個項目：
1. **清晰明確的指示**
2. **提供上下文參考資訊**：主要是想要降低 AI 產出的幻覺 (Hallucination)，而這邊更進一步的處理就會是 RAG (Retrieval Augmented Generation)。
3. **拆解複雜任務**：會受限 LLM 的 token 數量限制，或是精準度，這時候就可以分拆成多個項目處理。背後可能就會用到 function call 或 tool use。
4. **持續迭代測試**：這個部分是最重要的，因為 prompt 的設計是一個不斷調整的過程。所要有明確的成功指標與評估方式。

![Prompt engineering](/assets/images/2024/20241210/prompt-engineering.png)

這次分享主要聚焦在 **清晰明確的指示** 部分

## 清晰明確的指示
這邊我主要分成幾個小項目
1. **包含詳細資訊**：**人、事、時、地、物** 與 **專業術語、關鍵字** 兩個部分
2. **提供範例**
3. **指定角色**：**系統或使用者** 與 **風格與語調** 兩個部分
4. **結構提示**：例如 Markdown 的語法或是 XML tag 的使用
5. **指定任務步驟**：**要求列出推理步驟** 與 **列出步驟順序提供參考** 兩個部分
6. **限制輸出**：**限制輸出長度或數量** 與 **限制輸出格式** 兩個部分

![Clear Prompt](/assets/images/2024/20241210/clear-prompt.png)

