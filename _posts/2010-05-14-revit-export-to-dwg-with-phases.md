---
layout: post
title: Revit Export to DWG with Phases
date: 2010-05-14 11:56:48
author: Eric Stimmel
tags: [AutoCAD, Revit]
abstract: While I try to get my head above water at work (and put the polishing touches on a few longer posts) I thought this would be a good time to share a little Revit workflow tip I discovered yesterday...
---

While I try to get my head above water at work (and put the polishing touches on a few longer posts) I thought this would be a good time to share a little Revit workflow tip I discovered yesterday. I am working on a new project with some consultants who are working in, well, not-Revit. We export our backgrounds to them as DWG files and they astutely pointed out that our exports weren't showing existing features on separate layers. I never noticed this before since most of our projects are new buildings, so the amount of demo and existing walls, doors, windows and other features were pretty minimal if not nonexistent. It was a reasonable request, so I did a little digging and questioning and actually found very little. So I was left to testing and this is what I discovered. 

Revit can export views to AutoCAD and maintain the phase information of the objects (contrary to my past experiences) by separating objects on in different phases onto different layers. It will do this by appending a code to the end of the layer, so for example if you have a wall set to export onto layer **A-WALL-FULL**, if that wall is set to be demolished it will export onto **A-WALL-FULL**<em>DEMO</em> and an existing-to-remain wall will export to **A-WALL-FULL**<em>EXST</em>. 

The trick to this is to set the Phase Filter of the view being exported to **Show All**. If the view you are exporting is set to a phase filter of **Show Complete** there will not be any phases appended to the layers; all objects, regardless of phase, that are visible will be exported to the same specified layer (in this case **A-WALL-FULL**), but if your phase filter is set to **Show All** then existing (EXST) and demo (DEMO) will be appended to the layers for any objects that are set accordingly. 

I am not clear if these codes (EXST and DEMO) are hard coded or if they can be modified in a setting somewhere, but this seems sufficient for most needs. It's not AIA Standard layer naming, but it is close enough and if we needed to, we could add a line to our post-processing script to update the layer names in the exported files. (More on this post-processing in another post.)
