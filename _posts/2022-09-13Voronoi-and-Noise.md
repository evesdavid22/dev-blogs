---
layout: post
title: Voronoi and Noise
subtitle: Building blocks of generation
tags: [voronoi, noise, perlin, unity, unityengine, procedural_generation, procgen]
readtime: true
published: false
---

# The Blank Slate

I find the most intimidating part of projects is always in the beginning, when you have an empty solution (or project window, in my case) and lots of ideas running around your head that you really want to put down in writing before they flit away.

Lucky, then, that I started the blog when I was just past the start line on this project. As stated previously, I'm working in **Unity**, specifically Unity 2021.3.4f1 which I believe is a LTS version. I'm only using the bare 2D template - one starting scene in 2D camera mode, with one directional light that does precisely nothing to 2D icons.

The first idea I want to explore is one carried out by several far better developers in the past, the idea that a rectangular polygon (the map) can be partitioned into a set of polygons that, if joined back together, would reform the map. These polygons represent different subregions of the map, and are used to define things such as riverways and roads.

Here are some inspirational posts based on this idea:
* [Pierre Vigier's _Vagabond_ game blog](https://pvigier.github.io/2019/05/12/vagabond-map-generation.html)
* [Amit Patel's Polygonal Map Generation for Games](http://www-cs-students.stanford.edu/~amitp/game-programming/polygon-map-generation/)
* [Red Blob Games' Voronoi maps tutorial](https://www.redblobgames.com/x/2022-voronoi-maps-tutorial/)

As stated in _About Me_, I don't have an enormous amount of time for building my own implementations of various algorithms. There is also an element of reinventing the wheel here as almost all of the algorithms I will be using have already been implemented in C# by somebody else in a much more efficient manner. So I searched around and found a few really good libraries to test implementations of Voronoi diagrams inside Unity.

Before I dive into those libraries and which ones I chose to use, I'm going to add a quick couple of notes here on the various algorithms and key definitions in play, in case you aren't already familiar with them (if you are, feel free to skip to the next header, 'Shoulders of Giants'):

## Primer on geometry

These are simplified definitions that are just useful for a basic understanding of what's going on 'under the hood' here. For a more detailed exploration of geometry and topology, check out these sources:

* [Introduction to Topology, by University of Michigan students](https://www.math.colostate.edu/~renzo/teaching/Topology10/Notes.pdf) - Despite the foreword's disclaimer, a very helpful source on understanding topology, which is part of the mathematics underlying computer graphics. Be warned, however, it is quite dry and requires a bit of background knowledge of mathematics to fully understand.
* [Introduction to Computer Graphics, by David J. Eck](https://math.hws.edu/eck/cs424/downloads/graphicsbook-linked.pdf) - More accessible than the above, mainly concerned with JavaScript and OpenGL with some references to Blender and image manipulation programs. Probably more relevant to what we are doing here.
* [Catlike Coding's great tutorials on procedural meshes in Unity](https://catlikecoding.com/unity/tutorials/procedural-meshes/) - By far the most relevant, Catlike Coding's tutorials are invaluable resources for understanding not just everything I'll mention here but several topics that I wouldn't dare touch for their complexity. Jasper Flick exhibits the enviable combination of a deep understanding of subject matter and the ability to impart it in understandable terms to his audience.

For this project, I'll need an understanding of the following key definitions:

* **Vertex/Vertices** - A point or points in space, in our case represented by a 2-dimensional vector (x,y). Multiple vertices collected together can describe part of a polygon.
* **Edge** - The line joining two vertices.
* **A polygon** - Any shape consisting of vertices and edges that connect them.
* **Triangulation** - The name of the process that takes a number of vertices and collects them together in triangles, drawing edges between each pair of vertices that are part of the same triangle.

Game engines take polygons and triangulate them in order to display them on the player's computer. They keep the number of computations required to display graphics low.

Unity has terminology of its own to describe certain things. In particular, a collection of vertices with triangles that connect them is called a **Mesh**, which is displayed to the player using a **Mesh Renderer**. Developers can build meshes using scripting as long as they generate vertices and triangles and feed them into Unity's mesh constructor in the right way.

The above definitions lead into these key ideas:

* **Delaunay triangulation** - An algorithm that takes in vertices and triangulates them. A lot more complex than it sounds (involving things like checking circumcircles) which is why we lean on a published library to carry out the algorithm.
* **Voronoi diagram** - Also known as the 'Dual' of the Delaunay triangulation, which is what you get when you join all the points at the center of the circumcircles generated by the Delaunay triangulation.

For some neat image references, see the [relevant Wikipedia page](https://en.wikipedia.org/wiki/Delaunay_triangulation).

This is an example of the end result I am looking for when I want to generate a Voronoi diagram in Unity:

![A Voronoi diagram](https://github.com/evesdavid22/dev-blogs/blob/ac29e4664424481188b01d034b72781cccefe1f9/assets/img/A_Voronoi_Diagram.png)

# Shoulders of Giants
