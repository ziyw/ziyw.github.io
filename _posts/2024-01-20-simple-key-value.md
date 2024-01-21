---
layout: post
title: 'This Week in Coding: Simple Key-Value Store' 
---

From last week's persist hashmap, it seems naturally leading to a key-value store. 
So I started a project to have a grpc service that have basic `put(key,value)` and `get(key)` functions.

Code link: [simplekv](https://github.com/ziyw/simplekv)

`simplekv` is still in progress, but the basic function is done: 
1) grpc server is listening to put and get calls from client
1) client call `put(key, value)` will persist the key-value to a file. Persisted files are divided to Pages. So each time, we only need to load and flush one file. 
2) client call `get(key)` can fetch the value from the corersponding page file. 

Page is decided by a hash function, currently set up max of 10 pages. 

Still working on the error handling, memory management... But it's really fun to start think more in go lang. 
Meanwhile I'm thinking about when a week is more coding heavy, it feels inevitable to have less to talk about since all things I want to say is cover in the code. 
Will think about how to balance this. 

