---
layout: code-sample-rhinoscript
title: Scripting the Split Command
author: dale@mcneel.com
platforms: ['Windows']
apis: ['RhinoScript']
languages: ['VBScript']
keywords: ['rhinoscript', 'vbscript']
categories: ['Uncategorized']
description: Demonstrates how to script the Split command using RhinoScript.
origin: http://wiki.mcneel.com/developer/scriptsamples/splitbrep
order: 1
---

```vbnet
Function DoBrepSplit(brep, cutter)

   ' Declare local variables
   Dim saved, cmd

   ' Set default return value  
   DoBrepSplit = Null

   ' For speed, turn of screen redrawing
   Rhino.EnableRedraw False

   ' Save any selected objects
   saved = Rhino.SelectedObjects

   ' Unselect all objects
   Rhino.UnSelectAllObjects

   ' Select the brep
   Rhino.SelectObject brep

   ' Script the split command
   cmd = "_Split _SelID " & cutter & " _Enter"
   Rhino.Command cmd, 0

   ' By preselecting the brep, the results of
   ' Split will be selected. So, get the selected
   ' objects and return them to the caller.
   DoBrepSplit = Rhino.SelectedObjects

   ' Unselect all objects
   Rhino.UnSelectAllObjects

   ' If any objects were selected before calling
   ' this function, re-select them
   If IsArray(saved) Then Rhino.SelectObjects(saved)

   ' Don't forget to turn redrawing back on
   Rhino.EnableRedraw True

End Function
```