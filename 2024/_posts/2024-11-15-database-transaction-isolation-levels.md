---
title: 什麼是 Transaction Isolation Levels
date: 2024-11-15 15:28 +0800
author: chuehnone
categories: [學習]
tags: [database, isolation]
render_with_liquid: false
image:
  path: /assets/images/20241115/isolation-levels.png
  alt: isolation levels
---

## Transaction
在說明 Transaction Isolation Levels 之前，我們先來了解一下 Transaction 的概念。
Transaction 是指在資料庫上執行一包單筆或多筆 SQL 指令，這些 SQL 指令可以是 Select、Insert、Update、Delete 等等，而這些指令在這次 Transaction 時，視為同一包，只會一起成功或資料狀態不變。


## ACID
而 Transaction 有四個特性，也就是我們很常聽到的 ACID
- 原子性 (Atomicity)：這次 Transaction 全部成功，或是全部回歸原樣，資料狀態與執行前一樣。
- 一致性 (Consistency)：這次 Transaction 執行完後，資料庫多張資料表的狀態是一致的。代表多張資料表的資料結果會是一致的新資料或舊資料，不會有新舊混雜的情況發生。
- 隔離性 (Isolation)：每個 Transaction 之間是獨立的，不會互相影響。主要避免同時有多筆 Transaction 進行造成髒資料問題。
- 持久性 (Durability)：成功寫入後，不會因為系統當機或是其他問題而造成資料消失。


## Read Phenomena
有了上述的基本概念，當多個 Transaction 同時存取資料庫時，可能會發生一些讀取問題
- 髒讀 (Dirty Read)：一個 Transaction 讀取到另一個 Transaction 尚未 Commit 的資料，造成過程中讀到髒資料。
![Dirty Read](/assets/images/20241115/dirty-read.png)

- 不可重複讀 (Non-Repeatable Read)：一個 Transaction 在讀取資料時，另一個 Transaction 修改了資料，導致第一個 Transaction 重新讀取時，資料不一樣。
![Non-Repeatable Read](/assets/images/20241115/non-repeatable-read.png)

- 幻讀 (Phantom Read)：：一個 Transaction 在讀取資料時，另一個 Transaction 新增或刪除了資料，導致第一個 Transaction 重新讀取時，資料不一樣。
  ![Phantom Read](/assets/images/20241115/phantom-read.png)

## Isolation Levels
為了解決上述的問題，資料庫提供了不同的 Isolation Levels，讓使用者可以根據需求來選擇適合的 Isolation Levels。
- Read Uncommitted：最低的隔離等級
  - 執行效能最高 
  - 允許：髒讀、不可重複讀、幻讀。
- Read Committed：
  - 允許：不可重複讀、幻讀
  - 不允許：髒讀。
- Repeatable Read：
  - 允許：幻讀
  - 不允許：髒讀、不可重複讀。
- Serializable：最高的隔離等級
  - 執行效能最低
  - 不允許：髒讀、不可重複讀、幻讀。

如圖示
![Isolation Levels](/assets/images/20241115/isolation-levels.png)

那為什麼會有這樣的需求出現呢？主要是為了實現隔離，不外乎就是透過 Lock 機制來達成，而 Lock 會造成效能的問題，所以會需要根據需求來選擇適合的 Isolation Levels，進而提升併發效能。

## 其他
在 Microsoft SQL Server 中，則是有多一個 Snapshot Isolation，詳細可以參考 [SQL Server 中的快照集隔離](https://learn.microsoft.com/zh-tw/dotnet/framework/data/adonet/sql/snapshot-isolation-in-sql-server)。
