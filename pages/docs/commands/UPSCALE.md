---
title: UPSCALE
tags: review
---

UPSCALE
-------

 The **upscale** command is used to interpolate attribute values from
 nodes of a fine source mesh to node attributes of a coarse sink mesh.
 The subroutine finds nodes of the fine source mesh within the Voronoi
 cell of every node in the coarser sink mesh. Nodes on cell boundaries
 are assigned to two or more sink nodes. Then the attributes of all the
 source nodes within a source node's cell are upscaled into a single
 value based on the chosen method. Mesh elements and connectivity are
 ignored and only node values are used to upscale values on to the sink
 mesh nodes.

 A kdtree node search is used to find the source mesh nodes located in
 each of the Voronoi sink point volumes. It is possible for source
 nodes to occur on the boundary of multiple Voronoi volumes. By
 default, all nodes found in each Voronoi volume are used to upscale to
 the enclosed sink node. In this case, source nodes on multiple Voronoi
 boundaries will be included in upscale calculations more than once.
 The keyword option **single** can be used for situations that require
 the sum of nodes in each Voronoi space to equal the total of source
 points used. This one-to-one correspondence is written to the source
 cmo attribute pt\_gtg. This attribute can be reused during multiple
 calls to the **upscale** command and will greatly reduce CPU time. The
 keyword that allows the attributes to be kept as part of the sink cmo
 is **keepatt**. Note that information regarding duplicate nodes on
 Voronoi volume boundaries will be lost if the pt\_gtg is used instead
 of the default search.

 The **upscale** method options provide choices for the calculation of
 the associated set of source nodes on to the single sink node. The
 scale\_method parameter includes **sum**, **min**, **max**, and
 averages **ariave**, **harave**, **geoave**. For all positive data
 sets containing at least one pair of nonequal values, the harmonic
 mean is always the least of the three means, while the arithmetic mean
 is always the greatest of the three and the geometric mean is always
 in between.

 

  The format for the command line is as follows:

  **upscale** / scale\_method / cmosink, attsink / 1,0,0 / cmosrc,
  attsrc /

  [**boundary\_choice**] [keepatt] [set\_id]

  Keywords appearing after the source cmo attribute name are optional
  and may appear in any order.

  scale\_method is the choice of upscale calculation applied to each
  set of source nodes within each sink Voronoi cell where x(1) to x(n)
  are the values of source nodes 1 to n found for the sink point. The
  choices are as follows:
 
   

   **ariave** - For each sink point, calculate the arithmetic mean of
   n values from source attribute attsrc

   sink\_val = (x(1) + x(i)... + x(n)) / n

   for 4 values; 1,2,3,4 ariave = 2.5

   

   **geoave** - For each sink point, calculate the geometric average
   of n values found in attsrc

   sink\_val = ( x(1) 
* x(i)... 
* x(n) )
*
*(1/n)

   for 4 values; 1,2,3,4 geoave = 2.21336

   

  **harave** - For each sink point, calculate the harmonic mean of n
  values from source attribute attsrc

  sink\_val = n / ( 1/x(1) + 1/x(i)... + 1/x(n) )

  for 4 values; 1,2,3,4 harave = 1.92



  **min** or **max** - For each sink point, assign the min or max
  source attribute from n values found in attsrc

  sink\_val = min(x(1),x(i),x(n))

  for 4 values; 1,2,3,4 min = 1

   

   sink\_val = max(x(1),x(i),x(n))

   for 4 values; 1,2,3,4 max = 4

   

   **sum** - For each sink point, calculate the sum of n values from
   source attribute attsrc

   sink\_val = x(1) + x(i)... + x(n)

   for 4 values; 1,2,3,4 sum = 10

   

 
  

  cmosink, attsink are the cmo name and attribute name to write sink
  values into. The scale method detirmines which calculation is
  applied to the source attribute value and written to the sink
  attribute. All integer attributes are converted to double for the
  calculations. The resulting values are then converted to the nearest
  integer if the sink attribute is integer.

 
  indexed\_set is the set of sink nodes to write scaled values to.
  1,0,0 will select all sink nodes
 
  cmosrc, attsrc are the cmo name and attribute name are the cmo and
  attribute to interpolate from. Points from the source grid will be
  located within the Voronoi volumes of sink nodes.

   

   
 
  The following parameters are optional for the command **upscale**. 
 
  **boundary\_choice** provides a method of choice when source nodes are
  found on the boundary of multiple Voronoi volumes of sink nodes. By
  default, each set of souce nodes found within each volume are used
  to calculate an upscale value for the sink node. In this case if
  duplicate nodes occur on multiple cells, the sum number of nodes
  used in upscale calculations will exceed the sum total of nodes in
  the source mesh. If the number of source nodes used must equal the
  number of source mesh nodes, choose an **boundary\_choice** to detirmine
  which sink volume an boundary node should be assigned to. The result
  is a one-to-one correspondence with each source point assigned to a
  single sink node id which is stored in source attribute pt\_gtg.
  Source nodes that are found on shared Voronoi boundaries are flagged
  in source attribute dups\_gtg.
 
   **single** selects the Voronoi volume of the first sink node
   encountered and does not use any after that.

   **divide** not implemented.

   **multiple** uses all source nodes found in each sink Voronoi
   volume.

 
  att\_option is used during multiple calls to **upscale** with the
  same two grids. It keeps source attributes created during the search
  routines and uses these attributes to look up associated node
  numbers. The **upscale** command uses kdtree to create the source
  attribute pt\_gtg that associates source nodes to sink node volumes.
  Note that this correlation is one-to-one and source nodes sharing
  multiple Voronoi volume boundary are tagged in a second source
  attribute called dups\_gtg.
 
   **delatt** deletes any attributes created during the kdtree
   searches. By default these attributes are removed.

   

   **keepatt** keeps attributes pt\_gtg and dups\_gtg created during
   the kdtree searches. The source node attribute pt\_gtg has the
   first found sink node id. The node attribute dups\_gtg is flagged
   each time the source node occurs in a sink Voronoi cell, allowing
   the user to find source nodes on cell boundaries. Use of this
   attribute will greatly reduce CPU time.

   
   **set\_id** creates and keeps the source attribute pt\_gtg
   containing sink id numbers found from the sink mesh. This is the
   same attribute created and kept for the **keepatt** option except
   that if the attribute already exists, it is deleted and re-created
   with a new search. This is recomended if the pt\_gtg attribute
   exists, but user is not sure the current sink mesh is the same as
   used to create the attribute.
 
  **FORMAT:**
 
   **upscale** / scale\_method / cmosink, attsink /1,0,0/ cmosrc,
   attsrc / &

    [ **keepatt  delatt** ]  [ **set\_id** ]  [ **single 
   divide** ]
 
  **EXAMPLES:**
 
       upscale / sum / cmo_sink icount /1,0,0/ cmo_src ival
       upscale / sum / cmo_sink icount /1,0,0/ cmo_src ival/
       single keepatt

       upscale / min / cmo_sink imin /1,0,0/ cmo_src ival/ single
       keepatt set_id

       upscale / max / cmo_sink imax /1,0,0/ cmo_src ival/
       keepatt

       upscale / ariave / cmo_sink ave_val /1,0,0/ cmo_src xval/
       upscale / harave / cmo_sink har_val /1,0,0/ cmo_src xval/
       upscale / geoave / cmo_sink geo_val /1,0,0/ cmo_src xval/

 
  EXAMPLES 1 and 2:

    Upscale 1221 source points to 10 sink points with using method
    **sum** and showing the difference between allowing multiple use of
    nodes on Voronoi cell boundaries and the single option which uses
    nodes on cell boundaries only once. Images showing the source and
    sink points are shown below.
   
    
               Example 1:                         Example 2:                        
                                                                          
      cmo/setatt/cmo\_src/ival/1,0,0/   cmo/setatt/cmo\_src/ival/1,0,0/ 
      1
                                  1
                                
      **upscale / sum **/ cmo\_sink     **upscale / sum **/ cmo\_sink   
      icount /1,0,0/ cmo\_src ival
       icount /1,0,0/ cmo\_src ival/   
      math/sum/cmo\_src/sumtot/1,0,0/   math/sum/cmo\_src/sumtot/1,0,0/
               
      cmo\_src/ival                     cmo\_src/ival
                         
      In this example, search will      
                                 
      find the sets of source nodes     This is the same as Example 1   
      enclosed within each sink         except that duplicate boundary  
      Voronoi cell.The ival attribute   points will be counted for the  
      values are added for each set     first found Voronoi volume and  
      and written to the sink icount    skipped thereafter. This        
      attribute. Because the attribte   one-to-one correspondance of    
      ival has all values set to 1,     source nodes to sink Voronoi    
      the icount attribute will         volume will be stored in the    
      contain the number of source      source attributes pt\_gtg with  
      nodes found in each Voronoi       sink node numbers, and          
      volume. The source node values    dups\_gtg containing flags of   
      will be counted regardless if     the duplicate boundary points.  
      they are on a Voronoi boundary    These attributes will not be    
      and are in multiple Voronoi       deleted.
                         
      volumes. The result with          In this example, math/sum will  
      duplicate boundary points will    result in a total equal to the  
      be a sum of points used greater   number of nodes used.           
      than the total number of source                                    
      mesh points.
                                                        
      In this example, math/sum will                                     
      result in at total greater than                                    
      the number of nodes used if                                        
      there are duplicatate Voronoi                                      
      boundary points.                                                   
    
         cmo/setatt/COARSE_MO/idebug 6      cmo/setatt/COARSE_MO/idebug 6 
         upscale/sum/COARSE_MO,icount/      upscale/sum/COARSE_MO,icount/ 
     1,0,0/FINE_MO/imt keepatt          1,0,0/FINE_MO/imt/single keepatt  
                                                                          
         pt_gtg attribute added to sou      nodes on Voronoi boundaries s 
     rce cmo.                           et to a single source volume.     
                                                                          
         dups_gtg attribute added to s      pt_gtg being used for sink no 
     ource cmo.                         de id numbers.                    
                                                                          
                                            dups_gtg being used for nodes 
                                         on duplicate cell boundaries.    
         UPSCALE METHOD:        sum                                       
                                                                          
                                            UPSCALE METHOD:        sum    
                options:    keepatt  m                                    
     ultiple                                                              
                                                   options:    keepatt    
                   10  Sink Nodes of i   single                           
     count in course mesh: cmoc                                           
                                                      10  Sink Nodes of i 
                 1221  Source Nodes of  count in course mesh: cmoc        
      imt1 in fine mesh: cmof                                             
                                                    1221  Source Nodes of 
                                         imt1 in fine mesh: cmof          
           Source Nodes    Percent Don                                    
     e                                      SKIPPING POINT SEARCH... usin 
                                        g lookup attribute pt_gtg         
                     306       25 %                                       
                                                                          
                                              Source Nodes    Percent Don 
                     611       50 %     e                                 
                                                                          
                                                        306       25 %    
                     916        %                                       
                                                                          
                                                        611       50 %    
                    1221      100 %                                       
                                                                          
                                                        916        %    
                    1221 Total source                                     
     nodes searched.                                                      
                                                       1221      100 %    
         ---     Sink id   # of nodes                                     
     used   calculated value ---                                          
                                                       1221 Total source  
                       1                nodes searched.                   
     1               1                                                
                                            ---     Sink id   # of nodes  
         Duplicate nodes                used   calculated value ---       
       1                 1                                                
                                                          1               
                       2                188               188             
     108               108                                                
                                                          2               
                       4                108               108             
     1               1                                                
                                                          4               
         Duplicate nodes                181               181             
       8                 8                                                
                                                          5               
                       5                256               256             
     256               256                                                
                                                          6               
                       6                192               192             
     192               192                                                
                                                          8               
                       8                 72                72             
      72                72                                                
                                                          9               
                       9                128               128             
     128               128                                                
                                                         10               
                      10                 96                96             
      96                96                                                
                                                          8 sink nodes ou 
                       8 sink nodes ou  t of                10 assigned v 
     t of                10 assigned v  alues.                            
     alues.                                            1221 source nodes  
                    1230 source nodes   out of            1221 used as so 
     out of            1221 used as so  urce values.                      
     urce values.                                         9 duplicate nod 
                       9 duplicate nod  es on Voronoi boundaries used onl 
     es on Voronoi boundaries used mul  y once.                           
     tiple times.                           UPSCALE/sum/ from imt1 to ico 
         UPSCALE/sum/ from imt1 to ico  unt Done.                         
     unt Done.                                                            
                                                                          
                                            cmo/printatt/COARSE_MO/icount 
         cmo/printatt/COARSE_MO/icount                                    
                                                                          
                                            Attribute: icount             
         Attribute: icount                                                
                                                                          
                                                     1        188         
                  1        1                                            
                                                                          
                                                     2        108         
                  2        108                                            
                                                                          
                                                     3          0         
                  3          0                                            
                                                                          
                                                     4        181         
                  4        1                                            
                                                                          
                                                     5        256         
                  5        256                                            
                                                                          
                                                     6        192         
                  6        192                                            
                                                                          
                                                     7          0         
                  7          0                                            
                                                                          
                                                     8         72         
                  8         72                                            
                                                                          
                                                     9        128         
                  9        128                                            
                                                                          
                                                    10         96         
                 10         96                                            
                                                                          
                                                                          
                                                                          
         math/sum/COARSE_MO/sumtot/1,0                                    
     ,0/COARSE_MO/icount                                                  
         icount sum =       1230            math/sum/COARSE_MO/sumtot/1,0 
                                        ,0/COARSE_MO/icount               
                                                                          
                                            icount sum =       1221       
                                                                        
  
 
**EXAMPLE 2 IMAGES:** 

These images show the 10 numbered sink points and
the 1221 source points. In this example all source points have an
imt1 value of 1. The sink points each have a value in icount equal
to the number of nodes used for the associated Voronoi volume. The
red lines show the Voronoi cell boundaries for the 10 sink points.

Source points all equal to 1,

Sink points colored by upscaled value. 

<img src="https://lanl.github.io/LaGriT/assets/images/upscale_ex2_imt.png">  

**Source points colored by associated sink node id, attribute pt\_gtg. cell boundaries, attribute dups\_gtg.**

<img src="https://lanl.github.io/LaGriT/assets/images/upscale_ex2_id.png"> 

**Source points colored by number of duplicates.**

<img src="https://lanl.github.io/LaGriT/assets/images/upscale_ex2_dups.png">

    Example 3:

    Show results for the 3 versions of mean calcuations.
   
    +-----------------------------------------------------------------------+
                                                                           
         * use single quad element with two nodes located                  
         * so they will capture 4 nodes each from source                   
                                                                           
         * for source mesh FINE_MO with two quad elements                  
         * assign bottom nodes to 2 and top nodes to 8                     
                                                                           
         cmo setatt FINE_MO xmean 2.0                                      
         cmo setatt FINE_MO xmean 4,6,1 8.0                                
                                                                           
         * Upscale using averages                                          
         * and write to attributes for nodes 1 and 2 only                  
                                                                           
         ** *** Arithmetic mean ** ***                                       
         upscale/ariave/COARSE_MO amean/1,2,0/ FINE_MO/xmean/              
                                                                           
         ** *** Geometric mean ** ***                                        
         upscale/geoave/COARSE_MO gmean/1,2,0/ FINE_MO/xmean/              
                                                                           
         ** *** Harmonic mean ** ***                                         
         upscale/harave/COARSE_MO hmean/1,2,0/ FINE_MO/xmean/              
                                                                           
                                                                           
         ** *** SOURCE VALUES from FINE_MO ** **** **                         
                                                                           
         cmo printatt FINE_MO xmean                                        
                                                                           
         Attribute: xmean                                                  
                                                                           
                  1  2.00000E+00                                           
                                                                           
                  2  2.00000E+00                                           
                                                                           
                  3  2.00000E+00                                           
                                                                           
                  4  8.00000E+00                                           
                                                                           
                  5  8.00000E+00                                           
                                                                           
                  6  8.00000E+00                                           
                                                                           
                                                                           
         ** *** RESULT VALUES ** **** **                                      
                                                                           
                                                                           
         cmo printatt COARSE_MO amean                                      
                                                                           
         Attribute: amean                                                  
                                                                           
                  1  5.00000E+00                                           
                                                                           
                  2  5.00000E+00                                           
                                                                           
                  3  0.00000E+00                                           
                                                                           
                  4  0.00000E+00                                           
                                                                           
                                                                           
         cmo printatt COARSE_MO gmean                                      
                                                                           
         Attribute: gmean                                                  
                                                                           
                  1  4.00000E+00                                           
                                                                           
                  2  4.00000E+00                                           
                                                                           
                  3  0.00000E+00                                           
                                                                           
                  4  0.00000E+00                                           
                                                                           
                                                                           
         cmo printatt COARSE_MO hmean                                      
                                                                           
         Attribute: hmean                                                  
                                                                           
                  1  3.20000E+00                                           
                                                                           
                  2  3.20000E+00                                           
                                                                           
                  3  0.00000E+00                                           
                                                                           
                  4  0.00000E+00                                           
                                                                         
                                                                         
      +-----------------------------------------------------------------------+
       **Image 1 shows Arithmetic mean result of 5.0**
                          
       Result Sink nodes 1 and 2 are the two lower nodes of the single quad  
       element in image.
                                                        
       Source nodes are on the two adjacent quad elements.                   
                                                                             
           UPSCALE METHOD:     ariave                                        
                                                                             
                      4  Sink Nodes of amean in course mesh: cmoc            
                                                                             
                      2  Selected Set of Nodes will be written               
                                                                             
                      6  Source Nodes of xmean in fine mesh: cmof            
                                                                             
                                                                             
             Source Nodes    Percent Done                                    
                                                                             
                         3       25 %                                        
                                                                             
                         5       50 %                                        
                                                                             
                         6 Total source nodes searched.                      
                                                                             
           ---     Sink id   # of nodes used   calculated value ---          
                                                                             
                         1                4    0.5000000E+01                 
                                                                             
                         2                4    0.5000000E+01                 
                                                                             
                         2 sink nodes out of                 4 assigned valu 
       es.                                                                   
                         2 duplicate nodes on Voronoi boundaries used multip 
       le times.                                                             
           UPSCALE/ariave/ from xmean to amean Done.                         
                                                                             
                                                                         
   
<img src="https://lanl.github.io/LaGriT/assets/images/upscale_arithmetic.jpg">                              

       **Image 2 shows Geometric mean result of 4.0**
                           
       Result Sink nodes 1 and 2 are the two lower nodes of the single quad  
       element in image.
                                                        
       Source nodes are on the two adjacent quad elements.                   
                                                                             
           UPSCALE METHOD:     geoave                                        
                                                                             
                      4  Sink Nodes of gmean in course mesh: cmoc            
                                                                             
                      2  Selected Set of Nodes will be written               
                                                                             
                      6  Source Nodes of xmean in fine mesh: cmof            
                                                                             
                                                                             
             Source Nodes    Percent Done                                    
                                                                             
                         3       25 %                                        
                                                                             
                         5       50 %                                        
                                                                             
                         6 Total source nodes searched.                      
                                                                             
           ---     Sink id   # of nodes used   calculated value ---          
                                                                             
                         1                4    0.4000000E+01                 
                                                                             
                         2                4    0.4000000E+01                 
                                                                             
                         2 sink nodes out of                 4 assigned valu 
       es.                                                                   
                         2 duplicate nodes on Voronoi boundaries used multip 
       le times.                                                             
           UPSCALE/geoave/ from xmean to gmean Done.                         
                                                                             
<img src="https://lanl.github.io/LaGriT/assets/images/upscale_geometric.jpg">   

    +-----------------------------------------------------------------------+
     **Image 3 shows Harmonic mean result of 3.2**
                          
     Result Sink nodes 1 and 2 are the two lower nodes of the single quad  
     element in image.
                                                      
     Source nodes are on the two adjacent quad elements.                   
                                                                           
         UPSCALE METHOD:     harave                                        
                                                                           
                    4  Sink Nodes of hmean in course mesh: cmoc            
                                                                           
                    2  Selected Set of Nodes will be written               
                                                                           
                    6  Source Nodes of xmean in fine mesh: cmof            
                                                                           
                                                                           
           Source Nodes    Percent Done                                    
                                                                           
                       3       25 %                                        
                                                                           
                       5       50 %                                        
                                                                           
                       6 Total source nodes searched.                      
                                                                           
         ---     Sink id   # of nodes used   calculated value ---          
                                                                           
                       1                4    0.3200000E+01                 
                                                                           
                       2                4    0.3200000E+01                 
                                                                           
                       2 sink nodes out of                 4 assigned valu 
     es.                                                                   
                       2 duplicate nodes on Voronoi boundaries used multip 
     le times.                                                             
         UPSCALE/harave/ from xmean to hmean Done.                         
                                                                         
   
<img src="https://lanl.github.io/LaGriT/assets/images/upscale_harmonic.jpg">                                

  

  

  

 
