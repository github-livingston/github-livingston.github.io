---
GENERATOR: 'Mozilla/4.05C-SGI [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
---

 

 

 **Tutorial -- Generating Initial Grids Using the LaGriT Command
 Language:**

  The steps involved in generating three dimensional grids in the
 LaGriT command language are:

  

 1.[Define mesh objects.](definemo.md)[](definemo.md)

 2.[Define an enclosing volume](defineev.md).

 3.[Define interior interfaces.](DEFINEII.md)

 4.[Divide the enclosing volume into
 regions.](dividereg.md)[](dividereg.md)

 5
. [Assign material types to the regions.](assignmt.md)

 6.[Distribute points within the
 volume.](distributep.md)[](distributep.md)

 7
. [Connect the points into
 tetrahedra](%20%20%20%20connecttet.md%20%20%20%20%20%20%20%20%20%20%20)[](%20%20%20%20connecttet.md%20%20%20%20%20%20%20%20%20%20%20)

  

 Detailed descriptions of the LaGriT commands are given in Section II.
 This tutorial covers just the commands needed to generate a simple
 grid. The tutorial will explain how to generate a grid in a unit cube
 containing two materials separated by a plane. Lines that begin with
 an asterisk (
*) are comments; keywords are in **bold**.

