---
layout: post
title: 'This Week in Coding: Persist HashMap' 
---

This week spend some time thinking and coding about persisting a hashmap. As this persisting mechanism will be used in many DB stroage cases. 

Code link: [gocode project](https://github.com/ziyw/gocode/tree/main/go_persist_hashmap)

1. Encoding anything to byte array
  String to byte array is simple because string itself is just byte array. For numbers, it will need to be encoded using big endian or small endian. 

2. Persist metadata before content
  Because everything is just byte array when first reading from disk, it's important to prepare the meta data. 
  In my implementation, I have persist content `length` as metadata. 
  Each read, will first read the fixed size `length` metadata. Then we can determine range `[offset: offset+length]` will be the content range. 

     Full structure: 

     ```
     --- 4 bytes ----| --- 4 bytes --- |          --- n bytes ---      | 
     NUMBER OF ITEMS |   KEY_LENGTH    |   key content can be variable | 
     ```

3. Test cases 
  Tried table driven tests for the first time in go lang, it a very neat format as most of the test cases really just different input and outpute one to one map. 

That's all for this week. Happy coding! 
