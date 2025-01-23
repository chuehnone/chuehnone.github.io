---
title: 流量控制演算法：Leaky Bucket 與 Token Bucket
author: chuehnone
categories:
  - 學習
tags:
  - algorithm
  - Leaky Bucket
  - Token Bucket
date: 2025-01-23 19:03 +0800
---

在設計網路服務時，流量控制和資源管理是非常重要的課題。當系統面臨大量 Requests 或突發流量時，無限制地接受 Request 可能導致資源耗盡或服務中斷。
為了解決這些問題，必須有機制來限制流量並平衡系統負載。
**Leaky Bucket** 和 **Token Bucket** 是兩種常見的演算法，能夠有效地實現流量控制與資源管理，廣泛應用於 Rate Limiting 和 Traffic Shaping。
以下將介紹這兩種演算法的目的、如何使用以及實作範例。

## Leaky Bucket

### 目的
Leaky Bucket 演算法主要用於平滑網路流量，確保數據以穩定的速率處理。
可以防止突發流量影響系統穩定性，並提供簡單的 Rate Limiting 機制。
在特定場景下，Leaky Bucket 的優勢體現在其對穩定流量的控制能力，例如在處理需要均勻輸出的批量任務時，這種方式可以避免系統瞬間超載。
同時，Leaky Bucket 在實現和計算上相對簡單，適合需要低效能開銷的系統。

### 如何使用
1. 將 Request 當作流入水桶中的水滴。
2. 水桶有固定的容量，當水超過容量時，多出的水會被丟棄，這是模擬 Request 被拒絕的情境。
3. 水桶中的水會以固定速率流出，模擬伺服器以穩定速率處理 Request。

### 範例程式（Pseudo Code）
```
Initialize bucket with capacity and leak_rate
Set current_water = 0
Set last_check_time to current time

Function add_request():
    current_time = get current time
    elapsed_time = current_time - last_check_time
    last_check_time = current_time

    Reduce current_water by elapsed_time * leak_rate
    If current_water < 0:
        Set current_water = 0

    If current_water + 1 <= capacity:
        Increase current_water by 1
        Return True (request allowed)
    Else:
        Return False (request denied)
```

### 分散式系統情境
在分散式系統中，Leaky Bucket 可用於平滑多個節點的流量。
例如，當多個使用者同時訪問一個共享的資源時，Leaky Bucket 可確保每個節點以穩定的速率處理請求，避免突發流量導致系統過載。
此外，它可以部署在 API Gateway 上，對進入系統的流量進行限制。

### 效能與空間影響
Leaky Bucket 的效能開銷主要在於追蹤水桶中當前水量以及處理流量的速率。
由於只需追蹤單一數值（當前水量）和基本的時間計算，空間需求極低，效能開銷也相對較小，非常適合高併發的場景。
在高併發場景中，可以將水量更新操作優化為基於時間間隔的批量更新，減少頻繁的計算。
此外，對於多執行緒或多節點環境，可以使用鎖機制 (Lock) 或原子操作 (Atomic Operation) 來確保水桶中水量的正確性，同時避免併發問題。
這些細節有助於降低實現中的額外開銷並提升整體效能。

### 對應的 HTTP 狀態碼與 Retry-After
Leaky Bucket 並非專門設計用於計算重試時間，但可以根據剩餘水量和漏出速率推算出下一次可接受請求的時間。
如果要實現支援 `Retry-After`，則需返回基於剩餘水量的等待時間。
例如，若水量需要 2 秒才能降到可接受請求的水位，則返回 HTTP 狀態碼 `429 Too Many Requests`，並附帶標頭 `Retry-After: 2`。

### HTTP Response 範例
```http
HTTP/1.1 429 Too Many Requests
Retry-After: 2
Content-Type: application/json

{
  "error": "Too many requests, please try again later."
}
```
此實作範例說明了如何在返回 Rate Limiting 的同時告知客戶端應等待的時間，幫助其適當調整請求頻率。

## Token Bucket

### 目的
Token Bucket 演算法主要用於允許一定程度的突發流量，同時限制平均流量速率。
常用於限流器 (Rate Limiter)，允許短時間內的高流量，但在過載時會逐漸減速。
實際應用中，Token Bucket 廣泛用於 API Gateway 和 CDN 系統。
在 API Gateway 中，Token Bucket 用於對每個 API 使用者進行限流，根據使用者的需求允許短期高峰流量但控制長期平均速率；
在 CDN 系統中，Token Bucket 被用來限制每個客戶端的請求頻率，確保流量不會壓垮來源伺服器。
同時，它還能應對突發的大量 Request，保持服務穩定。

### 如何使用
1. 設定一個水桶，裡面存放 Token ，每個請求需要消耗一個 Token 才能執行。
2. Token 以固定速率添加到水桶中，模擬系統的可用資源。
3. 水桶有固定容量，當水桶的 Token 滿的時候，多出的 Token 會被丟棄。

### 範例程式（Pseudo Code）
```
Initialize bucket with capacity and refill_rate
Set current_tokens = capacity
Set last_refill_time to current time

Function consume():
    current_time = get current time
    elapsed_time = current_time - last_refill_time
    last_refill_time = current_time

    Increase current_tokens by elapsed_time * refill_rate
    If current_tokens > capacity:
        Set current_tokens = capacity

    If current_tokens >= 1:
        Decrease current_tokens by 1
        Return True (request allowed)
    Else:
        Return False (request denied)
```

### 分散式系統情境
在分散式系統中，Token Bucket 適合處理突發流量場景。
例如，某些微服務可能會在短時間內收到大量請求，Token Bucket 允許這些突發流量通過，同時在長時間內限制總流量，避免影響其他服務。
此外，Token Bucket 常被用於 API Gateway，為每個使用者或應用服務設定單獨的流量限制，確保資源公平分配。

### 效能與空間影響
Token Bucket 的效能影響取決於 Token 的生成速率和水桶容量大小。
由於需要頻繁更新 Token 數量，會產生一定的計算開銷。
此外，儲存 Token 數量與 Timestamp 的空間需求也較小，但比 Leaky Bucket 略高。
在高併發場景中，能接受突發流量的使其非常實用，儘管效能開銷稍高於 Leaky Bucket。

### 對應的 HTTP 狀態碼與 Retry-After
Token Bucket 更適合使用 `Retry-After`，因為 Token 是以固定速率補充的，可以直接計算下一個 Token 可用的時間。
例如，若補充速率為每秒 2 個 Token，且當前無 Token ，則可返回 `Retry-After: 0.5`，提示客戶端等待 0.5 秒再嘗試。

---

## 比較

| 特性             | Leaky Bucket                     | Token Bucket                      |
|----------------|--------------------------------|---------------------------------|
| 流量平滑         | 是                                | 否                                 |
| 突發流量         | 否                                | 是                                 |
| 使用場景         | 平滑流量、保護系統穩定              | 突發流量、控制平均流量             |
| 實現難度與維護成本   | 低，實現邏輯簡單且需求較少的資源       | 中等，需處理 Token 生成和併發問題           |
| 效能開銷         | 低                                | 中等                                |
| 空間需求         | 極低                              | 低                                 |


