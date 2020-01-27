---
layout: post
title: Revit Journal File Scripting
date: 2010-08-26 19:38:38
author: Eric Stimmel
tags: [Revit]
abstract: Our office uses a custom script to open Revit files...
---

Our office uses a custom script to open Revit files. It was developed, at least in part, by [JV][] and, as you might expect, carries with it lots of well thought out, but sometimes complex little pieces. I call it a script, but it's more than a couple of lines of code. I've been digging around in it and making a few tweaks and additions here and there to get it working with Revit 2011. One thing that's been a stumbling block is the addins. We are using the standards (Worksharing Monitor and Navisworks 2011 Exporter) as well as a few custom tools (these will require some more involved rework that's a little outside of my current capabilities) and then I have Ian Keough's [goBIM][] exporter for his wonderful, though still a little tempermental, goBIM iPhone app. I have noticed that, although Revit 2011 offers a new method of loading addins (the .addin manifest), Navisworks still uses a modification to the Revit.ini file. Worksharing Monitor and goBIM both use the .addin method which seems like a much easier path. When using our script to launch a file, only the Navisworks plugin is loaded. When launching a model directly from Revit all three plugins are loaded. This has led me to look at the journal file... and crack open [Mastering Autodesk Revit Architecture 2011][]. Hopefully I will be able to post further development here or at least a small note of success. For now... ![LoadFileScript][] 

**UPDATE:** After some research and hints on the most excellent [AUGI forums][], and more specifically the [thread mentioned in the book above][6] and a couple of newer threads by [dbaldacchino][7] and [david.kingham][8] detailing their own versions of this script, I have found corroboration that the new .addin method of loading addin's does not work when launching a file using a journal file. To [quote David Kingham][]:

> In 2011 Autodesk changed the way addins are loaded and a big flaw with
> this is addins do not get loaded when a journal file is used to open
> Revit (which is how I had previously opened projects)

So the mystery is solved and the rework begins. I have found that once I bypass the use of the journal file to open the files, <del>I am always prompted to choose which worksets to open</del> I can't control the opening behavior to specify worksets or open all. More testing is in progress - I should know more by the end of the weekend.

  [6]: http://forums.augi.com/showthread.php?t=65897 "The original thread"
  [7]: http://forums.augi.com/showthread.php?t=117310 "Dave Baldacchino's version"
  [8]: http://forums.augi.com/showthread.php?t=92831 "David Kingham's version"
  [JV]: http://allthingsbim.blogspot.com/
  [goBIM]: http://go-bim.iankeough.com/wordpress/
  [Mastering Autodesk Revit Architecture 2011]: http://www.amazon.com/gp/product/0470626968?ie=UTF8&tag=ericstimmel-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0470626968/
  [LoadFileScript]: http://ericstimmel.com/blog_imgs/Journal_LoadFileScript_sm.jpg
  [AUGI forums]: http://forums.augi.com/
  [quote David Kingham]: http://forums.augi.com/showpost.php?p=1075925&postcount=48

