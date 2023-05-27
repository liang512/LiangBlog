---
title: "Introduction to Mathematical Thinking Week2"
date: 2023-05-23T21:23:23+08:00
draft: false
author: Liang Li
tags: ["Math"]
math: true
description: "Implication and Equivalence"
---
# Implication
The implication is important in mathematics. $\phi$ implies $\psi$ is denoted as $\phi\implies\psi$, that means **the truth of $\psi$ follows from the truth of $\phi$**. And $\phi$ is called antecedent and $\psi$ is consequent. The truth table of $\phi\implies\psi$ as follows: 

<div style="margin-left: auto;
            margin-right: auto;
            width: 40%">

| $\phi$ | $\psi$ | $\phi\implies\psi$ |
| ------ | ------ | :----------------: |
| T      | T      |         T          |
| T      | F      |         F          |
| F      | T      |         T          |
| F      | F      |         T          |

</div>
The T denotes the truth and F denotes the false.

1. A true conclusion from a true assumption, so the first row is true. 
2. If that implication is true, that means $\psi$ would have to be T if $\phi$ is T. So we cannot have $\phi$ is T and $\psi$ is F if $\phi\implies\psi$ is T. Hence $\phi\implies\psi$ must be F.
3. We can look at "$\phi$ does not imply $\psi$" ($\phi\nRightarrow\psi$) that is even through $\phi$ is T, $\psi$ is nevertheless F. So $\phi\nRightarrow\psi$ is T if and only if $\phi$ is T and $\psi$ is F. In all other circumstances, $\phi\nRightarrow\psi$ is F, which means $\phi\implies\psi$ is T. So, the third and fourth rows are T.

> :memo: **Note:** The implication involves **causality**. For example, "$\sqrt{2}$ is irrational" does not imply "$1+1=2$", because this two statements has no relationship, they are independent of each other.

# Equivalence

Two statements $\phi$ and $\psi$ are said to be equivalent if each implies the other. It is denoted $\phi\Leftrightarrow\psi$ if $\phi\implies\psi$ and $\psi\implies\phi$. $\phi\Leftrightarrow\psi$ is true if $\phi$ and $\psi$ are both true or both false.

<div style="margin-left: auto;
            margin-right: auto;
            width: 70%">

| $\phi$ | $\psi$ | $\phi\implies\psi$ | $\psi\implies\phi$ | $\phi\Leftrightarrow\psi$ |
| ------ | ------ | :----------------: | :----------------: | :-----------------------: |
| T      | T      |         T          |         T          |             T             |
| T      | F      |         F          |         T          |             F             |
| F      | T      |         T          |         F          |             F             |
| F      | F      |         T          |         F          |             F             |

</div>

# Summary



## [Assignment 4](https://d3c33hcgiwev3.cloudfront.net/_3092f5c4fdb978572fc7d46a905b71cb_Assignment-4.pdf?Expires=1685145600&Signature=lejXPnSochGAHWXLEDiZZsBpyEtYm5zjrCBlD-tpKCPaWbpfSCbmDZwGOC8inJo8eS64CE6zmiz5rtnLm8wFY53zylYpid3mbarkCPK8wtJFCVq6qMS9Lq0qMsJ8GF1xx~7yOwuA0g3f3F97PAjzRHeZGSiAH1sRZoY0FNRHFyo_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A)

4. Proof of **modus ponens**: The rule of logic stating that if a conditional statement ($\phi\land(\phi\implies\psi)$) is accepted, and the antecedent ($\phi$) holds, then the consequent ($\psi$) may be inferred.

| $\phi$ | $\psi$ | $\phi\implies\psi$ | $\phi\land(\phi\implies\psi)$ | $[\phi\land(\phi\implies\psi)]\implies\psi$ |
| ------ | ------ | :----------------: | :---------------------------: | :-----------------------------------------: |
| T      | T      |         T          |               T               |                      T                      |
| T      | F      |         F          |               F               |                      T                      |
| F      | T      |         T          |               F               |                      T                      |
| F      | F      |         T          |               F               |                      T                      |
