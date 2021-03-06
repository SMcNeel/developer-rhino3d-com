---
title: Setting Camera Angle
description: Demonstrates how to set the camera angle using RhinoScript.
author: dale@mcneel.com
apis: ['RhinoScript']
languages: ['VBScript']
platforms: ['Windows']
categories: ['Uncategorized']
origin: http://wiki.mcneel.com/developer/scriptsamples/cameraangle
order: 1
keywords: ['rhinoscript', 'vbscript']
layout: code-sample-rhinoscript
---

```vbnet
Sub TestSetCameraAngle()

  ' Local constants (could easily prompt for these...)
  Const horz_angle = 7.3
  Const vert_angle = 5.5
  Const horz_res = 1200

  ' Local variables
  Dim view, vert_res

  ' Current view must be a perspective view
  view = Rhino.CurrentView()
  If Not Rhino.IsViewPerspective(view) Then
    Call Rhino.Print("Select a perspective view and rerun the script.")
    Exit Sub
  End If

  ' Calculate vertical resolution based on existing parameters    
  vert_res = CInt(Round((vert_angle * 2) / (horz_angle * 2) * horz_res))

  ' Set the viewport size
  Call Rhino.Command("_-ViewportProperties _Size " & CStr(horz_res) & " " & CStr(vert_res) & " _Enter _Enter", 0)

  ' Set the viewing angle
  If (horz_res < vert_res) Then
    Call Rhino.Command("_-PerspectiveAngle " & CStr(horz_angle), 0)
  Else
    Call Rhino.Command("_-PerspectiveAngle " & CStr(vert_angle), 0)
  End If

End Sub
```
