 **RADAPT**

  The command radapt performs r-adaption on 2D or 3D mesh objects. For
  simple smoothing see command smooth. **radapt** takes a 2D or 3D mesh
  object and moves nodes (specifically the nodes selected by
  ifirst,ilast,istride), without changing the connectivity of the
  grid, in order to adapt the mesh to best capture the behavior of a
  specified field or to an *adaptionfunction* (fadpt) supplied by the
  user.

  There are two adaptive smoothing algorithms available:
  1. **esug** --- Elliptic Smoothing for Unstructured Grids. This can
  only be used on triangular 2D mesh objects. If field is specified in
  the command line, **esug** will attempt to adapt the grid to the
  specified field. If the keyword **user** is specified in the command
  line, **esug** will attempt to adapt the grid to an *adaption
  function* defined by the user-supplied subroutine fadpt. (Ahmed
  Khamayseh and Andrew Kuprat, "Anisotropic Smoothing and Solution
  Adaption for Unstructured Grids", Int. J. Num. Meth. Eng., Vol. 39,
  pp. 3163-3174 (1996)).
  
  2. **mega** --- Minimum Error Gradient Adaption. For adaptive
  smoothing purposes, **mega** can only be used on 3D meshes, and only
  in conjunction with a user-supplied subroutine fadpt or with a user
  specified attribute field. If adaption is to an attribute field,
  then ****radapt**** may be instructed to use the interpolation mode
  associated with the attribute to **refresh** the attribute values.
  The default is **stale** in which case the attribute value will not
  be updated to reflect the new node position. In either case, the
  user is cautioned to carefully consider the validity of the data
  used for the adaption. **mega** can be used to adapt hybrid meshes
  as well as tetrahedral meshes. (Randolph E. Bank and R. Kent Smith,
  "Mesh Smoothing Using A Posteriori Error Estimates", SIAM J. Num.
  Anal. Vol. 34, Issue 3, pp. 9-9 (19))

  In the field adaption form, the user has specified a valid field
  from the current mesh object, and r-adaption is to be based upon
  this field. Typically, if the field has large gradients or curvature
  in a particular region, r-adaption using this field will cause nodes
  to be attracted to the region of interest. (**esug** adapts
  especially to large gradients, **mega** adapts especially to large
  second derivatives---"curvature".) If adaption is to an attribute
  field, then ****radapt**** may be instructed to use the interpolation
  mode associated with the attribute field to **refresh** the
  attribute values. The default is **stale** in which case the
  attribute value will not be updated to reflect the new node position
  adaption. In this case, the user should reduce the number of
  adaption iterations to less than 4, since r-adaption with stale data
  becomes meaningless. (See **maxiter**\_**sm** variable description
  below.) The user takes on the task of refreshing the field values by
  e.g. re-solving a PDE for the new field values on the new mesh. If
  **refresh** is specified, the r-adaption routine will automatically
  interpolate the new field values every iteration, using a call to
  the **doping** command. In this case, the number of adaption
  iterations need not be reduced from the default value of 25. In
  either case, the user is cautioned to carefully consider the
  validity of the data used for the adaption.

  In the **user** form, the mesh will r-adapt to the function returned
  by the subroutine fadpt which must be supplied by the user.

  Specifying **position** signifies that the x-y-z values of the nodes
  in the current mesh object will be altered. (Other argument values
  allow for modification options that are not yet implemented.)

  If **esug** is used (currently available in 2D only), the degree of
  node adaption will depend on the scale of the specified field. In
  this case, the results of adaption of the grid to the field can be
  altered by using one or more **field** commands beforehand to modify
  the field. For example, by increasing the scale of a field using
  **field** **/scale**, the **esug** algorithm will produce grids with
  increased numbers of nodes in the regions where the field
  experiences relatively large gradients. By volume averaging a field
  using **field** **/volavg**, **esug** will cause a more gentle form
  of adaption with a better grading of elements. By composing the
  values of the field with **log** or **asinh** using **field**
  /ompose**, one can cause **esug** to shift nodes to where the
  logarithm (or hyperbolic arcsine) of the field has interesting
  features, rather than where the field itself has interesting
  features. *Note: Since the* **mega** *adaptive smoothing algorithm
  is rigorously based on error minimization, it is in general of
  little or no value to modify the adaption function for this
  algorithm. In particular, rescaling has no effect on the output.*

  The code variable **maxiter**\_**sm** (default=25) can be set using
  the **assign** command before calling ****radapt****. This controls the
  maximum number of adaption iterations to be performed by ****radapt****.
  If convergence is detected , fewer iterations will be performed. If
  field data is allowed to become **stale** during the course of
  r-adaption, **maxiter**\_**sm** should be reduced (e.g. less than
  4).

 **FORMAT:**

**radapt** / position/  esugmega/ ifirst,ilast,istride / field/ refreshstale
**radapt** /  position/   esugmega / ifirst,ilast,istride /  user

 **EXAMPLES:**

Using **esug**, adapt all nodes in 2dmesh to the density field. Do
not update data.
 
		radapt / / esug **/ 1,0,0 / density
 
Assuming a default 3D cmo, use **mega** to adapt the mesh to the
adaption function supplied by the user via subroutine fadpt.
Afterwards dope the density field with the fadpt function values.
 
		radapt / / / 1,0,0 / *user
		doping / user / density / set /1,0,0/

 **FORMAT FOR fadpt**:

  subroutine fadpt(xvec,yvec,zvec,imtvec,nvec,time,fvec)

Argument | Description
--- | ---
xvec, yvec, zvec | Vectors of x, y, and z coordinates of the points where the function is to be evaluated.
imtvec | Vector of **imt** values (material types) for the case  where function value depends on material type as well as position
(ie. functions with discontinuities).
nvec | Vector length (= number of places where function is to be evaluated).
time | Time (scalar), for time-dependent functions.
fvec | Vector of adaption function values.

 
 **SAMPLE FUNCTIONS AND INPUT DECKS**

  To demonstrate adaptive smoothing using **mega**, examples are
  available which use the files
  [fadpt\_boron.f](../../fadpt_boron.f),[input.boron.3dtet](../../input.boron.3dtet),[input.boron.3dhex](../../input.boron.3dhex),[fadpt\_gyro.f](../../fadpt_gyro.f),
  [input.gyro.3dtet](../../input.gyro.3dtet),[input.gyro.3dhex](../../input.gyro.3dhex).

  1
. Boron density function fadpt\_boron.f. Load the file fadpt\_boron.f
  ahead of the **LaGriT** libraries; this will cause the default fadpt
  subroutine to be displaced by the one in this file. The result is that
  now 3D adaptive smoothing will attempt to adapt 3D tetrahedral or hybrid
  meshes to the boron density function devised by Kent Smith of Bell Labs.
  This function has a maximum value of 1.1 x 1018, and drops rapidly to
  zero; the function attains its largest values on a T-shaped region in
  space and provides very challenging isosurfaces to capture. Two input
  decks use this function:
 
   a
. input.boron.3dtet. This deck generates and adapts a tetrahedral mesh
   to the boron function.  A snapshot of the adapted grid may be seen at
   [boron.png<a href="https://lanl.github.io/LaGriT/assets/images/boron.png).

   b. input.boron.3dhex. This deck generates and adapts a hexahedral mesh
   to the boron function.   A snapshot of the adapted grid may be seen at
   [boron.hex.png.<a href="https://lanl.github.io/LaGriT/assets/images/boron.hex.png)
 
  2
. "Gyroscope function" fadpt\_gyro.f. This function has large second
  derivatives near three rings of unit diameter which are aligned with
  each of the three coordinate planes which pass through the origin.
  Adaption to this function results in the pulling of the grid towards the
  rings when running the following two input decks:
 
   a
. input.gyro.3dtet. This deck generates and adapts a tetrahedral mesh
   to the "gyroscope" function.   A snapshot of the adapted grid may be
   seen at [gyro.png<a href="https://lanl.github.io/LaGriT/assets/images/gyro.png).

   b. input.gyro.3dhex. This deck generates and adapts a hexahedral mesh to
   the "gyr/scope" function.   A snapshot of the adapted grid may be seen
   at [gyro.hex.png<a href="https://lanl.github.io/LaGriT/assets/images/gyro.hex.png).
 
  RELEVANT LaGriT VARIABLE FOR radapt

  The **maxiter\_sm** variable is provided to control the maximum
  number of iterations used by **radapt** on a single call. By
  default, this variable is set to 25, but this can be changed by the
  user. For example,
 
      assign / / / maxiter_sm / 50
      
  changes the maximum number of iterations to 50. If **radapt**
  detects a sufficient amount of convergence, it will terminate
  smoothing in less than **maxiter\_sm** iterations.
