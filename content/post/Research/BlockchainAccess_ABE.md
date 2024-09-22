---
title: "Blockchain-based access control"
date: 2024-09-22T18:54:01+08:00
draft: false
author: "LiangLi"
---

# Blockchain Based Multi-Authority Fine-Grained Access Control System With Flexible Revocation
> Meiyan Xiao , Qiong Huang , Member, IEEE, Ying Miao, Shunpeng Li, and Willy Susilo , Fellow, IEEE;
> IEEE TRANSACTIONS ON SERVICES COMPUTING'22

**Summary:** This paper first proposed a KP-ABE scheme with Multiple Authorities and Flexible Revocation called **MAFR-KP-ABE**. After that, the authors combine **MAFR-KP-ABE** and blockchain to achieve paid data sharing access control.
Technique:
- System model: **Hybrid storage**
- Access control: KP-ABE; DU paid the fee to DO on Ethereum to achieve access permission
- Threat model: 
- Privacy:
  - :white_check_mark: 
  - :x: attributes set
- DO encrypts data using a symmetric encryption algorithm and further encrypts the symmetric key with ABE algorithm. DO uploads data ciphertext and key ciphertext to **CSP**, and then uploads data sharing information on **Ethereum** (attributes set, hash value of the shared data, location of the shared data in CSP and information about fees).
- DU pays DO on Ethereum based on data sharing information. Then, DU request decryption keys from Attribute Authorities (AAs). Each AA verifies the payment transaction and sends the decryption key to the DU.
- DU searches the data according to data sharing information. Anyone can request ciphertext from CSP.
 

