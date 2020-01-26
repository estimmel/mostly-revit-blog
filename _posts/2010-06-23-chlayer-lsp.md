---
layout: post
title: ChLayer.lsp
date: 2010-06-23 19:28:12
author: Eric Stimmel
tags: [AutoCAD]
abstract: Here's a Autolisp script I wrote to help one of our project teams prepare their drawings as a conformed set to the client. They needed to print a set of drawings showing the revision deltas (those little triangles with numbers in them identifying which revision each change was a part of) but not the revision clouds. There were lots of these revision deltas and clouds (as there are with all projects) and they just needed a clean, readable set...
---

Here's a Autolisp script I wrote to help one of our project teams prepare their drawings as a conformed set to the client. They needed to print a set of drawings showing the revision deltas (those little triangles with numbers in them identifying which revision each change was a part of) but not the revision clouds. There were lots of these revision deltas and clouds (as there are with all projects) and they just needed a clean, readable set. 

So this seems reasonable enough and maybe even easy, just freeze the layer or layers with the revision clouds and not the layers with the revision deltas - this can be done with a simple AutoCAD script. I can post an example of this if someone asks - I write them for almost every project at some point or another. Even though we have some powerful custom tools that allow us to manage layer visibility externally, this kind of very basic scripting knowledge is invaluable. Particularly those specialists managing large projects, but even those users pulling together small sets with just few people can use something like this to speed things up and prevent repetative action errors. In this case it wasn't that simple (obviously, or I wouldn't be writing such a lengthy post) and if you've ever had to deal with a request like this you might ask if there are ever any cases that are that simple. Well... yes, there are. But now back to the task at hand... I'm sure you know where I'm going, the revision clouds and deltas were on the same layer in some files, they were on different, but inconsistently named layers in other files, other linework and text were drawn on the same layers as the deltas and revision clouds, some were drawn in the sheet file and others in the annotation file (an xref), etc. It was a big task considering there were 1000+ sheets and at least that many more xrefs that needed to be checked. With a deadline looming and no budget for manpower, this was not something we could brute force. We needed automation and quick. 

Below is the script I came up with in all it's commented glory. For now I'll just let is stand at that; it wasn't a perfect script and there was some measure of manual checking, but it got the bulk of the work done in short order. I'll have to let this post sit for awhile and come back to it after rereading it once or twice. I learned a lot about logic and scripting writing this and several portions of this script seem to reappear often enough to get their own post so for now, for the adventurous, enjoy! 

~~~~~~~~~~~~~~~ lisp
;;  
;; ChLayer.lsp  
;;  
;; ChLayer  
;; Routine to select rev clouds on a specified layer(s), move them to a non-plotting layer  
;; then freeze the new layer.  
;; by Eric Stimmel  
;;  
;; last updated 9/24/2008  
;;  
(defun c:chlayer (/ lay_name lay_name_new ss1 n index ent1 a1 a2 b1) ; Define the function  
(setq lay_name "A-ANNO-R*") ; Specify the layer(s) that the rev clouds are currently on  
(setq lay_name_new "A-ANNO-REVS-NPLT") ; Define target layer to change rev clouds to  
(setq ss1 (ssget "X" (list (cons 0 "LWPOLYLINE")(cons 8 lay_name)))) ; Select all lwpolylines on the specified layer  
(setq n (sslength ss1)) ; Measure the number of entities in the selection set ss1  
(setq index 0) ; Set the variable called index to 0  
(repeat n ; Begin the loop that pages through the selection set  
(setq ent1 (entget (ssname ss1 index))) ; Get the entity list and assigns it to ent1  
(setq b1  
(subst (cons 8 lay_name_new)  
(assoc 8 ent1)  
ent1  
)  
) ; Change the layer code for each object in the set  
(entmod b1) ; Modify the the entity's layer in the drawing  
(setq index (+ index 1)) ; Increas the index variable by 1 and loop  
) ; Close the repeat loop  
(command "LAYER" "FREEZE" "A-ANNO-REVS-NPLT" "") ; Freeze the new layer  
(princ) ; Exit quitely  
) ; Close the function  
(c:chlayer) ; Run the function  
~~~~~~~~~~~~~~~ 

PS - I'm sure I swiped some of this code from various places around the internet. I'm not sure from where or when, but thank you to everyone posting and explaining their code. I'll do my best to contribute and attribute whenever possible.

