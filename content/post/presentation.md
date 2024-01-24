
# 1
Hi, everyone. I'm Li Liang. This morning I'd like to talk to you about privacy-preserving task matching in crowdsourcing. My presentation's title is Bilateral Secure and Decentralized Crowdsourcing Task Matching Atop Consortium Blockchain. 

# 2. What is Crowdsourcing?
First of all, we review what is crowdsourcing. Crowdsourcing relies on hundreds and thousands of people working in parallel time, collaboratively, to go solve complex problems. 

It is seeking knowledge, goods, or services from a large body of people, including professional workers or freelancers. 
> 例子

For example, if there exists a company that wants to collect the weather situation in Shanghai. It can publish the task and recruit people who know the weather in a certain place, and collect the weather in various districts of Shanghai from these people. For example, A reports the weather in Baoshan is rainy. After, the company gets all weather situations from a large body of people.
> 优点

So, crowdsourcing has lower costs, higher speed, and richer creativity compared with traditional outsourcing.

# 3. Task Matching in Crowdsourcing
## Introduce crowdsourcing
Basically, crowdsourcing has three entities: the requester is a task owner who publishes tasks to the server for worker recruitment, and the worker is a task executor. 

## Introduce task matching 
Task matching is a key phase in crowdsourcing, which needs to assign tasks to qualified workers according to requester-side task requirements or/and worker-side task preferences. They may be intercepted by malicious parties. And crowdsourcing platform is often honest-but-curious, which means the server can honestly perform task matching, but it will attempt to learn any information from received messages.

In crowdsourcing task matching, besides matching efficiency and flexibility, security and privacy issues are particularly primary concerns of the requester and worker, because these data are sensitive information. 

# 4. Existing Solutions—Traditional Crowdsourcing

## Auction
In recent years, a line of works are presented to solve the privacy leakage problem in task matching. The existing privacy-preserving task-matching model mainly contains three types: auction-based, location-based, and keyword-based. 

<!-- In the auction-based model, the requester selects workers according to bids submitted by workers to maximize social welfare or minimize cost.

## Location
In the location-based model, the task is assigned according to the location of requesters and workers, such as selecting workers in a specific range or k nearest workers. 

## Keyword 
In the keyword-based model, task matching is more flexible. Requester uploads the task content with the task keyword, which includes task type, task location, and so on. And then the worker can according to his interest keyword select tasks.
 -->


These models are only based on single attribute to achieve task matching, and the application scenarios are different.

Auction-based is often used to maximize social welfare, location-based is often used in crowdsensing and keyword-based model is more flexible.

## Privacy protection method
For privacy, commonly used privacy protection methods are as follows: we can utilize commitment, hash function, or encryption algorithm to protect bids. Differential privacy is often used to protect location information. Searchable encryption is used to achieve privacy-preserving keyword-based task matching.

# 5. Existing Solutions—based on Blockchain
## Why blockchain?
### Drawbacks of previous works
These previous works were limited to the honest-but-curious adversary model. Furthermore, centralized crowdsourcing suffers from the notorious single-point-of-failure and collusion attacks. It may lead to unreliable matching and insufficient privacy protection issues. 

### Blockchain
Therefore, to solve these problems, blockchain-based crowdsourcing systems were proposed. Researchers use the properties of blockchain to build a decentralized crowdsourcing system.

## How to combine blockchain and crowdsourcing?

And, it is easy to combine blockchain and crowdsourcing, we just replace the centralized server with smart contracts to achieve reliable task matching. Right, it sounds simple. However, this will bring new privacy leakage challenges due to the transparency of smart contracts. 
<!-- 用加密技术，但是效率，链上开销 -->

# 6. Limitations of the Existing Solutions
Therefore, the existing solutions have the following limitations: The matching model is oversimplified, which means most schemes are based on coarse-grained location or keyword and only consider one-party requirements and privacy. Additionally, although some schemes use the blockchain to replace the centralized server, these schemes are not really decentralized because there still exists a trusted entity for distributing user keys. Finally, the on-chain operation suffers from high overhead. 

Therefore, a decentralized crowdsourcing with dual-side privacy-preserving and flexible task matching is required.

# 7. Motivations
In more detail, We aim to build a decentralized crowdsourcing system with no central trust and dual-side privacy-preserving task matching, the privacy of requesters and workers are both protected. And the task matching should be flexible, which means requesters can select workers based on fine-grained task requirements and workers can retrieve tasks based on interested keywords. Finally, the matching should be trusted, matching operations should be performed reliably.

# 8. ABE
Traditional public key encryption is one-to-one, a ciphertext can only be decrypted by one private key, but in ABE, a ciphertext can be decrypted by multiple private keys, that is, in the encryption stage of ABE, an access policy can be specified for the ciphertext, anyone who meets the access policy can decrypt it.

For example, the encryptor can specify an access policy A and B to cipher. And then if the decryptor's attribute set is AB, then he can decrypt the cipher. Certainly, the attribute set AC cannot decrypt the cipher.

# 9. Design Rationale of Our Scheme
This leads directly to the high-level design rationale of our scheme. In our scheme, the requester uploads the task ciphertext associated with task requirements denoted by vector $x$ to the blockchain, and the worker first retrieves the attribute key for attribute vector $v$ from the authority. Then, the worker can generate a search token associated with his interested keyword by running the $TokGen$ algorithm. The pre-defined smart contract then performs the $Search$ algorithm to achieve task matching if and only if the inner product of vectors $v$ and $x$ is $0$ and the task keyword and worker interested keyword are the same. Finally, the worker retrieves task cipher from the blockchain and derives task content. 

In this way, sensitive data on the requester side, such as task content and task requirements, are protected by an encryption algorithm, and sensitive data on the worker, such as attributes and keywords, are also protected by a search token algorithm. And flexible task matching can be achieved. The requester can select workers according to task requirements, and workers can filter tasks according to keywords.

Finally, the matching phase is performed on a smart contract, which guarantees our result is reliable.

# 10. Technique Overview
Now I'd like to move on to the technique overview. Note that TABE doesn't have a keyword search algorithm. To enable keyword search, we design $TokenGen$ algorithm and $Search$ algorithm by adding $\beta$-components to ciphertexts and search tokens. 

And then utilize the Viete formulas to generate policy and attribute vectors to reduce the ciphertext and key size. 

Finally, to resist malicious workers submitting incorrect attribute vector, we design 𝑃𝑟𝑜𝑜𝑓𝐺𝑒𝑛 algorithm and 𝑃𝑟𝑜𝑜𝑓𝑉𝑒𝑟𝑖𝑓𝑦 algorithm based on Pedersen Commitment.

# 11. Vector Generation

Now, I will explain the vector generation method based on the Viete formulas. 

We use the AND-Gate access structure with wildcard. In the access structure, each attribute has multiple possible values, the notation '+' denotes this value is positive, '-' denotes the opposite, and '*' denotes the don't care attribute. For example, in this table, Alice is a teacher in the CS department of University A, and Alice satisfies access structure W2 rather than W1. 

And the policy vector generation method is as follows:
we denote the policy vector $x$ equals ... where Gamma and x are computed as these formulas. And the attribute vector $v$ is computed as the formulas. 

# 12. Vector Generation—Example
For easy understanding, we give a vector generation example. The positive attribute value set J equals 1,4,6 and we set N equals 2. Then we compute $v$ in this way. V zero equals 1 to zero... Then the vector $v$ equals (3,11,53,-1). 

For access policy $W_2$, the positive attribute value set is Q and the wildcard attribute value set is P. Then we compute the vector x zero to x two and Gamma in this way. 

Finally, it is easy to check the inner product of v and x is zero.

# 13. Pedersen Commitment
Next, I will introduce a cryptographic commitment Pedersen Commitment, that allows one to generate a commitment to a message m without revealing m. At a later time, the commitment is opened by the sender to convince a receiver that the message is indeed m. 

The Pedersen Commitment has three algorithms: setup, commit and verify. 

The setup algorithm outputs two generators of a group G. 

The commit algorithm takes as input a message m and a random element in $\mathbb{Z}_p$ and outputs a commitment value $com=...$. 

The verify algorithm takes as input a commitment com, a message m, and an element r. This algorithm outputs 1 if com equals g to m times h to r, otherwise, outputs 0.

# 14. Algorithm syntax
Now, we give the algorithm syntax of our scheme. Our scheme is based on DIPE which has five basic algorithms. Setup, Authsetup, keygen, encrypt, and decrypt. 

Setup algorithm outputs public parameters. 

The Authsetup performed by each authority and it outputs a key pair for authority. 

The KeyGen generate a user secret key with public parameter, user global identifier GID, authority secret key ski and vector v.

The encrypt algorithm takes as input public key of all authorities, a vector x, a message m, and keyword w. It outputs cipher ctx. 

The decrypt outputs message m if the inner product of v and x is zero.

Besides, we discover proofGen and ProofVer algorithms to resist malicious user submit incorrect vectors. 

ProofGen takes as input authority index i and worker attribute set D. The authority outputs proof p. 

ProofVer takes as input all proof of authority and v submitted by user. It can verify the v whether correct.

Moreover, the TokenGen algorithm takes as input the user secret key and keyword w' to generate a serach token. And the search algorithm takes as input the tk_v and ct_x, outputs 1 if $x\times v=0$, which means the search is successful.


The latter part will be more technical. I just describe the high-level design.

# 15. System Initialization
Next, I will explain our scheme from the order in which the system runs.

First, in system initialization, the setup and authsetup algorithms are performed. 

Our scheme is based on asymmetric bilinear pairing. This A is k+1 by k matrix and U is k+1 by k+1 matrix. g and h are generated for pedersen commitment. in authsetup algorithm, we add the beta-components to enable later keyword search.

# 16. User registration
Next, the worker computes his attribute vector v and sends it to authority to get secret keys. To verify v, authorities first perform proofGen for this worker. Assume 𝐷 is worker’s attribute value managed by 𝐴𝑈_𝑖. 𝐴𝑈_𝑖 computes commitment for 𝐷 as this formula. After then, the authority can perform proofver algorithm to verify the vector. 

For ease to understand, we can see this example. Alice computes her vector as v. And then authorities compute the commitments of v as the table. For attribute 1, the commitments are in the first row, similarly, for attribute 4, the commitments are in the second row. 

Finally, the authority can check the $v_3$ whether satisfy this equation. we can conclude if the worker correctly computes v, then we have this equation.

# 17. User registration
After verification, the authority generates secret key for vector v. It first computes the mask value \mu. Finally, the secret key as this formula. key_i1 will be used to generate search token.

# 18. Search Token Generation
The worker generates search token tk_v follows this way. The main idea of the algorithm is to add a random value t. 

# 19. Task and keyword cipher uploading
In this phase, hybrid encryption is employed. The requester first selects a random symmetric key sk from G_T. And sk is encrypted by ABE with access policy x. In addition, this cipher also contains keyword associated components: C_1 and C hat. 

# 20. Reliable On-chain Task Matching
After that, smart contract performed task matching, that is search algorithm with tk_v and ct_x.

First, the smart contract computes e_1, this formula is responsible to test if the inner product of v and x equals 0.

After that, if this equation holds, task matching is successful.

we can see the left part and right part of this equation is same iff v times x equals 0 and keyword w equals w'.

At this point, our task matching is completed

# 21. Task Retrieval and Decryption
Finally, the worker retrieves task cipher from blockchain and decrypt it to perform the task.

# 22. Experiment
Next, let me briefly talk about the experimental performance
## Setting 
These are some experiment settings. the task matching is deployed on hyperledger fabric. And we use a test tool called tape simulate transactions.

## 1 off-chain
These graphs show the off-chain performance, in the left figure, we tested the time overhead of each algorithm with different N, that is maximum number of wildcards in access structure. 

KeyGen has the highest overhead. When N=25, the overhead is 900ms, but this is acceptable, because, for each user, KeyGen only needs to run once at registration. 

Additionlly, we compare our scheme with two works as the number of attributes increases. Our scheme shows better performance because its overhead is independent of the number of attributes.

## 2 on-chain
This is on-chain performance, we can see the throughput and latency of the task matching stage from the left figure with different N. 

In addition, there is on-chain performance in the task uploading phase and a comparison with the task matching in reference 6.

# 23. Summary
Well, that concludes my presentation today, to refresh your memory, I'll repeat the main points:

we design a policy-hiding multi-authority searchable ABE. we discover keyword search based on traditional ABE and reduce the size by utilizing viete.

Secondly, we proposed a decentralized crowdsourcing with no central trust and dual-side privacy-preserving and flexible task matching. 

Finally, we also give the security analysis of the scheme in the paper.

# 24. 
Thanks for your attention.  I am happy to answer any questions you might have.






