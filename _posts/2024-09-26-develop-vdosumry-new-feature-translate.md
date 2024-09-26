---
title: Vdosumry 新增翻譯摘要功能
author: chuehnone
date: 2024-09-26 15:58:00 +0800
categories: [開發]
tags: [Tool, vdosumry]
render_with_liquid: false
---

今天是 llama 釋出 3.2，嘗試用 [Vdosumry](https://github.com/chuehnone/vdosumry) 做 meta 這次發表會影片的摘要，但是摘要的結果卻是英文，所以就多增加了翻譯的功能

## 翻譯功能

這次新增了翻譯功能，主要是透過 ollama 進行翻譯，使用方式很簡單，指令如下

```bash
poetry run vdosumry "https://www.youtube.com/watch?v={youtube_youtube_id}" --language="zh-TW"
```

主要就是新增了參數 **--language**，因為是透過 ollama 翻譯，所以這個值可以是 code 也可以是其他文字

## 其他發現

嘗試也把 ollama 預設 model 改為 llama 3.2，但是在中文呈現結果沒有 llama 3.1 的結果好


Prompt
```
請將以下內容翻譯成 zh-TW 的語言：
```

原文
```
This appears to be a transcript from a presentation by a person (likely the CEO or founder) of a company that has developed a new type of augmented reality (AR) glasses. Here's a summary:

The speaker is introducing their latest product, called Orion, which is a pair of holographic AR glasses with a completely new display architecture. They highlight the key features of these glasses, including:

1. Tiny projectors and waveguides that allow for high-quality holographic displays.
2. Custom silicon and sensors that enable advanced tracking capabilities (hand, eye, voice).
3. A small battery-powered puck that helps power the whole system.

The speaker emphasizes the importance of being able to see through these glasses and make eye contact with others, which is not possible with traditional VR or AR systems. They also mention that this technology has the potential to revolutionize how we interact with computers in public spaces.

Some specific points made by the speaker include:

* Hand tracking allows for more intuitive interface control but may not be suitable for all situations (e.g., public use).
* Voice input is convenient, but sometimes you don't want to say what you're doing out loud.
* Eye-tracking enables selecting UI elements by looking at them.

The speaker also mentions that the company is working on incorporating a wrist-based neural interface into these glasses, which would allow users to control the device with their thoughts. However, there are still some things they want to "tune" and improve before shipping this as a consumer product.

Overall, the presentation seems to be about introducing a revolutionary new technology that has the potential to transform how we interact with computers in everyday life.
```

llama 3.1
```
這似乎是一份由公司的 CEO 或創始人作出的簡報的稿件，他們介紹了一款新型增強實境（AR）眼鏡，名叫「奧利翁」（Orion）。以下是簡報內容的一個概要：

演說者首先介紹了他們最新推出的產品「奧利翁」，這是一對全新的 holographic AR glasses。它們具有一種全新的顯示架構。他們特別強調了這款眼鏡的幾項核心功能：

1. Tiny projectors 和 waveguides，允許創造出高質量的 holographic 顯示。
2. Custom silicon 和 sensors，能夠實現進階的手、眼、聲音追蹤功能。
3. 一個小型充電式 puck，可以幫助整體系統運行。

演說者強調，穿著這款眼鏡可以看到周圍的環境，並與他人保持眼神接觸，這是傳統 VR 或 AR 系統無法達成的。他們也提到，這項技術可能會改變我們在公共空間中與電腦互動的方式。

演說者還針對這款眼鏡的幾個具體方面進行了介紹：

* 手部追蹤功能可以更簡單地控制界面，但是不能適用於所有情況（例如公共使用）。
* 聲音輸入是方便的，但是有時你可能不想聲明自己在做什麼。
* 眼部追蹤功能能夠通過視線選擇 UI 元素。

演說者還提到了，他們正在嘗試將神經接口整合到這款眼鏡上，這樣用戶就可以通過思想控制這個裝置。但是，公司還需要在推出這款產品前，做一些調整和改進工作。

整體而言，這份簡報似乎是在介紹一項革命性的新技術，它有可能變革我們日常生活中與電腦互動的方式。
```

llama 3.2
```
這 appears to be a transcript from a presentation by a person (likely the CEO or founder) of a company that has developed a new type of augmented reality (AR) glasses. Here's a summary：

講者正在介紹他的最新的產品，名叫Orion，是一款 holographic AR 磁鏡，具有完全不同的顯示架構。講者強調了這些眼鏡的關鍵特點，其中包括：

嚟小型 projectors 和 waveguides，它們能夠提供高品質的 holographic 顏面 displays。
自製的 silicon 和 sensor，它們可以啟動 advanced tracking capabilities (手，眼，聲音)。
一個小的电池-powered puck，它們幫助了整個系統。
講者強調了通過這些眼鏡和能夠看到對方眼睛接觸，哪是 traditional VR 或 AR 系統不能做到的。他们還提到，這種 technology 有 Potential 是如何 Revolutionize how we interact with computers in public spaces。

Some specific points made by the speaker include：

Hand tracking allows for more intuitive interface control，但可能不適合所有情況（例如，公共使用）。
Voice input 是 convenient，但有時候你不希望說出你正在做的事情的話。
Eye-tracking enables selecting UI elements by looking at them。
講者還提到，公司正努力在這些眼鏡中加入一種腕帶-based neural interface，它們可以使您控制裝置與您的思維。然而，這仍然有很多東西他們想要“tune” 和 改進，才能先推出這個為消費者產品。

整體來說，Presentation seemingly is about introducing a revolutionary new technology that has the potential to transform how we interact with computers in everyday life。
```
