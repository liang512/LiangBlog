---
title: "Revocation"
date: 2025-01-23T22:51:58+08:00
draft: false
---

# 灵活撤销
1. Direct revocation
The DO encrypts files with a separate revocation list (as a policy), preventing revoked users from decrypting the ciphertext while non-revoked DUs remain unaffected. However, all DOs must maintain an ever-growing revocation list, increasing ciphertext size over time.

Limitations: 
- Ciphertext size is linearly increasing with the number of revoked users.
- Users are represented with a unique ID. No anonymous.

2. Indirect revocation
A timestamp is embedded in the ciphertext, and the KGC periodically updates the private keys of non-revoked DUs. Revoked DUs cannot obtain valid key updates to decrypt future ciphertexts.


Q: The revoked users can decrypt past ciphertexts they were originally allowed to.

- 系统周期性地维护密钥
- 密钥使用次数
**Ciphertext delegation:** The storage server to periodically update the timestamps in all ciphertexts. (Dynamic credentials and ciphertext delegation for attribute-based encryption, CRYPTO 2012)

Limitations:
- all non-revoked users periodically update their keys;
- The storage server needs to periodically perform (unscalable) ciphertext delegation to prevent revoked users from decrypting past ciphertexts.


**另一种分类**
# Attribute revocation

## Attribute-based fine-grained access control with efficient revocation in cloud storage systems
Kan Yang, Xiaohua Jia, Kui Ren, ASIACCS '13

每个属性对应一个版本号，当一个用户的属性A被撤销时，更新系统中属性A的版本号。随后更新未被撤销的用户的密钥里与**属性A相关的组件**（Authority），以及系统中密文里和**属性A相关的组件**（更新密文在CS）。

    密钥密文都要更新

## New Ciphertext-Policy Attribute-Based Encryption with Efficient Revocation
Longhui Zu, Zhenhua Liu, Juanjuan Li,  IEEE International Conference on Computer and Information Technology'14

将CP-ABE的主密钥分为$\alpha=\alpha_1+\alpha_2$，$\alpha_1$用于生产用户属性私钥，$\alpha_2$用于生成CS的私钥。CS根据用户的属性对用户请求的密文执行Transform，如果有撤销的属性，则对密文使用$v_{x_i}$重随机；如果撤销之后的用户属性仍然满足访问策略，那么将$v_{x_i}$发送给用户协助解密。

    密文更新（转换）

## Efficient Decentralized Attribute-based Access Control for Cloud Storage with User Revocation

Jianwei Chen and Huadong Ma, ICC'14

属性撤销时authority对该属性对应的pk生成更新密钥，发送给未被撤销的用户。DO重新加密密文。

    密文密钥都更新

## Blockchain Based Multi-Authority Fine-Grained Access Control System With Flexible Revocation

Meiyan Xiao , Qiong Huang , Member, IEEE, Ying Miao, Shunpeng Li, and Willy Susilo , Fellow, IEEE, IEEE TRANSACTIONS ON SERVICES COMPUTING'22

authority的公钥中有和用户ID相关的信息，DO加密使用该公钥。撤销时，对应的Authority重新生成自己的公钥，随后DO重新加密，则被撤销的用户无法解密。每个authority管理一组属性，所以当一个authority撤销用户时，相当于撤销用户的相关属性。

# User revocation

## HASBE: A Hierarchical Attribute-Based Solution for Flexible and Scalable Access Control in Cloud Computing
Zhiguo Wan, Jun’e Liu, and Robert H. Deng, TIFS'2012

在密文和密钥中添加expiration time，如果密钥中的expiration time大于密文中的expiration time，可以解密。数字比较实用“bag of bits”，即将数字转为二进制，构建访问树。更新用户密钥只更新expiration time相关的组件

    用户密钥没有被删除；authority每次执行密钥更新；需要安全信道

## EASiER: Encryption-based Access Control in Social Networks with Efficient Revocation
Sonia Jahid, Prateek Mittal, Nikita Borisov, ASIACCS '11

引入一个trusted proxy在做密文转换时实现撤销，撤销使用“Efficient trace and revoke schemes”中的方法。不需要更新用户密钥，不需要更新密文。
![NP's revocation](../image.png)

    只支持有限个用户，系统设置好的t个用户。trusted proxy

## Optimized Ciphertext-Policy Attribute-Based Encryption with Efficient Revocation
Yang Li, Jianming Zhu, Xiuli Wang, Yanmei Chai and Shuai Shao, International Journal of Security and Its Applications'13

维护一个撤销后的用户ID集合，加密密文时嵌入到访问策略，用户密钥中有和ID相关的组件，如果已被撤销，则无法解密

## Dynamic User Revocation and Key Refreshing for Attribute-Based Encryption in Cloud Storage
Zhiqian Xu, Keith M. Martin, International Conference on Trust, Security and Privacy in Computing and Communications'12

将CP-ABE的主密钥分为$\alpha=\alpha_1+\alpha_2$，$\alpha_1$用于生产用户属性私钥，$\alpha_2$用于生成CS的私钥，半诚实的CS维护一个撤销列表，当用户请求数据时，检测是否为撤销用户作出相应的Transform实现撤销。

1. Sanitizer 检查密文...可验证（恶意Sanitizer）
2. 可撤销，用户撤销和属性撤销

# 公共可验证外包解密



# 考虑更多sender恶意的情况？