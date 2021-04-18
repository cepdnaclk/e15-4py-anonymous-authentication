---
layout: home
permalink: index.html

# Please update this with your repository name and title
repository-name: eYY-4yp-anonymous-authentication
title: Anonymous and Distributed Authentication for Peer to Peer Networks
---

[comment]: # "This is the standard layout for the project, but you can clean this and use your own template"

# Anonymous and Distributed Authentication for Peer to Peer Networks

#### Team

- E/15/350, Pasan Tennakoon, [email](pasan96tennakoon@gmail.com)
- E/15/180, Supipi Karunathilaka, [email](supipivirajini@gmail.com)

#### Supervisors

- Dr. Janaka Alawathugoda, [email](alawatugoda@eng.pdn.ac.lk)

#### Table of content

1. [Abstract](#abstract)
2. [Related works](#related-works)
3. [Methodology](#methodology)
4. [Experiment Setup and Implementation](#experiment-setup-and-implementation)
5. [Results and Analysis](#results-and-analysis)
6. [Conclusion](#conclusion)
7. [Publications](#publications)
8. [Links](#links)

---

## Abstract

## Introduction

The concept of Peer to peer (P2P) communication has gained significant attention in the network community over the years. Since the release of Napster in 1998 many P2P applications have been introduced. Bitcoin[1], BitTorrent, TOR[2], Freenet[3], etc are some of the more popular P2P applications. The absence of centralized authority is the main reason behind the popularity of P2P applications. This eliminates the need for an expensive central server. Also removes the vulnerability of a single point of failure. P2P networks are considered to be more efficient and scalable than traditional client-server applications. 
The decentralized nature of P2P networks makes it difficult to integrate traditional authentication mechanisms. Due to this many such networks focus on providing user anonymity rather than authentication. The reduced security of these networks has created a lot of possible threats [4]. These threats can vary from uploading malicious files to famous Sybil attacks [5]. Also, the anonymity feature of these networks has created a safe house for cyber criminals [6]. Not being accountable for his/her actions, held responsible and punished for malicious actions, P2P users have the freedom to misbehave. This can cause harm to the network and its users.

We suggest that even in an anonymous network there should be some level of accountability to protect the network and its users. Accountability is achieved through authentication.

To integrate an authentication mechanism into an anonymous P2P environment we need to solve two main challenges.
•Authenticate in a decentralized environment.
•Authenticate without revealing identity. 
These two points have been discussed separately since the start of the internet. Each point has its own difficulties and challenges. Authentication needs to tackle problems like the absence of a central server, certificate management in a distributed environment, the semi-trusted nature of peers, the unpredictable availability of peers, etc. Authentication needs to solve problems like not revealing sensitive information about authenticating party's identity, secure against misbehaving parties (cheating verifiers and cheating provers), unlinkability of authentication sessions, practicality, etc.

In this paper, we propose three new approaches for anonymous authentication in P2Pnetworks to solve the above problems.

1. Ring signature based approach.
2. Authenticated key sharing based approach.
3. Zero knowledge proof based approach.

We deploy these protocol in a P2P environment where certificates are managed by peers with elevated privileges (super peers). To solve the problems of semi-trusted nature and unpredictable availability of peers we utilize Shamir’s secret sharing[7] technique. Amore detailed explanation of these cryptographic primitives is given in section 3. Then we test the performance of these ideas in a practical environment developed using the.Net framework.

## Related works

### 2.1 Authentication in P2P
Absence of a central server makes authentication in peer to peer (P2P) networks complex.
Traditional cryptographic principles like Public Key Infrastructure (PKI) or Identity
based Public Key Certificates (ID-PKC) are based on a trusted third party. Establishing
a trusted third party in a semi-trusted network like P2P is a questionable task. Many
P2P networks propose trust and reputation management schemes to solve this problem.[8]
,[9], [10] use trust and reputation schemes to discover peers that can be considered as
trusted peers of the network. These trusted peers are used in authentication as trusted
third parties.
The idea of reputation management systems is to evaluate a peer’s trustworthiness
based on its interactions with other peers. There exist plenty of research in this area;
EigenTurst [11], NICE[12], Regret [13], PeerTurst[14], FuzzyTrust [15].
P2P systems that use reputation managements schemes to assist in authentication
suffer from an obvious flow. These schemes assume that the reputation system is intelligent
enough not to select malicious users as trusted peers. Trusting malicious peers to protect
sensitive information can harm the system. For example, CST [? ] elect a set of peers as
RPs (Reputed Peers) using EigenTrust. CST creates a pseudo-identity to hide the real
identity of the user. The link between the identity and the pseudo-identity is broken into
parts and stored in randomly selected RPs to protect users’ privacy. CST trusts RPs to
protect the users’ identity. However, EigenTrust is vulnerable to collaborative attacks
and therefore there exist a possibility that malicious peers are elected as RPs. Malicious
RPs can reveal the identity of a user and exploit their privacy.
Some researches suggest using a modified PKI for authentication in P2P networks
[16], [17]. Rather than having a single centralized authority, the responsibility of the
Certificate Authority (CA) is distributed across multiple peers in the network. This
improves the scalability and robustness of the authentication process.
The downside of using PKI in P2P is certificate management becomes complex. The
authentication process becomes difficult to implement effectively. [17] use a set of peers as
Authentication Servers (ASs). Even though this improves the scalability of the network,
introduce new security risks like unreliability in certificate access and verification.
To solve the problem of the absence of a centralized authority and at the same
time keep the authentication process reliable, modern authentication schemes utilize
blockchain technology. There is a lot of literature that proposes the idea of using
blockchain technology to create a Distributed PKI [18], [19], [20], [21]. This seems to be a
good solution to overcome the limitations of having a central trusted certificate authority.
Blockchain can make the process of a CA distributed, immutable and transparent.
Therefore can successfully solve the problems of malicious CAs, MITM attacks and single
point of failure. Blockchain is used as a distributed key-value data storage. The data
is public and readable to everyone.[22] propose the idea of using smart contracts to
certificate management.
The DPKI is only secure as long as honest nodes control collectively more than 51%
of computing power. Also some argues the need of blockchain to decentralized PKI since
the technology of blockchain is still new to the industry.
The PGP Web of Trust [23] is another way to navigate the problem of not having a
trusted central authority. WoT distribute the responsibility of a CA among users. The
core concept of WoT is trust chains. For a simpler explanation, assume A wants to
authenticate himself to B. There is a user C who trusts B. C can sign A’s certificate
after verifying its authenticity. Then A can send the signed certificate to B. Since C
has signed A’s certificate and B trusts C. B can trust A’s certificate is authentic. Using
indirect trust chains WoT creates a community of trusted users. However WoT is not
suitable P2P networks since, it is difficult for a new peer to join the network without
personally knowing a existing user of the network.

### 2.2 Anonymous Authentication in P2P
The concept of anonymous authentication has been around for sometime. Pseudo
Trust[24] has been one of the more popular publications of this topic. Pseudo Trust
(PT) utilize the concept of double pseudonyms combine with zero knowledge proofs to
authenticate users anonymously. PT also uses onion routing[2] and EigenTrust[11] trust
management to provide a complete file delivery system with anonymous authentication.
The anonymity comes from the one way property of the cryptographic hash functions. PT
neglect one important feature of using the concept of pseudonyms to obtain anonymity.
PT does not change PI (pseudo identity) prior to each authentication process. The PT
protocol requires PIC (certificate of pseudo identity) to be send to the other party to
start the authentication. Since PIC is same for a user, an eavesdropper can link two
communication sessions to a specific user.
[25] proposes an similar authentication scheme to PT for Internet of Vehicles (IoV).
The only difference is the slight change of the zero knowledge proof and absence of onion
routing the trust management. This also suffers from the same vulnerabilities as PT.
[10] present an interesting approach to anonymous authentication. PPAA uses tags
to obtain anonymity and at the same time link communication sessions. The idea is
to use IDs of the two parties involved in the communication session create a tag. The
two parties will not learn any knowledge other than the tag from running the protocol.
To avoid having the same tag for different communication sessions between the same
parties PPAA propose to include an event id into the tag design. Therefore only a party
involved in the communication will be able to link a communication session to a previous
session with the same party. The PPAA is secure in random oracle model if eXternal
Diffie-Hellmam (XDH) and q-SDH assumption holds.
CST[9] uses collaboration signature to authenticate users anonymously. As mentioned
in section 2.1 CST uses EigenTrust[11] reputation system to select trusted peers (RPs).
This is not safe in a semi-trusted environment like P2P networks. Other than that CST
is said to be resilient against impersonate attacks, traceability and collaboration attacks.
[26] presents a similar method as CST. They use FBST[27][Fair Blind Signatures] to
present novel authentication scheme that keep the anonymity of honest users. Similar to
CST this uses a trust management system called SOBIE to elect peers as super peers
(SPs) and reputed peers (RPs). They are assumed to be trust worthy and play and
important role in authentication. However, as mentioned previously trust management
systems are not perfect. Malicious peers can get elected as SPs and RPs and they are
able to revoke users’ anonymity. Similar to CST, [26] uses the concept of Shamir’s secret
sharing [7] to reduce the vulnerability of exposed RPs. [7][How to share a secret] present
a way to break a key and store it in multiple places and recreate the key when required.
[26] use this technique to break the key (link between ID and pseudo ID) and store it
among multiple RPs. Therefore even if few RPs got compromise it does not reveal user’s
identity. Also a user use anonymous multicast to communicate with a SP. This makes it
impossible for a SP to reveal an identity of a user.
[28] uses an combination of Merkle’s puzzles[29] and zero knowledge proofs to provide
anonymous authentication.

## Methodology
### 3.1 Cryptographic Primitives
#### 3.1.1 Zero Knowledge Proof

Zero knowledge Proof (ZKP) is a protocol that allows a prover to prove the possession of some secret to a verifier without revealing the secret or any information related to the secret. The first idea of ZKP was introduced by Shafi Goldwasser, Silvio Micali, and Charles Rackoff in [30]. Since then many different ZKPs have been published [31], [32], [33], [34]. ZKPs are widely used in cryptography to implement cryptographic protocols due to its privacy, authentication and low complexity. A zero knowledge proof consists of a prover and verifier. In a zero knowledge protocol, a prover must prove the knowledge of some secret using an interactive challenge-response scheme. The protocol must not reveal any information regarding the secret other than the knowledge of prover has the secret. A secure zkp must satisfy soundness, completeness and zero knowledge properties. There are two types of zero knowledge systems; interactive zero knowledge proofs and non-interactive zero knowledge proofs [35]. Our proposed protocol uses a zkp that utilize quadratic residues in modular arithmetic.

#### 3.1.2 Ring Signatures

The notion of ring signature was first introduced in 2001 by Ron Rivest, Adi Shamir and Yael Tauman Kalai in [36]. Ring signatures are used to digitally sign messages on behalf of a group. At the same time, makes it computationally difficult to find the exact signer. Ring signatures are designed to provide anonymity to the message signer. The same functionality is provided by group signatures [37]. The only difference in group signature is that it needs an authoritative entity to generate the signature. Therefore that entity can revoke the anonymity of the signer. Ring signatures do not depend on a third party to generate a signature. Ring signatures are spontaneous and provide unconditional anonymity. Over the years different ring signature schemes have been published with different features; threshold ring signatures [38], linkable ring signatures[39], revocable ring signatures[40], traceable ring signatures[41]. Consider a scenario where a group of k entities where each entity has a public key P<sub>i</sub> and a corresponding secret key S<sub>i</sub>. An entity r can generate a ring signature on a message m using (m, P<sub>1</sub>, . . . , P<sub>k</sub>, S<sub>r</sub>). Anyone with the knowledge of m, P<sub>1</sub>, . . . , P<sub>k</sub> can verify the ring signature. No one outside the group (without a secret key S<sub>i</sub>) can generate a valid ring signature for the same group.

#### 3.1.3 Shamir’s Secret Sharing

In 1979 Adi Shamir introduced the concept of Shamir’s secret sharing[7][How to Share a Secret]. This allows a secret to be divided into n parts. The secret can be reconstructed with atleast t parts where (1 ≤ t ≤ n). No knowledge about the secret can be learnt with (t-1) parts. The concept is based on polynomial interpolation. The idea is to generate a polynomial f(x) of (t-1) points. First we select (t-1) random positive integers such that (a1, a2, .., at−1). Then set a0 to the secret we want to share. These points are used to generate the polynomial f(x). f(x) = a<sub>0</sub> + a<sub>1</sub>x + a<sub>2</sub>x<sup>2</sup> + ... + a<sub>t−1</sub>x<sup>t−1</sup> Then we get n points (x<sub>i</sub> , y<sub>i</sub>) corresponding to the polynomial. Given any subset of t points a0 can be found by lagrange basis interpolation. 

li = <box> {x − x<sub>0</sub>}<over> {x<sub>i</sub> − x<sub>0</sub>} </box> /times \frac{x − x<sub>1</sub>} {x<sub>i</sub> − x<sub>1</sub>} \times ... \times \frac{x − x<sub>t−1</sub>} {x<sub>i</sub> − x<sub>t−1</sub>}

f(x) = X t−1 i=0 y<sub>i</sub>l<sub>i</sub>(x)


The idea of Shamir’s secret sharing is a popular concept in p2p systems. A p2p network does not have an centralized database to store peers’ keys. Storing keys in a selected set of peers might not be a good idea since p2p is a semi-trusted environment. For an example when a peer request a key from another peer, he might not respond. Therefore keys need to be broken into parts and distributed among multiple peers. A peer should be able to reconstruct a key without the knowledge of all the parts. [9], [26] are p2p anonymous authentication mechanisms that use the concept of Shamir’s secret sharing.

### 3.1 Conceptual design

#### 3.2.1 P2P network design

Using the .Net framework we implemented a hybrid P2P network[42]. A traditional hybrid peer to peer network consists of peers and super peers. Hybrid P2P systems is a combination of purely distributed P2P systems and mediated P2P systems. Hybrid systems are designed to overcome the problems of the two mentioned systems. These systems provide search efficiency of mediated P2P systems while maintaining the reliability of decentralization similar to pure P2P systems[43]. 
Our P2P network consists of three types of entities; the main server, ordinary peers (hereafter mentioned as peers) and super peers. A peer communicates with the main server only at the time of registration. Users join the network as peers. Peers are ordinary service requestors. They are connected to the system through super peers. Every peer is assumed to be behind a NAT environment. Peers with public IP addresses and higher computational power are promoted to be super peers. 
Super peers have more responsibility for the system. A super peer is connected to one or more other super peers in the network and responsible for one or more peers. They can communicate among other super peers using the super network. Super peers can join or leave the network at any time. Dynamic behaviour of super peers should not affect the connectivity of the network. Our design of the network is able to change the topology according to this dynamic behaviour of peers and maintain connectivity among existing super peers. 
A super peer is only responsible for nodes under his scope and does not know any information regarding other peers of the system. Therefore a node discovery process becomes an exhaustive task. This can be accomplished in two ways; flooding search and random walk. We utilize flooding search in this project since the random walk is not guaranteed to produce results[44].

#### 3.2.2 Distributed Certificate Management

The decentralized environment of the P2P network does not allow traditional methods of authentication. It’s difficult to maintain a centralized database of certificates where the availability of peers cannot be predicted. Distributing certificates among super peers is not a viable solution since super peers are not always available. Therefore all the certificates under this super peer remains not accessible. Also, malicious super peers might delete certificates from the network. The obvious solution is to keep multiple copies of the certificates. We propose a different solution by using Shamir’s secret sharing algorithm. The idea is to break the certificates into multiple parts and distribute across the P2P network. When needed, the certificates can be reconstructed from a minimal subset of the parts. A more detailed explanation of the implementation is given in section 3.3.1 .

#### 3.2.3 Proposed Authentication Schemes

#### Ring Signature Based approach 
The characteristics of ring signatures make it an interesting primitive in obtaining anonymous authentication. Ring signatures allows a message to be signed by a group of public keys. Making it impossible to identify the exact signer. The original ring signature scheme[36] and most of the proposed ring signatures provide complete anonymity. This is not suitable for authentication. This make it impossible to revoke the anonymity of malicious peers. Therefore we used the revocable ring signature scheme proposed in [40] to create a simple authentication protocol that protect users’ privacy. This is just a simple suggestion, of a way to obtain anonymous authentication using existing ring signature schemes. The idea is to challenge prover to generate a ring signature using a random nonce generated by a verifier. If the prover is able to accomplish this he can successfully authenticate himself. 

#### Authenticated key sharing based approach 
We propose a novel authentication mechanism that allows a peer to authenticate without revealing their identity. The basic idea of the protocol is to present prover a set of public keys and challenge to prove the knowledge of atleast one secret key corresponding to a public key from the set. This idea is simple but the protocol should not reveal any information related to the prover’s identity. Also a prover without a valid key pair should not be able to authenticate himself. To accomplish that we employ a authenticated key sharing scheme introduced in [45].

#### Zero Knowledge Proof Based Approach

Zkp is a popular approach to obtain anonymous authentication in p2p networks. This technique has been utilized in [24], [25] and [10]. Many of these approaches relies on pseudonyms to hide the identity. We propose a new authentication protocol that uses zero knowledge proofs to hide the identity among a group of users. The protocol achieves properties similar to ring signatures. This is an modification of the Schnorr’s zero knowledge proof [46]. The method is similar to the authenticated key sharing based approach in the sense that the challenge is to prove the knowledge of a secret key in a set of public keys. However unlike previous method, we use zero knowledge proofs to do that. Therefore this method achieve k anonymity.

### 3.3 Methodological approach

#### 3.3.1 Distributed Certificate Management

During the initial interaction of a peer, the corresponding super peer obtains the peer’s certificate. The super peer breaks the certificate into n parts using Shamir’s algorithm. The super peer then floods these parts across the network. Once a request to recreate the certificate(s) received. Super peer again floods a request(s) to collect the parts of the certificate. The super peers that are holding these parts will send them to the corresponding super peers. The original certificate can be recreated as long as r parts are received by the super peer (r ≤ n). 
This technique allows distributing certificates in a more dynamic way. As long as r super peers can be accessed, the certificate can be recreated. This method only requires minimal storage. That is, the size of a single part does not exceed the size of the certificate. This is also the more flexible approach. n and r can be changed for each certificate without affecting other certificates. However, then there needs to be a way to identify n and r for each certificate. 
n and r are performance metrics. Increasing n will increase the average key storage size in super peers. In section 6 we analyze the performance of increasing r while n is kept as a constant.

#### 3.3.2 Proposed Authentication Schemes

#### Ring Signature Based approach 
The protocol starts by the prover collecting a set of certificates from the super peer. Prover then randomly select a subset of the certificates. Then he verify the authenticity of the certificates and obtains the set of public keys from the subset of certificates using main server’s public key. Prover hides his own certificate among this subset of certificates and send them to the verifier to initiate the authentication. After authenticating the certificates, verifier obtains the set of public keys using main server’s public key. Then verifier generates a random nonce and challenge prover to generate a ring signature for this random nonce, using the above set of public keys. Prover use his secret key, the set of public keys and main server’s public key to generate a ring signature according to the algorithm proposed in [40]. Prover then sends the ring signature to the verifier. Verifier verifies the authenticity of the ring signature according to the random nonce he sent at the previous step. If the verification is successful, authentication is complete. Otherwise verifier sends a fail message. Authenticated key sharing based approach As same as the previous approach prover collects a set of certificates from the super peer. Then randomly select a subset out of them. After verifying the authenticity of the certificates prover extract the corresponding public keys. Prover mix his certificate into the subset of certificates and send them to the verifier. Verifier obtains the public keys after verifying the authenticity of the certificates. Then generate X = g<sup>x</sup> by selecting a random x. Then use the set of public keys to encrypt X. Thus creating a set of ciphertexts where each corresponds to a different public key from the set. Since one of the public key is prover’s, he will be able decrypt X with his secret key. After decrypting X, prover selects a random y and calculates Y = g<sup>y</sup> . Then generate K = X<sup>y</sup> . K is the shared key. Then he sends Y to the verifier encrypted with verifier’s public key. Verifier decrypts Y. Then compute K = Y<sup>x</sup> . At this stage both parties have the same shared key K. Verifier encrypts a random number R using a symmetric key encryption scheme using K as the key. Then challenge prover to decrypt this and send R back. If the prover generated the correct K at the previous steps, he will be able to decrypt R. Therefore prover can successfully authenticate himself. Otherwise verifier sends a fail message.

#### Authenticated key sharing based approach 
As same as the previous approach prover collects a set of certificates from the super peer. Then randomly select a subset out of them. After verifying the authenticity of the certificates prover extract the corresponding public keys. Prover mix his certificate into the subset of certificates and send them to the verifier. Verifier obtains the public keys after verifying the authenticity of the certificates. Then generate X = g<sup>x</sup> by selecting a random x. Then use the set of public keys to encrypt X. Thus creating a set of ciphertexts where each corresponds to a different public key from the set. Since one of the public key is prover’s, he will be able decrypt X with his secret key. After decrypting X, prover selects a random y and calculates Y = g<sup>y</sup> . Then generate K = X<sup>y</sup> . K is the shared key. Then he sends Y to the verifier encrypted with verifier’s public key. Verifier decrypts Y. Then compute K = Y<sup>x</sup> . At this stage both parties have the same shared key K. Verifier encrypts a random number R using a symmetric key encryption scheme using K as the key. Then challenge prover to decrypt this and send R back. If the prover generated the correct K at the previous steps, he will be able to decrypt R. Therefore prover can successfully authenticate himself. Otherwise verifier sends a fail message.

#### Zero Knowledge Proof Based Approach 
As same as the above two methods prover collects k certificates from the super peer. Then randomly select n-1 certificates and create C and P vectors as the above methods. However in this method public key is A<sub>u</sub> = g<sup>a<sub>p</sub></sup> where au is the private key. Similar to Schnorr’s protocol prover generates U. The difference is U contains factors of A<sup>vi</sup><sub>i</sub> where v<sub>i</sub> is a random number. This is generated only using the collected public keys (Prover’s public key is not in U). Prover then send U to the verifier. Verifier sends a challenge c to the prover. Prover xor all elements of vi with c to obtain v<sub>p</sub>. Then mix v<sub>p</sub> among the set of v<sub>i</sub> s and send them along with the set of public keys (including prover’s public key) to the verifier. Prover also sends r which is s − a<sub>p</sub>v<sub>p</sub>modp. Then prover does two steps of verification. First he xor vi s and check if it’s equal to c. If it is not terminate the authentication. Otherwise generate U<sup>′</sup> using r, A and v<sub>i</sub> s. If U = U<sup>′</sup> authentication is successful. Otherwise sends a fail message to the prover. A more detailed explanation is given in section 4.1.3 .

## Experiment Setup and Implementation

### 4.1 Proposed Schemes
#### 4.1.1 Ring Signature Based approach
#### Registration
1. A user has an ID which can be anything related to the identity of the user. Selects
a random number r<sub>u</sub>. Then generate a public key P<sub>u</sub> such that
P<sub>u</sub> = H1(ID, r<sub>u</sub>)
User then generates the private key S<sub>u</sub> corresponding to P<sub>u</sub>
User sends the registration request along with his ID, P<sub>u</sub> to the main server.
2. Main server verifies the identity of the user. Then the server signs P<sub>u</sub> with his
private key S<sub>s</sub> to generate Cert<sub>u</sub>. Then sends Cert<sub>u</sub> to the user.

#### Authentication

1. Prover collects k certificates from the super peer. Then randomly selects n-1
certificates from the the set. After verifying the authenticity of the selected
certificates prover generates C = {Cert<sub>1</sub>, Cert<sub>2</sub>, .., Cert<sub>n</sub>} which includes prover’s
certificate Cert<sub>p</sub> as well. Prover then obtain each corresponding public key from the
certificates to generate P = {P<sub>1</sub>, P<sub>2</sub>, .., P<sub>n</sub>}. Then send C to the verifier, encrypted
with verifier’s public key P<sub>v</sub>.
2. Verifier decrypts the message to obtain C. After verifying the authenticity of each
Certi
, verifier generates each P<sub>i</sub> using main servers public key P<sub>s</sub>. Then generate
H = Hash(P). Then sends H and a random nonce N to the prover.
3. Prover generate H′ = Hash(P) and if H ̸= H′
terminate the authentication.
Otherwise use his secret key S<sub>p</sub>, P and P<sub>s</sub> to sign N and generate ring signature
σ using [40] ring signature scheme. Then send σ to the verifier, encrypted with
verifier’s public key P<sub>v</sub>.
4. Verifier decrypts the message to obtain σ. Then verify whether σ corresponds to N
using P set of public keys (obtained in step 2). If the verification is success prover
is successfully authenticated. Otherwise verifier sends a fail message.

#### 4.1.2 Authenticated key sharing based approach
#### Registration

1. A user has an ID which can be anything related to the identity of the user. Selects
a public r<sub>u</sub>. Then generate
P<sub>u</sub> = H1(ID, r<sub>u</sub>)
P<sub>u</sub> is the public key of the user. User then generates the private key S<sub>u</sub> corresponding
to P<sub>u</sub>
User sends the registration request along with his ID, P<sub>u</sub> to the main server.
2. Main server verifies the identity of the user. Then the server signs P<sub>u</sub> with his
private key S<sub>s</sub> to generate Cert<sub>u</sub>. Then sends Cert<sub>u</sub> to the user.

#### Authentication

 1. Prover collects k certificates from the super peer. Then randomly selects n-1
certificates from the the set. After verifying the authenticity of the selected
certificates prover generates C = {Cert<sub>1</sub>, Cert<sub>2</sub>, .., Cert<sub>n</sub>} | C includes Certp as
well. Then send C to the verifier, encrypted with verifier’s public key (P<sub>v</sub>).
2. Verifier decrypts P using his secret key (S<sub>v</sub>). Generate H = Hash(P). Then
generate a random number x and obtain X = g<sup>x</sup>. Then generate n ciphertexts
CT = {C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>n</sub>}|C<sub>i</sub> = E<sub>P<sub>i</sub></sub>
(X|H). Verifier sends CT to the prover.
3. Prover selects the C<sub>i</sub> corresponding to his public key. Decrypt it using his secret
key (Sp) to obtain X and H. Generate H′ = Hash(P). Check if H = H′
. If not
terminate the session. Otherwise select a random number y to generate Y = g<sup>y</sup>
.
Then compute K = X<sup>y</sup>
. Prover sends Y back to the verifier encrypted with P<sub>v</sub>.
4. Verifier decrypts Y. Compute K = Y<sup>x</sup>
. Then generate another random number R,
generate E1<sub>K</sub>(R). E1(.) is a symmetric key encryption scheme. Then generate
H1 = Hash(R|K). Then send E1<sub>k</sub>(R) and H1 to the prover.
5. Prover decrypts the message with his knowledge of K to obtain R. Then use R and
his K to generate H1
′ = Hash(R|K). If H1 = H1
′
, prover sends R back to the
verifier. Otherwise terminate the authentication session.
6. Authentication is successful if the verifier obtains the same R. If not verifier sends
a fail message to the prover.

#### 4.1.3 Zero Knowledge Proof Based Approach
#### Setup

 1. P and Q are two large prime number where P-1 |Q.gisageneratorof acyclicgroupofZ<sup>∗</sup><sub>p</sub>
where order of the group is Q. P, Q and g are group parameters.

#### Registration

1. A user has an ID which can be anything related to the identity of the user. Selects
a random integer r<sub>u</sub>. Then generate a<sub>u</sub>
a<sub>u</sub> = H1(ID, r<sub>u</sub>)
such that a<sub>u</sub> is from [0, Q-1]. a<sub>u</sub> is the private key of the user. Then to generate
the public key A<sub>u</sub> user calculates
A<sub>u</sub> = g<sup>a<sub>u</sub></sup>modp
User sends the registration request along with his ID, A<sub>u</sub> to the main server.
2. Main server verifies the identity of the user. Then the server signs A<sub>u</sub> with his
private key K<sub>s</sub> to generate Cert<sub>u</sub>. Then sends Cert<sub>u</sub> to the user.


#### Authentication

1. Prover collects k certificates from the super peer. Then randomly selects n-1
certificates from the the set. After verifying the authenticity of the selected certificates prover generates C = {Cert<sub>1</sub>, Cert<sub>2</sub>, .., Cert<sub>n−1</sub>}. Prover then obtain each
corresponding public key from the certificates to generate P = {A<sub>1</sub>, A<sub>2</sub>, . . . A<sub>n−1</sub>}.
Prover then selects a random number s from the range [0, Q-1]. Then selects another
n-1 random numbers from the range [0, Q-1] to generate the V = {v<sub>1</sub>, v<sub>2</sub>, . . . , v<sub>n−1</sub>}.
Prover calculates
U = g<sup>s</sup>A<sup>v<sub>1</sub></sup>A<sup>v<sub>2</sub></sup>
. . . A<sup>v<sub>n−1</sub></sup>
Prover sends U to the verifier to initiate the authentication.
2. Verifier selects a random number c from the range [0, Q-1] and sends it to the
prover.
3. Prover calculates
v<sub>p</sub> = v<sub>1</sub> ⊕ v<sub>2</sub> ⊕ . . . v<sub>n−1</sub> ⊕ c
Then insert vp to the vector V such that V = {v<sub>1</sub>, . . . v<sub>p</sub>, . . . v<sub>n−1</sub>}. Prover also
update C = {Cert<sub>1</sub>, ..., Cert<sub>p</sub>, ..., Cert<sub>n−1</sub>} where Certp is prover’s certificate. Then
calculates
r = s − a<sub>p</sub>v<sub>p</sub>modp
Prover sends r, V, C to the verifier.
4. After verifying the authenticity of the certificates in C. Verifier calculates
c′ = v<sub>1</sub> ⊕ v<sub>2</sub> ⊕ . . . ⊕ v<sub>n</sub>
If c ̸= c′
, terminate the authentication session. Otherwise calculates

U′ = g<sup>r</sup>A<sup>v<sub>1</sub></sup>A<sup>v<sub>2</sub></sup>. . . A<sup>v<sub>n</sub></sup>
If U = U′
, authentication is successful. Otherwise terminate the authentication.

### 4.2 Testing

Testing of the system was done to understand the capabilities of the system. The testing was done cloud servers located in different countries. Intention was to mimic a world wide distributed network. Although a simulation environment would be ideal to do load testing on the system, absence of open-source platforms to simulate network environments which could run c sharp scripts was a problem. However, a real-world environment helps to understand the system performance in its operating environment. The tests were done to find the limitations of key sharing mechanism and to compare the performance of the three authentication protocols in a real environment. The first test was done to understand the performance of the key sharing mechanism. 

#### 4.2.1 Performance of key sharing 
Key sharing technique is an integral part of our implementation. The number of parts the key can be broken into (n) and the number of parts required to reconstruct a certificate (r) decides the availability of certificates. A high n value and low r value obtains a higher availability. Since distributing the parts of the certificates happens only once, in this experiment we measure the latency of the certificate reconstruction. Specifically, the experiment was done to identify how the latency of a successful certificate reconstruction varies with increasing n and r. The experiment was done by setting n = r. That is all parts of the certificate are required to reconstruct the certificate. First we break a randomly created certificate into n parts and distribute across the P2P network. Then we floods a SEARCH message requesting the parts of the certificate. The time was measured from the time of flooding the SEARCH message until the successful reconstruction of the certificate. We started with breaking the certificate into 2 parts and at each step we increased n by 2. We continued the experiment until n reached 20. For each n the experiment was done three times and we measured the average time. We also removed any outliers that could affect the results. Due to limited resources, we used only four publicly available servers each in a different country. The selected servers were located in Singapore, India, America and France. Multiple super-node instances were created at each server and super-nodes 20 were connected so that no two neighbour-nodes reside in the same country. This is to intentionally increase the latency of communication. 

#### 4.2.2 Performance of authentication protocols 
Anonymity of the authentication protocols depend on the number of certificates. Higher the number of certificates used in the protocol higher the anonymity of the prover. Therefore it is important that a protocol can handle a higher number of certificates. This experiment was done to measure the latency of a complete successful authentication session between a prover and a verifier. At each step we increased the number of ceritificates used in the protocol to measure how the latency varies. The experiment was done for the three proposed protocols in hope to compare the performance.

## Results and Analysis

### Ring Signature Based approach

The security of the protocol depends on the security of the ring
signature scheme[40]. The authors have proven the correctness,
revocation correctness, unforgeability and signer anonymity of the
signature scheme. They directly corresponds to the anonymity,
completeness, soundness of our suggested protocol.

#### Anonymity

Anonymity of the protocol depends on the properties of the ring
signature scheme. The scheme proves it obtains signer anonymity. The
proposed protocol does not reveal any information other than the set of
public keys P. The only information verifier can deduce is prover’s
public key P<sub>p</sub> is among the set P. Therefore this obtains k
anonymity.

#### Completeness

If a protocol has completeness, the protocol is said to be
comprehensive; an honest verifier will always be able to authenticate
himself.

The completeness of the protocol comes from the correctness of the ring
signature scheme[40]. The authors of the paper have mathematically
proven the correctness of the ring signature scheme. Therefore our
protocol is complete.

#### soundness

If a protocol has soundness property, the protocol is said to be
truthful; a cheating prover will never be able to authenticate himself.

Since the ring signature scheme has proven it’s unforgeability, a
cheating prover will not be able to forge a ring signature. The proposed
protocol obtains soundness.

#### Impersonation

Impersonation is when a malicious user (M) impersonates another user. A
protocol that accomplish soundness and completeness is secure against
impersonation attacks. Therefore this protocol is secure against
impersonation.

#### Replay Attacks

A replay attack is when an adversary saves a previously sent message(s)
and replay it later to gain an advantage. Let’s assume a scenario where
a malicious user (hereafter mentioned as M) is eavesdropping on a
authentication session. M can save message in step 1 (Msg1) and message
in step 3 (Msg3), replay it later in the hope to authenticate himself.

Msg1 is encrypted. Therefore M will not be able to reveal it’s content.
When Msg1 is replayed, verifier will respond with a random N and H.
Without the knowledge of P or C prover will not be able to generate the
correct ring signature. Therefore will not be able to authenticate
himself. Replaying Msg3 will not gain anything unless verifier generates
the same N as the original authentication. Probability of this scenario
is 1/N, which can be reduced by increasing the domain of N.

### Authenticated key sharing based approach

#### Anonymity

The protocol hides the identity of the prover among a group of selected
peers. The group is selected by the prover at random. Therefore verifier
cannot manipulate P to obtain a knowledge about the prover.

A cheating verifier may use different x values to obtain prover’s
identity. Verifier will generate a set of x = {x<sub>1</sub>, x<sub>2</sub>, ..., x<sub>n</sub>} and
generate X = {X<sub>1</sub>, X<sub>2</sub>, ..., X<sub>n</sub>} | X<sub>i</sub> = g<sup>x<sub>i</sub></sup>. Then
verifier can generate CT = {C<sub>1</sub>, C<sub>2</sub>, ..., C<sub>n</sub>} |
C<sub>i</sub> = E<sub>p<sub>i</sub></sub>(X<sub>i</sub> | H). By doing so, verifier hope to identify
which C<sub>i</sub> prover was able to decrypt. Then verifier can link that
C<sub>i</sub> to corresponding P<sub>i</sub> to reveal provers identity.

However, this will not allow verifier to reveal prover’s identity since
at step 4 verifier needs to generate K without the knowledge of exact X
the verifier received. Therefore will not reveal any information about
the prover unless verifier can successfully guess the X<sub>i</sub> prover
decrypted. Successfully random guessing X<sub>i</sub> has a probability of 1/n.

Another possibility is using the above method and generating a vector of
K = {K<sub>1</sub>, K<sub>2</sub>, ..., K<sub>n</sub>} where each K<sub>i</sub> correspond to a different
x<sub>i</sub>. Then at step 4 select a random K<sub>v</sub> and send E1<sub>k<sub>v</sub></sub>(R). By
this verifier hopes to find which K<sub>i</sub> the prover generated. This can
be done by replicating the decryption process using the elements of K
vector. Then check what K<sub>i</sub> generate a similar output. However this is
not possible due to H1 hash. Since this must include the correct key,
prover will know the malicious intentions of the verifier and terminate
the authentication process.

This methods does not provide k anonymity. Since prover always terminate
the authentication whenever the protocol was not correctly followed,
verifier can use this knowledge to reduce the scope of prover’s
identity. For an example, verifier generate CT as half of the C<sub>i</sub> are
incorrectly formed and other half is correctly formed. If the prover
terminate the authentication process, prover’s public key is one of the
misformed public keys. If the prover continues the authentication
process, prover’s public key is one of the correctly formed public keys.

#### Completeness

If the prover indeed has a secret key corresponding to any one of the
public keys in set P, prover can successfully decrypt X. Therefore can
obtain the correct key (k) for step 5.

K' = X<sup>y</sup>
K' = (g<sup>x</sup>)<sup>y</sup>
K' = (g<sub>y</sub>)<sub>x</sub>
K' = K

Since prover generate the correct key (K). He can successfully decrypt
R. Therefore can successfully authenticate himself.

#### Soundness

A cheating prover does not have a secret key corresponding to any of the
public keys in P. To authenticate himself as a member he has to
correctly guess X at step 3 or correctly guess R at step 5. Both it is
statistically impossible since X and R are generated randomly by the
verifier for each communication session.

Therefore unless prover can obtain a secret key and a corresponding
public key from a another registered user, it is not possible to
authenticate himself.

#### Impersonation

Since protocol accomplish both soundness and completeness, this protocol
is secure against impersonation attacks.

#### Replay Attacks

A replay attack is when an adversary saves a previously sent message(s)
and uses it again to gain an advantage. Let’s assume a scenario where a
malicious user (hereafter mentioned as M) is eavesdropping on a
communication session. M can save message in step 1 (Msg1) , message in
step 3 (Msg3) and/or message in step 5 (Msg5), replay it later in the
hope to authenticate himself.

If Msg1 was replayed this will not gain any advantage for M. Since M
does not know any secret key corresponding to the set P, he will not be
able to authenticate unless by random guessing X or R in step 3 and step 5.
Storing Msg3 will not help since without the knowledge of y, M will
not able to generate K. Only possibility of succeeding in a replay
attack is if the verifier generate the same R as the original
authentication. Then M can replay Msg5 to successfully authenticate
himself as a valid prover.

### Zero Knowledge Proof Based Approach

#### Anonymity

The only information the protocol reveals is that the prover has the
knowledge of an a<sub>p</sub>. Protocol hides the A<sub>p</sub> (public key) corresponds
to that a<sub>p</sub> among the set of P public keys. Identifying the exact
public key of the prover is not feasible. Therefore the protocol obtains
k anonymity.

#### Completeness

If the prover possesses the correct a<sub>p</sub>; the secret key corresponding
to A<sub>p</sub>, only then the prover will be able to generate r such that the
U generated by the verifier will be equal to the U received to the
verifier at step 1.

U' = g<sup>r</sup> A<sup>v<sub>1</sub></sup> … A<sup>v<sub>p</sub></sup> … A<sup>v<sub>n-1</sub></sup>
U' = g<sup>(s - a<sub>p</sub>v<sub>p</sub>)</sup> A<sup>v<sub>1</sub></sup> … A<sup>v<sub>p</sub></sup> … A<sup>v<sub>n-1</sub></sup>
U' = g<sup>s</sup> g<sup>-a<sub>p</sub>v<sub>p</sub></sup> A<sup>v<sub>1</sub></sup> … (g<sup>a<sub>p</sub></sup>)<sup>v<sub>p</sub></sup> … A<sup>v<sub>n-1</sub></sup>
U' = g<sup>s</sup> g<sup>-a<sub>p</sub>v<sub>p</sub></sup> … g<sup>a<sub>p</sub>v<sub>p</sub></sup> … A<sup>v<sub>n-1</sub></sup>
U' = g<sup>s</sup> A<sup>v<sub>1</sub></sup> … A<sup>v<sub>n-1</sub></sup>
U' = U

#### Soundness

Let’s consider a cheating prover as a prover who does not possess a
private key a<sub>p</sub> corresponding to a public key A<sub>p</sub>.

Without a a<sub>p</sub> a prover will not be able to generate

r = s - a<sub>p</sub>v<sub>p</sub> mod p.

At step 3, prover is required to generate v<sub>p</sub> by xoring elements of V
with the challenge c. This operation ensures that xoring elements in V
vector (including v<sub>p</sub>) at the verifier’s side would generate c.
Therefore to pass the first step of verification V must be well formed.
Without the knowledge of the valid a<sub>p</sub> a prover will not be able to
generate r to cancel out the g<sup>a<sub>p</sub>v<sub>p</sub></sup> component at the last step of
the verification.

The only possibility is random guessing. The probability of guessing
$a_p$ without any information is 1/Q. Since Q is selected to be a large
prime number, probability of that happening is statistically
insignificant.

#### Impersonation

As we explained previously a protocol that accomplish soundness and
completeness is secure against impersonation attacks. Therefore this
protocol is secure against impersonation.

#### Replay Attacks

Let’s assume a scenario where a malicious user (hereafter mentioned as
M) is eavesdropping on a communication session. M can save Msg1 at step
1 and Msg3 at step 3, and replay the messages later in the hope to
authenticate himself.

When M replays Msg1 verifier will respond with a random challenge.
Without the knowledge of s, a<sub>p</sub>, V and P vectors M will not able to
continue further. Therefore only replaying Msg1 will not be successful.
Replaying Msg3 as the response for the challenge will cause the first
step of the verification to fail. Since c is chosen randomly by the
verifier, the old v<sub>p</sub> will not correspond to the new c. Therefore
xoring elements of V will not be equal to c and verifier will terminate
the authentication process. This will only be successful if the same c
is chosen at the two authentication processes. The probability of this
happening is 1/Q. As mentioned in previous cases this is statistically
insignificant.

Modifying the Msg3 will not gain any advantage to M. As mentioned under
soundness proof, without a valid a<sub>p</sub> authenticating will be
infeasible.

## Conclusion

## Publications

1. [Semester 7 report](./)
2. [Semester 7 slides](./)
3. [Semester 8 report](./)
4. [Semester 8 slides](./)
5. Author 1, Author 2 and Author 3 "Research paper title" (2021). [PDF](./).

## Links

[//]: # " NOTE: EDIT THIS LINKS WITH YOUR REPO DETAILS "

- [Project Repository](https://github.com/cepdnaclk/anonymous-authentication)
- [Project Page](https://cepdnaclk.github.io/anonymous-authentication)
- [Department of Computer Engineering](http://www.ce.pdn.ac.lk/)
- [University of Peradeniya](https://eng.pdn.ac.lk/)

[//]: # "Please refer this to learn more about Markdown syntax"
[//]: # "https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet"
