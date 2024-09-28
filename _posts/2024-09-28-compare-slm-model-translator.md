---
title: 針對 llama 3.2 與 phi 3.5 和 gemma 2 翻譯的比較
author: chuehnone
date: 2024-09-28 16:58:00 +0800
categories: [學習]
tags: [AI, llama, phi, gemma]
render_with_liquid: false
---

在上篇針對 [Vdosumry](https://github.com/chuehnone/vdosumry) 新增了翻譯功能，衍伸發現 llama 3.2 的結果不如我的預期。

查了一下 [Meta Blog 有分享相關的 benchmark](https://ai.meta.com/blog/llama-3-2-connect-2024-vision-edge-mobile-devices/)

![](/assets/images/20240928/llm-benchmark.png)

在這份 benchmark 是拿 llama 3.2 跟 phi 3.5 mini 和 gemma 2 做比較，所以就好奇拿上次同樣的英文來翻譯成中文，結果會是什麼。

比較之前，先針對這幾個模型做一下簡單的比較。

## 模型比較

| Benchmark  | llama 3.2 3B | llama 3.2 1B | phi 3.5 mini | gemma 2 2B |
|------------|--------------|--------------|--------------|------------|
| Parameters | 3.21 B       | 1.24 B       | 3.82 B       | 2.61 B     |
| Size       | 2.0 GB       | 1.3 GB       | 2.2 GB       | 1.6 GB     |


## 翻譯比較

### Prompt

```
# 請將以下內容翻譯成台灣中文

{{query}}
```

### {{query}}

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

### llama 3.2 3B

```
以下是原文的翻譯：

這appears to be a transcript from a presentation by a person (likely the CEO or founder) of a company that has developed a new type of augmented reality (AR) glasses。以下是一個總結：

會議上介紹了公司最新的產品「奧里昂」（Orion），是一對具有全新顯示架構的光學增強現實（Augmented Reality）眼鏡。「奧里昂」是一對可以顯示高質量光學幻覺的眼鏡，具備以下關鍵功能：

1.  錯誤的projectors和waveguides，可以顯示高質量的光學幻覺。
2.  使用custom silicon和感應器，可以啟動advanced tracking capabilities（手、眼睛、聲音）。
3.  一小塊電池能夠 powering整個系統。

會議上的speaker強調了透過眼鏡和看見他人的作用，這對於傳統的VR或AR系統来说是不可能的。他们還提到這項เทคโนโลย有機會 revolutionize 我們與電腦在公共空間的交互方式。

會議上有一些特定的說明，例如：

*   手指追踪允許更親近的界面控制，但不一定適合所有情況（例如：公共使用）。
*   聲音輸入是方便的，但是 sometimes你想說你在做什么但不想說出來。
*   眼部追蹤可以通過看到 UI element 的方式選擇。

會議上提到公司正在於將一款手臂-Based  neural interface 將這些眼鏡內接入，將讓用戶能夠控制device使用心腦接觸。然而，尚有許多要進行「tune and improve」之前才會發送給消費者。

整體而言，這個 presentations Seems to be about introducing a revolutionary new technology that has the potential to transform how we interact with computers in everyday life。
```

### llama 3.2 1B

```
這裡翻譯成台灣中文：

「這看起來是由一個公司出場的演說，該公司正推出的新型態的增強視覺（AR）眼镜。該演說概述：

該講師是介紹最近發生的新產品——名為Orion的Augmented Reality（增強視覺）眼鏡，並解釋其一些重要的特點：

1. 這些眼鏡使用小型燈燒和波guid器來產生高質量的增強視覺表現。
2. custom的 Silicon 和感應結構，enable advanced tracking能力（手指、眼睛、語音）。
3. 一個小型電池板，幫助 powering whole system。

講師強調，在這些眼鏡中可以看到自己的眼球和面孔，從而提高視覺上的互動。該技術對於在公眾場所使用增強視覺系統具有極大潛力。

某些特點被讲到了的還有：

* 手指感應能夠更方便地控制交互式界面，但可能不適合所有情況（例如公共用途）。
*語音感應是便利的，但是你也许不想說出你現在做的事情。
* 眼視覺上顯示的UI元素可以通過看個他的眼睛來選擇。

講師還提到該公司正在嘗試將一個手臂基底結構（Neural Interface） incorporation 到這些眼鏡中，能夠讓使用者通過想著控制眼鏡來控制device。然而，這裡仍有很多點需要「調整」和改進。

總的來說，這個演說似乎是關注將一種全新的增強視覺技術推向大眾生活中的革命性效果。
```

### phi 3.5 mini

```
這是一則可能由公司聯合總經理或企業的共同設計者所進行的會議紀錄。以下是台灣中文版摘要：

在此次介紹中，他們正式展示了新型公司開發出來的Orion—一款全新設計的虛擬實境（VR）頭盔。以下是重點：

1. 使用微型放大機和波長管道，能提供高品質的虛擬投影。
2. 定制集成電路及傳感器以達到先進的監控能力（手、目、口語）。
3. AI驅動小型電池片，提供支持系統全部功能。

講者特別強調了Orion頭盔的一大步進展：可以在面前看到自身及交流目光點同人，而非像依賴老式VR或AR系統所需要的偽存在。他也提出了這一技術未來能重新定義我們使用公共空間交互電腦的方法，而不是直接站在面前看機器人操控者盤數字。

他提到了以下要注意之點：

* 手指動作可用于更自然便利的界面控制，對公共使用有限需求（如交通等）不理想。
*口語入力方式為輕易且便利，但時候你不希望以此形式透露自身的動作或行動。
* 用大腦神經對話可直接選取UI元素範例（如按鈕）。

他並提到公司正在研究和開發加入Orion頭盔的手臂基於大腦神經對話控制，希望能使用者操作器件直接思想中。然而他也指出仍有些功能需要進一步微调和改良之前才能正式送到消費市場上班。

全書的大方向是展示了這個如同在身家中看見機器人主管、更新自然且高效交流電腦所需要經濟和心理可能性，以改造我們日常生活當中的技術接觸方式。
```

### gemma 2 2B

```
##  這份內容是公司創辦人/ CEO 介紹一款新型擴增實境 (AR) 眼鏡的簡報內容。以下是重點整理：

**介紹:**

* 主講者介紹他們最新產品，稱為「歐利安」(Orion)，是一款具有全新顯示架構的Holo AR 眼鏡。
* 主講者重點介紹其功能，包括:
    1. 小型投影機和波導，實現高品質的 Hologram display。
    2. 自訂矽和感應器，實現精確的追踪功能（手、眼睛、語音）。
    3. 小型電池供電小 puck，為整個系統提供動力。

**重點:**

* 主講者強調能透過這些眼鏡看到世界並與他人進行眼神交流的重要性，這在傳統 VR 或 AR 系統中無法實現。
* 他們也提到這項技術有潛力改變我們在公共空間中與電腦互動的方式。

**其他重點:**

* 手指追踪允許更直觀的介面控制，但可能不適用於所有情況（例如公共使用）。
* 语音输入方便快捷，但有時你不想在公開場合說出你想做的事情。
* 眼睛追踪可以通過眼神來選擇 UI 元素。

**未來展望:**

* 主講者提到公司正在研發wrist-based 神經接口技術，讓使用者可以用思緒控制設備。
* 但是，他們還需要調整和優化一些細節，在推出消費者產品之前進行調整。

**總結:**

* 此簡報旨在介紹一個具有革命性新技術，其潛力將改變我們日常生活中與電腦互動的方式。 
```

## 結論

可以看到這四個結果的翻譯結果都有些許不同

- **llama 3.2 3B** 的翻譯結果，會直接出現大量的原文
- **llama 3.2 1B** 的翻譯結果，則是會有晶晶體，比較接近口語些（？）
- **phi 3.5 mini** 的翻譯結果，則是語意有點不順
- **gemma 2 2B** 的翻譯結果，除了翻譯外，還多了些額外的調整

就單純以這次的翻譯，我個人會比較偏好 **gemma 2 2B** 的結果
