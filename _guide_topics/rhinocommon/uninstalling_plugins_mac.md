---
title: Uninstalling Plugins (Mac)
description: unset
author: dan@mcneel.com
apis: ['RhinoCommon']
languages: ['C#']
platforms: ['Mac']
categories: ['Fundamentals']
origin: unset
order: 8
keywords: ['first', 'RhinoCommon', 'Plugin', 'removing', 'uninstalling']
layout: toc-guide-page
---


# Uninstalling Plugins (Mac)

This guide explains how to uninstall/remove plugins in Rhino for Mac.  This guide presumes you have plugins installed that you would like to remove.


## Overview

Rhino for Mac does not (yet) have a Plugin Manager.  However, uninstalling plugins is very easy.  You simply remove the plugin folder from the *~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/* folder[^1] and then restart Rhino.

## Step-by-Step

1. **Quit Rhino**, if it is current running.
1. In **Finder**, navigate to the *~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/* folder.  If you [can't find this folder](#user-library), you can do the following...
   1. In the **Finder** toolbar, in the **Go** menu, select **Go to Folder...**
![finder_go]({{ site.baseurl }}/images/uninstalling_plugins_mac_01.png)
   1. In the **Go to Folder** dialog, paste the following path:
   *~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/*
![paste_path]({{ site.baseurl }}/images/uninstalling_plugins_mac_02.png)
   1. Click **Go**.  A Finder window should open showing the contents of the folder.
1. **Remove** (move or delete) the plugin's folder from the *MacPlugIns* folder...
![drag_to_trash]({{ site.baseurl }}/images/uninstalling_plugins_mac_03.png)
1. **Restart** Rhino.


## Behind the Scenes

When Rhino for Mac launches, it searches the contents of the:

*~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/*

folder scanning the sub-folders recursively looking for *.rhp* files.  When it finds such file, Rhino for Mac attempts to load this plugin.  If it cannot find a plugin, it will not load said plugin...it's *that* simple.


#### User Library

By default, the User Library folder is hidden from view.  

To make your Library visible in the Finder:

1. In **Finder**, navigate to your **Home** (*~*) folder.  You must be in your Home folder for this to work.
1. Press **Command-J** to bring up the **Finder View** options dialog...
![finder_view_options]({{ site.baseurl }}/images/finder_view_options.png)
1. Check the **Show Library Folder** check box.  Now your Library should show up in the view.  You may want to drag this folder to your Favorites area of the Finder sidebar for easy access later.

---

## Related topics

- [Creating a Plugin Installer (Mac)]({{ site.baseurl }}/guides/rhinocommon/plugin_installers_mac/)

---

## Footnotes

[^1]: Do not confuse this path with */Library/Application Support/McNeel/Rhinoceros/*, which is the system-wide Library location.
