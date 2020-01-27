---
layout: post
title: Remove Hyperlinks from Images in Excel  
date: 2013-10-29 17:37:00
author: Eric Stimmel  
tags: [VBA, Excel]  
abstract: Here's a VBA snippet for removing hyperlinks from images in Excel.  
---

I don't really know much about VBA except what I observed being written around me for AutoCAD and Excel several years ago, but I had a need for some today. It's pretty simple, but if you have a bunch of images linked to files on your computer in an Excel spreadsheet and want to remove the hyperlinks before sending the file to anyone here's a little macro that will do the trick.

```VBA
Sub RemoveImageHyperlink()
	' Loop through each image and remove the hyperlink
	Dim Pic As Shape
	For Each Pic In ActiveSheet.Shapes
		If Pic.Type = msoPicture Then
		Pic.Hyperlink.Delete
		End If
	Next Pic
End Sub
```

I'll leave it to you to figure out how to open the VBA editor and make run it.

