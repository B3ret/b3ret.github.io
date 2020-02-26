---
layout: post
date: 2015-09-16
title: vtkBioeng for vtk 6.2
categories: programming
tags: [C++, vtk]
---

For an upcoming mesh collision problem in one of my C++/vtk/Qt projects I wanted to try
the collision filter in the vtkBioeng package
([website](http://www.bioengineering-research.com/software/vtkbioeng), [git
repository](https://github.com/glawlor/vtkbioeng)). However, the current source code is
not compileable with vtk 6.x, because backwards compatibility with vtk 4.x code was
removed.

<!--more-->

I therefore adapted the CMake scripts and source code myself to make it compile with vtk
6.2. Since I’m not an expert in vtk module development, I don’t want to integrate my
changes into the original repository and therefore uploaded the changes to my own public
[git repository](https://github.com/B3ret/vtkbioeng6).

I basically just applied all the steps listed in the migration guides from the following
sources:

{% include image_50.html src="/assets/2015-09-16-vtkbioeng-for-vtk62/vtkbioeng-1024x911.png"
                         descr="Output of vtkbioeng test case" %}

* [vtk wiki migration guide](https://vtk.org/Wiki/VTK/VTK_6_Migration_Guide)
* [vtk wiki build system migration](https://vtk.org/Wiki/VTK/Build_System_Migration)
* [mitk migration guide](http://www.mitk.org/wiki/VTK6_Migration_Guide)

I’m pretty sure some additional work can and needs to be done, especially in the CMake
script, but these changes seem to work well enough for me. You can see the output of the
first test case on the right.

Known issues:

* Only tested with C++. I’m pretty sure the wrappers (TCL? Java?) don’t work
* Not tested thoroughly. (The first testcase looks ok, the second one seems to behave
  weirdly.) However, I will update the repository in case I make further changes  once I
  start using the filter in my production code..-.

**Update 2020-02-26**: I'm moving my website to GitHub pages and in the process I'm
tidying up the wording of this article and getting rid of the comment section. However,
I'm migrating useful old comments onto here as well (anonymized):

---

> M., June 23, 2016 at 10:59:  
> Great, I Just had to add a definition in vtkCollisionDetectionFilter.h :  
> `#define VTK_LARGE_FLOAT 1.0e+38F;`  
> to compile it with vtk 6.3
>
> I’m trying it now...

---

> G., November 25, 2016 at 09:43:  
> Thanks for all you efforts , it will grately help ful all the vtk comunity
>
> G., November 28, 2016 at 17:04:  
> Hi, i am getting folowing error when confugure using cmake , am unble resolve this
> please tell if have any idea
>
> `Error : VTK_MAKE_INSTANTIATOR2`  
>
> G., November 28, 2016 at 17:15:  
> Hi, i am getting folowing error when confugure using cmake , am unble resolve this
> please tell if have any idea
>
> `Error : VTK_MAKE_INSTANTIATOR3`
>
> note: sorry for last message

(I couldn't find the solution for this person)

---

> A. (Maintainer of vtkbioeng), June 25, 2018 at 18:00:  
> Thanks Benjamin that s been on my todo list for a while. I ll test out your 6.2
> migration and integrate your code.
