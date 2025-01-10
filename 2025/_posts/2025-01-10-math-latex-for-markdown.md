---
title: 在 Markdown 使用 LaTeX 顯示數學公式
categories:
  - 工具
tags:
  - LaTeX
date: 2025-01-10 11:51 +0800
math: true
---

有時候總會有需要顯示數學公式，這篇文章是紀錄常見的 LaTeX 數學公式在 Markdown 中的使用方式。

## 行內公式

使用 `$...$` 包裹公式，即可顯示行內數學公式。

### 方程式

在同一行顯示的範例 $y = x^2 + 2x + b$

```markdown
$y = x^2 + 2x + b$
```

### 分數

在同一行顯示的範例 $\frac{a}{b}$

```markdown
$\frac{a}{b}$
```

### 根號

在同一行顯示的範例 $\sqrt {a^2 + b^2}$

```markdown
$\sqrt {a^2 + b^2}$
```

## 區塊公式

使用 `$$...$$` 包裹公式，即可顯示區塊數學公式。

### 矩陣

$$
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
$$

```markdown
$$
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
$$
```

### 積分
$$
\int_a^b x^2 dx = \frac{b^3}{3} - \frac{a^3}{3}
$$

```markdown
$$
\int_a^b x^2 dx = \frac{b^3}{3} - \frac{a^3}{3}
$$
```

### 極限
$$
\lim_{x \to \infty} \frac{1}{x} = 0
$$

```markdown
$$
\lim_{x \to \infty} \frac{1}{x} = 0
$$
```

## 其他

[在线数学公式编辑器](https://www.2weima.com/gongshi.html)：一個方便的線上工具，可以產出 LaTeX / HTML Img / MathML。
