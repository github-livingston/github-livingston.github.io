 **EXTRACT**

  This command produces a 2D mesh object from a 3D mesh object. A
  material interface, a plane , an isosurface or a network may be
  extracted. A plane may be defined by three points in the plane, by a
  vector normal to the plane, by three points on the axes of the
  space, or by the coefficients of the plane equation ax+by+cz=d. An
  isosurface is defined by the value of the surface and the mesh
  object attribute to test for this value. An interface is defined by
  the material(s) bounding the interface. region1, [region2]are the
  material numbers or the material region (mregion) names whose
  interface is to be extracted. Use **-all-** to extract from all
  interfaces. The **[pset](../conventions.md)** syntax can be used
  to limit the action of the extract with the interface and network
  options only. The other options ignore pset.  The output 2D mesh
  object is cmoout; the input 3D mesh object is cmoin.
 
  A network is defined as the material interface network from the mesh
  object. Unlike the other extract forms, this extracts the "parent"
  interface and not the "child" interface, and ignores boundaries. The
  output cmo also contains a new attribute "map" which maps nodes in
  the output cmo to (parent) nodes in the input cmo. This is supposed
  to work for 2D meshes (tri, quad, or hybrid) in 2D or 3D and 3D
  meshes (tet, pyr, pri, hex or hybrid).
 
  The surfmesh option is described by following the link:
  **[extract/surfmesh.](dump/EXTRACT_SURFMESH.md)**
 
  The output MO will be oriented such that the outward normal of the
  plane that defines the surface will point in the same direction as
  the normals for the triangles in the output MO. If the command
  extracts on an isosurface, the output MO will be oriented such that
  the normals for the triangles point in the direction of increasing
  field. If the command extracts on an interface, the output MO
  triangles will be oriented the same as the triangles extracted from
  region1 of the input MO. In the case of a plane extracted along all
  or a portion of a material interface, only those points that lie
  inside the material (i.e.: away from the direction of the normal)
  will be picked up. If the extraction is on a boundary, the normal to
  the extraction plane must point out of the material in order for
  points to be picked up.

 **FORMAT:**

 **extract** **/plane**/hreepts/x1,y1,z1/x2,y2,z2/x3,y3,z3/ifirst,ilast,istride/cmoout/cmoin

 **extract** **/plane** **/ptnorm**/x1,y1,z1/xn,yn,zn/
 ifirst,ilast,istride/cmoout/cmoin

 **extract** **/plane** **/axes**/xv,yv,zv/ifirst,ilast,istride/cmoout/

 **extract** **/plane** **/abcd**/a,b,c,d/
 ifirst,ilast,istride/cmoout/cmoin

 **extract** **/isosurf**/attribute/value/
 ifirst,ilast,istride/cmoout/cmoin

 **extract** **/intrface**/region1/ifirst,ilast,istride/cmoout/cmoin

 **extract** **/intrfac2**/region1/region2/ifirst,ilast,istride/cmoout/cmoin

 **extract/network**/ifirst,ilast,istride/cmoout/cmoin

 **extract/surfmesh**/1,0,0/cmoout/[cmoin]

 EXAMPLE:

		cmo/create/3dmesh/

		* add an attribute to contain a field for refinement and extraction
		cmo/addatt/3dmesh/boron
		cmo/modatt/3dmesh/boron/ioflag/gx/
		cmo/modatt/3dmesh/boron/interp/linear/

		*  simple unit cube divided into 2 region by a horizontal plane
		surface/cube/reflect/box/.0,.0,.0/1.,1.,1./
		surface/mid/intrface/plane/0.,0.,.5/1.,0.,.5/1.,1.,.5/
		region/r1/ le cube and le mid /
		mregion/m1/ le cube and lt mid /
		region/r2/ le cube and gt mid /
		mregion/m2/ le cube and gt mid /

		* start out with just a few nodes
		createpts/xyz/3,3,3/0.,0.,0./1.,1.,1./1,1,1/
		setpts
		search
		settets

		* put some values on the field
		doping/gaussian/boron/set/1,0,0/xyz/0.0,0.0,0.0/1.,0.,0./0.5/ &
		3.23e+20/0.063/

		* use refine to add more detail - note only linear interpolation
		* between the few original nodes - one would never really do this
		without

		* recalculating the field on the finer mesh
		refine/maxsize///edge/1,0,0/0.01,0.0,0.0/
		recon
		refine/constant/boron/linear/edge/1,0,0/1.3+20/
		recon

		* extract a plane
		extract/plane/threepts/0.,0.,0./1.,0.,0./1.,0.,1./1,0,0/2dmesh/3dmesh
		pset/p1/geom/xyz/0.,0.,0./.5,.5,.5/

		* extract a plane - note pset is ignored!
		extract/plane/threepts/0.,0.,0./1.,0.,0./1.,0.,1./pset,get,p1/2dm1/3dmesh
		dump/gmv/gmv.3dm/3dmesh/
		dump/gmv/gmv.2dm/2dmesh/
		dump/gmv/gmv.2d1m/2dm1/
		cmo/select/3dmesh

		* refine some more
		refine/constant/boron/linear/edge/1,0,0/1.3+20/
		recon

		* now get an isosurface
		extract/isosurf/boron/1.0e+20/1,0,0/2dm2/3dmesh
		dump/gmv/gmv.2dm2/2dm2

		* get the boundary of one region
		extract/intrface/m1/1,0,0/2dm3/3dmesh
		dump/gmv/gmv.2dm3/2dm3

		* get the interface between two regions
		extract/intrfac2/m1/m2/1,0,0/2dm4/3dmesh
		dump/gmv/gmv.2dm4/2dm4

		* try the network option
		extract/network/1,0,0/2dm5/3dmesh
		dump/gmv/gmv.2dm5/2dm5

		* get the surface mesh - note interface plane is included
		extract/surfmesh/1,0,0/2dm6/3dmesh
		dump/gmv/gmv.2dm6/2dm6
		finish
