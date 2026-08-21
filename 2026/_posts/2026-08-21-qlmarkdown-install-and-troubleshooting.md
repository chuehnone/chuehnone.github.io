---
title: 用 QLMarkdown 讓 macOS 空白鍵直接預覽 Markdown
author: chuehnone
categories:
  - 工具
tags:
  - macOS
  - Markdown
  - Quick Look
  - Homebrew
  - Tool
date: 2026-08-21 09:07 +0800
---

在 Finder 選一個檔案按空白鍵，就會跳出 Quick Look 預覽，這是 macOS 很好用的功能。但預設情況下 `.md` 檔按空白鍵，看到的是**沒有渲染過的原始文字** —— `# 標題` 就真的顯示成 `# 標題`，`**粗體**` 兩邊的星號也都在。

平常筆記、README、專案文件都是 Markdown，每次要確認內容還得開編輯器，實在有點麻煩。[QLMarkdown](https://github.com/sbarex/QLMarkdown) 就是來解決這件事的：裝上之後按空白鍵，Markdown 會直接渲染成排版好的樣子。

## 安裝

用 Homebrew 最省事：

```bash
brew install --cask qlmarkdown
```

寫這篇時的版本是 1.5.2，需求是 macOS 11 以上。也可以直接去 [GitHub Releases](https://github.com/sbarex/QLMarkdown/releases) 下載 dmg 手動安裝。

**但裝完不會馬上生效**，這是我這次踩到的坑，後面詳細說。

## 裝完必做的兩件事

### 1. 開啟一次 QLMarkdown.app

```bash
open -a QLMarkdown
```

這步不能跳過。macOS 只有在 app **實際被執行過一次**之後，才會把 bundle 裡的 Quick Look extension 註冊到系統的 PlugInKit。沒開過 app，系統根本不知道有這個外掛存在。

### 2. 在系統設定裡啟用 extension

開啟 **系統設定 → 一般 → 登入項目與延伸功能 → Quick Look**，把 **QLMarkdown** 打勾。

舊版 macOS 的路徑是 **系統設定 → 隱私權與安全性 → 延伸功能 → Quick Look**。

註冊過的 extension 預設是**停用**狀態，這一步只能手動點，沒有指令可以代勞。

打勾之後，回 Finder 選一個 `.md` 檔按空白鍵，就會看到渲染後的結果了。

## 預期成效

裝好之後的差別：

| | 裝之前 | 裝之後 |
|---|---|---|
| 標題 | 顯示 `# 標題` | 依層級呈現不同大小的標題 |
| 粗體、斜體 | 星號原樣露出 | 正常呈現粗體與斜體 |
| 程式碼區塊 | 連 ``` 一起顯示 | 語法高亮的程式碼區塊 |
| 表格 | 一堆 `\|` 對不齊 | 排版好的表格 |
| 連結、圖片 | 顯示 Markdown 語法 | 可點的連結、直接顯示圖片 |

除了空白鍵預覽，Finder 的檔案縮圖也會跟著變成渲染後的樣子，在一堆 `.md` 檔裡找東西時滿有感的。

QLMarkdown 主視窗本身就是設定面板，可以調整主題配色、語法高亮樣式、是否啟用 GFM 擴充（表格、任務清單、刪除線等）、字體大小這些選項。改完設定後的預覽會即時反映。

另外它還附了一支 CLI，可以把 Markdown 轉成 HTML：

```bash
/Applications/QLMarkdown.app/Contents/Resources/qlmarkdown_cli input.md > output.html
```

## Q&A

### Q1: 裝好了，按空白鍵還是純文字，為什麼？

我這次遇到的就是這個。原因通常是**上面那兩件事沒做**，尤其是第一件 —— app 從來沒被開啟過。

先確認 extension 有沒有註冊：

```bash
pluginkit -mAvvv | grep -A3 QLMarkdown
```

有註冊的話會看到類似這樣的輸出：

```
org.sbarex.QLMarkdown.QLExtension(1.5.2)
            Path = /Applications/QLMarkdown.app/Contents/PlugIns/Markdown QL Extension.appex
             SDK = com.apple.quicklook.preview
   Parent Bundle = /Applications/QLMarkdown.app
```

**完全沒有輸出** = 系統沒註冊到，去做第一件事（開啟 app）。
**有輸出但預覽還是純文字** = 註冊了但沒啟用，去做第二件事（系統設定打勾）。

### Q2: 為什麼「沒開過 app」會讓外掛失效？

Quick Look extension 是包在 app bundle 裡面的 `.appex`：

```bash
ls /Applications/QLMarkdown.app/Contents/PlugIns/
# Markdown QL Extension.appex
```

檔案雖然在硬碟上，但 macOS 的 PlugInKit 是在 app 首次執行時才去掃描並註冊裡面的 extension。在那之前，對系統來說這個外掛等於不存在。

所以「檔案存在」跟「系統認得」是兩回事，這也是為什麼裝完一定要開一次。

### Q3: 我是手動下載 dmg 安裝的，開了 app 還是沒註冊？

檢查一下 quarantine 屬性：

```bash
xattr -l /Applications/QLMarkdown.app
```

如果看到 `com.apple.quarantine`，代表這是從網路下載的檔案，macOS 的 Gatekeeper 會擋。清掉它：

```bash
xattr -dr com.apple.quarantine /Applications/QLMarkdown.app
open -a QLMarkdown
```

用 `brew install --cask` 裝的話一樣會帶上 quarantine 屬性，只是通常開啟 app 時 Gatekeeper 會正常放行，比較少卡在這關。

注意：清除 quarantine 等於跳過 Gatekeeper 檢查，只對確定來源可信的 app 這樣做。

### Q4: 兩件事都做了還是沒用？

Quick Look 有快取，重置一下：

```bash
qlmanage -r
qlmanage -r cache
killall Finder
```

### Q5: 怎麼確認 Quick Look 現在真的是用 QLMarkdown 在渲染？

用 `qlmanage` 產一張縮圖來看：

```bash
qlmanage -t -s 400 -o . test.md
```

會在當前目錄產生 `test.md.png`。打開來看，如果 `#` 和 `**` 這些符號還原樣露在畫面上，那就是系統內建的文字預覽器在處理，QLMarkdown 還沒真的接手。

### Q6: 會不會拖慢 Finder？

日常大小的 Markdown 檔沒什麼感覺。真的很大的檔案（幾 MB 的文件）渲染會慢一點，但這種情況本來就不多。

### Q7: 支援哪些語法？

底層用 [cmark-gfm](https://github.com/github/cmark-gfm)，也就是 GitHub 那套 Markdown 實作，所以表格、任務清單、刪除線、自動連結這些 GFM 擴充都有。另外還支援 footnotes、emoji、YAML front matter 等，這些都可以在 app 的設定面板裡個別開關。

寫 Jekyll 文章時前面那段 YAML front matter 也能正確處理，不會被當成內文亂渲染。

## 小結

整件事的重點就一句：**裝完要開一次 app，然後去系統設定打勾**。

這兩步在 Homebrew 安裝時不會自動完成，而 `brew install` 跑完又是成功訊息，很容易誤以為已經好了。留個紀錄，之後換電腦重裝時可以直接照做。
