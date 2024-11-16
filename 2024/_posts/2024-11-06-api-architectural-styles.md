---
title: API 架構風格
author: chuehnone
date: 2024-11-06 09:52 +0800
categories: [學習]
tags: [API]
render_with_liquid: false
image:
  path: /assets/images/2024/20241106/api-styles-table.png
  alt: API 架構風格比較表格
---

最近挺常看到一些關於 API 架構風格的文章，簡單記錄一下來源跟簡介。


## 簡介 API
API 全名是 Application Programming Interface，是定義軟體之間如何互動的規範。API 可以讓不同的軟體系統之間進行溝通，讓不同的軟體系統之間可以互相使用對方的服務。

可以把 API 想像成一座橋梁，橋的寬度和設計方式就是 API 的定義。橋設計好後，車子才能通過。至於要怎麼建這座橋（例如用什麼材料或建築方法），就是由軟體決定要採用哪種 API 架構。這樣資料才能透過 API 在不同的應用程式之間順利傳遞。


## 常見的 API 架構風格

### SOAP
SOAP 全名是 Simple Object Access Protocol，是一種基於 XML 的通訊協定，用於在網際網路上交換資訊。SOAP 通常運行在 HTTP 或 SMTP 之上。

SOAP 資料格式如下
```xml
<?xml version='1.0' Encoding='UTF-8' ?>
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope"> 
 <env:Header>
  <m:reservation xmlns:m="http://travelcompany.example.org/reservation" 
		env:role="http://www.w3.org/2003/05/soap-envelope/role/next">
   <m:reference>uuid:093a2da1-q345-739r-ba5d-pqff98fe8j7d</m:reference>
   <m:dateAndTime>2007-11-29T13:20:00.000-05:00</m:dateAndTime>
  </m:reservation>
  <n:passenger xmlns:n="http://mycompany.example.com/employees" 
		env:role="http://www.w3.org/2003/05/soap-envelope/role/next">
   <n:name>Fred Bloggs</n:name>
  </n:passenger>
 </env:Header>
 <env:Body>
  <p:itinerary xmlns:p="http://travelcompany.example.org/reservation/travel">
   <p:departure>
     <p:departing>New York</p:departing>
     <p:arriving>Los Angeles</p:arriving>
     <p:departureDate>2007-12-14</p:departureDate>
     <p:departureTime>late afternoon</p:departureTime>
     <p:seatPreference>aisle</p:seatPreference>
   </p:departure>
   <p:return>
     <p:departing>Los Angeles</p:departing>
     <p:arriving>New York</p:arriving>
     <p:departureDate>2007-12-20</p:departureDate>
     <p:departureTime>mid-morning</p:departureTime>
     <p:seatPreference></p:seatPreference>
   </p:return>
  </p:itinerary>
 </env:Body>
</env:Envelope>
```

主要會有 `Envelope` 為根節點， `Header` 和 `Body` 為子節點。
`Header` 用來傳遞訊息的 Meta 資料，通常會有授權資訊或其他摘要資訊。
`Body` 則是實際的資料。


### Rest
Rest 全名是 Representational State Transfer，是一種軟體架構風格。Rest 通常運行在 HTTP 之上。實作了 Rest 架構的 API 服務稱為 `Restful API`。

Rest 架構有幾個原則： 

- **介面統一**：就是有明確的規範。
- **無狀態**：是指每次呼叫 API 時，同樣的參數得到的結果是一樣的。
- **可快取**：因為無狀態的特性，所以當同樣的呼叫發生時，第二次呼叫可以直接回傳快取的結果。
- **分層系統**：可以理解為呼叫 API 時，伺服器回傳資料前，可能會在背後呼叫多個其他伺服器服務取得結果並組出最終結果回傳給使用者。
- **程式碼在需要時可下載**：這是指在特別的情況下，會需要支援下載程式原始碼的功能。

而常見的 Rest API 資料格式，會有 JSON 或 XML 格式。


### GraphQL
GraphQL 是一種由 Facebook 開發的 API 語言。GraphQL 有一個特點是可以讓客戶端自由選擇要取得的資料，而不是由伺服器決定要回傳什麼資料。

GraphQL 與 Rest 架構極為相似，主因是因為 GraphQL 是為了解決 Rest 架構風格的問題而衍生出來。

在 Rest 時，會面臨到常見的問題是，固定的資料結構而有過多或不足的資料的情況發生，導致會有開發重複或是效能問題，甚至有資料傳輸過多的問題發生。而 GraphQL 就是為了解決這些問題而生。

因此 GraphQL 能夠極為彈性的取得資料，並且可以在一次呼叫中取得多個不同類型的資料，這樣可以減少多次呼叫 API 的次數，提升效能。


### gRPC
gRPC 是一種由 Google 開發的高效能、開源的 RPC 框架。讓應用程式可以直接呼叫伺服器端的方法，就像呼叫本地方法一樣。


### Webhook
Webhook 是一種 API 的應用，是一種異步的 API。當某些事件發生時，伺服器會主動發送 HTTP 請求到指定的 URL，通知事件發生。


### WebSocket
WebSocket 是一種雙向通訊協定，可以在單個 TCP 連線上提供全雙工通訊。WebSocket 可以在應用程式和伺服器之間建立持久性連線，並且可以在伺服器和應用程式之間進行即時通訊。


## 比較表格
以下是一個簡單的比較表格，來比較這幾種 API 架構風格的特性。
![](../assets/images/2024/20241106/api-styles-table.png)


## 參考

- [Understanding API Timeline and Security](https://www.linkedin.com/pulse/understanding-api-timeline-security-kavitha-b-/)
- [What are the main API Architecture Styles](https://newsletter.techworld-with-milan.com/p/what-are-the-main-api-architecture)
- [Top 6 Most Popular API Architecture Styles You Need to Know (with Pros, Cons, and Use Cases)](https://dev.to/kanani_nirav/top-6-most-popular-api-architecture-styles-you-need-to-know-with-pros-cons-and-use-cases-564j)
- [什麼是 RESTful API](https://aws.amazon.com/tw/what-is/restful-api/)
- [Introduction to GraphQL](https://graphql.org/learn/)
- [gRPC overview](https://cloud.google.com/api-gateway/docs/grpc-overview)
