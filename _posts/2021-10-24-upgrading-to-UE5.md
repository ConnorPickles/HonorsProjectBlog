---
layout: post
title:  "Upgrading to UE5"
date:   2021-10-24 23:49:00 -0800
categories: lidar ue5 lighting
---

Time to make the jump to UE5. While this process wasn't completely smooth, things certainly went much better than I had originally thought.

The first error I ran into was to do with disk space. After installing UE5, I only had around 1GB of disk space left. The installer actually came up with a warning and recommended that I free some space up. Upon opening the editor I immediately noticed that a good portion of the icons looked as if they had had their [pixels scrambled...](http://henrysprojects.net/projects/cv-image-scramble.html) probably a sign that I needed to take the warning seriously. I downloaded WizTree (after recently hearing that it was a much better alternative to WinDirStat) and started deleting/uninstalling a few key things. After freeing up some space and restarting Unreal, the icons looked a lot more normal.

First, I took a moment to familiarize myself with UE5's interface. It's mostly identical to UE4, with the exception of the content browser which now disappears by default when it loses focus, clearing up more space for the viewport. Combine this with the more modern look and I'm already enjoying UE5 more than UE4. I didn't dwell on this thought for long though, as I wanted to see how lucky I would be with plugin support. In UE4, I enabled the LiDAR plugin simply by opening the plugins menu and enabling it. As luck would have it, the same thing worked for UE5! I was quite relieved that I wouldn't have to come up with my own mechanism for importing the data.

I moved along, re-creating the time of day slider in UE5. This process was relatively uneventful. Along the way I noticed that the SkySphere was really messing up the lighting in the evening since it seemed to contain it's own static sun that was lighting the scene. By setting the "Sun Brightness" to 0 I was able to eliminate this issue, and even see some starts when I looked up! I also tried editing the point cloud this time, as clicking on the "Edit Mode" option no longer provided a warning about loading the entire point cloud into RAM. I figured that UE5 might be doing some more intelligent memory management behind the scenes! This was quickly disproven a minute or two into playing around with the edit mode when Unreal completely crashed. A lesson in not completely relying off autosave...

Before I wrapped up for the evening, I took a quick look a couple more things. First, I loaded up the Quixel Bridge and signed in. Surprisingly I couldn't find a simple water texture! I also tried to look at C++ code for the LiDAR data, and finding the option to create a new C++ class was a bit of a pain since it's in a different spot now in UE5. After I created a dummy class I was able to generate a Visual Studio project and open it up. I poked around in the source files for the LiDAR plugin, as I believe I will have to look at individual points eventually and I will likely have to use C++ to do that. 

As I was writing this post, I stumbled across a console variable for the LiDAR plugin, ```r.LidarPointBudget```, with a default value of ```1000000```. Hold on, how many points are in this cloud?? 85,745,754. I've only been seeing a fraction of the points! Below is a comparison of the two point limits. Increasing the point budget enough to see all the points **drastically** reduces performance, so while it's quite interesting to see individual trees in immense detail, I won't be able to use all the points on a regular basis.

![](../../../../images/initial_test_ue5.png) ![](../../../../images/all_points.png)