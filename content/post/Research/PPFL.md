---
title: "Privacy-Preserving Federated Learning"
date: 2024-11-18T18:55:31+08:00
draft: true
Description: "Privacy-preserving federated learning (PPFL)"
---

# PPFL
## Existing PPFL
### Based on differential privacy (DP)
- Low model accuracy
### Based on homomorphic encryption (HE)
- Exchange the secret key between participants. Thus, it requires participants to act honestly
### Based on secret sharing scheme
- Extra communication rounds
### PPFL based on FE
- Enhanced performance with a **single communication round** per training iteration
- 
<!-- | Paper | HS | OD | PP | PA | VDI | VAP | PV | SA | RE | KS |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | -->


---
# HybridAlpha: An Efficient Approach for Privacy-Preserving Federated Learning
> CCS, Workshop on Artificial Intelligence and Security, 2019
> 
Client $u_i$ encrypt the local model parameter $\mathbf{x_i^t}$ in $t$-th round using Multi-input function encryption for inner product (MIFE-IP) and send the ciphertexts to aggregator. Then, the aggregator request the decryption key for weight vector $\mathbf{y}$ from KGC. The aggregator performs $\mathit{Decrypt}$ algorithm to get $<(\mathbf{x_i})_{i\in U}, \mathbf{y}>$ where $U$ is the selected users in this round.

**Mix-and-match attack (MMA)**: The aggregator decrypts $(ct_1^{t}, ct_2^{t})$ to get $\mathbf{z}_1=\mathbf{x}_1^t+\mathbf{x}_2^t$ (assume that $\mathbf{y}=<1>$). Then, in the next round, he decrypts $(ct_1^{t+1}, ct_2^{t})$ to get $\mathbf{z}_2=\mathbf{x}_1^{t+1}+\mathbf{x}_2^t$. Hence, the aggregator can learn the model parameter difference of $u_1$ by $\mathbf{z}_2-\mathbf{z}_1=\mathbf{x}_1^{t+1}-\mathbf{x}_1^t$.

# Privacy-Preserving Federated Learning via Functional Encryption, Revisited
> TIFS'2023
- address MMA from different rounds: binds a mask associated with round number $t$ in ciphertext
- avoid the use of the third trusted KGC in the system: decentralized multi-client functional encryption
- hide all intermediate models from the aggregator

However, this scheme is still vulnerable to MMA from different users in same round. Assume we have $(ct_1^{t}, ct_2^{t}, ct_3^{t})$, we can decrypt partial ciphertexts to get $\mathbf{z}_{12}=\mathbf{x}_1^t + \mathbf{x}_2^t$, $\mathbf{z}_{13}=\mathbf{x}_1^t+\mathbf{x}_3^t$, and $\mathbf{z}_{23}=\mathbf{x}_2^t+\mathbf{x}_3^t$.

# Privacy Preserving Federated Learning from Multi-Input Functional Proxy Re-Encryption
> ICASSP 2024, Peking University

They claim the above paper still suffer from mix-and-match attack.

# An Efficient and Secure Privacy-Preserving Federated Learning via Lattice-Based Functional Encryption
> ICC 2024

They claim this paper resist mix-and-match attack by session key but lack security analysis.

# CryptoFE: Practical and Privacy-Preserving Federated Learning via Functional Encryption

# Decentralized Multi-Client Functional Encryption for Inner Product With Applications to Federated Learning
> TDSC 2024

# The blockchain-based privacy-preserving searchable attribute-based encryption scheme for federated learning model in IoMT
> Concurrency and Computation: Practice and Experience, 2023

When the attributes of participants satisfy the access policy of model, they can get the initial model and then training it. Then, the participants using HE to protect the model parameters.
> The writing is bad.

# VOSA: Verifiable and Oblivious Secure Aggregation for Privacy-Preserving Federated Learning
> TDSC 2023

The malicious aggregator may deviate the protocol or execute different computation to capture private gradients of honest users. Meanwhile, it may modify or forge the aggregated result and proof for deceiving the users to accept a wrong global parameter.

## On the Security of Verifiable and Oblivious Secure Aggregation for Privacy-Preserving Federated Learning
This comment pointed out that VOSA is insecure, in which local gradients/aggregation results and their corresponding authentication tags/proofs can be tampered with without being detected by the verifier. 

