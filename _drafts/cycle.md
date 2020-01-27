---
layout: post
title: Cycle
author: Eric Stimmel
date: 2010-12-14 22:02:30
tags: [AutoCAD, Revit, Rhino]
abstract: Here's a quick one. A colleague of mine asked me what the AutoCAD command was for choosing which object to select when there are overlapping lines...
---

Here's a quick one. A colleague of mine asked me what the AutoCAD command was for choosing which object to select when there are overlapping lines where you want to select. Ever since I first used Rhino and saw how it dealt with this problem and then later how Revit handled it, I wished that AutoCAD had something similar. Well apparently it does. It's called selection cycling and it works a little bit differently that it's counterparts in Rhino and Revit. See the descriptions and screenshots below.

## AutoCAD

As with everything in AutoCAD there a couple of ways to do this and there are system variables that control whether you use the current controls or the legacy controls. This behavior has probably been in AutoCAD for quite some time, but since I only have AA2008 and AA2011 installed and I only recently learned about this command, I won't pretend to give anyone a history lesson. Nevertheless, the system variable LEGACYCTRLPICK (available in 2008 and 2011) leads me to believe that this functionality predates 2008. By default, in newer versions of AutoCAD, LEGACYCTRLPICK is set to 0 which means pressing CTRL and left-clicking an object will select subobjects on 3D solids. Setting this value to 1 enables the legacy behavior of cycling through overlapping objects. There is no need to go back to this legacy setting because in newer versions you cycle through objects by pressing Shift + Spacebar and left-clicking. You can see below that I have drawn a rectangle and a line that overlap. If I press and hold Shift + Spacebar and left-click in the area where they overlap, I will select a different object each time. To accept the highlighted selection I hit enter (or spacebar or right-click depending on your user settings). ![AutoCAD Selection Cycling][]

## Rhino

Rhino uses a more interactive method which is very intuitive and does not require prior knowledge of a special key combination. When you try to select something in Rhino, if your mouse cursor is close to more than one object, a small dialog box pops up with a list of all the objects it thinks you might have wanted to select. The most likely object is immediately highlighted and first in the list. As you mouse over the list, the corresponding object is highlighted and until you select something from the list, it remains active. ![Rhino Selection Cycling][]

## Revit

With Revit, we are back to using a combination of key commands and mouse gestures. Here you mouse over an object and the foremost object or the first encountered is highlighted as what will be selected if you left-click. As you move your mouse around, other objects or sub (supra?) objects will be highlighted and if you hit the Tab key you will cycle through objects that are on top of each other. You can Tab through or into complex object, links, groups, etc to get to the one you want. This is pretty powerful and easy to use once you know it's there and almost becomes the lingua franca of interacting in Revit. ![Revit Selection Cycling][] Of course there are other ways to select objects in each of these applications and there are ways to make them behave more like one another, but these are pretty much the standard or out of the box settings. It's interesting to me to consider the user interface decisions made in each of these instances and, at least in a very broad brush manner, compare that to the users of each of each software. I'm speaking generally here, but it's details like this that lower the barrier to entry and guide users through the workflow. I'd be interested to hear other people's thoughts about this topic. I'm sure it will surface again and again on this blog.

  [AutoCAD Selection Cycling]: http://ericstimmel.com/blog_imgs/AutoCADSelection.png
  [Rhino Selection Cycling]: http://ericstimmel.com/blog_imgs/RhinoSelection.png
  [Revit Selection Cycling]: http://ericstimmel.com/blog_imgs/RevitSelection.png

