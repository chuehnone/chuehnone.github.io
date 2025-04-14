---
title: DataGrip 顯示 tinyint 為 boolean？其實不是資料錯了！
author: chuehnone
categories:
  - 學習
tags:
  - DataGrip
  - tinyint
date: 2025-04-14 10:53 +0800
---

最近升級 DataGrip 後，發現所有 tinyint 資料都被顯示成 boolean，讓人一度以為資料有誤。但實際用其他工具查詢，發現資料其實是正確的，問題出在 DataGrip 的設定上。

爬文後才知道這其實是個已知問題，只是這次升級後才首次遇到。

✅ 解決方法如下：
1. 在側邊欄的 DB 連線，點擊右鍵選單裡的 Properties
2. 進到 Advanced 分頁
3. 新增一個參數：
  -	Key： `tinyInt1isBit`
  -	Value： `false`

![](/assets/images/2025/20250414/advanced.png)

設定完成後，重新連線就能正確顯示 tinyint 資料了，不再誤認成 boolean！

