---
layout: post
title: Spot Elevations and Model Graphics Style
date: 2010-09-20 15:36:03
author: Eric Stimmel
tags: [Revit, RevitTips]
abstract: Just a quick tip here that I always forget about...
---

Just a quick tip here that I always forget about and somehow ends up frustrating me for 15 minutes until I realize what's going on. 

Here's what happens: I am attempting to place a spot elevation in a plan view and find that I can only select an edge or endpoint; if I try to select an open area on a floor I get the universal "NO" symbol (i.e. the circle with a slash through it). My next 10-15 minutes are spent checking the associated level, the view range, various properties, the floor object, etc. Then I notice that the view is set to Wireframe. 

The moral of the story - if you want to use spot elevations, your view's Model Graphics Style *must* be set to Hidden Line. I suppose there's some logic to this, but it's not entirely clear. 

![Model Graphics Style - Hidden Line][] 

**UPDATE:** Okay, a quick web search informs me that [I'm not the first person to run across this issue and blog about it][].

  [Model Graphics Style - Hidden Line]: http://ericstimmel.com/blog_imgs/ModelGraphicsStyle-Hiddenline.png
  [I'm not the first person to run across this issue and blog about it]: http://revitclinic.typepad.com/my_weblog/2009/01/spot-elevations-dont-find-the-floor.html

