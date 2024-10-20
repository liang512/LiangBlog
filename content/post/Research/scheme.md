---
title: "Scheme"
date: 2024-01-24T10:39:25+08:00
draft: false
---

# 1
- Attribute vector $v$ -> $g^v$
- Policy vector $x$ -> $rx$, where $r\leftarrow Z_p$
- Verify $g^{v\cdot rx}=g^0$


# System Model
1. Requester is **semi-honest**, which means that they honestly perform protocol but may attempt to learn the privacy of other users.
2. Worker may claim the honest CS doesn't return correct matching tasks. 
   想要申请自己不满足任务需求的任务，栽赃服务器返回了错误的结果； keyword; collude
   
3. Server：为了节省算力返回错误的匹配结果;篡改密文
   
    public verifiable outsourced ABE: Worker 拒绝任务后可通过proof验证 Server进行了正确匹配；

# Verifiability:
1. 对于Worker是否满足Requester制定的访问策略，可将双方的属性向量（任务访问策略向量）秘密共享or使用同态commitment：
   - 对向量$v=(v_0,v_1,v_2)$: Authority授权密钥时声称向量对应位置的commitment。如$AU_0$计算$Com(v_0)=g^{v_0}h^{r_0}$，最后将$Coms=(Com(v_0), Com(v_1), Com(v_2))$发送到区块链存储。
   - 对向量$x(x_0,x_1,x_2)$: 利用Two-party secret sharing，首先Requester对$x$进行两方的加法秘密共享$x_0 = x_0^1+x_0^2$...
   - 验证：**$Com(v_0,r_0)^{x_0^1}\cdot Com(v_0,r_0)^{x_0^2}=Com(v_0\cdot x_0,r_0\cdot x_0)$** 
     - $\prod \limits_{i=0}^2 Com(v_i x_i)=Com(0)$
     - <font color="red">忽略了随机数r</font> ，$Com(v_0,r_0)^{x_0^1}\cdot Com(v_0,r_0)^{x_0^2}=Com(v_0\cdot x_0,r_0\cdot x_0)$
     - $\prod \limits_{i=0}^2 Com(v_i x_i)=g^{v\cdot x}h^{\sum \limits_{i=0}^n r_i\cdot x_i}=g^0\cdot h^{{\sum \limits_{i=0}^n r_i\cdot x_i}}$ 

2. 对于Worker是否满足Requester制定的访问策略，可将双方的属性向量（任务访问策略向量）秘密共享or使用同态commitment：
   - 对向量$v=(v_0,v_1,v_2)$: Authority授权密钥时声称向量对应位置的commitment。如$AU_0$计算$Com(v_0)=g^{v_0}h^{r_0}$，最后将$Coms=(Com(v_0), Com(v_1), Com(v_2))$发送到区块链存储。
   - 对向量$x(x_0,x_1,x_2)$: 利用Two-party secret sharing，首先Requester对$x$进行两方的加法秘密共享$x_0 = x_0^1+x_0^2$...
   - 验证：**$Com(v_0)^{x_0^1}\cdot Com(v_0)^{x_0^2}=Com(v_0\cdot x_0)$** 
     - $\prod \limits_{i=0}^2 Com(v_i x_i)=Com(0)$
     - <font color="red">忽略了随机数r</font> ，$Com(v_0,r_0)^{x_0^1}\cdot Com(v_0,r_0)^{x_0^2}=Com(v_0\cdot x_0,r_0\cdot x_0)$
     - $\prod \limits_{i=0}^2 Com(v_i x_i)=g^{v\cdot x}h^{\sum \limits_{i=0}^n r_i\cdot x_i}=g^0\cdot h^{{\sum \limits_{i=0}^n r_i\cdot x_i}}$ 

Fog nodes: 
    semi-honest

multi-authority ABE

可验证：
**anyone** can verify matching result whether correct
    
Two parts:
1. Worker是否有权限，Worker的属性是否满足任务需求，即是否满足属性加密谓词。
2. Keyword是否包含在匹配结果中，即Trapdoor是否match密文。
   
**private verification：**
1. Worker自己执行一遍解密，需要配合签名或者哈希判断解密结果是否正确。
2. 如果Match，Worker在本地执行一遍Search算法;  如果返回没有Match的密文😩，Worker对所有密文解密得到对应密文的Bloom filter，然后判断搜索的关键字是否包含在Bloom Filter。
   
**public verification：**
不能公布Bloom filter；验证要是高效的：不能比重新执行一遍Search算法消耗还多；
1. 直接将Search算法中的中间变量公开，Public verifier只需进行乘法；同时验证了Two parts；但是，如果服务器公布错误的值，也会通过verify。存在的问题：服务器可能公布错误的值。。。。加密另一个消息并公布哈希值，然后用$e_1$解密，判断是否相等，以此来验证$e_1$是否正确。

# 20240131
**Bug**：
1. $e(g_1^{\sigma_uA^\top U}, g_2^{y_{u,2}h/\sigma_u})=e(g_1,g_2)^{y_{u,2}hA^\top U}$ 提前将随机数$\sigma$消掉
- The CS checks wether the following equation is holds:
$$e(g_1,g_2)^{y_{u,2}hA^\top U}=e(g_1,g_2)^{(k-y_{u,1})hA^\top U}$$
If the equation holds, then CS can claim $y_u=k$.

2. cs没有返回全部结果

**Solutions**:
1. 扩大$k$的取值范围
   - 使用韦达定理 $k\in\mathbb{Z^+}$
   - 需要用户自己计算属性向量，为了抵御恶意用户申请错误的密钥，改为单机构才可以
   - 用户撤销、外包部分解密
  
2. ...
# 20240729


Search Trapdoor: $\{t_1=\alpha_i^{r}, t_2=\alpha_i^{ry}\}$ ($\alpha_i$ is secret key)

CS performs partial decryption to get $\{C'=Y_w^{sr}, $C''=Y_w^{sry}, C_0=k'\cdot Y_w^s\}$

Worker obtains task encryption key by $\frac{C_0}{C'^{\frac{1}{r}}}=\frac{k'\cdot Y_w^s}{Y_w^s}=k'$.

**Public verifiability for ciphertext outsourcing decryption:**

If the worker denies the output of the outsourced decryption by CS:

1. The worker publishes $y$ to the blockchain for verification.

2. Verifiers check the following situations:
- If $t_1^y=t_2$ and $C'^y=C''$, then CS transforms the ciphertext correctly. 
- If $t_1^y=t_2$ and $C'^y\neq C''$, then CS transforms the ciphertext incorrectly. 
- If $t_1^y\neq t _2$, then the search trapdoor is invalid. 

Security: 
- $t_1$ and $t_2$ do not leak any information about $\alpha_i$.

> **Error**
> 
> If CS directly outputs $C'=e(t_1,g), C''=e(t_2,g)$, then $C'^y=C''$ also holds. **In this case, CS did not transform the ciphertext correctly, but still passed the verification.**

# 20241020
- 让sanitizer去审查DO发送的密文是否正确（密文中的访问策略是否和他声明的一样），需要将访问策略暴露给sanitizer
- 将访问策略以明文的方式输入TEE，之后只输出final ciphertext进行隐藏访问策略，敌手不能将访问策略和final ciphertext联系起来