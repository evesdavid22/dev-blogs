---
layout: post
title: Introduction, and the first project
subtitle: Welcome to the blog
gh-repo: evesdavid22/dev-blogs
gh-badge: [star, fork, follow]
tags: [intro,procedural-generation]
comments: true
---

This post is going to serve as an introduction to the blog and a brief summary of the first project I'm going to be blogging about on here.

This blog is currently aimed at documenting my experiences with procedural generation. Some posts may take the form of tutorials, but most will probably of the 'show off' variety with screenshots and short snippets of descriptions.

Future paths for the blog (>3 months out) could see it become a place to talk about game development or to pursue projects looking at subjects associated with procedural generation such as machine learning and data science.

## About myself

I am involved in software development and maintenance professionally, but my involvement is hands-off and far removed from the topics covered in this blog. As such I will avoid trying to 'teach' too much with this blog as there is a fairly large risk that I would be passing on incorrect or inefficient techniques.

I work entirely in C# (c-sharp or cs), though I've used Python, R, and Java in the past. I've been bitten by the game development bug so the majority of my posts here will use material generated in the Unity game engine ([Found here](https://unity.com/), alternatives are available). The end-goal of several projects may be to build small-to-medium-sized games using what's been learned so far.

## The first project

The first *big idea* I want to start work on is a map generator in the vein of, for example, [Azgaar's](https://azgaar.github.io/Fantasy-Map-Generator/). My primary goals for this project are:

1. The results should be verisimilitudinous - that is, someone should be able to look at the map and easily imagine what it might look like from the ground. There should be no obvious incongruities e.g. rivers that have no source and suddenly disappear.
2. The results should be somewhat scalable - I want to be able to generate large (in layman's sense, not in the computing sense) maps, or multiple small maps that exhibit continuity.
3. The project should be easily portable into a game engine such as Unity.

I am not constraining myself to performative code for two primary reasons: one is that I don't have a lot of spare time to be working on this project, and optimisation would eat up a huge chunk of it for not much reward (A game running such a generator would not be running it more than once or twice in a single session in any case); and two, I'm just not particularly good at it, especially not in a space that I have little experience in.

### Some inspiration, or Touchstones

There are several extremely successful implementations of procedural generation in maps out there right now. The first that I encountered and that got me started on this journey was [Dwarf Fortress](http://www.bay12games.com/dwarves/). 

|![DF Map](/assets/img/DF-Map.png){: .mx-auto.d-block :}|
|:--:|
|If you understand this, you've spent your time well.|

Of course, more contemporary map generators now exist. Such as the aforementioned Azgaar's, here are some others that you may have heard of:
* [Donjon](https://donjon.bin.sh/fantasy/world/)
* [Red Blob Games' map generator](https://www.redblobgames.com/maps/mapgen2/)
* [Sebastian Lague's procedural terrain](https://github.com/SebLague/Procedural-Landmass-Generation) (This one includes a companion tutorial series on Youtube!)

### A teaser for the next post

The next post, and official first post on this subject, is going to cover the initial shape of the map. It is probably going to mention **Voronoi diagrams**, **triangulation**, and **Perlin noise**.

