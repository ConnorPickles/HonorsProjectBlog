---
layout: post
title:  "Wrapping Up"
date:   2021-11-29 1:40:00 -0800
categories: ue5 c++ pdal
---

The timeline for this project is coming to a close, so it's time for me to talk about the issues I've been stuck on recently.

## VCPKG Issues

My last post ended with me attempting to install pdal using vcpkg, and encountering problems with curl installing. There are numerous threads online about this sort of problem. Unfortunately for me, my particular issues don't seem to line up with any of them. I tried clearing out vcpkg completely and re-building everything while specifiying `x64-windows` as recommeneded [here](https://stackoverflow.com/questions/59291118/a-suspected-bug-in-vcpkg-curl-on-windows). I tried every solution I could from [this thread](https://github.com/microsoft/vcpkg/issues/14524). ~~I even made a small blood sacrifice to Microsoft~~. Sadly, nothing was able to get vcpkg working, and pdal remains uninstalled on my machine.

## Docker

I remembered that my supervisor had recommended using Docker for future projects, to ensure a clean environment. I figured that, although late in the game, it might be worthwhile to try incorporating Docker into this project; perhaps I would be able to install pdal. Not long into the process of installing and learning the basics of Docker, I realized that getting Visual Studio to work with Docker would be a bit of a challenge (Windows vs Linux). I still read through the Docker tutorial as I didn't really understand what Docker did or why it was important before, so it was an interesting and valuable read. I also had to install WSL in order to install Docker, which was actually quite welcome as I really enjoy WSL and hadn't gotten around to installing it on my new machine.