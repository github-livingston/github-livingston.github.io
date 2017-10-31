---
title: EXTRUDE
tags: ok
---

 **EXTRUDE**

  This command takes a topologically 1d or 2d mesh (a line, a set of
  line segments, or a planar or non-planar surface) and extrudes it
  into three dimensions along either the normal to the curve or
  surface (default), along a user defined vector, or to a set of
  points that the user has specified.

  If the extrusion was along the normal of the surface or along a user
  defined vector, the command can optionally find the external surface
  of the volume created and return that to the user.

 **FORMAT:**

  **extrude**/mesh1/mesh2/**constmin**/offset**/volumebubble**/[**norm**x1,y1,z1]

  OR

  **extrude**/mesh1/mesh2**/interp**/layers**/range1/range2**

  where **range1** and **range2** are defined as
  **[pset,get,** pset_name ** ** ifirst,ilast,istride **]**

 mesh1 is the name of the resulting mesh.

 mesh2 is the name of the initial mesh. This mesh must be made up of
 **lines, tris, quads, or hybrids**.

 **const** is a keyword that indicates that the distance from each of
 the points in the initial mesh along the extruding vector will be
 equal to offset.Therefore, if you wanted the extruded mesh to have the
 same surface or edge characteristics as the original mesh on both the
 initial and newly formed surface or edge, you would use **const**.

 ** min** is a keyword and indicates that the minimum distance along the
 extruding vector to a reference plane that is perpendicular to the
 extruding vector will be equal to offset. This means that if you want
 an extruded mesh with at least one flat side, you would use ** min**.
 This also means that if you use ** min**, extrude computes the "bottom
 point" on the initial mesh, or the point closest to the reference
 plane, and then extrudes that point by min, all the other points will
 therefore be extruded by a larger distance. This avoids the problem of
 having the initial mesh intersect the reference plane that forms the
 "bottom" of the created mesh.

 **interp** is a keyword and indicates a different kind of extrusion.
 Instead of giving the initial mesh a direction in which to be
 extruded, this keyword specifies that the initial mesh is made up of
 two sets of points to be connected. These point sets are defined by
 **range1** and **range2**. The ranges can be defined using the
 standard LaGriT techniques of **pset**, **get**, &lt;pset name&gt; or
 ifirst, ilast, istride.

 layers is the number of layers of elements that will be placed between
 the original two surfaces. This is a good point distribution
 technique. The final number of layers of points will be equal to
 layers+1. It must be an integer.

 offset is the length of extrusion. It can either be an integer or a
 real.

 **volume** is a keyword and indicates that the volume that was
 extruded is to be returned to the user (i.e., the operation will
 result in either a topologically 2d (quad) mesh if the initial mesh
 was topologically 1d, or a topologically 3d (prism or hex) mesh if the
 initial mesh was topologically 2d). **bubble** is a keyword and
 indicates that the external surface of the volume created will be
 returned. If bubble is used, hextotet will be called on the final
 surface, as well as extract.

 The final argument is optional. It must either be the keyword
 **norm**, or a three valued vector (in cartesian space) specifying a
 direction. The default, if no argument is provided, is **norm**. If
 **norm** is chosen, the element area weighted normal to the surface or
 curve is computed, and the initial mesh is extruded in that direction.
 Otherwise, if a vector value is specified, the vector is normalized,
 and its direction used to extrude the initial mesh.

 **NOTES:**

  This code works on meshes containing lines, quads, triangles, or
  hybrid polygons. If there are lines in the initial mesh, they become
  quads; tris become prisms; and quads become hexes. If bubble is
  used, however, lines are not permitted because they do not result in
  a mesh that extract and hextotet agree with. The code will error out
  in this situation.

  It is very possible to create an invalid mesh object with this
  command, especially if the initial mesh is a multivalued surface, or
  if the extruding vector is in a direction parallel to the plane the
  initial surface is in. You have been warned.

  If the **interp** keyword is used, the code expects the number of
  points in **range1** and **range2** to be equal, and to correspond
  such that the first point in **range1** will connect to the first
  point in **range2** in the final mesh object, etc. Other setups will
  result in a twisted, perhaps invalid mesh object.

 **EXAMPLES:**

  **extrude**/cmo\_hex/cmo\_quad/**const**/5.0**/volume**

  This would result in hexes being created out of the initial quad
  sheet. First, since **const** and **volume** are used, the quad
  sheet will be extruded a constant amount from each point. Second,
  since the extruding vector and **norm** are omitted, the extrusion
  will occur on the average normal to the plane. Therefore, this
  command will result in a mesh of hexahedrons extruded 5.0 units in
  an orthogonal direction. (Or, more succinctly, a mesh of
  parallelopipeds of height 5.)

  **extrude**/cmo\_prism/cmo\_tri**/ min**/10**/volume**/1,2,-1

  This command would result in prisms being created out of the initial
  tri sheet. First, since ** min** is used, the "bottom" of the
  extruded volume would be a plane. Second, because the vector 1, 2,
  -1 is specified, the extrusion will be in that direction (again the
  magnitude is not important, the vector is normalized to a unit
  vector), not in the direction of the average normal.

  **extrude**/cmo\_bigbox/cmo\_quad/**const**/5.0**/bubble**/

  This would result in a surface surrounding an amalgamation of
  parallelopipeds created from the initial quad sheet. First, since
  **const** is used the quads will be extruded a constant amount from
  each point in the quad sheet. Second, since the extruding vector and
  **norm** are omitted, the extrusion will occur on the average normal
  to the plane. Therefore, this command will result in a mesh of tris
  that form the surface of a group of parallelopipeds extruded 5.0
  units in an orthogonal direction.

  **extrude**/cmo\_arbshape/cmo\_tri**/ min**/7.5**/bubble**/3,-2.5,-6

  This command would result in a mesh of tris that form a surface
  enclosing a volume of prisms being created out of the initial tri
  sheet. First, since ** min** is used, the "bottom" of the surface
  would be a plane. Second, because the vector 3, -2.5, -6 is
  specified, the extrusion will be in that direction (again the
  magnitude is not important, the vector is normalized to a unit
  vector), not in the direction of the average normal of the initial
  tri surface.

  **extrude**/cmo\_prism/cmo\_tris**/interp**/14**/pset, get,**
  bottom**/pset, get,** top

  This command would result in a mesh of prisms being created out of
  the two sets of tri sheets in cmo\_tris as well as 14-1 layers of
  additional tris that would be interpolated. First, since interp is
  used, the pset defined by bottom would end up connected to the pset
  defined by top. Second, there would be 14 layers of elements that
  would be placed between the psets top and bottom, so that the
  resulting grid would have 15 layers of points that would be
  connected to one another to form prisms.
