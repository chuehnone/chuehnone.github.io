---
title: GitHub repository -  arxiv-txt 將 ArXiv 轉為純文字工具
categories:
  - 學習
tags:
  - github
  - repository
  - arxiv
date: 2025-03-02 11:29 +0800
---

- GitHub repository: [arxiv-txt](https://github.com/jerpint/arxiv-txt)

在處理學術論文時，會需要將 ArXiv PDF 轉換為純文字，以便 AI 解析、檢索或進一步分析。
[arxiv-txt](https://github.com/jerpint/arxiv-txt) 就是來完成這項工作，適用於 LLM、AI 應用與學術研究。

如果不想在本地端部署服務，也可以直接使用 [arXiv-txt.org](https://arxiv-txt.org/) 來轉換論文內容。

## 專案特色

### 支援 ArXiv ID 或完整網址輸入
![](/assets/images/2025/20250302/search.png)
首先可以輸入 ArXiv 的 ID，或是完整的連結，點擊 `Open` 就可以看到下圖的結果

### 雙欄顯示模式
![](/assets/images/2025/20250302/overview.png)
左邊的 Summary 其實就是摘要的內容，如 https://arxiv.org/abs/1706.03762 這篇的摘要。

右邊的 PDF 則是將 PDF 轉為純文字，但是缺少了圖片或表格關係，只有文字內容，所以在閱讀上並不是很方便。

### 提供 API
如果要取得 Summary 可以透過以下方式
```
GET https://arxiv-txt.org/raw/abs/{id}
```

如果要取得 PDF 可以透過以下方式
```
GET https://arxiv-txt.org/raw/pdf/{id}
```

## 使用情境

- 提供給 LLM 使用
- 程式分析與數據檢索

## 結論

提供本地部署服務，一個簡單實用的工具，讓學術研究者可以更方便地處理 ArXiv 論文。
