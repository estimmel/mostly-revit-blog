---
layout: post
title: Changing The Workset Of An Array
date: 2011-08-24 00:05:49
author: Eric Stimmel
tags: [Revit]
abstract: Ever needed to change the workset of an array? A couple of days ago I did, and to my surprise, I couldn't do it...
---

Ever needed to change the workset of an array? A couple of days ago I did, and to my surprise, I couldn't do it. Okay, eventually I figured it out and I'll explain the head smackingly simple solution since I couldn't find any blog posts describing it, but it was a really frustrating 30 minutes of Google searches and failed attempts by me and a couple of my colleagues to get there. 

The *trick* if you'd like to call it that, is in figuring out how to select the array itself. You might think that selecting one of the items in the array would select the array because the array is kind of like a wrapper around the object, but that only selects the *Array Group*. 

![Selecting an item in an array.][] 

You might then assume that by selecting *all* the items within the array you would be selecting the array itself because, well, the array is all of the things in the array. You would be wrong. 

![Selecting all items in an array.][] 

At this point you might start wondering whether or not there *is* an array object and that perhaps the problem is something altogether different. Maybe the elements aren't editable. Nope. Perhaps the *Array* category isn't visible - no, there is no *Array* category. You might start Googling or asking your neighbor, then, almost by chance, as you are clicking around on everything and anything, you select the modal line above the arrayed objects and as if my royal decree, the workset parameter activates and it's possible to change the workset of *the array*. So, to be clear, you have to select one of the objects in the array to make the array (manifest as a line with a number above it) visible and then select the array (the line with the number above it). 

![Selecting the array.][]

  [Selecting an item in an array.]: http://ericstimmel.com/blog_imgs/ArrayGroup.png
  [Selecting all items in an array.]: http://ericstimmel.com/blog_imgs/AllArrayGroups.png
  [Selecting the array.]: http://ericstimmel.com/blog_imgs/Array.png

