---
layout: post
date: 2014-04-10
title: Life insurance calculation core
categories: programming
tags: [C#, Design Patterns, SQL, Visual Studio, TFS]
---

During my studies I worked part time in the life insurance math department at the
[GRAWE](http://www.grawe.at/en/index.htm). After smaller initial projects I started
working on a novel C#.net program for prototyping new life insurance products. It was
meant to replace a small TurboPascal program that was in use at the time and has long
exceeded its software complexity and memory limits.

**Problem**: Develop a calculation core to do calculations for all insurance products that
every existed in the company or any of its many subsidiaries.

<!--more-->

At first I thought that complex mathematical issues would be the biggest challenge.
However, life insurance math is mainly basics, like sums, probabilities, and interest
calculations. The tough challenges were to organize the code for calculating over 1000
different products without duplicating code, providing means to compute contract changes,
and having all this code tested within the small scale project.

{% include image_100.html src='/assets/2014-04-10-life-insurance-calc/ablebensformel.png'
                          descr='Life insurance formula' %}

I organized the code using established software engineering practices. Basic product
parameters are stored in a Microsoft SQL database. The C# code heavily uses design
patterns, a few examples are

* Strategy, to prevent duplicate code wherever possible,
* Proxy, to represent contract changes, and
* Abstract Factory, to provide unified creation and usage for different product families,
* Chain of Responsibility, to organize several rule systems with completely different
  structures.

Over time the small prototype project grew into a substantial solution. In the end my
calculation core was more powerful than any other core within the company, was easy to
extend, and covered the three main types of life insurance the company sold (“classic”
life insurance, unit-linked life insurance, and annuity insurance). It also came with its
own regression test suite.

After I finished my studies I was asked to replace the other existing calculation cores
with mine. When I left the company as agreed on after two years, I had successfully
replaced three existing calculation cores and my successors are working on replacing the
last remaining one.

The company also decided to start a similar project to replace the calculation cores for
the other insurance branches (non-life insurances). I helped with the initial design and
setup of this project and, as far as I know, it is doing well so far.

{% include image_100.html src='/assets/2014-04-10-life-insurance-calc/R3_masked.png'
                          descr='R3 - Direct interface for mathematicians' %}
