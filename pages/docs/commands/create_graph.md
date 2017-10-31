---
title: CREATE_GRAPH
tags: ok
---

**CREATE\_GRAPH**

 Create a node or dual (element) adjacency graph. If node option is
 selected, the graph of node adjacency is created, if dual option is
 selected, the graph of element adjacency (dual graph) is created.

 For details of METIS algorithms and descriptions of the third command
 line argument see:

 <a href="http://glaros.dtc.umn.edu/gkhome/views/metis"> </a>

 See [METIS](metis.md)documentation for description of graph format.

 The default name of the attributes that are created are different
 depending on which option (metis or lagrit) is used.

 `create_graph / metis / [node  dual] / [nxadj] / [nadjncy]  create_graph/ lagrit / dual / jtetoff / jtet   `

 See the [dump](DUMP2.md) command for options to output the adjacency
 graph to a file.`   `

**LIMITATIONS**

 The metis option will not work on a hybrid mesh. Supported element
 types are tri, tet, quad, hex.

 The /lagrit/ option will only produce the dual adjacency graph. The
 only option for the name of the graph arrays are jtetoff and jtet. The
 present implementation is just a wrapper on the [geniee](GENIEE.md)
 command.

 See instructions in documentation of the [metis](metis.md) command.

METIS Interface to LaGriT

 METIS can be freely distributed provided that:

-   A reference to the following paper is included: *“A Fast and Highly
    Quality Multilevel Scheme for Partitioning Irregular Graphs”. George
    Karypis and Vipin Kumar. SIAM Journal on Scientific Computing, Vol.
    20, No. 1, pp. 359—392, 1999.*
-   The original documentation <a href="http://glaros.dtc.umn.edu/gkhome/fetch/sw/metis/manual.pdf">  (download PDF file of manual) </a> and copyright notice is included
-   METIS 4.0 Copyright 2001-06, Regents of the University of Minnesota

**FORMAT:**

create_graph / metis / [node  dual] / [nxadj] / [nadjncy]

**EXAMPLES:**

		 create_graph / metis / dual / -def- / -def-  
		 create_graph / metis / node / -def- / -def-  
		 create_graph / metis / dual / ie1 / ieadj1  
		 create_graph / metis / node / in1 / inadj1  
		 create_graph / lagrit / dual / jtetoff / jtet

