---
title: TRANS
tags: ok
---

 **TRANS**

In the first form of this command, **trans** translates a selected set
of points (ifirst,ilast,istride) in X,Y,Z space by picking one specific
point (xold,yold,zold) in the set of points and moving it to new
coordinates (xnew,ynew,znew) with a linear translation. This will then
cause the remaining points in the set to be moved by the same
translation.

In the second form, if enter is selected, the points set is
translated so that (0,0,0) is located at the midpoint of min x,y,z and
max x,y,z of the mesh. If **zero** is selected, the points set is
translated so that (0,0,0) is located at the min x,y,z of the mesh. If
**original** is selected, the points set is translated to the original
location before **enter** or **zero** was called. Currently all
translations are **xyz** (**rtp** and **rtz** are reserved for future
implementation). The values in the next optional field indicate the axes
along which to translate. For example, 1,1,0 or x,y will translate along
the x and y axes, the z values will not change.

**FORMAT:**

**trans**/ifirst,ilast,istride/xold,yold,zold/xnew,ynew,znew

**trans**/ifirst,ilast,istride/**enter** **zero** **original**/[**xyz** **rtp** **rtz**]/ [xdim,ydim,zdim]

EXAMPLE:

**trans** **/pset,get,** mypoints/0.,0.,0./2.0,2.0,0./

The points in the **pset** mypoints will be moved 2 in the positive x
direction and 2 in the positive y direction.

[Click here for demos](../demos/main_trans.md)
