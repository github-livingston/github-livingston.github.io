---
GENERATOR: 'Mozilla/4.05C-SGI [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: RM
---

** ** 

 **RM**

  Removes any points that are within the specified point range and
  specified volume of space. This is done in Cartesian (**xyz**),
  cylindrical (**rtz**), or spherical (**rtp**) coordinates. It should
  be noted that in cylindrical coordinates, theta is the angle in the
  XY- plane with respect to the x-axis, while in spherical coordinates
  theta is the angle with respect to the Z-axis and phi is the angle
  in the XY-plane with respect to the X-axis. In cylindrical
  coordinates the cylinder always lines up along the z axis; use the
  **coordsys** command before issuing the **rm** command if the points
  to be removed are not aligned with the z-axis; then issue a final
  **coordsys** command to return to normal. Also note that the points
  that are removed become dudded out (point type set to 21) and are
  not removed from the data array.
 
  The other options are:
 
  geometry -- **xyz**, **rtz**, **rtp**

  ifirst,ilast,istride -- point range to search

  xmin, ymin, zmin -- minimums of geometry type coordinates

  xmax, ymax, zmax -- maximums of geometry type coordinates

  xcen, ycen, zcen -- center of removal space for geometry

  xscale, yscale, zscale -- scaling factors for geometry limits

 

 **FORMAT:**

  **rm** / geometry
  /ifirst,ilast,istride/xmin,ymin,zmin/xmax,ymax,zmax/ xcen,ycen,zcen
  / [xscale,yscale,zscale]

 EXAMPLE:

 **rm** **/xyz**/1,0,0/2.,2.,2./4.,4.,4./0.,0.,0./

 **rm/rtz**/1,0,0/0.,0.,0./1.,360.,10./0.,0.,0./
