---
title: "Sanitizable Encryption"
date: 2023-07-24T14:58:50+08:00
draft: false
author: "Liang Li"
Description: "记录最近看到的一个新的概念：Sanitizable Encryption"
---


# <cite> Sanitizable Access Control System for Secure Cloud Storage Against Malicious Data Publishers [^Susilo2021]</cite>
[^Susilo2021]: W. Susilo, P. Jiang, J. Lai, F. Guo, G. Yang and R. H. Deng, "Sanitizable Access Control System for Secure Cloud Storage Against Malicious Data Publishers," in IEEE Transactions on Dependable and Secure Computing, vol. 19, no. 3, pp. 2138-2148, 1 May-June 2022, doi: 10.1109/TDSC.2021.3058132.

这篇文章考虑加密者（Data Owner,DO）恶意的情况时，如何保证数据的隐私性。

我们首先要清楚恶意的DO会做什么事情：
1. 嵌入错误的访问策略让无权限的用户解密；
2. 将密钥泄露给无权限的用户；

   ![check](../image.png)
1. 对以上的1，增加一个可信的Sanitizer在密文上执行check操作，检查是否嵌入了正确的访问策略，其实相当于执行了一遍ABE的解密操作，将与访问策略$M$关联的密文组件与**随机选择**的属性集合$S\in M$对应的密钥（这个密钥并不是authority生成，而是sanitizer按照密钥形式仿造的，仅为了验证）配对,通过验证则为正确的密文，此时的密文解密需要恢复出$e(g,g)^{\alpha s}$；
2. 通过上述访问策略验证后，还需考虑DO直接将加密密钥泄露给无权限的用户。可信的sanitizer重新生成一个密文(访问策略秘密值为$s\prime$)，然后将两个密文聚合在一起，此时的密文解密需要恢复出$e(g,g)^{\alpha (s+s')}$；

**问题：**
- 对以上的1，随机选择的属性集合$S$满足访问策略是否可以确定密文就正确：例如DO声称访问策略为M="A"，但是在加密时使用错误的访问策略$M'$="A or B"，在check时随机选择的属性集合为$\{ A \}$，也可以通过验证，但是此时携带有属性B的私钥的用户也可以解密。**并未解决第一个问题**。
- 泄漏访问策略，不具备匿名性

# <cite> Sanitizable Cross-System Authorization for Secure Communication in Intelligent Connected Vehicle [^Zhao2023]</cite>
[^Zhao2023]: Y. Zhao, H. Yu, Y. Liang, H. Jiang, G. Marine and Y. Ren, "Sanitizable Cross-System Authorization for Secure Communication in Intelligent Connected Vehicle," in IEEE Transactions on Vehicular Technology, doi: 10.1109/TVT.2023.3287569.

对IBE的密文，可以解决第一个问题
![check_1](../image-1.png)

# <cite>A Sanitizable Access Control With Policy-Protection for Vehicular Social Networks [^Zhao2023A]</cite>
[^Zhao2023A]: Y. Zhao, H. Yu, Y. Liang, M. Conti, W. Bazzi and Y. Ren, "A Sanitizable Access Control With Policy-Protection for Vehicular Social Networks," in IEEE Transactions on Intelligent Transportation Systems, doi: 10.1109/TITS.2023.3285623.

访问策略是AND-Gate，可以解决第一个问题
![check2](../image-2.png)

# <cite>Verifiable Outsourced Attribute-Based Encryption Scheme for Cloud-Assisted Mobile E-health System [^Miao2023]</cite>
[^Miao2023]: Y. Miao et al., "Verifiable Outsourced Attribute-Based Encryption Scheme for Cloud-Assisted Mobile E-health System," in IEEE Transactions on Dependable and Secure Computing, doi: 10.1109/TDSC.2023.3292129.

将外包加密与这个场景结合，服务器需要将访问策略嵌入密文，sanitizer检测服务器输出的密文是否正确，这个应用场景比上面那个更贴切生活一些。
- check密文时仍然存在和第一篇一样的问题
- 访问策略的泄漏
![MiaoSystem](../image-miao-system.png)

# Secure and Fine-Grained Flow Control for Subscription-Based Data Services
Access control encryption based on KP-ABE.
- 泄漏属性集合

# Fine-Grained and Sanitizable Access Control Service for IoT-Based Digital Subscriptions
- 泄漏访问策略

# Bilateral Control for Secure Communication against Replay Attack in ORAN-based Vehicular Networks
checking 公式有错误？

# Attribute-Based Bilateral Access Control with Sanitization and Trust Management for IIoT
针对MABE
Sanitizer不检查密文中的访问策略是否正确，加入了trust management，维护DO的trust value，但DO的trust value小于一个阈值时，Sanitizer将不广播该密文。

# Purified Authorization Service With Encrypted Message Moderation

** The sanitization operation based on a fixed computation method is indeed a re-randomization over the ciphertext. **

本文不针对ABE或者IBE，sanitizable public key encryption

Check算法检测密文是否超过了过期时间：密文中有一个时间戳，加密时生成签名，check算法先验证签名，再获取当前时间戳，检测时间是否超过了expiry



# Conclusion 

- Check的本质思想就是执行了一遍解密操作，并未将消息解密出来
- Sanitizing的关键思想就是给密文重新绑定另一个密文，另一个密文组件一定是可信生成的
- 基于ABE的都需要将密文的访问策略（CP-ABE）或者属性集合（KP-ABE）发送给sanitizer，直接导致隐私泄漏

# Reference
