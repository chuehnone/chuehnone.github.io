---
title: 設定 GitHub private commit email，保護隱私又保留貢獻紀錄
author: chuehnone
categories:
  - 教學
tags:
  - github
date: 2025-01-07 14:12 +0800
---

當你使用 Git 進行版本控制時，commit 記錄中會公開顯示你的 email。這可能導致聯絡資訊的外洩，甚至引來垃圾郵件。

![GitHub 貢獻紀錄](/assets/images/2025/20250107/home.png)

如果你不希望在 commit 中外洩你的聯絡資訊，而且又能夠保有 GitHub 貢獻紀錄如上圖，可以透過以下步驟設定 GitHub private commit email。

## 操作步驟

**1.** 登入 GitHub 帳號，點擊右上角個人照片，進入 [Settings](https://github.com/settings/profile)

![](/assets/images/2025/20250107/flow-1.png){: w="200" h="100" .normal }

**2.** 進到設定頁面，到側邊欄選擇 [Emails](https://github.com/settings/emails)

![](/assets/images/2025/20250107/flow-2.png){: w="200" h="100" .normal }

**3.** 勾選 Keep my email addresses private

![](/assets/images/2025/20250107/flow-3.png)

**4.** 接著在本地端設定，將 commit email 改為 GitHub private email

```shell
git config --global user.email "{youremail}@users.noreply.github.com"
```
註：`{youremail}` 請替換為你的 GitHub private email，通常會是`數字+帳號`的組合（可在 Emails 頁面查看）。

**5.** 檢查是否設定成功

```shell
git config --global user.email
```

若顯示的是你的 GitHub private email，則設置成功！

## 參考資料
GitHub 官方文件：[Setting your commit email address](https://docs.github.com/en/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)
