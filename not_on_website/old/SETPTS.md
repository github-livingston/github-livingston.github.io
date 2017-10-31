---
GENERATOR: 'Mozilla/4.7 
[en
] (X11; I; IRIX 6.5 IP32) 
[Netscape
]'
Generator: Microsoft Word 98
title: SETPTS
---

 **SETPTS**

Sets point types and material regions by calling **surfset** and
**regset** routines. **** Generate constraint table. The material (imt1)
attribute is set based on the **mregion** commands. Interior and
external boundary nodes should be assigned to exactly one **mregion**;
these nodes will be assigned an **imt1** value that corresponds to the
**mregion.** A node which is on an interface will be assigned to any
**mregion** and will be given an **imt1** value of "**interface**" (an
integer equal to one more than the number of material regions.) Node
types are assigned based on whether a node is on a surface and what type
the surface(s) is.

This command must be executed before **connect.**

FORMAT:

**setpts**

**setpts/no\_interface**

This allows one to set the imt values of nodes without getting any nodes
labeled imt=interface. This is useful if you do not want settets to
create parent child chains at interface points. The actual imt value
given may be determined by roundoff error so should not be used in cases
where there are a large number of interface points.  It is useful for
setting imt values of an rzbrick mesh in which interface points only
occur due to the coincidental point very near the geometry defining
surface.

**setpts****/closed\_surfaces****/reflect**

The **closed\_surfaces** option works with geometries in which all
regions and mregions are defined by closed surfaces. The nodes that fall
on more than one surface are labeled as interface nodes. Nodes which
fall on exactly one surface are labled external reflective boundary
nodes. Nodes which are external boundary interface nodes are not labeled
correctly and **resetpts/itp** must be called to correct the point
types. An input file using the closed\_surfaces option might look like:

cmo/create/s1///tri

read/avs/surfaces

cmo/create/3dmesh

surface/surface1/inticons/sheet/s1

copyts/3dmesh/s1/

cmo/release/s1/

cmo/create/52///tri/

read/avs/surf2.avs

surface/surface2/inticons/sheet/s2

copypts/3dmesh/s2

cmo/release/s2/

region/release/s2

region/r1/le surface1

region/r2/le surface2

mregion/mr1/lt surface1

mregion/mr2/lt surface2

setpts/closed\_surfaces/reflect

connect

settets

resetpts/itp
