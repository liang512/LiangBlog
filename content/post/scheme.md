---
title: "Scheme"
date: 2023-07-22T13:21:49+08:00
draft: true
---

# Paper
- Provably Secure Ciphertext Policy ABE

    AND-Gate; CCA security
- Multi-authority Attribute-Based Encryption
- Verifiable Outsourced Attribute-Based Encryption Scheme for Cloud-Assisted Mobile E-health System

# 1
- Attribute vector $v$ -> $g^v$
- Policy vector $x$ -> $rx$, where $r\leftarrow Z_p$
- Verify $g^{v\cdot rx}=g^0$


# Scheme
1. Requester： 
2. Worker：可能恶意，拒绝任务（谎称无法解密; keyword; collude）
   
3. Server：为了节省算力返回错误的匹配结果;篡改密文
   
    public verifiable outsourced ABE: Worker 拒绝任务后可通过proof验证 Server进行了正确匹配；

