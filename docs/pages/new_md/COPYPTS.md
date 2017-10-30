---
GENERATOR: 'Mozilla/4.72 [en] (X11; U; Linux 2.2.14-5.0 i686) [Netscape]'
Generator: Microsoft Word 98
title: COPYPTS
---

 

 **COPYPTS**

  

  Copy a point distribution. There are two distinct forms of this
  command. The first format is designed to copy points from one mesh
  object into another. In this form if the names of the source and
  sink mesh objects are omitted, the current mesh object will be used.
  The copy may be restricted to a subset of points by including the
  source point information. Points in the sink mesh object will be
  overwritten if sink\_stride is not zero. Attribute fields may be
  specified for both the source and sink mesh object. For example the
  x-coordinate field in the source mesh object (xic) may be placed in
  the y-coordinate field of the sink mesh object. Attribute values
  will be copied from the source mesh object to the sink mesh object.
  The user is warned that these values might not make sense in their
  new context.
  The second form of this command is included for historic reasons: it
  duplicates points within a mesh object including all the attributes
  of the points. Also note that if no sink points or sink stride are
  specified, then the copied points are placed at the end of the data
  arrays (see third FORMAT) otherwise the copied points are written
  over the existing points starting at the 1st sink point. Note also
  that the first form of the command gives the arguments sink first
  then source whereas the second form gives the source then the sink.

 **FORMAT:**

  

  **copypts**/sink\_cmo/source\_cmo/1st\_sink\_point/sink\_stride/1st\_source\_point/last\_source\_point/

  source\_stride/sink\_attribute\_name/source\_attribute\_name

  **copypts**/1st\_source\_point/last\_source\_point/source\_stride/1st\_sink\_point/sink\_stride

  **copypts** /1st\_point/last\_point/stride

 **EXAMPLES:**

  **copypts**/3dmesh/2dmesh /

      Copy all points in 2dmesh to the end of the 3dmesh point list.

  **copypts**/3dmesh/2dmesh/0,0**/pset,get,**mypoints/

      Copy the point set named mypoints from 2dmesh to the end of
  3dmesh point list.

  **copypts/3dmesh/2dmesh/100,4/pset,get,mypoints/boron/arsenic**/

  **   ** Copy the arsenic field from the point set named mypoints
  from 2dmesh replacing the boron field at every fourth point
  beginning at point 100 in 3dmesh**.**

  **copypts/pset,get,mypoints/0,0**/

  **  **  Duplicate the point set named mypoints from the current mesh
  object and place the duplicated points at the end of the point
  list.

  **copypts/**//0,0**/pset,get,mypoints**/

  Duplicate the point set named mypoints from the current mesh object
  and place the duplicated points at the end of the point list. Same
  effect as the example directly above. The current mesh object is
  used since the fields are blank on the command line

