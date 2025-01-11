---
title: 解決 Dify 新增 ollama 模型失敗 Errno 111 狀況
author: chuehnone
categories:
  - 教學
tags:
  - Dify
  - Ollama
image:
  path: "/assets/images/2025/20250111/home.png"
  alt: Dify 新增 Ollama 模型失敗
date: 2025-01-11 13:35 +0800
---

在 Dify 新增 Ollama 模型時，可能會遇到以下錯誤訊息：

![](/assets/images/2025/20250111/error.png)

```markdown
An error occurred during credentials validation: HTTPConnectionPool(host='localhost', port=11434): 
Max retries exceeded with url: /api/chat (Caused by NewConnectionError('<urllib3.connection.HTTPConnection object at 0xffff630b0f50>: 
Failed to establish a new connection: [Errno 111] Connection refused'))
```

這個在 [Dify 文件](https://docs.dify.ai/development/models-integration/ollama)上也有提到，主要是因為用 docker 服務起的 Dify 無法連接到本地端的 Ollama 服務。

解決方法也很簡單，改用 `host.docker.internal` 來連接 Ollama 就可以了。

![](/assets/images/2025/20250111/config.png)
