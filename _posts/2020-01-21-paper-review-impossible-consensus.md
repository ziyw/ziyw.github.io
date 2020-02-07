---
layout: post
title: Impossibility of Distributed Consensus with One Faulty Process  
---

[Paper Note]

This paper mathematically proves that it is impossible to achieve distributed consensus even when only one faulty process exists. 

Consensus is a group of processes agree on a binary value. It is important for distributed systems. Like, for distributed data base, all data manager processes need to agree on decision to keep or discard a transaction. That is the "Transaction commit problem". 

The ideal situation is everything is reliable. In the real world, failure can happen anywhere There could be process crashes, network partitioning, message can be lost or distorted, or "Byzantine fault". 

The paper proves that even a single faulty process can cause the consensus protocol fail to reach an agreement. 

This paper talks about distributed consensus with the following postulates:
- Completely asynchronous processes. Which means the speed of each processes is unknown to each other. Messages can have delayed. Each process doesn't have access to sync clock, therefore time-out can't be used. 
- Reliable message system: each message eventually will be send to the destination process.

Then the paper gives a very mathematical proof. The abstraction of a consensus protocol is quite elegant. 

Here is the abstraction:

- Consensus protocol P, an async system of N processes (N >= 2) 
- For each process: 
	- Internal state: input register, output register, program counter, internal storage. Input/output register value is within {b, 0 ,1}. 
	- Initial state: fixed value for all internal state except input register. output register has init value b. 
	- Decision state: when output register value is decided by transition function. 
- Message system: 
	- Message (p, m) pair, p is destination process, m is the message value 
	- Message buffer, a queue of messages 
	- Two operations
		- `send(p,m)`: place (p,m) in message buffer 
		- `receive(p)`: if message is delivered, return m, remove pair from the buffer. If not, return null, don't change buffer. 
- Configuration: internal states of all processes and message buffer 
- Step: from one configuration to anther. 
- Event: apply a step on configuration. 
- Schedule: a finite or infinite sequence of events that can be applied on a configuration. 
- Run: the sequence of steps in the schedule. 

I wont' keep the detailed proof in there. The basic idea is 1) The init configuration can have 2 potential result values 2) faulty process can leads to a situation that it can always take steps to go to a configuration that have 2 potential result values.  

This paper proves that in order to achieve distributed consensus, it's inevitable to require additional information (more than just the message) from each processes to reach an agreement from most of them and most of them needs to be alive.  


