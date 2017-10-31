
 **COORDSYS**

  This routine defines a local coordinate system to be in effect until
  another coordinate system is defined or the normal coordinate system
  is reset. The new coordinate system is defined by specifying an
  origin, a point on the new x-z plane and a point on the new z-axis.
  These points are specified in the normal coordinate system. The
  options available in iopt are:
 
   **define** define a new local coordinate system

   **normal** return to the normal coordinate system

   **save** save the current coordinate system for recall

   **restore** recall the last saved coordinate system

 **FORMAT:**

  **coordsys**/iopt/x0,y0,z0/xx,xy,xz/zx,zy,zz

  where x0,y0,z0 is the location of the new origin, xx,xy,xz is a
  point on the new x-z plane and zx,zy,zz is a point on the new
  z-axis. These points are defined with the normal coordinate system,
  and used only with the **define** option.
