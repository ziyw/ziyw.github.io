---
layout: post
title: 'Build: My todo list' 
tags: note
---

![Screenshot of todolist current state](/assets/images/todo-list-screenshot.png)

Wrote a small todo list app for Mac in Swift.
Main function is the same to normal todolist, just a list of uncomplete tasks, displayed with a status icon. 
The difference is this app allows me to keep track of the start and finish time for a task.
This way I can see how long does it take for me to complete a thing.

Few thoughts on this project:
- Took way longer than I think. At some point I just can't understand "@State"? And keep trying to by-pass the rule that View won't update normal variables. 
In retrospective is silly, but how view handles variables and view lifecycle was not exactly obvious to me. 

- The last time I wrote Swift was when it first released, so SwiftUI and Swift Data are definitely new to me. This "Swift Data is a wrapper for Core Data, Core Data is a wrapper for SQLite" situation is nice?

- Haven't built anything with a decent UI in a while, making the app looks nice is very satisfying. But also more complicated than I thought. Gave up a couple of design just because "making sense" is more important than "looking good" to me for this project.

- This app is purely in Swift, since it's only for MacOS,
but seems like anything done for other apple devices still need a blend of Objective-C and Swift. 

- Probably will add a "timetable"-ish thing in the future to see what I'm doing during the day analytic data. 

- First project that I actually use more ChatGPT, it's nice to drop questions you don't how to describe, overall not bad. 

In general, fun experience.