---
title: "SomeIdeas"
date: 2023-05-21T14:50:15+08:00
draft: true
author: "Liang"
---

<!-- # Two-Client Inner-Product Functional Encryption with an Application to Money-Laundering Detection
    we can treat the position vector of the worker as x and the position vector of the requester as y. -->

# Our Scheme

- In our scheme, when the attributes of the user change, he does not need to re-request attribute secret keys for each authority by using a secret sharing scheme. While DIPE scheme needs to generate N new secret key when the user's attribute changes.
- 对必需属性进行确定性的属性加密检测后，对可选属性集采用相似度匹配

# Multi-keyword Search

参考 “Privacy-Preserving Task Recommendation Services for Crowdsourcing” 中 Matrix-based 


# Public Verifiability
Search 算法在不可信服务器上执行
  ## 关键字
  问题：服务器为了节省算力等，返回不完全的匹配（直接返回空）结果或者错误的匹配结果。
  
  目标：各方可验证结果中的密文和陷门中的关键字，Requester 需要验证Worker搜索陷门中包含特定关键字，Worker 需要验证任务中包含特定关键字

  思路：Bloom Filter -> Cuckoo Filter, Hash

  ## 密文 (Integrity)
  问题：由于硬件或软件故障导致密文错误，中间人修改，服务器修改密文。

  目标： Worker 需要验证密文没有被篡改。
  
  思路：Signature, MAC

  ## Woker合法性
  问题：Worker解密收到的任务密文后，因为某些原因想拒绝任务，Worker对外宣称自己无法解密该密文来拒绝服务。此时Worker已查看任务内容，泄漏了Requester隐私信息。

  目标：验证Worker的属性密钥可以解密对应的密文，即Worker的属性向量和任务向量正交。
  
  思路：对用户向量和任务向量做一个加密处理或者编码，使其处理之后不会泄漏信息且内积仍为0（将向量放到指数）；或把匹配过程计算的中间值公开

# Registered ABE in data sharing scenario

# Access control encryption + FAME + hidden policy
动机：医生通过公共云存储将文件分享给商人，将加密文件的访问策略析取商人。