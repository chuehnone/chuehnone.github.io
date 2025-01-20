---
title: JWT 跟 JOSE 的關係是什麼？
author: chuehnone
categories:
  - 學習
tags:
  - JOSE
  - JSON
  - JWS
  - JWE
  - JWT
  - JWK
  - JWA
  - signing
  - encryption
date: 2025-01-20 15:08 +0800
---

如果曾經接觸過 API 身份驗證，應該對 JWT (JSON Web Token) 不陌生。
它是目前廣泛使用的一種身份驗證技術。然而，JWT 只是 JOSE (JSON Object Signing and Encryption) 標準的一部分。

JOSE 是處理 JSON 數位簽章與加密而定義的標準，特別是在身份驗證與資料保護。

以下將介紹 JOSE 的五個主要部分：

## JWS (JSON Web Signature)

用於對 JSON 資料進行數位簽章，確保資料的完整性與來源的可信性。

## JWE (JSON Web Encryption)

用於對 JSON 資料進行加密，確保資料的機密性。

## JWK (JSON Web Key)

定義一種用於表示金鑰的 JSON 格式，用來儲存和金鑰交換。

## JWA (JSON Web Algorithms)

列出 JOSE 使用的演算法清單，包括數位簽章和加密演算法。

## JWT (JSON Web Token)

JOSE 的具體應用，用於在不同系統之間安全傳遞信息。

JWT 包含 3 個部分：

1. **Header**：使用的簽章或加密演算法。
  ```json
{
  "alg": "HS256",
  "typ": "JWT"
}
  ```
  `alg` 指定簽章演算法，`typ` 指定 token 類型。

2. **Payload**：儲存需要傳遞的資料內容。
  ```json
{
  "iss": "Issuer",
  "sub": "Subject",
  "aud": "Audience",  
  "exp": 1517239022,
  "nbf": 1516939022,
  "iat": 1516239022,
  "jti":  "123456"
}
  ```
  `iss` 指定發行者，`sub` 指定主題，`aud` 指定接收者，`exp` 指定過期時間，`nbf` 指定生效時間，`iat` 指定發行時間，`jti` 指定 JWT ID。
  其中 `iat`、`nbf`、`exp` 這三個是容易搞混的，三個關係會是 `iat` <= `nbf` < `exp`。

3. **Signature**：用於驗證資料完整性的數位簽章。

![](/assets/images/2025/20250120/home.png)

## 參考
- [JOSE - JSON Object Signing and Encryption](https://www.redhat.com/en/blog/jose-json-object-signing-and-encryption)
- [JWT](https://jwt.io/)
- [JOSE (JSON Object Signing and Encryption) Framework](https://medium.com/apinizer/jose-json-object-signing-and-encryption-framework-aeefcf27775)
