---
GENERATOR: 'Mozilla/4.7 [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: ZQ
---

 **ZQ**   Deprecated command; **cmo/setatt** is now preferred

Set or print node attribute values of a selected set of nodes.

To print, omit the 
`value' field.

For printing, attributes are grouped as follows:

Group1: isq,imt,itp (material type and point types)

Group2: x,y,z (coordinates)

To print, specify any one of a group and all will be printed.

To set an attribute value, set value and all selected nodes will be set
to this value.

Attribute added with a **cmo/addatt** command may also be printed or
changed.

**FORMAT:**

**zq**/iattribute/ifirst,ilast,istride/value

EXAMPLE:

**zq** **/imt**/1,100,2/material1/

will set all odd numbered points between 1 and 100 to material type

`material 1'

**zq/xic**/1,0,0/

will print coordinates of all points
