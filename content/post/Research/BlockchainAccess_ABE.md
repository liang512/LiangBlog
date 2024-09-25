---
title: "Blockchain-based access control"
date: 2024-09-22T18:54:01+08:00
draft: false
author: "LiangLi"
---

# Blockchain Based Multi-Authority Fine-Grained Access Control System With Flexible Revocation
> Meiyan Xiao , Qiong Huang , Member, IEEE, Ying Miao, Shunpeng Li, and Willy Susilo , Fellow, IEEE;
> IEEE TRANSACTIONS ON SERVICES COMPUTING (TSC **CCF A**) 2022

**Summary:** This paper first proposed a KP-ABE scheme with Multiple Authorities and Flexible Revocation called **MAFR-KP-ABE**. After that, the authors combine **MAFR-KP-ABE** and blockchain to achieve paid data sharing access control.
|   |   |
| :---: | :----: | :---: |
| User revocation :white_check_mark: | Multi-authority :white_check_mark: | Verification of data integrity (hash value) :white_check_mark: |
| Privacy of attributes set in ciphertext :x: | Outsourced decryption :x: |

- System model: **Hybrid storage**
- Access control: KP-ABE; DU paid the fee to DO on Ethereum to achieve access permission
<!-- - Threat model:  -->
  <!-- - :white_check_mark: user revocation; multi-authority; Verification of data integrity (check if the hash value of the decrypted data is the same as the hash value recorded on the blockchain); 
  - :x: privacy of attributes set in ciphertext; outsourced decryption;  -->

- DO encrypts data using a symmetric encryption algorithm and further encrypts the symmetric key with ABE algorithm. DO uploads data ciphertext and key ciphertext to **CSP**, and then uploads data sharing information on **Ethereum** (attributes set, hash value of the shared data, location of the shared data in CSP and information about fees).
- DU pays DO on Ethereum based on data sharing information. Then, DU request decryption keys from Attribute Authorities (AAs). Each AA verifies the payment transaction and sends the decryption key to the DU.
- DU searches the data according to data sharing information. Anyone can request ciphertext from CSP.
- Question:question:
  - The ciphertexts must be re-encrypt after user revocation.
  - Algorithm $\textbf{KeyGen}$ seems modify the public key of the authority. So do they need to re-encrypt the ciphertext every time they run $\textbf{KeyGen}$?
 
# A Hybrid Blockchain-Edge Architecture for Electronic Health Record Management with Attribute-based Cryptographic Mechanisms
> Hao Guo, Member, IEEE, Wanxin Li*, Member, IEEE, Mark Nejad, Member, IEEE, and Chien-Chung Shen, Member, IEEE
> IEEE TRANSACTIONS ON NETWORK AND SERVICE MANAGEMENT 2022

|   |   |
| :---: | :----: | :---: |
| Hybrid storage :white_check_mark: | multi-authority :white_check_mark: | Verification of access  :white_check_mark: |
| access policy :x: | outsourced decryption :x: |

# An Expressive Fully Policy-Hidden Ciphertext Policy Attribute-Based Encryption Scheme With Credible Verification Based on Blockchain
> Zhaoqian Zhang , Jianbiao Zhang , Member, IEEE, Yilin Yuan , and Zheng Li
> IOT J, 2022

|   |   |
| :---: | :----: | :---: |
| Hybrid storage :white_check_mark: | policy hidden :white_check_mark: | Verification of access on blockchain :white_check_mark: |
| verification of correctness of decryption (hash) :white_check_mark: | outsourced decryption :x: |

# Accountable Attribute-Based Data-Sharing Scheme Based on Blockchain for Vehicular Ad Hoc Network
> Zhenzhen Guo , Gaoli Wang , Yingxin Li , Jianqiang Ni, Runmeng Du, and Miao Wang
> IOT J, 2023

**Summary:** The authors mainly solved the key abuse problem. 1) **Consortium blockchain** maintained by AAs is deployed. The key distribution operation is recorded on the blockchain for verification. 2) They also designed CP-ABE scheme with white-box traceability and efficient user revocation to avoid user key abuse.
> Access control is executed by **semi-honest RSU**. RSUs hold user-specific keys for partial decryption. DU direcyly request data from RSU. Then, RSU executes the partial decryption on ciphertext and sends the results to DU. 

User-uploaded data can be stored in IPFS.

|   |   |
| :---: | :----: | :---: |
| Hybrid storage :white_check_mark: | Privacy of access policy :x: | Privacy of user attributes :x: |
| Outsourced decryption :white_check_mark: | Private verification of the correctness outsourced decryption  (hash) :white_check_mark: | user revocation :white_check_mark: | Verification of access control :x: |

# Flexible and secure access control for EHR sharing based on blockchain
> Peng Li, Dehua Zhou, Haobin Ma, Junzuo Lai
> Journal of Systems Architecture

**Summary:** The authors proposed a policy hiding ABKS scheme with online/offline encryption. The $\textsf{Search}$ algorithm performed on the blockchain, so the public verification of access control is achieved.

|   |   |
| :---: | :----: | :---: |
| Hybrid storage :x: | Privacy of access policy :white_check_mark: | Privacy of user attributes :white_check_mark: |
| Outsourced decryption :white_check_mark: | Public verification :white_check_mark: | user revocation :x: |
