---
title: "Blockchain-based access control"
date: 2024-09-22T18:54:01+08:00
draft: false
author: "LiangLi"
---

<!-- 总表 -->
# Summary Table
> **HS**: Hybrid Storage, **OD**: Outsourced Decryption, **PP**: Privacy of Policy, 
> **PA**: Privacy of Attributes, **VDI**: Verification of Data Integrity, **VAP**: Verification of Access Permission,
> **PV**: Public verification, **SA**: Sanitization, **RE**: Revocation, **KS**: Keyword Search
---
| | HS | OD | PP | PA | VDI | VAP | PV | SA | RE | KS |
| :---: | :----: | :---: | :----: | :---: | :---: | :----: | :---: | :----: | :---: | :---: |
| [Xiao2022](#Xiao2022) | :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :white_check_mark: | VAP | :x: | :white_check_mark: | :x: |
| [Zhang2022](#Zhang2022) | :white_check_mark: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | VAP | :x: | :x: | :x: |
| [Guo2023](#Guo2023) | :white_check_mark: | :white_check_mark: | :x: | :x:| :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :x: |
| [Li2024](#Li2024) | :x:(without CS) | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | All | :x: | :x: | :white_check_mark: |
| [Jiang2024](#Jiang2024) | :white_check_mark: | :x: | :x: | :x: | :x: | :x: | :x: | :white_check_mark: | :x: | :x: |
| [He2022](#He2022) | :white_check_mark: | :x: | :x: | :x: | :x: | :x: | :x: | :x: | :x: | :x: |
| [Yan2023](#Yan2023) | :x: | :white_check_mark: | :white_check_mark: | :question: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: |
| [Zhao2023](#Zhao2023) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :x: | :x: | :x: | :x: | :x: |

# <span id="Xiao2022">Blockchain Based Multi-Authority Fine-Grained Access Control System With Flexible Revocation</span>
> Meiyan Xiao , Qiong Huang , Member, IEEE, Ying Miao, Shunpeng Li, and Willy Susilo , Fellow, IEEE;
> IEEE TRANSACTIONS ON SERVICES COMPUTING (TSC **CCF A**) 2022

**Summary:** This paper first proposed a KP-ABE scheme with Multiple Authorities and Flexible Revocation called **MAFR-KP-ABE**. After that, the authors combine **MAFR-KP-ABE** and blockchain to achieve paid data sharing access control.

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
 

# <span id="Zhang2022">An Expressive Fully Policy-Hidden Ciphertext Policy Attribute-Based Encryption Scheme With Credible Verification Based on Blockchain </span>
> Zhaoqian Zhang , Jianbiao Zhang , Member, IEEE, Yilin Yuan , and Zheng Li
> IOT J, 2022
**Summary:** The signature of data hash value stored on the blockchain. The smart contract process the preverification to verify the access right.


# <span id="Guo2023">Accountable Attribute-Based Data-Sharing Scheme Based on Blockchain for Vehicular Ad Hoc Network</span>
> Zhenzhen Guo , Gaoli Wang , Yingxin Li , Jianqiang Ni, Runmeng Du, and Miao Wang
> IOT J, 2023

**Summary:** The authors mainly solved the key abuse problem. 1) **Consortium blockchain** maintained by AAs is deployed. The key distribution operation is recorded on the blockchain for verification. 2) They also designed CP-ABE scheme with white-box traceability and efficient user revocation to avoid user key abuse.
> Access control is executed by **semi-honest RSU**. RSUs hold user-specific keys for partial decryption. DU direcyly request data from RSU. Then, RSU executes the partial decryption on ciphertext and sends the results to DU. 

User-uploaded data can be stored in IPFS.

# <span id="Li2024">Flexible and secure access control for EHR sharing based on blockchain</span>
> Peng Li, Dehua Zhou, Haobin Ma, Junzuo Lai
> Journal of Systems Architecture, 2024

**Summary:** The authors proposed a policy hiding ABKS scheme with online/offline encryption. The $\textsf{Search}$ algorithm performed on the blockchain, so the public verification of access control is achieved.


# <span id="Jiang2024">SanIdea: Exploiting Secure Blockchain-Based Access Control via Sanitizable Encryption</span>
> Peng Jiang , Member, IEEE, Qi Liu, and Liehuang Zhu , Senior Member, IEEE

> IEEE TIFS'2024

**Summary:** The authors proposed a sanitizable multi-authority attribute-based encryption scheme (sMABE). Then they proposed SanIdea by integrating the blockchain with SMABE to ensure the correctness of the secret key parts. 

Question:question:
- The authorities store master secret keys on the blockchain. 
- The sanitication only contains randomness process.

# <span id="He2022">An Efficient Ciphertext-Policy Attribute-Based Encryption Scheme Supporting Collaborative Decryption With Blockchain</span>
> Ying He, Haiyan Wang, Yuan Li, Ke Huang, Victor C. M. Leung, Life Fellow, IEEE, F. Richard Yu, Fellow, IEEE, and Zhong Ming, IOT J, 2022

For any user group, when the user’s attribute set cannot access the ciphertext alone, the private key of other users in the same group can be used for collaborative decryption with the permission of the data owner. 

Private blockchain is responsible for collaborative decryption information transmission (ciphertext) between users.


# <span id="Yan2023">Access control scheme based on blockchain and attribute-based searchable encryption in cloud environment</span>
> Liang Yan, Lina Ge, Zhe Wang, Guifen Zhang, Jingya Xu & Zheng Hu, Journal of Cloud Computing: Advances, Systems and Applications 2023

Hidden policy ABKS with attribute revocation and blockchain are employed to achieve a distributed fine-grained access control scheme. Data symmetric ciphertexts are stored on IPFS and ABE ciphertexts are stored on the blockchain. Smart contracts execute search algorithm.

Privacy of user attributes :question: DO generates attribute key 

# <span id="Zhao2023">ERSChain: Towards secure and flexible educational resource sharing using consortium blockchain and revocable ciphertext-policy attribute-based encryption</span>
> Gang Zhao, Hui He, Bingbing Di, Tong Wu
> Concurrency and Computation: Practice and Experience 2023 (CCF C)

This paper proposed revocable CP-ABE with outsourced decryption for educational resource sharing to relize fine-grained access control. The encrypted data stored on off-chain server. On the blockchain, the hash value for sharing data are recorded. 
