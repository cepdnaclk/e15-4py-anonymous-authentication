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

The concept of Peer to peer (P2P) communication has gained significant attention inthe network community over the years. Since the release of Napster in 1998 many P2Papplications have been introduced. Bitcoin[1], BitTorrent, TOR[2], Freenet[3], etc aresome of the more popular P2P applications. The absence of centralized authority is themain reason behind the popularity of P2P applications. This eliminates the need for anexpensive central server. Also removes the vulnerability of a single point of failure. P2Pnetworks are considered to be more efficient and scalable than traditional client-serverapplications.The decentralized nature of P2P networks makes it difficult to integrate traditionalauthentication mechanisms. Due to this many such networks focus on providing useranonymity rather than authentication. The reduced security of these networks has createda lot of possible threats [4]. These threats can vary from uploading malicious files tofamous Sybil attacks [5]. Also, the anonymity feature of these networks has created a safehouse for cybercriminals [6]. Not being accountable for his/her actions, held responsibleand punished for malicious actions, P2P users have the freedom to misbehave. This cancause harm to the network and its users.

We suggest that even in an anonymous network there should be some level of accountabilityto protect the network and its users. Accountability is achieved through authentication.

To integrate an authentication mechanism into an anonymous P2P environment we needto solve two main challenges.•Authenticate in a decentralized environment.•Authenticate without revealing identity.These two points have been discussed separately since the start of the internet. Eachpoint has its own difficulties and challenges. Authentication needs to tackle problems likethe absence of a central server, certificate management in a distributed environment, thesemi-trusted nature of peers, the unpredictable availability of peers, etc. Authenticationneed to solve problems like not revealing sensitive information about authenticatingparty’s identity, secure against misbehaving parties (cheating verifiers and cheatingprovers), unlinkability of authentication sessions, practicality, etc.

In this paper, we propose three new approaches for anonymous authentication in P2Pnetworks to solve the above problems.

    1. Ring signature based approach.
    2. Authenticated key sharing based approach.
    3. Zero knowledge proof based approach.

We deploy these protocol in a P2P environment where certificates are managed bypeers with elevated privileges (super peers). To solve the problems of semi-trusted natureand unpredictable availability of peers we utilize Shamir’s secret sharing[7] technique. Amore detailed explanation of these cryptographic primitives is given in section 3. Thenwe test the performance of these ideas in a practical environment developed using the.Net framework.

## Related works

## Methodology

## Experiment Setup and Implementation

## Results and Analysis

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
