---
title: "身份基加密"
date: 2025-03-05T15:13:30+08:00
draft: false
author: 李梁
description: 本文将详细介绍第一篇实现了正式身份基加密的文章 Identity-Based Encryption from the Weil Pairing
---
# 前言
在传统的电子邮件系统中，如果 Alice 想给 Bob 发送一封加密邮件，需要使用 Bob 的公钥加密来加密邮件，进而需要一个公钥证书颁发机构（Certificate Authority，CA）对系统中的公钥一一生成证书，用户才可以放心地使用公钥；此外这种加密方案缺乏语义性，即加密所用的公钥是一个群元素。可以看出，公钥证书的管理给系统带来了存储和计算方面的巨大开销。

为了解决这一问题，在1984年，著名密码学家 Shamir 提出是否可以构造一个公钥加密方案，它可以使用任意的字符串作为公钥加密数据。随后，身份基加密（Identity-Based Encryption，IBE）应用而生，在使用身份基加密的电子邮件系统中，当 Alice 想要给 Bob 发送邮件时，只需使用 Bob 的邮件地址“bob@company.com”作为公钥即可生成密文，Bob 向私钥生成中心（Private Key Generator，PKG）请求对应于自己邮件地址的私钥，随后使用该私钥便可完成解密。在该密码体制内，无需管理公钥证书，且任意字符串都可以作为加密公钥。

2003年，Boneh 和 Franklin 提出了第一个**完全实现**身份基加密的文章详。强调完全实现，是因为在这之前的身份基加密方案要么是无法抵御用户合谋攻击，要么需要抗篡改的硬件支持。本文提出了在随机预言机模型（Random Oracle Model，ROM）下可以抵御选择明文攻击的适应性安全（Chosen plaintext security，IND-CPA）的方案和可以抵御选择密文攻击的适应性安全的方案（Chosen ciphertext security，IND-CCA）。

# 预备知识
待补充
# 身份基加密定义
本节首先给出身份基加密的算法定义，随后对其正确性和安全模型进行描述。
## 算法定义
一个身份基加密方案$\epsilon$包含以下4个算法：
- $\mathsf{Setup}(k)\rightarrow (\mathsf{mpk,msk})$: 系统初始化算法输入安全参数$k$，输出系统主公钥$\mathsf{mpk}$和主私钥$\mathsf{msk}$；
- $\mathsf{Extract}(\mathsf{mpk},\mathsf{msk},\mathsf{ID}) \rightarrow d$：密钥生成算法输入系统主公钥$\mathsf{mpk}$、主私钥$\mathsf{msk}$、和用户身份$ID$，输出用户$ID$的私钥$d$；
- $\mathsf{Encrypt}(\mathsf{mpk},ID,M)\rightarrow C$：加密算法输入系统主公钥$\mathsf{mpk}$、用户$ID$和明文$M$，输出密文$C$；
- $\mathsf{Decrypt}(\mathsf{mpk},d,C)\rightarrow M$：解密算法输入系统主公钥$\mathsf{mpk}$、用户$ID$的私钥$d$和密文$C$，输出明文$M$。

**正确性**：给定安全参数$k$，对于任意用户$ID$和明文$M$，如果$(\mathsf{mpk},\mathsf{msk})\leftarrow \mathsf{Setup}(k)$，$d\leftarrow \mathsf{Extract}(\mathsf{mpk},\mathsf{msk},ID)$，$C\leftarrow \mathsf{Encrypt}(\mathsf{mpk},ID,M)$，则
$$\Pr{[\mathsf{Decrypt}(\mathsf{mpk},d,C)=M]}=1.$$

## 安全模型

### 适应性选择明文安全（Chosen plaintext security，IND-CPA）
称一个IBE方案是IND-CPA的，如果对于任意多项式时间的敌手$\mathcal{A}$，在下述的IND-CPA游戏中获胜的概率是可忽略的：
- 初始化：挑战者$\mathcal{C}$选取一个安全参数$k$并运行$\mathsf{Setup}$算法，将系统主公钥$\mathsf{mpk}$发送给$\mathcal{A}$，自己保留主私钥$\mathsf{msk}$；
- 阶段1：$\mathcal{A}$发起对挑战者的询问$q_1,\dots,q_m$，其中$q_i$是下述询问：
  - $\mathsf{Extract_q}(ID_i)$：$\mathcal{A}$选择一个$ID_i$，挑战者返回私钥$d_i$给敌手；
- 挑战阶段：$\mathcal{A}$选择两个长度相同的消息$M_0$和$M_1$和一个身份$ID$，$\mathcal{C}$发送相应的密文$C\leftarrow \mathsf{Encrypt}(\mathsf{mpk},ID,M_b)$给$\mathcal{A}$，其中$b$随机选自于 $\{0,1\}$；
- 阶段2: $\mathcal{A}$发起对挑战者的询问$q_{m+1},\dots,q_n$，其中的询问和阶段1相同；
- 猜测：$\mathcal{A}$输出一个猜测$b^\prime$，如果$b^\prime=b$，那么$\mathcal{A}$赢得游戏；
我们定义敌手$\mathcal{A}$的优势为
$$\text{Adv}_{\mathcal{A}}^{\text{IND-CPA}}(k)=|\Pr{[b^\prime=b]}-1/2|.$$

> 称IBE方案$\epsilon$是适应性选择明文安全的，如果对于任意多项式时间的敌手$\mathcal{A}$，$\text{Adv}_{\mathcal{A}}^{\text{IND-CPA}}(k)$是可忽略的。

### 适应性选择密文安全（Chosen ciphertext security，IND-CCA）