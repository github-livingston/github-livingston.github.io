---
GENERATOR: 'Mozilla/4.05C-SGI [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: FIELD
---

 

 **FIELD**

  The FIELD Command option manipulates one or more specified fields in
  the Current Mesh Object
 
  
*For all points in the specified point set, we compose the field
  value with the specified composition function. The composition
  functions allowed are currently **asinh** and **log**. So, for
  example, if 'i' is in the point set and **asinh** is the composition
  function, we have the assignment:
 
   field(i) = asinh(field(i)).
 
  
*The **field** **/mfedraw** command causes a binary dump of the
  specified fields to two files in the **mfedraw** input format.
  **mfedraw** is a graphics package for visualizing moving piecewise
  linear functions of two variables, such as those originally
  encountered in Moving Finite Elements. The files are named
  'root1.bin' and 'root2.bin', where 'root' is the root file name
  argument. Because the graphics data are a function of two variables,
  you must supply two orthonormal vectors (x1,y1,z1) and (x2,y2,z2)
  which specify the graphics coordinate axes. More precisely, given 3D
  coordinates (x,y,z), the 2D graphic coordinates will then be
  (x
*x1+y
*y1+z
*z1 , x
*x2+y
*y2+z
*z2). So, for example, the
  choice:
 
   /x1,y1,z1/x2,y2,z2/ = /1.,0.,0./0.,1.,0./
 
  causes the 'z' coordinate to be discarded while the 'x' and 'y'
  coordinates are unchanged.
 
  
*The **field** **/scale** option scales the field values of the
  specified points. scale option can take on the values **normalize**,
  **multiply**, and **divide**. If **normalize** is specified, we
  multiply all the field values by **factor**/(fieldmax-fieldmin),
  where 'fieldmax' and 'fieldmin' are the maximum and minimum values
  taken over the point set. This has the effect of normalizing the
  field so that the new difference between the maximum and minimum
  values is equal to **factor**. If **multiply** is specified, we
  multiply all the field values in the point set by **factor**. If
  **divide** is specified, we divide all the field values in the point
  set by **factor.**
 
  
*The **field** **/volavg** option, for all the members of the point
  set and for all specified fields, replaces the point field values
  with values that represent the average of the field(s) over the
  control volumes associated with the points. The averaging option
  specifies what kind of control volume is to be used; the choices are
  **voronoi** and **median**. iterations is an integer that specifies
  a repeat count for how many times this procedure is to be performed
  on the field(s). The affect of this process is to broaden and smooth
  the features of the field(s), similar to the effect of a diffusion
  process. The **voronoi** choice, unlike the **median**. choice,
  produces a diffusive effect independent of mesh connectivity.
  However, again unlike the **median**. choice, it requires that the
  mesh be Delaunay, or incorrect results will occur.

 **FORMAT:**

  **field** **/compose**/composition
  function/ifirst,ilast,istride/field list/

  **field** **/mfedraw**/root file name/x1,y1,z1/x2,y2,z2/field list/

  **field/scale **/scale option/factor/ifirst,ilast,istride/ field
  list /

  **field** **/volavg**/averaging
  option/iterations/ifirst,ilast,istride/filed list/

 **EXAMPLES:**

  **field** **/compose** **/asinh**/1,0,0**/field** **/scale** **/normalize**/4.**field** **/volavg** **/voronoi**/4/1,

  

