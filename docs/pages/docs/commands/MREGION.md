---
title: MREGION
tags: ok
---

**MREGION**

Define a material region from a set of surfaces by logically
combining the surface names and region names. A material region may
be removed from the geometry by specifying the release keyword.
To define material rgion, the operator **lt, le, gt**, and **ge**
are applied to previously defined surfaces according to the
following rules.

**lt** -- if the surface following is a volume then **lt** means inside
not including the surface of the volume. If the surface is a plane or a
sheet lt means the space on the side of the plane or sheet opposite to
the normal not including the plane or sheet itself.

**le** -- if the surface following is a volume then **le** means inside
including the surface of the volume. If the surface is a plane or a
sheet le means the space on the side of the plane or sheet opposite to
the normal including the plane or sheet itself.

**gt** -- if the surface following is a volume then **gt** means outside
not including the surface of the volume. If the surface is a plane or a
sheet **gt** means the space on the same side of the plane or sheet as
the normal not including the plane or sheet itself.

**ge** -- if the surface following is a volume then **ge** means outside
including the surface of the volume. If the surface is a plane or a
sheet **ge** means the space on the same side of the plane or sheet as
the normal including the plane or sheet itself.

The operators **or, and**, and **not** applied to regions or modified
surfaces mean union, intersection and complement respectively.
Parentheses are operators and are used for nesting. Spaces are required
as delimiters to separate operators and operands; parentheses are
operators and must be surrounded by spaces. Internal interfaces should
be excluded when defining material regions. (i.e. use **lt** and **gt**
). External boundaries should be included when defining material
regions. If a material regions consists of more than one region and the
regions touch (i.e. share a region interface), then the region interface
is not a material interface -- all the points on the region interface
are interior to the material region. In this case use **le** or **ge**
to include these region interface points in the material region as
interior points.

Defining a material region will cause the information associated with
this material region to be stored under the name of
the [geometry](../geometries.md) of the current mesh object.  Releasing
the material region will remove this information.

**FORMAT:**

**mregion**/ material_region\_name/region definition

**EXAMPLES:**

**mregion**/ material_region\_name**/release**

**mregion**/mat1/ **le** box1 **and** ( **lt** sphere1 **and** ( **lt**
plane1 **or gt** plane2 )) 

**mregion**/mat2/ regiona **or** regionb 

 
