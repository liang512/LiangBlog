---
title: "Papers"
date: 2023-06-04T16:15:02+08:00
draft: false
author: "Liang"
description: "论文阅读记录"
---

# Keyword-based matching
## Proxy-Free Privacy-Preserving Task Matching with Efficient Revocation in Crowdsourcing [^1]

这篇文章提出了一个无需代理重加密的基于关键字的任务匹配模型，支持用户撤销。[作者公布代码](https://github.com/jgshu/pMatch)。

基本模型是经典的基于可搜索加密的关键字匹配模型，之后加入了 Server-Local Revocation (SLR)，实现用户撤销的思想很简单：服务器维护一个撤销用户列表 **Revocation List (RL)**，当有用户离开系统时，将该用户的相关信息存入RL实现撤销，在每次执行匹配算法时，服务器会先验证改用户是否在RL在，如果在RL中，则此次搜索终止，如不在RL中，说明此次搜索合法，进行匹配操作。

之后为了减少RL的存储开销，作者提出了Global Revocation (GR)，为密钥、密文、搜索陷门加入了**版本号（version number）**，系统周期性地执行$ReKeyGen$算法，清空RL，重新生成公钥、主私钥和密文更新密钥（用来更新之前版本的密文），并为worker分发新的密钥。

优点：撤销机制简单

缺点：每次匹配均需进行两次pairing操作以检查用户权限；在 GR 中，密钥机构需要周期性地上线执行$ReKeyGen$算法，即使是在RL为空时？（作者没有考虑这一点）。

思考：学习到了撤销机制的实现方法：维护撤销用户列表和版本号。

> :memo: **Note:** 写文章思路：先写出一个基础方案，之后进行扩展，本文在基础匹配方案上扩展了用户撤销机制。先写SLR，然后针对 SLR 中RL的存储开销问题，提出GR，让系统定期清空RL，引入版本号。

# ABE

## Registered Attribute-Based Encryption (RABE)
size of CRS quadratic in L
time of registration linear in L----slow 
size of mpk, hdk and time of enc, dec polylogarithmically with L

Main Contribution: resolve leakage of master secret key (msk) problem.

limitations: 
- Exist priori bound L on the number of users in the system
- Trusted output CRS


# Task Assignment

## Bid-based
 ### Personalized Location Privacy Trading in Double Auction for Mobile Crowdsensing
 保护用户位置隐私
 ### Truthful Online Double Auctions for Mobile Crowdsourcing: An On-Demand Service Strategy
 不保护bid
 ### Truthful online double auctions for dynamic mobile crowdsourcing
 不保护bid
 ### Edge Resource Prediction and Auction for Distributed Spatial Crowdsourcing With Differential Privacy
 采用非对称加密保护bid

## Location-based 
 ### Towards preserving worker location privacy in spatial crowdsourcing 2015
 加法同态，在位置密文上进行运算比较来分配
 ### PriRadar: A Privacy-Preserving Framework for Spatial Crowdsourcing, 2020
 利用**属性加密**，将位置经纬度设置为密文访问策略。且保护了任务内容
 ### Protecting Location Privacy of Users Based on Trajectory Obfuscation in Mobile Crowdsensing 2022
 差分隐私
 ### RoPriv: Road Network-aware Privacy-preserving Framework in Spatial Crowdsourcing 2023
 差分隐私
 ### iTAM: Bilateral Privacy-Preserving Task Assignment for Mobile Crowdsensing 2021
 minimize travel distance; Bilateral privacy includes task requirements and worker profiles; 
 Paillier同态
 ### Privacy-Preserving Online Task Assignment in Spatial Crowdsourcing: A Graph-based Approach 2022
 差分隐私混淆位置
 ```
 @INPROCEEDINGS{9796827,
  author={Wang, Hengzhi and Wang, En and Yang, Yongjian and Wu, Jie and Dressler, Falko},
  booktitle={IEEE INFOCOM 2022 - IEEE Conference on Computer Communications}, 
  title={Privacy-Preserving Online Task Assignment in Spatial Crowdsourcing: A Graph-based Approach}, 
  year={2022},
  volume={},
  number={},
  pages={570-579},
  doi={10.1109/INFOCOM48880.2022.9796827}}
 ```

## Keyword-based
 ### Secure Task Recommendation in Crowdsourcing 2016
 利用可搜索加密以及代理重加密
 ### Privacy-Preserving Task Recommendation Services for Crowdsourcing 2018
 SSE 代理重加密 多关键字，使用多项式表示任务需求和工人兴趣
 ### Anonymous Privacy-Preserving Task Matching in Crowdsourcing 2018
 SSE 代理加密，提供用户匿名性且可实现追踪和撤销
 ### Privacy-Preserving Task Matching with Threshold Similarity Search via Vehicular Crowdsourcing 2021
 SSE proxy re-encryption. 先基于关键字检索，然后根据位置筛选， 同时保护了关键字和位置
 ### PPTA: Privacy-Preserving Task Assignment Based on Inner-Product Functional Encryption in SAM 2023 Xu
 同时保护关键字和位置
 ### PPTA: A location privacy-preserving and flexible task assignment service for spatial crowdsourcing 2023 Zhou
 仅位置，使用两方的加法秘密共享,将工人位置和任务位置分别分割成两个秘密共享出去，但是安全性较弱，要求两个crowdsourcing server provider不合谋


# Blockchain-based Crowdsourcing

 ### Differentially Private Crowdsourcing With the Public and Private Blockchain
 identity and location 


[^1]: Shu, Jiangang, et al. "Proxy-free privacy-preserving task matching with efficient revocation in crowdsourcing." IEEE Transactions on Dependable and Secure Computing 18.1 (2018): 117-130.