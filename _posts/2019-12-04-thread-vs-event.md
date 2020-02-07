---
layout: post
title: Thread vs Event
---
 
This is a review of the paper *Why events are a bad idea (for high-concurrency servers)*. 

Summary: this paper is about why using threads is not a bad idea for high-concurrency applications. 

This paper first talked about what people think are the advantages of using events.
Then by introducing the duality of threads and events, they made their point as threads and events can receive similar performance theoretically. 
To take a further step to the point that threads is more suitable for hight concurrency apps, they briefly argued that using threads is actually better in **performance**, **control flow**, **synchronization**, **state management** and **scheduling**, especially enhanced compiler can improve thread performance.  

For evaluation, they implemented a user-space thread library and used it in a test web server. 

The final conclusion is **Use threads for high-concurrency apps. Use events for UI.**  

Personal notes:

- Some ideas in this paper are overlapped with *Why Threads Are A Bad Idea* by John Ousterhout. 
I can only find the lecture slides of Outsterhout's paper. 
Outsterhout gave a brief intro to both threads and event systems in the slides, which I think is nice to have. It makes the paper/slides more self-contained and reduced the unnecessary frustration caused by using different terms.


- From my limited experience, this idea above is already an idiom in software development. 
The paper didn't mention much about who was actually using event system and making those criticism about threads. 
Which leaves me the frustration on with whom this paper is trying to argue with and whom this paper is trying to convince.
Would be nice to have a few solid references to the software using event systems compares to the ones using threads.  

- A detailed comparison between threads and events can be a very good personally practice for multithread programming. I'm putting it into my todo list. 

Reference  // TODO: better reference format  
[1] *Why events are a bad idea (for high-concurrency servers)*   
[2] *Why Threads Are A Bad Idea*  

