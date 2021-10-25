---
layout: post
title:  "Creating a Blog"
date:   2021-10-20 17:20:00 -0800
categories: blog github-pages themes
---

You know, I was hoping that setting this up wouldn't take more than an hour, but as always with tech it wound up taking way longer with way more headaches than I had hoped for.

After the meeting from earlier in the week, I decided I would take the recommendation and set up a blog to chronicle the journey of working on this project. I briefly thought about the best platform to set this up on. Derek had mentioned something about a node.js setup, but I'm not particularly experienced with node.js and I had no desire to jump down that particular rabbit hole. I didn't want anything fancy. Fortunatley, I remembered that [GitHub Pages](https://pages.github.com/) exists. GitHub offers free website hosting for each repository you own, and I had set up a repository a few years back to host a project I was working on at the time. I figured it would be rather simple to set up a basic blog in this way. Blogs are a super common website format, surely the process woudn't be too bad.

*sigh*

Creating a new repository for the blog and getting a homepage set up was easy peasy. Initialize a repo, enable GitHub Pages, pick a theme. No problem. Unfortunately, none of the default themes GitHub provides seemed to support the blog format. Alright, that's fine, a quick google search brought up a [tutorial](https://www.kiltandcode.com/2020/04/30/how-to-create-a-blog-using-jekyll-and-github-pages-on-windows/) on how to create a blog using Jekyll and GitHub Pages (Jekyll is the tool that GitHub Pages uses to serve your website). I followed this tutorial, making sure to change the config to my desired title, url, theme, etc. I eagerly pushed my changes, only to find that I had completely broken my site.

What followed was an hour or more of googling, attempting various combinations of settings, resetting the site a few times, all in an attempt to get the thing to work. In the end, my problem was that I was trying to change the theme. Not all themes are compatible with the blog format, and every theme can customize the config it requires. By trying to apply multiple themes to the same config, I was breaking the site. After figuring this out I attempted to use a non-default theme I liked that supported a blog format, but I was still unsuccessful in getting the site to display anything. I eventually resigned myself to using the default theme, not wanting to spend any more time setting up the blog for the day. I may revisit the theme in the future, but for now it's at least working. Let's hope it stays that way.