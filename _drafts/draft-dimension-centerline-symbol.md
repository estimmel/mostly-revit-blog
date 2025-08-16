---
layout: post
title: Dimension: Centerline Symbol  
date: 2012-11-02 10:55:00  
author: Eric Stimmel  
tags: [Revit]  
abstract: How does a dimension witness line know it's a centerline?  
---

If the reference plane in a family is "Center Front/Back" or "Center Left/Right" then dimensioning to it will tell the dimension witness line that it's a centerline and if your dimension style specifies to show a symbol when dimensioning to a centerline, it will show up. Even if that isn't supposed to be the center - in other words, if the family is built incorrectly.

