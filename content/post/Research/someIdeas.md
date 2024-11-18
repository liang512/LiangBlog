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

# Access control encryption（ACE） + FAME + hidden policy
动机：医生通过公共云存储将文件分享给商人，将加密文件的访问策略析取商人。
- Fine-grained control over information flow

## Paper List
### Attribute-Based Access Control Encryption

### A Parallel Secure Flow Control Framework for Private Data Sharing in Mobile Edge Cloud
> IEEE TRANSACTIONS ON PARALLEL AND DISTRIBUTED SYSTEMS, VOL. 33, NO. 12, DECEMBER 2022, Qinlong Huang , Member, IEEE, Lixuan Chen, and Chao Wang
Attribute-based outsourced ACE (AOACE) scheme
- malicious senders in the organization may encrypt the obtained sensitive files and upload them to the cloud server, hence specific receivers can access these files. For example, a research assistant may send the product documents to an intern in the production department. Moreover, the senders may even leak the message keys to unauthorized receivers, which will make some receivers access data without valid decryption keys.

### LMIBE: Lattice-Based Matchmaking Identity-Based Encryption for Internet of Things
> IEEE ACCESS
这篇文章搞错了Sanitizer的作用


# Matchmaking encryption (ME)
## 检测属性策略和关键字策略，相比于ABKS有什么优势？
- ABKS中密文与DO指定的访问策略和密文的关键字相关
- ME中的密文与DO指定的访问策略和DO的属性（DO有一个加密密钥）相关

## ME和Dual-policy ABE (DPABE) 有什么区别？
- DPABE的密钥生成算法需要输入属性和访问策略，即用户的密钥已经和属性与访问策略**同时**绑定
- ME中用户有两个密钥：与属性相关的密钥和，与访问策略相关的密钥。更加灵活。
- A-ME只有一个密钥，但是ME和A-ME可以提供authenticity（对用户DO属性的认证），DPABE不能

## Paper List
### Match in My Way: Fine-Grained Bilateral Access Control for Secure Cloud-Fog Computing
- 与ME最初定义略有不同，本篇在密钥中绑定了策略而不是属性
- This paper proposed a KP-MABE scheme. Ciphertext is associated with the attributes sets of DO ($\sigma$) and DU ($\phi$). The matching algorithm takes input on sender's policy $\mathcal{S}$ and ct to verify. The decryption algorithm takes input on dk associated with receiver's policy $\mathcal{R}$ and ct. The matching is correct iff $\mathcal{S}(\sigma)=1$, and the decryption is successful iff $\mathcal{R}(\phi)=1$.


# 🙋‍♂️是否可以同时利用ME和ACE构造一个访问控制方案 (Attribtue-based Access Control Matchmaking Encryption) AACME
- ME中的DO如果是恶意的，DO给密文绑定一个错误的访问策略...
1. 有人做过吗？
2. 有没有应用场景？是否贴切生活？
3. 

## Privacy-Preserving Bilateral Fine-Grained Access Control for Cloud-Enabled Industrial IoT Healthcare
> IEEE TRANSACTIONS ON INDUSTRIAL INFORMATICS, VOL. 18, NO. 9, SEPTEMBER 2022
基于《Match in My Way》论文，使用MABE进行双向访问控制