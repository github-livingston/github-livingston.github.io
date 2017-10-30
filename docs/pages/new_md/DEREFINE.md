---
GENERATOR: 'Mozilla/4.7C-SGI [en] (X11; I; IRIX64 6.5 IP30) [Netscape]'
Generator: Microsoft Word 98
title: DEREFINE
---

  
 **DEREFINE**

  This routine derefines a mesh by deleting points using the merge
  routine based on one of the following refine\_types. **edge** will
  refine if element edge length is less then value. **volume** will
  merge if element volume is less than value. The merge routine will
  first attempt the smallest element edge then the next smallest, etc.
  **aspect** will derefine where aspect ratio is less than value.
  **pinchedge** will allow merging of adjacent points across a thin
  layer to eliminate the layer where it is too thin. **pinchedge**
  should be used only with pointtype1 and pointtype2 both equal to 2.

  Two criteria are currently enabled; **minsize** and **merge**.
  **minsize** allows merges if the calculation implied by refine\_type
  is less than value. **merge** will merge the following first\_point
  and second\_point. The field option is not enabled and should be
  left default. The user specifies which merges are acceptable by
  designating the allowable pointtypes. Nodes with pointtype1 are
  merged to nodes of pointtype2. If pointtype1 and pointtype2 are both
  equal to 2, the code only merges if the nodes are both on the same
  material interface (use **pinchedge** if deleted nodes should be on
  different interfaces of the same material). **derefine** will not
  merge if an unacceptable element is created. **derefine** will work
  on material interfaces if all the children are set with the
  **settets** command. Various combinations of **derefine** may be
  used to improve the mesh. **recon** may be used to return to a
  delaunay mesh after using the **derefine** command.

 **FORMAT:**

  **derefine/minsize**/field/pointtype1
  pointtype2/refine\_type/first\_point/last\_point/stride/value

  **derefine** **/merge**/first\_point/second\_point

 EXAMPLE:

  **derefine/minsize**//0 0**/aspect**/ 1 0 0/1.e-3

  **derefine/minsize**//0 2**/volume** **/pset,get**,apset/5.

  **derefine/minsize**//10  10**/edge**/1 0 0/5.

  **derefine/minsize**//2 2**/pinchedge**/1 0 0/1

  **derefine/merge**/21/22
