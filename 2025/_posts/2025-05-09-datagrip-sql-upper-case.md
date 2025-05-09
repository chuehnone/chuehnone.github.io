---
title: DataGrip SQL 關鍵字調整成顯示大寫英文字母
author: chuehnone
categories:
  - 學習
tags:
  - DataGrip
date: 2025-05-09 11:00 +0800
---

在某次升級後，發現我的 DataGrip SQL 語法關鍵字變成小寫了，這讓我有點不習慣，因為我習慣使用大寫的 SQL 關鍵字。

通常我都會習慣 Reformat Code 來調整 SQL 語法的格式，但這次發現 Reformat Code 並沒有改變關鍵字的大小寫。

![Reformat Code](/assets/images/2025/20250509/reformat_code.png)

所以才開始了有這篇文章的紀錄，備註一下，幫助下次又遇到時可以調整回來。

## 調整 SQL 關鍵字大小寫

選單進入 Settings

![Settings](/assets/images/2025/20250509/settings.png)

搜尋 `Code Style` 找到 SQL 區塊，選擇使用的 Database

![Code Style](/assets/images/2025/20250509/code_style.png)

發現 MySQL 的設定裡面有勾選繼承了通用 SQL 設定 `Inherit general SQL style`，考慮到共用，決定回頭改 General SQL 的設定。

![MySQL Settings](/assets/images/2025/20250509/mysql.png)

在 General SQL 的 Case 裡面，找到 `Keywords`，選擇 `To upper`，這樣就可以讓 SQL 語法的關鍵字顯示成大寫了！

![General SQL Settings](/assets/images/2025/20250509/general.png)

---
以上就是這次的簡單紀錄，如果有相同困擾的人，可以參考這個方法來調整 DataGrip 的 SQL 語法關鍵字大小寫。
