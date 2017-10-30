---
title: RZ
tags: ok
---

 **RZ**

  This command adds points to the mesh. It can distribute points
  evenly or according to a ratio zoning method.

  **xyz** specifies Cartesian coordinates.

  **rtz** specifies cylindrical coordinates.

  **rtp** specifies spherical coordinates.

  **line** this option implies xyz and will distribute n1 nodes from
  (xmin,ymin,zmin) to (xmax,ymax,zmaz)

  When using the rtz or rtp coordinate systems the center is at
  (0,0,0). Use a **trans** command to move the center. For the
  **rtz** command, minimum and maximum coordinates are the triplets:
  radius from the cylinder's axis, angle in the xy-plane measured from
  the x-axis and height along the z-axis. For the **rtp** command
  minimum and maximum coordinates are the triplets: radius from the
  center of the sphere axis, angle in the zy-plane measured from the
  positive z-axis and the angle in the xy-plane measured from the
  positive x-axis (see II.a.11). Note that the **rtz** always results
  in a (partial) cylinder of points centered around the z axis. Use
  the **rotateln** command to orient the cylinder. For example, to
  center the cylinder around the y axis, specify the x axis as the
  line of rotation in the **rotateln** command.
  ni,nj,nk number of points to be created in each direction.

  xmin,ymin,zmin minimums for coordinates.

  xmax,ymax,zmax maximums for coordinates.

  iiz,ijz,ikz if =0 then mins and maxs are used as cell centers

  if =1 then mins and maxs are used as cell vertices

  iirat,ijrat,ikrat ratio zoning switches (0=off,1=on)

  xrz,yrz,zrz ratio zoning value - distance is multiplied by this
  value for each subsequent point.

   

 **FORMAT:**

 **rz** **/xyz** **rtz** **rtp**ni,nj,nk/xmin,ymin,zmin/xmax,ymax,zmax/ iiz,ijz,ikz/[iirat,ijrat,ikrat/xrz,yrz,zrz/]

 **rz/line**/np///xmin,ymin,zmin,xmax,ymax,zmax/iiz,ijz,ikz/

 

 **EXAMPLES:**

      rz /xyz /5,3,10 /0.,2.,0. /5.,6.,2. /1,1,1/

 This results in a set of 150 points, five across from x=0. to x=5., 3
 deep from y=2. to y=6. and 10 high from z=0. to z=2.

      rz/rtz/4,6,11 /0.,0.,0. /3.,360.,10. /1,0,1/

 This results in 264 points arranged around the z- axis. There are 3
 rings of points at distances r=1., r=2. and r=3. from the z-axis.
 There are 11 sets of these three rings of points and heights z=0.,
 z=1., z=2.,...,z=10. In each ring there are 6 points where each pair
 of points is separated by 60°; note that ijz=0 requests that points be
 placed at cell centers, hence the first point will be at 30° not at
 0°. Corresponding to r=0, there will be 6 identical points at 11
 intervals along the z-axis at heights z=0., z=1., z=2.,...z=10.
 **Filter** should be used to remove these duplicate points.
