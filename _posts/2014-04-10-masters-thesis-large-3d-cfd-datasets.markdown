---
layout: post
date: 2014-04-10
title: Master’s Thesis on large 3d CFD datasets
categories: programming
tags: [C++, vtk, Qt, ParaView]
---

In my Master’s thesis I used C++ in conjunction with the [vtk](http://www.vtk.org/)
framework to process CFD datasets of up to two Gigabytes in size.

**Problem**: Cluster a large, dense, three-dimensional
[CFD](http://en.wikipedia.org/wiki/Computational_fluid_dynamics) simulation result into
homogeneous areas that can be used for graph based simulation and visualization.

<!--more-->

{% include image_50.html src="/assets/2014-04-10-masters-thesis/res-vis-1-twoinlets.png"
                         descr="A picture of an underhood CFD air flow simulation result"
                         %}

My work included custom pre-processing, the research and implementation of existing
algorithms, as well as the development of a new algorithm. Due to the research-typical,
open formulation of the problem statement, there is no closed, complete solution of the
problem. Nevertheless I pin-pointed the best existing clustering algorithm for the graph
based simulation. In addition I developed a useful graph based visualization technique for
exploring CFD datasets that utilizes my own clustering algorithm.

The abstract of my thesis captures the essence of my solution. The full thesis can be
downloaded at the end of this post.

> Results from computational fluid dynamics (CFD) simulations are generally complex and
> difficult to understand. This work proposes a new method that computes from a given
> simulation result, e.g., the underhood flow of air around a car engine, a sparse>
> directed graph network with a few hundred nodes. The goal is a graph that preserves the
> essential properties of the flow in such way that it is suitable for applications
> ranging from> information visualization to flow simulation. The algorithm finds bundles
> of similar streamline segments, which are then mapped back to the original dataset in
> order to produce a> complete partition. A flow graph is derived from this partition by
> integration over the CFD cells. By utilizing a custom-built simulation framework, the
> proposed method is shown to produce meaningful graphs, which can be used within the>
> mentioned application areas.

The work was carried out for the [Virtual Vehicle Research Center](http://www.v2c2.at/en/)
and supervised by Sven Havemann of the [CGV (TU
Graz)](https://www.tugraz.at/institutes/cgv/home/). You can download it below.

---

[Download Master’s
Thesis](/assets/2014-04-10-masters-thesis/Thesis_Hopfer_FINAL_ONLINE_2011-12-05.pdf)
