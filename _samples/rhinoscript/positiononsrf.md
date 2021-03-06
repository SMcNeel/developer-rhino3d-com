---
title: Positioning Objects on a Surface
description: Demonstrates how to positioning objects on a surface using RhinoScript.
author: dale@mcneel.com
apis: ['RhinoScript']
languages: ['VBScript']
platforms: ['Windows']
categories: ['Uncategorized']
origin: http://wiki.mcneel.com/developer/scriptsamples/positiononsrf
order: 1
keywords: ['rhinoscript', 'vbscript']
layout: code-sample-rhinoscript
---

```vbnet
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
' PositionOnSrf.rvb -- February 2009
' If this code works, it was written by Dale Fugier.
' If not, I don't know who wrote it.
' Works with Rhino 4.0.
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
Option Explicit

Sub PositionOnSrf

  Dim objs, srf, box, p0, p1, pt, arr, i

  objs = Rhino.GetObjects("Select objects to position on surface")
  If IsNull(objs) Then Exit Sub

  srf = Rhino.GetObject("Select surface", 8)
  If IsNull(srf) Then Exit Sub

  Rhino.EnableRedraw False

  For i = 0 To UBound(objs)
    box = Rhino.BoundingBox(objs(i))
    If IsArray(box) Then
      p0 = box(0)
      p1 = box(2)
      pt = Array((p1(0)+p0(0))/2,(p1(1)+p0(1))/2,(p1(2)+p0(2))/2)
      arr = Rhino.ProjectPointToSurface(pt, srf, Array(0,0,1))
      If IsArray(arr) Then
        Rhino.MoveObject objs(i), pt, arr(0)
      End If
    End If
  Next

  Rhino.EnableRedraw True

End Sub

'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Rhino.AddStartupScript Rhino.LastLoadedScriptFile
Rhino.AddAlias "PositionOnSrf", "_NoEcho _-RunScript (PositionOnSrf)"
```
