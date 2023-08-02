
# 1
Hi, everyone. I'm Li Liang. My research interests include attribute-based encryption, blockchain-based application, and crowdsourcing. This morning I'd like to talk to you about privacy-preserving task matching in crowdsourcing. My talk's title is Bilateral Secure and Decentralized Crowdsourcing Task Matching Atop Consortium Blockchain. 

# 2. What is Crowdsourcing?
First of all, we review what is crowdsourcing. Crowdsourcing relies on hundreds and thousands of people working in parallel time, collaboratively, to go solve complex problems. Crowdsourcing burst into the scene in the early 2000s. Overall, crowdsourcing is seeking knowledge, goods, or services from a large body of people, including professional workers or freelancers. 
> 例子

For example, if there exists a company that wants to collect the weather situation in Shanghai. It can issue the task and recruit people who know the weather in a certain place, and collect the weather in various districts of Shanghai from these people. For example, people A report the weather in Baoshan is rainy. After, the company gets all weather situations from a large body of people.
> 优点

So, crowdsourcing has lower costs, higher speed, and richer creativity compared with traditional outsourcing and business mechanisms. And it is widely employed in our daily life.

# 3. Task Matching in Crowdsourcing
## Introduce crowdsourcing
Basically, crowdsourcing has three entities: the requester is a task owner who publishes tasks to the server for worker recruitment, and the worker is a task executor. 

## Introduce task matching 
Task matching is a key phase in crowdsourcing, which needs to assign tasks to qualified workers according to requester-side task requirements or/and worker-side task preferences. 

In crowdsourcing task matching, besides matching efficiency and flexibility, security and privacy issues are particularly primary concerns of the requester and worker, because these data are sensitive information. These data may be subject to man-in-the-middle attacks and intercepted by malicious parties in the middle. And crowdsourcing platforms are often honest-but-curious, which means the server can honestly perform task matching, but it will attempt to learn all possible information from received messages.

# 4. Existing Solutions—Traditional Crowdsourcing

## Auction
In recent years, a line of works are presented to solve the privacy problem in task matching. The existing privacy-preserving task-matching model mainly contains three types: auction-based, location-based, and keyword-based. In the auction-based model, the requester selects workers according to bids submitted by workers to maximize social welfare or minimize cost.

## Location
In the location-based model, the task is assigned according to the location of requesters and workers, such as selecting workers in a specific range or k nearest workers. 

## Keyword 
In the keyword-based model, task matching is more flexible. Requester uploads the task content with the task keyword, which includes task type, task location, and so on. And then the worker can according to his interest keyword select tasks.

Overall, the above models can achieve task matching, but the application scenarios are different. Auction-based is often used to maximize social welfare, location-based is often used in crowdsensing and keyword-based model is more flexible.

## Privacy protection method
For privacy, commonly used privacy protection methods are as follows: we can utilize commitment, hash function, or encryption algorithm to protect bids. Differential privacy is often used to protect location information. Searchable encryption is used to achieve privacy-preserving keyword-based task matching.

# 5. Existing Solutions—based on Blockchain
## Why blockchain?
### Drawbacks of previous works
These previous works were limited to the honest-but-curious adversary model. Furthermore, centralized crowdsourcing suffers from the notorious single-point-of-failure issue, collusion with users. And it may lead to unreliable matching and insufficient privacy protection issues. 

### Blockchain
Therefore, to solve these problems, blockchain-based crowdsourcing systems were proposed. Researchers use the properties of blockchain to build a decentralized crowdsourcing system.

## How to combine blockchain and crowdsourcing?

And, it is easy to combine blockchain and crowdsourcing, we just replace the centralized server with smart contracts to achieve reliable task matching. Right, it sounds simple. However, this will bring new privacy protection challenges due to the transparency of smart contracts. 
<!-- 用加密技术，但是效率，链上开销 -->

# 6. Limitations of the Existing Solutions
Furthermore, the existing solutions have the following limitations: The matching model is oversimplified, which means most schemes are based on coarse-grained location or keyword and only consider one-party requirements and privacy. Additionally, although some schemes use the blockchain to replace the centralized server, these schemes are not really decentralized because there still exists a trusted entity for distributing user keys. Finally, the on-chain operation suffers from high overhead. 

Therefore, a decentralized crowdsourcing with dual-side privacy-preserving and flexible task matching is required.

# 7. Motivations
So, the motivations are obvious. We aim to build a decentralized crowdsourcing system with no central trust and dual-side privacy-preserving task matching, the privacy of requesters and workers are both protected. And the task matching should be flexible, which means requesters can select workers based on fine-grained task requirements and workers can retrieve tasks based on interest keywords. Finally, the matching should be trusted, matching operations should be performed reliably.

# 8. ABE
Next, I will introduce the ABE. ABE is a generalization of traditional public-key encryption that offers fine-grained access control over encrypted data, which enables the ciphertext associated with access policy and user attribute key associated with an attribute set. If and only if the attribute set satisfies the access policy, the decryption can be successfully performed.

For example, the encryptor can specify an access policy A and B to cipher. And then if the decryptor's attribute set is AB, then he can decrypt the cipher. Certainly, the attribute set AC cannot decrypt the cipher.

# 9. Design Rationale of Our Scheme
This leads directly to the high-level design rationale of our scheme. In our scheme, the requester uploads the task ciphertext associated with task requirements denoted by vector $x$ to the blockchain, and the worker first retrieves the attribute key for attribute vector $v$ from the authority. Then, the worker can generate a search token associated with his interest keyword by running the $TokGen$ algorithm. The pre-defined smart contract then performs the $Search$ algorithm to achieve task matching if and only if the inner product of vectors $v$ and $x$ is $0$ and the task keyword and worker interest keyword are same. Finally, the worker retrieves task cipher from the blockchain and derives task content. 

# 10. Technique Overview
Now I'd like to move on to the technique overview. Note that TABE doesn't have a keyword search algorithm, so we discover $TokenGen$ algorithm and $Search$ algorithm to enable keyword search based on DIPE. 

And then utilize the Viete formulas to generate policy and attribute vectors to reduce the ciphertext and key size. 

Finally, due to the attribute vector computed on the worker himself, we design 𝑃𝑟𝑜𝑜𝑓𝐺𝑒𝑛 algorithm and 𝑃𝑟𝑜𝑜𝑓𝑉𝑒𝑟𝑖𝑓𝑦 algorithm based on Pedersen Commitment to resist malicious workers submitting incorrect attribute vector.

# 11. Vector Generation

Now, I will explain the vector generation method based on the Viete formulas. 

First, we use the AND-Gate access structure with wildcard. In the access structure, each attribute has multiple possible values, the notation '+' denotes this value is positive, '-' denotes the opposite, and '*' denotes the don't care attribute. For example, in this table, Alice is a teacher in the CS department of University A, and Alice satisfies access structure W2 rather than W1. 

And the policy vector generation method is as follows:
we denote the policy vector $x$ equals ... where Gamma and x are computed as these formulas. And the attribute vector $v$ is computed as the formulas. 

# 12. Vector Generation—Example
For easy understanding, we give a vector generation example. The positive attribute value set J equals 1,4,6 and we set N equals 2. Then we compute $v$ in this way. V zero equals 1 to zero... Then the vector $v$ equals (3,11,53,-1). 

For access policy $W_2$ the positive attribute value set is Q and the wildcard attribute value set is P. Then we compute the vector x zero to x two and Gamma in this way. 

Finally, it is easy to check the inner product of v and x is zero.

# 13. Pedersen Commitment
Next, we introduce a cryptographic commitment Pedersen Commitment, that allows one to generate a commitment to a message m without revealing m. At a later time, the commitment is opened by the sender to convince a receiver that the message is indeed m. 

The Pedersen Commitment has three algorithms: setup, commit and verify. 

The setup algorithm generates two generators of a group G. 

The commitment algorithm takes as input a message m and a random element in $\mathbb{Z}_p$ and outputs a commitment value $com=...$. 

The verify algorithm takes as input a commitment com, a message m, and a element r. This algorithm outputs 1 if com equals g to m times h to r, otherwise, outputs 0.




