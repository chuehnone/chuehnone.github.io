---
title: 使用 Architectural Decision Records (ADRs)
author: chuehnone
date: 2024-10-23 10:58:00 +0800
categories: [學習, 工具]
tags: [Architectural Decision Records, ADRs, Tool, adr-tools, graphviz]
render_with_liquid: false
---

**Architectural Decision Records** 翻譯成中文，是架構決策記錄，簡稱 ADRs。這是一種記錄軟體架構決策的方式，可以讓團隊更容易了解為什麼要做這樣的決策，以及這個決策的背景。

更多內容可以參考 [GitHub adr organization](https://adr.github.io/)

今天主要來分享怎麼使用 ADRs。

## 使用方式

可以自行建立檔案，或是透過 [adr-tools](https://github.com/npryce/adr-tools) 來建立。

這是使用 adr-tools 生成的初始範例

透過 adr-tools 來初始化純放的檔案路徑，並會生成第一個 0001 檔案
```bash
adr init ./
```

產生的資料有
```bash
.
├── .adr-dir
└── 0001-record-architecture-decisions.md
```

**.adr-dir** 的內容如下
```markdown
./
```

內容就是儲存指定的路徑

**0001-record-architecture-decisions.md** 的內容如下
```markdown
# 1. Record architecture decisions

Date: 2024-10-23

## Status

Accepted

## Context

We need to record the architectural decisions made on this project.

## Decision

We will use Architecture Decision Records, as [described by Michael Nygard](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions).

## Consequences

See Michael Nygard's article, linked above. For a lightweight ADR toolset, see Nat Pryce's [adr-tools](https://github.com/npryce/adr-tools).
```

可以看到內容會有以下幾個部分：
- 標題
- 決策日期
- 狀態
- 背景
- 決策
- 結果

再依照這次的決策做修改即可。


## 新增文件

```bash
adr new Implement REST API
```

目錄結構如下
```bash
.
├── .adr-dir
├── 0001-record-architecture-decisions.md
└── 0002-implement-rest-api.md
```

**0002-implement-rest-api.md** 的內容如下
```markdown
# 2. Implement REST API

Date: 2024-10-23

## Status

Accepted

## Context

The issue motivating this decision, and any context that influences or constrains the decision.

## Decision

The change that we're proposing or have agreed to implement.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
```

## 新增文件取代舊資料

```bash
adr new -s 2 Implement RESTful APIs
```

目錄結構如下
```bash
.
├── .adr-dir
├── 0001-record-architecture-decisions.md
├── 0002-implement-rest-api.md
└── 0003-implement-restful-apis.md
```

**0002-implement-rest-api.md** 的內容如下
```markdown
# 2. Implement REST API

Date: 2024-10-23

## Status

Superceded by [3. Implement RESTful APIs](0003-implement-restful-apis.md)

## Context

The issue motivating this decision, and any context that influences or constrains the decision.

## Decision

The change that we're proposing or have agreed to implement.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
```

可以看到 Status 有做調整，並且指向了 **0003-implement-restful-apis.md** 檔案


**0003-implement-restful-apis.md** 的內容如下
```markdown
# 3. Implement RESTful APIs

Date: 2024-10-23

## Status

Accepted

Supercedes [2. Implement REST API](0002-implement-rest-api.md)

## Context

The issue motivating this decision, and any context that influences or constrains the decision.

## Decision

The change that we're proposing or have agreed to implement.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
```

新增的內容，在 Status 也可以看到被取代的檔案連結


## 產生流程圖

我們會先產出 dot 檔案，再透過 [graphviz](https://graphviz.org/) 來產生流程圖

```bash
adr generate graph > graph.dot
dot -Tpng graph.dot graph.png
```

就可以產出這張圖片

![ADR Graph](/assets/images/20241023/graph.png)


## 其他範例

[AWS ADR 範例](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/appendix.html)

```markdown
# Title

This decision defines the software development lifecycle approach for ABC application development.

# Status

Accepted

# Date

2022-03-11

# Context

ABC application is a packaged solution, which will be deployed to the customer's environment by using a deployment package. We need to have a development process that will enable us to have a controllable feature, hotfix, and release pipeline.

# Decision

We use an adapted version of the GitFlow workflow to develop ABC application.
```
