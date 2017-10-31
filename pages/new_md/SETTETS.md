---
GENERATOR: 'Mozilla/4.7 [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: SETTETS
---

 

 **SETTETS**

Set element color **(**itetclr) and create child points at interior
interfaces. This command can also be used to set the node color from the
element color.

If there are no options **settets** and **settets/color\_tets** sets the
color of all elements using the following tests. If the element contains
a non-interface point, the element color is set to this value. If the
element is comprised entirely of interface points, the centroid of the
element is calculated and the material region containing this point is
determined; the element color is set to this material. If the centroid
of the element is not in any material region, the centroid must be on an
interface surface. In this case all vertices of the element are examined
and the material common to all vertices is selected as the element
color.

**settets**/ **parents** has exactly the same behavior as **settets**
except that existing values of itetclr are used for elements containing
non-interface nodes.

**geometry**  sets the  element color  based on the material region
containing the centroid of the element for all elements; existing values
of itetclr are ignored.

**color\_points**  sets the node material (imt1) from the element color
(itetclr); existing values of itetclr are not changed.

**settets/newtets** has the same behavior ** ** as **settets** except
that existing positive values of itetclr are not changed.

**settets/normal** assigns the itetclr array of a triangle mesh to an
integer value depending on the normal vector direction.  There are 26
possible direction that correspond to the 6 faces, 12 edges and 8
corners of a cube.  In general most triangles will be assigned one of 6
values which correspond to the 6 sectors which are within  degrees of
the 6 unit vectors: 1 0 0 , 0 1 0 , 0 0 1, -1 0 0, 0 -1 0, 0 0 -1

NOTE:  Valid only for triangle mesh.

 

 

**FORMAT:**

**settets**

**settets** **/parents**

**settets** **/geometry**

**settets** **/color\_tets**

**settets** **/color\_points**

**settets/normal**
