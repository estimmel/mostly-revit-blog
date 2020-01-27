---
layout: post
title: Coordinate Section Boxes 
date: 2012-08-03 14:24:00  
author: Eric Stimmel  
tags: [Revit]
abstract: There is a simple solution to getting the extents of a section box from one Revit model to another. 
---

Okay, maybe this is common knowledge, but I've never been able to find a reference in all my searching and questioning. The problem is this - I have four models that are large. I want to do a Navisworks clash detection on only a portion of the model - say, level 15. I can export from a 3D view using a section box that crops my model to the desired portion of the building, but how do I get the same cropped 3D view into my other models? I can't insert the view, I can't get the numerical extents of the section box, I *can* however copy and paste the section box from one model to another. This is so simple, I'm sure I just never tried it before. I'm doing this in Revit 2013, but I went back to 2012 and verified it works there as well. This creates a new view with the same view settings and name as the original view - it's as if the section box *is* the view.
