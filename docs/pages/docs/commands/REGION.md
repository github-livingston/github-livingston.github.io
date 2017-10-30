---
title: REGION
tags: ok
--- 

**REGION**

  Define a geometric region from the set of surfaces by logically
  combining the surface names.  A region may be removed from the
  geometry by specifying the release keyword.
 
  To define a region, the operators **lt, le, gt, and ge** are applied
  to previously defined surfaces according to the following rules.
 
**lt** -- if the surface following is a volume then lt means
inside not including the surface of the volume. If the surface is
a plane or a sheet lt means the space on the side of the plane or
sheet opposite to the normal not including the plane or sheet
itself.

**le** -- if the surface following is a volume then le means
inside including the surface of the volume. If the surface is a
plane or a sheet le means the space on the side of the plane or
sheet opposite to the normal including the plane or sheet itself.

   
 **gt** -- if the surface following is a volume then gt means
   outside not including the surface of the volume. If the surface is
   a plane or a sheet **gt** means the space on the same side of the
   plane or sheet as the normal not including the plane or sheet
   itself.

   
 **ge** -- if the surface following is a volume then ge means
   outside including the surface of the volume. If the surface is a
   plane or a sheet **ge** means the space on the same side of the
   plane or sheet as the normal including the plane or sheet itself.

   The operators or, and, and not applied to surfaces mean union,
   intersection and complement respectively. The parentheses
   operators, (and ), are used for nesting. Spaces are required as
   delimiters to separate all operators and operands. Internal
   interfaces should be included in exactly one region. In the event
   of conflicting region commands, the one occurring last in the
   input stream takes precedence.
   Defining a  region will cause the information associated with this
   material region to be stored under the name of the
   [geometry](../geometries.md) of the current mesh object. 
   Releasing the  region will remove this information.

 **FORMAT:**

  **region**/region\_name/region definition
  
   **region**/region\_name**/release**

 **EXAMPLES:**

  **region**/reg1**/le** sphere1 **and** ( **lt** plane1 **or** **gt**
  plane2 )
  
  **region**/reg2**/le** sphere1 **and** ( **ge** plane1 **and**
  **le** plane2 )
  
  **region**/reg1**/release**
 
