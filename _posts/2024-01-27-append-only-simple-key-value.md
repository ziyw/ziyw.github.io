---
layout: post
title: 'This Week in Coding: Append Only Simple Key-Value' 
---

Code link: [simplekv](https://github.com/ziyw/simplekv)

`simplekv` changed a lot this week. 
Inspired by [Bitcask](https://docs.riak.com/riak/kv/2.2.3/setup/planning/backend/bitcask/index.html), I have changed the imlementation from previous "directly persisting a hashmap" to "append only log file enhanced by hashmap" key-value store. 

### Use cases: 
Append-only store for key-value store works best when 1) small amount of keys 2) there are a lot writes but not many reads. Because the way we only keep hash of key-offset in memory, seeking reads on file still takes more time. 

### Storage: Segment
Key-value are stored in segment file. Each segment have it's content and a in-memory hashmap. 
Segment content is an append-only file. Key-value pair are stored as byte array, appended to the end of the current segment file. 
Hashmap stores key-offset pairs in memory. Key is the existing keys in the current segment. Offset is the start of the index where the key-value pair is stored in the segment file. 

#### Compress and Merge 
As there are more write into the segment file, inevitably it will grow too big. 
There are two steps to control the size of a segment file 
1. Compress current segment file and write into a new one: compress current segment by only keep the latest key-value pair for each key and write the new content into a new segment. This way we can elimiate all older values. 
2. Merge: merging two compressed segment and make a third one can elimiate all the duplicate keys between two files, further reducing file numbers and sizes. 

`simplekv` is still under-building, there will be more complete functions and a final write-up with all the impl details, also a benchmark to see how fast it can actually be. 
In general it was a very fun week to work on it. Happy coding.