---
layout: post
title: 'This Week in Coding: Raft' 
---

This week I spent some time reading about Raft. I feel relieved to know there are other people who also think Paxos is hard to understand and even create a new method to solve the consensus problem. 

This blog is not going to explain Raft in detail. I think people have already done a pretty good job [1,2,3,4]. Here are some thoughts on system design after the reading. 

- Prioritize understandability. When the design is more understandable, efficient code will follow.
- Steps to explain a hard problem: 
    - The first step is to make your goal clear.
    - Break the question down. Before getting into the nitty-gritty, creating a framework of your solution only contains the main steps. Then moving into the details.
    - Reduce the memory burden (single data flow direction, reduce state spaces, ...)  Keep everything as simple as possible.

Raft is a good design with good writing. It makes solving consensus problem look easy. But the fact that Paxos came out in the 80s but Raft came out 2014 reminds me how hard that actually is. It's inspiring to read it. It also humbles me as a programmer. In the end, the power of a good design is it just makes you feel a little bit more optimistic about future. :)

References:
1. [Raft Website (with nice Raft visulization)](https://raft.github.io/) 
2. [Raft paper](https://raft.github.io/raft.pdf) 
3. [More detailed](https://github.com/ongardie/dissertation#readme) 
4. [A comparison between paxos and raft](https://arxiv.org/abs/2004.05074)

