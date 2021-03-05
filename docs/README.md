---
layout: home
permalink: index.html

# Please update this with your repository name and title
repository-name: eYY-4yp-project-template
title:
---

[comment]: # "This is the standard layout for the project, but you can clean this and use your own template"

# Project Title

#### Team

- eNumber, Name, [email](mailto:name@email.com)
- eNumber, Name, [email](mailto:name@email.com)
- eNumber, Name, [email](mailto:name@email.com)

#### Supervisors

- Name, [email](mailto:name@eng.pdn.ac.lk)
- Name, [email](mailto:name@eng.pdn.ac.lk)

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

## Related works

## Methodology

### 3.1 Cryptographic Primitives

#### 3.1.1 Zero Knowledge Proof

Zero knowledge Proof (ZKP) is a protocol that allows a prover to prove the possession
of some secret to a verifier without revealing the secret or any information related to
the secret. The first idea of ZKP was introduced by Shafi Goldwasser, Silvio Micali, and
Charles Rackoff in [30]. Since then many different ZKPs have been published [31], [32],
[33], [34]. ZKPs are widely used in cryptography to implement cryptographic protocols
due to its privacy, authentication and low complexity.
A zero knowledge proof consists of a prover and verifier. In a zero knowledge protocol,
a prover must prove the knowledge of some secret using an interactive challenge-response
scheme. The protocol must not reveal any information regarding the secret other than the
knowledge of prover has the secret. A secure zkp must satisfy soundness, completeness
and zero knowledge properties.
There are two types of zero knowledge systems; interactive zero knowledge proofs
and non-interactive zero knowledge proofs [35]. Our proposed protocol uses a zkp that
utilize quadratic residues in modular arithmetic.

#### 3.1.2 Ring Signatures

The notion of ring signature was first introduced in 2001 by Ron Rivest, Adi Shamir and
Yael Tauman Kalai in [36]. Ring signatures are used to digitally sign messages on behalf
of a group. At the same time, makes it computationally difficult to find the exact signer.
3.1 Cryptographic Primitives 9
Ring signatures are designed to provide anonymity to the message signer. The same
functionality is provided by group signatures [37]. The only difference in group signature
is that it needs an authoritative entity to generate the signature. Therefore that entity
can revoke the anonymity of the signer. Ring signatures do not depend on a third party
to generate a signature. Ring signatures are spontaneous and provide unconditional
anonymity.
Over the years different ring signature schemes have been published with different
features; threshold ring signatures [38], linkable ring signatures[39], revocable ring
signatures[40], traceable ring signatures[41].
Consider a scenario where a group of k entities where each entity has a public key Pi
and a corresponding secret key Si. An entity r can generate a ring signature on a message
m using (m, P1, . . . , Pk, Sr). Anyone with the knowledge of m, P1, . . . , Pk can verify the
ring signature. No one outside the group (without a secret key Si) can generate a valid
ring signature for the same group.

#### 3.1.3 Shamir’s Secret Sharing

In 1979 Adi Shamir introduced the concept of Shamir’s secret sharing[7][how to share a secret]. This allows a secret to be divided into n parts. The secret can be reconstructed
with atleast t parts where (1 ≤ t ≤ n). No knowledge about the secret can be learnt
with (t-1) parts.
The concept is based on polynomial interpolation. The idea is to generate a polynomial
f(x) of (t-1) points. First we select (t-1) random positive integers such that (a1, a2, .., at−1).
Then set a0 to the secret we want to share. These points are used to generate the
polynomial f(x).
f(x) = a0 + a1x + a2x
2 + ... + at−1x
t−1
Then we get n points (xi
, yi) corresponding to the polynomial. Given any subset of t
points a0 can be found by lagrange basis interpolation.
li =
x − x0
xi − x0
×
x − x1
xi − x1
× ... ×
x − xt−1
xi − xt−1
f(x) = X
t−1
i=0
yi
li(x))

The idea of Shamir’s secret sharing is a popular concept in p2p systems. A p2p
network does not have an centralized database to store peers’ keys. Storing keys in a
selected set of peers might not be a good idea since p2p is a semi-trusted environment.
For an example when a peer request a key from another peer, he might not respond.
Therefore keys need to be broken into parts and distributed among multiple peers. A
peer should be able to reconstruct a key without the knowledge of all the parts. [9], [26]
are p2p anonymous authentication mechanisms that use the concept of Shamir’s secret
sharing.

### 3.2 Conceptual design

#### 3.2.1 P2P network design

Using the .Net framework we implemented a hybrid P2P network[42]. A traditional
hybrid peer to peer network consists of peers and super peers. Hybrid P2P systems is
a combination of purely distributed P2P systems and mediated P2P systems. Hybrid
systems are designed to overcome the problems of the two mentioned systems. These
systems provide search efficiency of mediated P2P systems while maintaining the reliability
of decentralization similar to pure P2P systems[43].
Our P2P network consists of three types of entities; the main server, ordinary peers
(hereafter mentioned as peers) and super peers. A peer communicates with the main
server only at the time of registration. Users join the network as peers. Peers are ordinary
service requestors. They are connected to the system through super peers. Every peer is
assumed to be behind a NAT environment. Peers with public IP addresses and higher
computational power are promoted to be super peers.
Super peers have more responsibility for the system. A super peer is connected to one
or more other super peers in the network and responsible for one or more peers. They
can communicate among other super peers using the super network. Super peers can
join or leave the network at any time. Dynamic behaviour of super peers should not
affect the connectivity of the network. Our design of the network is able to change the
topology according to this dynamic behaviour of peers and maintain connectivity among
existing super peers.
A super peer is only responsible for nodes under his scope and does not know any
information regarding other peers of the system. Therefore a node discovery process
becomes an exhaustive task. This can be accomplished in two ways; flooding search and
random walk. We utilize flooding search in this project since the random walk is not
guaranteed to produce results[44].

#### 3.2.2 Distributed Certificate Management

The decentralized environment of the P2P network does not allow traditional methods
of authentication. It’s difficult to maintain a centralized database of certificates where
the availability of peers cannot be predicted. Distributing certificates among super peers
is not a viable solution since super peers are not always available. Therefore all the
certificates under this super peer remains not accessible. Also, malicious super peers
might delete certificates from the network. The obvious solution is to keep multiple
copies of the certificates. We propose a different solution by using Shamir’s secret sharing
algorithm. The idea is to break the certificates into multiple parts and distribute across
the P2P network. When needed, the certificates can be reconstructed from a minimal
subset of the parts. A more detailed explanation of the implementation is given in section
3.3.1 .

#### 3.2.3 Proposed Authentication Schemes
<<<<<<< HEAD

##### Ring Signature Based approach

=======
Ring Signature Based approach
>>>>>>> f4254a788dd54633b62e4b6940d1f87728f9a089
The characteristics of ring signatures make it an interesting primitive in obtaining
anonymous authentication. Ring signatures allows a message to be signed by a group of
public keys. Making it impossible to identify the exact signer. The original ring signature
scheme[36] and most of the proposed ring signatures provide complete anonymity. This
is not suitable for authentication. This make it impossible to revoke the anonymity of
malicious peers. Therefore we used the revocable ring signature scheme proposed in
[40] to create a simple authentication protocol that protect users’ privacy. This is just
a simple suggestion, of a way to obtain anonymous authentication using existing ring
signature schemes. The idea is to challenge prover to generate a ring signature using a
random nonce generated by a verifier. If the prover is able to accomplish this he can
successfully authenticate himself.
Authenticated key sharing based approach
We propose a novel authentication mechanism that allows a peer to authenticate without
revealing their identity. The basic idea of the protocol is to present prover a set of public
keys and challenge to prove the knowledge of atleast one secret key corresponding to
a public key from the set. This idea is simple but the protocol should not reveal any
information related to the prover’s identity. Also a prover without a valid key pair should
not be able to authenticate himself. To accomplish that we employ a authenticated key
sharing scheme introduced in [45].

##### Zero Knowledge Proof Based Approach

Zkp is a popular approach to obtain anonymous authentication in p2p networks. This
technique has been utilized in [24], [25] and [10]. Many of these approaches relies on
pseudonyms to hide the identity. We propose a new authentication protocol that uses
zero knowledge proofs to hide the identity among a group of users. The protocol achieves
properties similar to ring signatures. This is an modification of the Schnorr’s zero
knowledge proof [46]. The method is similar to the authenticated key sharing based
approach in the sense that the challenge is to prove the knowledge of a secret key in a
set of public keys. However unlike previous method, we use zero knowledge proofs to do
that. Therefore this method achieve k anonymity

### 3.3 Methodological approach

#### 3.3.1 Distributed Certificate Management

During the initial interaction of a peer, the corresponding super peer obtains the peer’s
certificate. The super peer breaks the certificate into n parts using Shamir’s algorithm.
The super peer then floods these parts across the network. Once a request to recreate
the certificate(s) received. Super peer again floods a request(s) to collect the parts
of the certificate. The super peers that are holding these parts will send them to the
corresponding super peers. The original certificate can be recreated as long as r parts
are received by the super peer (r ≤ n).
This technique allows distributing certificates in a more dynamic way. As long as r
super peers can be accessed, the certificate can be recreated. This method only requires
minimal storage. That is, the size of a single part does not exceed the size of the
certificate. This is also the more flexible approach. n and r can be changed for each
certificate without affecting other certificates. However, then there needs to be a way to
identify n and r for each certificate.
n and r are performance metrics. Increasing n will increase the average key storage
size in super peers. In section 6 we analyze the performance of increasing r while n is
kept as a constant.

#### 3.3.2 Proposed Authentication Schemes

Ring Signature Based approach
The protocol starts by the prover collecting a set of certificates from the super peer.
Prover then randomly select a subset of the certificates. Then he verify the authenticity
of the certificates and obtains the set of public keys from the subset of certificates using
main server’s public key. Prover hides his own certificate among this subset of certificates
and send them to the verifier to initiate the authentication. After authenticating the
certificates, verifier obtains the set of public keys using main server’s public key. Then
verifier generates a random nonce and challenge prover to generate a ring signature for
this random nonce, using the above set of public keys. Prover use his secret key, the set
of public keys and main server’s public key to generate a ring signature according to the
algorithm proposed in [40]. Prover then sends the ring signature to the verifier. Verifier
verifies the authenticity of the ring signature according to the random nonce he sent at
the previous step. If the verification is successful, authentication is complete. Otherwise
verifier sends a fail message.
Authenticated key sharing based approach
As same as the previous approach prover collects a set of certificates from the super
peer. Then randomly select a subset out of them. After verifying the authenticity of the
certificates prover extract the corresponding public keys. Prover mix his certificate into
the subset of certificates and send them to the verifier. Verifier obtains the public keys
after verifying the authenticity of the certificates. Then generate X = g
x by selecting a
random x. Then use the set of public keys to encrypt X. Thus creating a set of ciphertexts
where each corresponds to a different public key from the set. Since one of the public
key is prover’s, he will be able decrypt X with his secret key. After decrypting X, prover
selects a random y and calculates Y = g
y
. Then generate K = Xy
. K is the shared key.
Then he sends Y to the verifier encrypted with verifier’s public key. Verifier decrypts Y.
Then compute K = Y
x
. At this stage both parties have the same shared key K. Verifier
encrypts a random number R using a symmetric key encryption scheme using K as the
key. Then challenge prover to decrypt this and send R back. If the prover generated
the correct K at the previous steps, he will be able to decrypt R. Therefore prover can
successfully authenticate himself. Otherwise verifier sends a fail message.

Authenticated key sharing based approach
As same as the previous approach prover collects a set of certificates from the super
peer. Then randomly select a subset out of them. After verifying the authenticity of the
certificates prover extract the corresponding public keys. Prover mix his certificate into
the subset of certificates and send them to the verifier. Verifier obtains the public keys
after verifying the authenticity of the certificates. Then generate X = g
x by selecting a
random x. Then use the set of public keys to encrypt X. Thus creating a set of ciphertexts
where each corresponds to a different public key from the set. Since one of the public
key is prover’s, he will be able decrypt X with his secret key. After decrypting X, prover
selects a random y and calculates Y = g
y
. Then generate K = Xy
. K is the shared key.
Then he sends Y to the verifier encrypted with verifier’s public key. Verifier decrypts Y.
Then compute K = Y
x
. At this stage both parties have the same shared key K. Verifier
encrypts a random number R using a symmetric key encryption scheme using K as the
key. Then challenge prover to decrypt this and send R back. If the prover generated
the correct K at the previous steps, he will be able to decrypt R. Therefore prover can
successfully authenticate himself. Otherwise verifier sends a fail message.

Zero Knowledge Proof Based Approach
As same as the above two methods prover collects k certificates from the super peer.
Then randomly select n-1 certificates and create C and P vectors as the above methods.
However in this method public key is Au = g
aumodp where au is the private key. Similar
to Schnorr’s protocol prover generates U. The difference is U contains factors of A
vi
i where
vi
is a random number. This is generated only using the collected public keys (Prover’s
public key is not in U). Prover then send U to the verifier. Verifier sends a challenge c to
the prover. Prover xor all elements of vi with c to obtain vp. Then mix vp among the set
of vi s and send them along with the set of public keys (including prover’s public key)
to the verifier. Prover also sends r which is s − apvpmodp. Then prover does two steps
of verification. First he xor vi s and check if it’s equal to c. If it is not terminate the
authentication. Otherwise generate U
′ using r, A and vi s. If U = U
′ authentication is
successful. Otherwise sends a fail message to the prover. A more detailed explanation is
given in section 4.1.3 .

As same as the above two methods prover collects k certificates from the super peer. Then randomly select n-1 certificates and create $C$ and $P$ vectors as the above methods. However in this method public key is $A_u = g^{a_u} mod p$ where $a_u$ is the private key. Similar to Schnorr's protocol prover generates U. The difference is U contains factors of $A_i^{v_i}$ where $v_i$ is a random number. This is generated only using the collected public keys (Prover's public key is not in U). Prover then send U to the verifier. Verifier sends a challenge c to the prover. Prover xor all elements of $v_i$ with c to obtain $v_p$. Then mix $v_p$ among the set of $v_i$ s and send them along with the set of public keys (including prover's public key) to the verifier. Prover also sends r which is $s - a_pv_p mod p$. Then prover does two steps of verification. First he xor $v_i$ s and check if it's equal to c. If it is not terminate the authentication. Otherwise generate $U^{\prime}$ using r, A and $v_i$ s. If $U = U^{\prime}$ authentication is successful. Otherwise sends a fail message to the prover. A more detailed explanation is given in section 4.1.3 .

## Experiment Setup and Implementation

### 4.1 Proposed Schemes

#### 4.1.1 Ring Signature Based approach

##### Registration

1. A user has an ID which can be anything related to the identity of the user. Selects
   a random number ru. Then generate a public key Pu such that
   Pu = H1(ID, ru)
   User then generates the private key Su corresponding to Pu
   User sends the registration request along with his ID, Pu to the main server.
2. Main server verifies the identity of the user. Then the server signs Pu with his
   private key Ss to generate Certu. Then sends Certu to the user.

##### Authentication

1. Prover collects k certificates from the super peer. Then randomly selects n-1
   certificates from the the set. After verifying the authenticity of the selected
   certificates prover generates C = {Cert1, Cert2, .., Certn} which includes prover’s
   certificate Certp as well. Prover then obtain each corresponding public key from the
   4.1 Proposed Schemes 16
   certificates to generate P = {P1, P2, .., Pn}. Then send C to the verifier, encrypted
   with verifier’s public key Pv.
2. Verifier decrypts the message to obtain C. After verifying the authenticity of each
   Certi
   , verifier generates each Pi using main servers public key Ps. Then generate
   H = Hash(P). Then sends H and a random nonce N to the prover.
3. Prover generate H′ = Hash(P) and if H ̸= H′
   terminate the authentication.
   Otherwise use his secret key Sp, P and Ps to sign N and generate ring signature
   σ using [40] ring signature scheme. Then send σ to the verifier, encrypted with
   verifier’s public key Pv.
4. Verifier decrypts the message to obtain σ. Then verify whether σ corresponds to N
   using P set of public keys (obtained in step 2). If the verification is success prover
   is successfully authenticated. Otherwise verifier sends a fail message.

#### 4.1.2 Authenticated key sharing based approach

##### Registration

1. A user has an ID which can be anything related to the identity of the user. Selects
   a public ru. Then generate
   Pu = H1(ID, ru)
   Pu is the public key of the user. User then generates the private key Su corresponding
   to Pu
   User sends the registration request along with his ID, Pu to the main server.
2. Main server verifies the identity of the user. Then the server signs Pu with his
   private key Ss to generate Certu. Then sends Certu to the user.

##### Authentication

1. Prover collects k certificates from the super peer. Then randomly selects n-1
   certificates from the the set. After verifying the authenticity of the selected
   certificates prover generates C = {Cert1, Cert2, .., Certn} | C includes Certp as
   well. Then send C to the verifier, encrypted with verifier’s public key (Pv).
2. Verifier decrypts P using his secret key (Sv). Generate H = Hash(P). Then
   generate a random number x and obtain X = g
   x
   . Then generate n ciphertexts
   CT = {C1, C2, ..., Cn}|Ci = EPi
   (X|H). Verifier sends CT to the prover.
3. Prover selects the Ci corresponding to his public key. Decrypt it using his secret
   key (Sp) to obtain X and H. Generate H′ = Hash(P). Check if H = H′
   . If not
   terminate the session. Otherwise select a random number y to generate Y = g
   y
   .
   Then compute K = Xy
   . Prover sends Y back to the verifier encrypted with Pv.
4. Verifier decrypts Y. Compute K = Y
   x
   . Then generate another random number R,
   generate E1K(R). E1(.) is a symmetric key encryption scheme. Then generate
   H1 = Hash(R|K). Then send E1k(R) and H1 to the prover.
5. Prover decrypts the message with his knowledge of K to obtain R. Then use R and
   his K to generate H1
   ′ = Hash(R|K). If H1 = H1
   ′
   , prover sends R back to the
   verifier. Otherwise terminate the authentication session.
6. Authentication is successful if the verifier obtains the same R. If not verifier sends
   a fail message to the prover.

#### 4.1.3 Zero Knowledge Proof Based Approach

##### Setup

1. P and Q are two large prime number where P-1 |Q.gisageneratorof acyclicgroupofZ
   ∗
   P
   where order of the group is Q. P, Q and g are group parameters.

##### Registration

1. A user has an ID which can be anything related to the identity of the user. Selects
   a random integer ru. Then generate au
   au = H1(ID, ru)
   such that au is from [0, Q-1]. au is the private key of the user. Then to generate
   the public key Au user calculates
   Au = g
   aumodp
   User sends the registration request along with his ID, Au to the main server.
2. Main server verifies the identity of the user. Then the server signs Au with his
   private key Ks to generate Certu. Then sends Certu to the user.

##### Authentication

1. Prover collects k certificates from the super peer. Then randomly selects n-1
   certificates from the the set. After verifying the authenticity of the selected certificates prover generates C = {Cert1, Cert2, .., Certn−1}. Prover then obtain each
   corresponding public key from the certificates to generate P = {A1, A2, . . . An−1}.
   Prover then selects a random number s from the range [0, Q-1]. Then selects another
   n-1 random numbers from the range [0, Q-1] to generate the V = {v1, v2, . . . , vn−1}.
   Prover calculates
   U = g
   sA
   v1A
   v2
   . . . Avn−1
   Prover sends U to the verifier to initiate the authentication.
2. Verifier selects a random number c from the range [0, Q-1] and sends it to the
   prover.
3. Prover calculates
   vp = v1 ⊕ v2 ⊕ . . . vn−1 ⊕ c
   Then insert vp to the vector V such that V = {v1, . . . vp, . . . vn−1}. Prover also
   update C = {Cert1, ..., Certp, ..., Certn−1} where Certp is prover’s certificate. Then
   calculates
   r = s − apvpmodp
   Prover sends r, V, C to the verifier.
4. After verifying the authenticity of the certificates in C. Verifier calculates
   c
   ′ = v1 ⊕ v2 ⊕ . . . ⊕ vn
   If c ̸= c
   ′
   , terminate the authentication session. Otherwise calculates
   4.2 Testing 19
   U
   ′ = g
   rA
   v1A
   v2
   . . . Avn
   If U = U
   ′
   , authentication is successful. Otherwise terminate the authentication.

### 4.2 Testing

Testing of the system was done to understand the capabilities of the system. The testing
was done cloud servers located in different countries. Intention was to mimic a world
wide distributed network. Although a simulation environment would be ideal to do load
testing on the system, absence of open-source platforms to simulate network environments
which could run c sharp scripts was a problem. However, a real-world environment helps
to understand the system performance in its operating environment. The tests were done
to find the limitations of key sharing mechanism and to compare the performance of the
three authentication protocols in a real environment.
The first test was done to understand the performance of the key sharing mechanism.
4.2.1 Performance of key sharing
Key sharing technique is an integral part of our implementation. The number of parts the
key can be broken into (n) and the number of parts required to reconstruct a certificate
(r) decides the availability of certificates. A high n value and low r value obtains a higher
availability. Since distributing the parts of the certificates happens only once, in this
experiment we measure the latency of the certificate reconstruction. Specifically, the
experiment was done to identify how the latency of a successful certificate reconstruction
varies with increasing n and r. The experiment was done by setting n = r. That is
all parts of the certificate are required to reconstruct the certificate. First we break a
randomly created certificate into n parts and distribute across the P2P network. Then we
floods a SEARCH message requesting the parts of the certificate. The time was measured
from the time of flooding the SEARCH message until the successful reconstruction of
the certificate. We started with breaking the certificate into 2 parts and at each step
we increased n by 2. We continued the experiment until n reached 20. For each n the
experiment was done three times and we measured the average time. We also removed
any outliers that could affect the results.
Due to limited resources, we used only four publicly available servers each in a
different country. The selected servers were located in Singapore, India, America and
France. Multiple super-node instances were created at each server and super-nodes
4.2 Testing 20
were connected so that no two neighbour-nodes reside in the same country. This is to
intentionally increase the latency of communication.
4.2.2 Performance of authentication protocols
Anonymity of the authentication protocols depend on the number of certificates. Higher
the number of certificates used in the protocol higher the anonymity of the prover.
Therefore it is important that a protocol can handle a higher number of certificates. This
experiment was done to measure the latency of a complete successful authentication
session between a prover and a verifier. At each step we increased the number of
ceritificates used in the protocol to measure how the latency varies. The experiment was
done for the three proposed protocols in hope to compare the performance.

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

    K' = X^y
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

- [Project Repository](https://github.com/cepdnaclk/repository-name)
- [Project Page](https://cepdnaclk.github.io/repository-name)
- [Department of Computer Engineering](http://www.ce.pdn.ac.lk/)
- [University of Peradeniya](https://eng.pdn.ac.lk/)

[//]: # "Please refer this to learn more about Markdown syntax"
[//]: # "https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet"
