---
layout: post
title: 'This Week in Coding: BufferManger Made Simple' 
---

In the beginning, there is computer, making beep boop sounds.
Then there is the question, how do I persist some data and fetch it efficiently.
What if I want to persist A LOT of data and fetch some specific ones efficiently. 
Here I am, at the age and mental maturity that doesn't allow me to dance around those questions anymore. I have to start to read about database.

## This week in coding
New year, same me, but with a little bit more thinking. 

2023 is the year I realize it's very hard to apply other people's roadmaps to my own path now.
"People want you to want what they want. If you want the same things they want, then their wants is validated. If you don't want the same things, you lack of wanting can, to certain people, come across as judgment." as Ann Patchett wrote in These Precious Days. 

2023 was basically a disorienting experience of me finding out the old goals don't apply anymore. Turns out if you don't chase the same goal as the world, the world will let you know immediately, and maybe as a warning sign to push you back to the same wanting system. And I do feel like shit a lot of times.

A toxic trait I picked along the way was, the more I learn, the more guilty I feel. As soon as I learn something new, I have an instant guilty feeling that I should have known about it earlier. What the actual f***?! In this logic I should be born with all knowledge loaded ready to fire. This might be the single worst neural path I have ever formed. 

But this is not the end of the story. Thinking through the old belif system was a nice sobering experience, to sort out what's really matter, to build up the courage to follow a new goal. Starting from 2024, I want to see a personal progression into deeper, meaningful topics. "This week in coding" will be a personal documentation of this journey, with zero judgement. It is time to sit down and write things with a full heart.

## Database BufferManager Made Simple
Here is a question I didn't get until knee deep into Database, why do we need BufferManger and what does it do? 
This is my personal attempt to explain buffer manager in plain english, so next week I can do BufferManger made hard. :) 

First is the purpose of a database. A database is a software who persists your data on disk and retrives them fast when you need it. 

Persist and retrive data on disk is not a big problem in a small scale. 
Put everything in a single file, everytime you want to read file, open the file, read it line by line, find what you need, done.
As data size gets bigger, saving in a single file is less feasiable as read through a single giant file could be very slow. 
The solution is simple, divide the data into pages. 

From here, database saves data like a book in real life. 
Instead of putting the whole book content on a giant single piece of paper, books have fixed-size pages and each page have about the same amount of data. 
When you need to look up something in the book, go to index of the book, find the word, then go to the page. ("hello", p50), if you look for "hello", you go to P50. That's exactly how DB works, when you look up something, DB will have a index of all pages, then it will find the page with the content. 
Index is sorted in some way (alphabetically, or numerically), so when you search index, you don't need to read the whole index to find the answer.

Then the problem is, if an index is too big, finding certain content will still take too long, even when index is sorted. Here comes B-Tree! Basically B-Tree is a tree structure that can be as flat and balacenced as possible to store sorted content. The purpose of B-Tree is to use as less pages as possible to save a tree structure.

Here is a problem I didn't know I don't know. All these years of learning trees, I'm fluent when trees living in memory, aka when tree node pointer are direct memory pointers. But I didn't know how pointers work in disk setting! On disk, each node on B-Tree is a page, and to find the next node, pointers are defined as 
```
Pointer on disk = (page_id, offset, length of the content) 

```

Using this triplet can locate content on disk when content is divided to pages. 

Then finally, Buffer Manager. Buffer Manager manages memory usage. To read a page on disk, you have to load it into memory first.
Because files on disk is way bigger than memory size, DB can't load all content into memory, DB can't even load all index pages to memory. The idea is only load the ones that gonna be used and unload those are not used anymore. 
When retrive data, BufferManager first load the root index page (root node of the index B-Tree), then go to the next node on the tree (which is another page), then after all pages are loaded, evict a page on memory before load another page from disk, and when page content changes, flush them to disk.

That's really it, database is saving data like a book on disk and BufferManager is the one finding the content using index. 

Happy new year! There will be new adventures. Happy coding.