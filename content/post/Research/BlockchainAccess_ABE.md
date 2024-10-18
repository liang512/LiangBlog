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
> **VT**: Verification of Transformation by CS
---
| | Paper | HS | OD | PP | PA | VDI | VAP | PV | SA | RE | KS |
|:-:| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|1| [Xiao2022](#Xiao2022) | :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :white_check_mark: | VAP | :x: | :white_check_mark: | :x: |
|2| [Zhang2022](#Zhang2022) | :white_check_mark: | :x: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | VAP | :x: | :x: | :x: |
|3| [Guo2023](#Guo2023) | :white_check_mark: | :white_check_mark: | :x: | :x:| :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :x: |
|4| [Li2024](#Li2024) | :x:(without CS) | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | both | :x: | :x: | :white_check_mark: |
|5| [Jiang2024](#Jiang2024) | :white_check_mark: | :x: | :x: | :x: | :x: | :x: | :x: | :white_check_mark: | :x: | :x: |
|6| [He2022](#He2022) | :white_check_mark: | :x: | :x: | :x: | :x: | :x: | :x: | :x: | :x: | :x: |
|7| [Yan2023](#Yan2023) | :x: | :white_check_mark: | :white_check_mark: | :question: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: |
|8| [Zhao2023](#Zhao2023) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :x: | :x: | :x: | :x: | :x: |
|9| [Fan2020](#Fan2020) | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :white_check_mark: | :x: | :x: | :x: | :x: | :x: |
|10| [Cui2020](#Cui2020) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :white_check_mark: | both | :x: | :x: | :x: |
|11| [Yang2023](#Yang2023) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :x: |
|12| [Gan2023](#Gan2023) | :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :x: | :x: | :x: | :x: | :x: |
|13| [Hou2024](#Hou2024) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :white_check_mark: | both | :x: | :x: | :x: |
|14| [Jiang2022](#Jiang2022) | :white_check_mark: | :white_check_mark: | :x: | :x: | :white_check_mark: | :x: | :x: | :x: | :white_check_mark: | :x: |
|14| [Guo2023](#Guo2023) | :white_check_mark: | :white_check_mark: | :x: | :x: | :x: | :x: | :x: | :x: | :white_check_mark: | :x: |



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

# <span id="Fan2020">A Secure and Verifiable Data Sharing Scheme Based on Blockchain in Vehicular Social Networks</span>
> Kai Fan , Member, IEEE, Qiang Pan , Kuan Zhang , Member, IEEE, Yuhan Bai, Shili Sun , Hui Li , Member, IEEE, and Yintang Yang , Member, IEEE,
> IEEE TRANSACTIONS ON VEHICULAR TECHNOLOGY, 2020

This paper stores the access policy and hash value of data on the blockchain so that the data user can perform self-certification. The data user retrieves the access policy from the blockchain to check whether their attributes satisfy the access policy. If the check passes, they request the data from the CS. Moreover, the authors design a policy-hiding scheme. However, the policy-hiding scheme does not resist attribute guessing attacks.

# <span id="Cui2020"> Pay as You Decrypt: Decryption Outsourcing for Functional Encryption Using Blockchain </span>
> Hui Cui , Zhiguo Wan , Xinlei Wei, Surya Nepal ,and Xun Yi
> TIFS'2020

This paper proposed a functional encryption scheme with payable outsourced decryption, which allows anybody to check the correctness of the answer for the outsourcing computation task provided by an untrusted third party. The verification algorithm is executed by the smart contract. However, the verification algorithm needs to re-execute decrypt algorithm. This doesn't make sense

# <span id="Yang2023"> Blockchain-based multi-authority revocable data sharing scheme in smart grid </span>
> Xiao-Dong Yang, Ze-Fan Liao, Bin Shu and Ai-Jia Chen
> Mathematical Biosciences and Engineering, 2023

They utilized the multi-authority online/offline ABE with user revocation and blockchain to achieve fine-grained data sharing. The hash value of data is stored on the blockchain for verification of decryption results.

# <span id="Gan2023">Fine-grained Data Rights Governance in Blockchain-based Cloud-edge Communications</span>
> Weilin Gan, Mingyang Zhao, Hongchen Guo, Chuan Zhang, Jianan Hong, and Liehuang Zhu
> IEEE GLOBECOM'23

This paper allows the data user to edit the ciphertext by employing chameleon hashes trapdoors.

# <span id="Hou2024">Blockchain-based efficient verifiable outsourced attribute-based encryption in cloud</span>
> Zesen Hou, Jianting Ning, Xinyi Huang, Shengmin Xu, Leo Yu Zhang
> Computer Standards & Interfaces, 2024

This paper based on ["Pay as You Decrypt"](#Cui2020) and places the generation of the transformation key in KGC, reducing user-side overhead. 

# <span id="Jiang2022">Attribute-Based Encryption With Blockchain Protection Scheme for Electronic Health Records</span>
> Yu Jiang , Xiaolong Xu , and Fu Xiao
> IEEE TRANSACTIONS ON NETWORK AND SERVICE MANAGEMENT, 2022

By storing the uploaded encrypted data in the blockchain in the form of transaction records, the integrity of the data is guaranteed, which facilitates the traceability of EHR generation.
It supports attribute revocation.

# <span id="Guo2023">Revocable Blockchain-Aided Attribute-Based Encryption With Escrow-Free in Cloud Storage</span>
> Yuyan Guo , Zhenhua Lu , Hui Ge , and Jiguo Li
> IEEE TRANSACTIONS ON CLOUD COMPUTING,  2023

This paper proposed a revocable blockchain-aided ABE with escrow-free (BC-ABE-EF) system. The keys are generated between the blockchain and the data
user through a secure key issuing protocol, and the blockchain cannot obtain the user’s full key alone.
