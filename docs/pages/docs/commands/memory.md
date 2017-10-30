---
title: memory
tags: ok
---

memory
------

These commands report the current state of LaGriT's dynamic memory
allocation. LaGriT arrays are referenced by memory management by a two
part name, block name and partition name. It is allocated in integer or
real blocks(real is implemented as real
*8). Each memory block is
preceeded by a header and terminated by a trailer. Different platforms
will have different values for integer and real word lengths. LaGriT
developers read more on LaGriT memory management at **[Memory
Manager](../memmang.md)**


The following memory keywords are recognized:

 **memory / verify  **

 verify the integerity of LaGriT memory manager storage by checking
 that the known blocks have not been overwritten. If corruption is
 detected, an array map will be printed. Nothing is printed if there
 memory is successfully verified.

 **memory / print  **

 print an address map of the LaGriT managed arrays. For each array the
 following is printed; index, length, type, memory address, associated
 name, and partition. The partition is the grouping of arrays by usage.
 Common partitions include the mesh object (by name), global memory,
 and temporary memory for work arrays.

     MEMORY SIZES : 
      Sizeof char    (type 3) =  1 bytes      Sizeof long        =   4 bytes
      Sizeof real*8  (type 2) =  8 bytes      Sizeof pointer     =   4 bytes
      Sizeof integer (type 1) =  4 bytes      Sizeof INT_PTRSIZE =   4 bytes

     INDEX         LENGTH    TYPE     ADDRESS     NAME                           PARTITION
       29          40000000   2     -14248416 xic                              cmo1    
        1                10   3       143632720 global_name                      global_lg
       31          40000000   2      1760710688 zic                              cmo1    
       30          40000000   2      2080714784 yic                              cmo1   

     Total BYTES =    2.400E+09   Total MEGABYTES =    2.400E+03

 **memory / maxmalloc  **

 Report estimate of possible amount of memory available for allocation
 by LaGriT. This test will make incremental calls to internal LaGriT
 memory allocation (mmgetblk) until failure. The report will include
 the total Megabytes where allocation succeeded, and amount at which
 allocation failed. This command will also print a map of the memory
 manager storage.

      .... 

      MMGETBLK ERROR: value exceeds sizeof:            4
      MAX ALLOC SIZE:    4294967296.0000000     
      ATTEMPTED SIZE:    6553600048.0000000     
      MMGETBLK: return early with error flag:          -21
       
      Succeeded at     819.20000000000005       MEGABYTES
      Failed at        1638.4000000000001       MEGABYTES


 The 64 bit version for memory routines will look slightly different:

     MEMORY SIZES : 
      Sizeof char    (type 3) =  1 bytes      Sizeof long        =   8 bytes
      Sizeof real*8  (type 2) =  8 bytes      Sizeof pointer     =   8 bytes
      Sizeof integer (type 1) =  4 bytes      Sizeof INT_PTRSIZE =   8 bytes

     ....

     util_malloc_: Out of memory, malloc return: (nil) 
        Requested value: 104857600000.000000 =    8 bit unsigned int 
      MMGETBLK FAILED: Array array_01 with bytes:          104857600096
      MMGETBLK: return ending with error flag:                    -1
       
      Succeeded at     52428.800000000003       MEGABYTES
      Failed at        104857.60000000001       MEGABYTES


**EXAMPLES:**

**memory / verify**

**memory / print**

**memory / maxmalloc**
