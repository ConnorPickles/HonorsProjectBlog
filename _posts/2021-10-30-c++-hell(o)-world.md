---
layout: post
title:  "C++ Hell(o) World"
date:   2021-10-30 2:59:00 -0800
categories: ue5 c++
---

Today's session of work started off with the goal of adding some Esri ground cover data to the existing LiDAR data in Unreal. Is that what happened? Far from it, but we'll get to that.

## Odds and Sods

I forgot to mention in the last post that I had looked into some C++ libraries that can handle point cloud data, specifically in the `.laz` format. While I haven't dug too deeply into any particular library, it looks like they [do exist](https://pdal.io/api/cpp/index.html).

I also came across a method of adding some more definition to the point cloud, courtesy of the [Unreal docs](https://docs.unrealengine.com/4.27/en-US/WorkingWithContent/LidarPointCloudPlugin/EnableEyeDomeLightingMode/). It does add a lot of definition, but the image is quite jittery even when the camera isn't moving:

![](../../../../images/test_with_ppv.png)

Anyway, time to look at that ground cover data. Downloading the data itself was pretty simple. However, here is a photo of the smallest tile I was able to find (the blue lines are a single tile).

![](../../../../images/ground_cover_tile.png)

Hmmmm. Alright, a tad more data than I need, but it's accurate up to 10 meters which isn't terrible. The annoying part is that the data is provided as a Tagged Image File Format (`.tif`), which Unreal doesn't support (that didn't stop me from trying to import it twice, crashing Unreal after a minute or so each time). I realized that I wasn't going to be able to use the ground cover data to remove and points from the LiDAR data within Unreal, which meant it was finally time to start creating my own C++ code.

## Creating a Custom C++ Class (Part 1/?)

Unfortunately there isn't a great deal to write about regarding the progress I made, as most of my time was spent trying to get Visual Studio and Unreal to play nice. I'm attempting to create my own barebones class and instantiate it to prove I can hook in to the code. To do this I added a new C++ class from within Unreal and selected the "None" option, meaning the new class would not inherit from an existing class and only contained a default constructor/deconstructor. I then attemped to edit my new class, using the existing `MyGameModeBase` as a template since it's essentially empty to start. I won't go into the details of the entire process as it involved a lot of googling and restarting VS/Unreal, so here's what I learned:

  - There is no good way to delete a C++ class in Unreal. You have to close Unreal and VS, delete a bunch of folders as well as the solution file, then rebuild the VS project after deleting the source files of the class you want to remove.
  - When attempting to hook a class into Unreal's reflection system:
    - The class must inherit from something, and every class in Unreal is a child of `UObject` (I thought I was done with Java)
    - The actual class name must add the [appropriate prefix](https://docs.unrealengine.com/4.27/en-US/ProductionPipelines/DevelopmentSetup/CodingStandard/)
    - All implemented methods must also use this prefix
    - You must `#include` the class that you want to inherit from
  - Using `UObject` instead of `AActor` comes with some quirks. I wound up following [this article](https://geeks-world.imtqy.com/articles/475622/index.html) as a guide.

I'm currently at the point where I can open and edit the event graph for my class, and it can be referenced by other blueprints in Unreal (I know this because it appears in certain dropdown menus). The next problem I'm working on is actually instantiating the class so I can run my code.

My current plan is to use custom C++ classes to overlay various data. This will mean finding a way to import and work with every data format I need. Once this is done, I should be able to procedurally objects to the world through some combination of C++ and blueprints. What is abundantly clear to me now is that any comparison of data will have to be done in custom C++ code, and Unreal will primarily be used to display the result.