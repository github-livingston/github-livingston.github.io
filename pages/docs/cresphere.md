---
GENERATOR: 'Mozilla/4.7 [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: RZS
---

 **CREATEPTS/SPHERE**

Builds a sphere by generating coordinates of points and also modifies
zoning by ratio-zoning point distributions. See the **rz** command for
more details. The ** ** itype flag defines what type of sphere will be
generated.

itype=1 generates a sphere by gridding the faces of a cube and then
projecting the vertices onto a sphere. The number of nodes per shell is
of the form 6
*i
*
*2.

itype=2 generates a sphere by subdividing an icosahedron placed on the
surface of a sphere.

Icosahedral gridding is made up of 10 diamonds per shell. Each diamond
is made up of n
*
*2 nodes (where n must be of the form 2
*
*i+1). There
are 2 nodes (the poles of the sphere) at which 5 diamonds meet and 10
nodes where 3 diamonds meet; hence there are a minimum of 12 nodes per
shell. The number of nodes per shell can be 12, 42, 162, 642,...

itype= 1 or 2 or diamond distributes points only, call **connect** to
generate connectivity information.

nr is the number of radial shells

npt is the upper limit of the number of points in a shell

itype=8 generates a hexahedral icosahedron grid. This option distributes
points and generates the grid connectivity data structures.

xirad,xorad are the inner and outer radii of the sphere. For itype=8
reverse inner and outer radii.

xcen,ycen,zcen are the coordinates of the center of the sphere

iz  if =0 then mins and maxs are used as cell centers

         if =1 then mins and maxs are used as cell vertices

irat is ratio zoning switch (0=off,1=on)

rz is ratio zoning value - distance is multiplied by the value for each
subsequent point.

itype = diamond generates the points for one diamond of the icosahedron

**FORMAT:**

**createpts/sphere**/itype/nr,npt,xirad,xorad/xcen,ycen,zcen/iz/irat,rz

**EXAMPLES:**

         createpts/sphere/8/5/162/1.0,0.5/0.,0.,0./1,0,0.0/

         createpts/sphere/2/5/162/0.5,1.0/0.,0.,0./1,0,0.0/

         createpts/sphere/diamond/5/162/1,.5/0,0,0/1,

 

