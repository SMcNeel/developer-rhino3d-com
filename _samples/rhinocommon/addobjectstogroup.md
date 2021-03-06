---
title: Add Objects to Group
description:
author:
apis: ['RhinoCommon']
languages: ['C#', 'Python', 'VB.NET']
platforms: ['Cross-Platform']
categories: ['Adding Objects']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/addobjectstogroup
order: 1
keywords: ['add', 'objects', 'group']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result AddObjectsToGroup(Rhino.RhinoDoc doc)
  {
    Rhino.Input.Custom.GetObject go = new Rhino.Input.Custom.GetObject();
    go.SetCommandPrompt("Select objects to group");
    go.GroupSelect = true;
    go.GetMultiple(1, 0);
    if (go.CommandResult() != Rhino.Commands.Result.Success)
      return go.CommandResult();

    List<Guid> ids = new List<Guid>();
    for (int i = 0; i < go.ObjectCount; i++)
    {
      ids.Add(go.Object(i).ObjectId);
    }
    int index = doc.Groups.Add(ids);
    doc.Views.Redraw();
    if (index >= 0)
      return Rhino.Commands.Result.Success;
    return Rhino.Commands.Result.Failure;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function AddObjectsToGroup(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim go As New Rhino.Input.Custom.GetObject()
	go.SetCommandPrompt("Select objects to group")
	go.GroupSelect = True
	go.GetMultiple(1, 0)
	If go.CommandResult() <> Rhino.Commands.Result.Success Then
	  Return go.CommandResult()
	End If

	Dim ids As New List(Of Guid)()
	For i As Integer = 0 To go.ObjectCount - 1
	  ids.Add(go.Object(i).ObjectId)
	Next i
	Dim index As Integer = doc.Groups.Add(ids)
	doc.Views.Redraw()
	If index >= 0 Then
	  Return Rhino.Commands.Result.Success
	End If
	Return Rhino.Commands.Result.Failure
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext

def AddObjectsToGroup():
    go = Rhino.Input.Custom.GetObject()
    go.SetCommandPrompt("Select objects to group")
    go.GroupSelect = True
    go.GetMultiple(1, 0)
    if go.CommandResult()!=Rhino.Commands.Result.Success:
        return go.CommandResult()

    ids = [go.Object(i).ObjectId for i in range(go.ObjectCount)]
    index = scriptcontext.doc.Groups.Add(ids)
    scriptcontext.doc.Views.Redraw()
    if index>=0: return Rhino.Commands.Result.Success
    return Rhino.Commands.Result.Failure


if __name__ == "__main__":
    AddObjectsToGroup()
```
{: #py .tab-pane .fade .in}
