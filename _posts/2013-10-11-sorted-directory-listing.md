---
layout: post
title: Sorted Directory Listing  
date: 2013-10-11 12:56:00
author: Eric Stimmel  
tags: [windows]  
abstract: A quick Windows commandline one-liner to get a list of files and folders.   
---

As I've said before, it's always good to know your way around the commandline on Windows (or any platform for that matter). You can get a lot done with a few short commands. Today I want to document one simple command that I use quite often with one option that I usually forget and have to look up when it's important. The command is to write a list of file and folder names to a text file. That's it. Simple, but think about how you would get this otherwise - not so easy[^admission]. 

Open the commandline, navigate to the folder you want to get a listing for and type the following at the commandline.

```
dir /b /o:n > list.txt
``` 

The `dir` is a [directory listing][] and the `/b` option tells it to show just the bare file (or folder) name. the `/o` option tells it to sort the listing and the `:n` modifier tells the sorting to be by name. There are other options for sorting, but you can also just leave the `/o:n` portion off and paste the text into Excel or use your text editor to sort the list if you need it. That's the part I always forget...

I use this because I often want to send someone a list of filenames or occasionally I want to create a batch file that renames files, so I use this to get the original filenames and go from there in a text editor or Excel.


  [directory listing]: http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/dir.mspx?mfr=true
  [^admission]: Okay, there might be a way - I admit that I didn't look very hard. 
