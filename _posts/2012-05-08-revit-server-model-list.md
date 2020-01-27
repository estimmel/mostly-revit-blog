---
layout: post
title: Revit Server Model List Using the REST API 
date: 2012-05-08 12:32:00 
author: Eric Stimmel  
tags: [Revit Server, AutoHotKey]
abstract: Using the REST API to get a list of models from Revit Server.
---

We've been looking into Revit Server for awhile at work, but never found the right project to use as a pilot until recently. There's finally a project where our team is split between two different physical locations on the same WAN and Revit Server makes sense. 

We have used GlobalScape WAFS in the past, quite successfully, when we needed access to a set of models from various locations not on the same WAN. This was before Revit Server even had that capability. That, however is a different blog post - forthcoming. 

I'm sure I'll write more about this as the project develops, but today I wanted to go over how to obtain a list of files from the Revit Server without using Revit. 

I need to create local files of all the project (.rvt) files in a specified directory on the Revit Server. Autodesk provides a [command line tool][tool] for making a local copy of a single file and this works well - we'll need it - but it's limited. First, you can only make one local file at a time. Our project has four files, but what about when there are 10 files? Or 50 files? Or 10 projects each with more that five files? We have projects like that, they just aren't currently using Revit Server. The second limitation is that you must know the name of the model before making the local copy. Again, there are only four models and I know their names, but we're going to do this anyway. 

The command line local file creation utility does not provide an option for returning a list of models in a specific folder, so we'll need to turn to the API. Revit Server uses the [REST API][]. I'll be using [AutoHotKey][] in my example, but you can use any language. Jeremy Tammik has [some helpful information][tbc] with links to Autodesk's documentation and examples. If you have the Revit SDK installed, you also have the Revit Server SDK which includes a PDF titled Revit Server REST API Reference which will be invaluable. On my machine, it can be found here: 

```
C:\Program Files (x86)\Revit 2012 SDK\Revit Server SDK\Revit Server REST API Reference.pdf
```

We'll need to make a specially formed HTTP request. This is a common task for web applications and consequently there are several libraries written in AutoHotKey that can do this - I've chosen to use [HTTPRequest.ahk by VxE][httprequest]. Revit Server will respond to this request by sending back [JSON][] formatted data. To get the filenames (or the project names in the future) we'll need to parse the response. Again, JSON is common on the web and I easily located [json.ahk][jsonahk] by [polyethene][] to help with this task. There are a couple of other scripts I gathered on the [AutoHotKey Forums][ahkforum] that I've linked to in the code. That's about it. Once we are able to dynamically gather the file/project names, we can do something with them. My script below just shows the list of files in a message box and then writes it to a text file, but we could also call the Revit command line tool and loop through the project folder to make local/backup copies of every model without having to know the model names in advance.

So here's the script.

```autohotkey
;;
;; AutoHotkey_L Version:  1.x
;; Language:            English
;; Platform:            x64
;; Author:              Eric Stimmel
;;
;; Script Function:
;;	Query Revit Server and return a list of models from a specified folder.
;;

#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.
#SingleInstance force
#Persistent

; include the supporting scripts
#include HTTPRequest.ahk
#include json.ahk
#include autoByteFormat.ahk

; create a new GUID for the HTTP header
; http://www.autohotkey.com/community/viewtopic.php?t=84037
TypeLib := ComObjCreate("Scriptlet.TypeLib")
NewGUID := TypeLib.Guid
StringReplace, NewGUID, NewGUID, {,,All
StringReplace, NewGUID, NewGUID, },,All
; MsgBox %NewGUID% ; for debugging

; create the headers
; <host> is the name of your server
URL := "http://<host>/RevitServerAdminRESTService/AdminRESTService.svc/|My Revit Server Project/contents"
In_POST__Out_Data := ""
In_Out_HEADERS := % "User-Name: " . A_UserName . "`nUser-Machine-Name: " . A_ComputerName . "`nOperation-GUID: " . NewGUID
Options := "Method: GET"

; make the request
HTTPRequest(URL, In_POST__Out_Data, In_Out_HEADERS, Options)

; MsgBox % In_POST__Out_Data ; for debugging - this should show the request that is sent

; set up our while loop
increment = 0
name = Models[%increment%].Name
model = % json(In_POST__Out_Data, name)

While model
{
	size = Models[%increment%].ModelSize
	modelsize = % json(In_POST__Out_Data, size)
	modelsize := autoByteFormat(modelsize)
	modelList = %modelList%%model%`t%modelsize%`n
	increment++
	name = Models[%increment%].Name
	model = % json(In_POST__Out_Data, name)
}

; MsgBox %In_Out_HEADERS% ; for debugging - this should show what is returned (see below for a sample)
MsgBox %modelList% 									; show the list in a message box
FileAppend, %modelList%, C:\ModelList.txt 			; write the list to a text file

ExitApp  
```
	
Here's what the server returns. I've formatted it for ease of reading. You should be able to figure out what's going on... If you uncomment the "In_POST__Out_Data" message box, you'll get this unformatted in a message box. You can also write it to a text file for further analysis or just to see what you get.

```json
{
	"Path":"My Revit Server Project",
	"DriveFreeSpace":204557041664,
	"DriveSpace":250056704000,
	"Folders":[],
	"LockState":0,
	"ModelLocksInProgress":null,
	"Models":[
		{
			"LockState":0,
			"ModelLocksInProgress":null,
			"ModelSize":12398749,
			"Name":"ARCH-1.rvt",
			"ProductVersion":2,
			"SupportSize":46843
		},
		{
			"LockState":0,
			"ModelLocksInProgress":null,
			"ModelSize":19581057,
			"Name":"STRUC-1.rvt",
			"ProductVersion":2,
			"SupportSize":7929
		},
		{
			"LockState":0,
			"ModelLocksInProgress":null,
			"ModelSize":7515290,
			"Name":"ARCH-2.rvt",
			"ProductVersion":2,
			"SupportSize":20218
		},
		{
			"LockState":0,
			"ModelLocksInProgress":null,
			"ModelSize":19395162,
			"Name":"STRUC-2.rvt",
			"ProductVersion":2,
			"SupportSize":5881
		}
	]
}
```

  [tool]: http://wikihelp.autodesk.com/Revit/enu/2012/Help/Revit_Administration_Guide/0002-Revit_Se2/0008-Revit_Se8/0010-Managing10/0024-Revit_Se24  
  [REST API]: http://en.wikipedia.org/wiki/Representational_state_transfer  
  [AutoHotKey]: http://l.autohotkey.net  
  [tbc]: http://thebuildingcoder.typepad.com/blog/2011/11/revit-server-rest-api.html  
  [httprequest]: http://www.autohotkey.com/community/viewtopic.php?t=73040  
  [jsonahk]: http://www.autohotkey.com/community/viewtopic.php?t=34565  
  [polyethene]: http://www.autohotkey.net/~polyethene/  
  [JSON]: http://json.org/  
  [ahkforum]: http://www.autohotkey.com/community/  
    