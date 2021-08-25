# Community bonding period

## 7 May 2012

-   build the brl-cad svn on VM successfully.
-   build the brlcad-7.18.4 on windows(vs2005),but some link error
    occured from libtclcad.lib(solved go_init(..)undefined)

## 8 May 2012

-   get familiar with the Brep structure.

`    ON_CurveArray m_C2;//Pointers to parameter space trimming curves (used by trims)`
`    ON_CurveArray m_C3;//Pointers to 3d curves (used by edges)`
`    ON_BrepEdgeArray m_E;//edges`
`    ON_BrepFaceArray m_F;//faces`
`    ON_BrepLoopArray m_L;//loops`
`    ON_SurfaceArray m_S;//Pointers to parametric surfaces (used by faces)`
`    ON_BrepTrimArray m_T;//trims`
`    ON_BrepVertexArray m_V;//vertexs`
![](/wiki/user/img/brep.jpg)
figure:[1](http://brlcad.org/w/images/5/5e/Brep.jpg)

## 9 May 2012

-   solve the link problem when build brlcad_18.4 in vs2005.(function
    go_init(..) undefinded)
-   understand some important point about NURBS. 3D NURBS is not tensor
    product surface,but it can be represented into tensor product
    surface by mapping 3D NURBS into 4D using homogeneous
    coordinate.(The NURBS BOOK page 30)
-   circle Arc can be represented by
    vector{(1,1,0,1),(1,1,1,1),(2,0,2,2)}in yz plane

## 10 May 2012

-   build brlcad-SVN successfully on my ubantu.(PS:/sh/make_deb.sh is a
    good tool)
-   study some about Nonuniform Scaling of Surfaces.

## 12 May 2012

-   find that the ehy.brep is lack of face and loop in brep
    structure.add them to make a correct brep.

`   int surfindex = (*b)->m_S.Count();`
`   (*b)->NewFace(surfindex - 1);`
`   int faceindex = (*b)->m_F.Count();`
`   (*b)->NewOuterLoop(faceindex-1);`

## 13 May 2012

-   find that computing the longest edge size is in the
    bspile/nurb_tess.c and the nurbs is represented by the form of
    struct face_g_snurb that is different from the ON_BrepSurface.It
    needs to implement a new interface for the longest edge size.

## 15 May 2012

-   configure some plug-in unit for my vim (e.g ctags,cscope,winmanger)

## 19 May 2012

-   submit a patch of brep_debug.cpp.check if the index is in the range
    and string of letter.

# Coding period

## *Week 1*

### 21 May 2012

-   read the code of brep_debug.cpp which has many functions to debug
    the geometry in struct of Brep in mged.

### 23 May 2012

-   update the patch of brep_debug.cpp.add the sub command 'info
    T','info E' for display the information of trims and edges in
    brep.Also, make the 'info' dispaly the information in a range of
    indexed elements for keeping sync with the 'plot'.

### 25 May 2012

-   add a subcommand 'plot SCV' to display nurbs control point net

### 27 May 2012

-   waste a lot of time to test the opennurbs' API of:

` int CreateMesh(const ON_MeshParameters& mp, ON_SimpleArray<ON_Mesh*>& mesh_list) const; `

-   but,it seems difficult to make a good ON_MeshParameters to create
    mesh successfully.read the sources of opennurbs_mesh.cpp

`ON_Mesh* ON_BrepFace::CreateMesh( `
`           const ON_MeshParameters& mp,`
`           ON_Mesh* mesh`
`           ) const`
`{`
` return 0;`
`}`

## *Week 2*

### 29 May 2012

-   do some works on converting nurbs curve and surface to bezier

### 31 May 2012

-   do some works on comput the intersection between a line and a bezier
    curve/surface
-   some materials: the nurbs book and Curves and Surfaces for Computer
    Aided Geometric Design: A Practical Guide.

### 1 June 2012

-   implement RT_ADD_VLIST(vhead, pt1, BN_VLIST_POINT_DRAW) in
    src/libdm/dm-plot.c but it seems that dm-plot.c has nothing relation
    with the brep_debug.cpp

### 2 June 2012

-   implement RT_ADD_VLIST(vhead, pt1, BN_VLIST_POINT_DRAW) in
    src/libdm/dm-ogl.c and upload the patch.
-   make progress for subcommand 'plot SCV' in mged.The patch can
    display not only the control net,but the control point.

## *Week 3*

### 4 June 2012

-   one step that make 2d trimming curve into 3d can be skip because the
    BREP struct has the edge in 3d corresponding to the 3d trimming
    curve.
-   study the qd tree and kd tree for subdivision of nurbs surface in
    paper and the approximation error for the subdivision.

### 6 June 2012

-   figure out the coving triangles to avoid cracks when making boundary
    curve tessellation.
-   figure out the trimming curve tracing when splitting the trimming
    curve into bezier patch.(the active edge,active leaftree)

### 8 June 2012

-   read the opennurbs API and find the
    ON_NurbsCurve::MakePiecewiseBezier() can clamps ends and adds knots
    so the NURBS curve has bezier spans (all distinct knots have
    multiplitity = degree) ,the ON_NurbsSurface also has the same
    member method.It is a better way to convert trimming curve and
    surface into bezier
-   read the opennurbs API and find the ON_NurbsCurve::InsertKnot() can
    make the conversion between Nurbs and Bezier if setting the
    parameter multiplicity equal to degree.,the ON_NurbsSurface also
    has the same member method.

### 10 June 2012

-   add 'info TB' 'SB' to display information piecewise bezier of
    trimcurve and surface.patch has been upload
-   add 'plot TESS index plotres' to draw the trimesh of a nurbs
    surface. the tess has not taken apporimmation into consideration and
    just simply subdivide u,v into plotres steps;

## *Week 4*

### 12 June 2012

-   upload the patch to implement the adaptive bezier subdivision and
    triangle mesh display which includes the function
    bezierApporixmation(...),bezierSubdivision_kdtree..
-   read opennurbs_ext.cpp,especially figuring out the function of

` BBNode* SurfaceTree::surfaceBBox(...)`
` BBNode* initialBBox(...)`
` BBNode*SurfaceTree::subdivideSurfaceByKnots(...)`
` BBNode* SurfaceTree::subdivideSurface(...)`

-   SurfaceTree::subdivideSurfaceByKnots and BBNode\*
    SurfaceTree::subdivideSurface can help me to create the kd/qdtree as
    a represent of bezier subdivision.But the recursion termination
    condition is different.

### 14 June 2012

-   In function of SurfaceTree::subdivideSurface() at
    src/opennurbs_exp.cpp,line 1528 to 1531:

`           const ON_Surface* surf = m_face->SurfaceOf();`
`            localsurf->FrameAt(u.Mid() - uq, v.Mid() - vq, frames[5]);`
`            localsurf->FrameAt(u.Mid() - uq, v.Mid() + vq, frames[6]); `
`            localsurf->FrameAt(u.Mid() + uq, v.Mid() - vq, frames[7]);`
`            localsurf->FrameAt(u.Mid() + uq, v.Mid() + vq, frames[8]);`

Interval u,v is in gloable area, So I think the four lines above need to
be modified.

-   Read the BBNode structure in opennurbs_exp.cpp, BBNode will be used
    to represent the node in qd/kd tree and handling the trimcurve.

### 16 June 2012

-   upload a patch in opennurbs_ext.cpp
-   add three functions below to subdivide bezier,in opennurbs_ext.cpp

`           BBNode* subdivideSurfaceToBezier(...)`
`           BBNode* subdivideBezier(...)`
`           double getBezierApporixmation(...)`

-   add two functions below to create BezierTree root as the struct of
    BBNode

`          bool setFace(ON_BrepFace* face, bool removeTrimmed);`
`          BBNode* createBezierTreeNode();`

## *Week 5*

### 18 June 2014

-   compare surface split between

`           BBNode* subdivideSurfaceToBezier(...)`
`           BBNode* subdivideBezier(...)`
`and `
`          BBNode*SurfaceTree::subdivideSurfaceByKnots(...)`
`          BBNode* SurfaceTree::subdivideSurface(...)`

the original method seem to be unsymmetric when split ell.brep
sphere.brep. But the new method has not taken the edge length into
consideration,so the ratio of lengths in u,v direction may be too long
or too small.

-   understand SurfaceTree::subdivideSurface() at
    src/opennurbs_exp.cpp,line 1528 to 1531, it comes to the same
    result when replacing localsurf into surf because the localsurf's
    domain is change along with the split.

### 20 June 2012

-   figure out the functions below in brep_debug.cpp which is used to
    draw trimmed BBNode of surface.But these functions seem not be able
    to remark the intersections of BRNode and trimcurve

`           void drawBBNode(....)`
`           void drawisoU(....)`
`           void drawisoV(....)`
`           void drawisoUCheckForTrim(.....)`
`           void drawisoVCheckForTrim(.....)`

-   figure out the trimflag of BBNode: m_trimmed,m_checkTrim and the
    function of preptrim() in opennurbs_ext.pp.

when a BBNode is remark as m_trimmed is true, the BBNode has been
remove out from the surface. When a BBNode is remark as m_trimmed is
true, the BBNode in uv region has intersections with the BRNode of
trimcurve,so it need to be check again and compute the interections if
needed.

### 22 June 2012

-   figure out the functions below in opennurbs_ext.h which can help me
    to comput the intersection between BBNode and trimcurve.

`      fastf_t BANode`<BA>`::getCurveEstimateOfU(fastf_t v, fastf_t tol) const`
`      fastf_t BANode`<BA>`::getCurveEstimateOfV(fastf_t v, fastf_t tol) const`

-   add a function below to return the parameter t of the intersection
    based on the two functions above

`      template`<class BA>
`      fastf_t BANode`<BA>`::getCurveEstimateOfT(fastf_t value, bool direction, fastf_t& t, fastf_t tol) const`

-   add a function to sort the BRNode in CurveTree by the t in parameter
    region.

`     sortT(BRNode* first, BRNode* second);`

### 24 June 2012

-   implement TrimNode and TrimLoop to represent the struct of untrimmed
    regions in parameter area.some functions included below:

`      TrimLoop(ON_Interval m_u,ON_Interval m_v):tol(0.000001);//construct`
`      TrimNode* findPos(TrimNode* n);//find the position to insert for a new trimnode`
`      TrimNode* findSamePoint(const ON_2dPoint& pt);//find the node whose point in parameter is equal to pt`
`      bool linkOnTrimNode(TrimNode* pre,TrimNode* next);//link two trimnode which both within the bboxing`
`      bool insertInEdge(TrimNode* pos, TrimNode* n);//insert a new node`
`      TrimNode* travelLoop(TrimNode* n,int step);//travel from a trimnode to form a close loop`

## *Week 6*

### 26 June 2012

-   start to implement BVNode<BV>::doTrimming function in
    opennurbs_ext.cpp.
-   implement getLeavesIntersection(....) to find the bboxings of
    curveleaves which have intersections with the BBNode in UV region
-   calculate the intersection between edge of bboxing and trimcurve's
    leaves(bottom,top,left,right)
-   solve some special sitiuations: intersection on the conner of
    bboxing.

### 28 June 2012

-   continue to implement BVNode<BV>::doTrimming function in
    opennurbs_ext.cpp.
-   deal with a special situation: trim curve is collinear with the
    bboxing's edge. if the start or end point of trim curve is within
    bboxing's edge, it is regarded as the intersection between edge and
    trimcurve.
-   in function of BANode<BA>::isTrimmed(const ON_2dPoint& uv, fastf_t
    &trimdist) const , ' &lt;= ' is used to compare float number. It may
    cause error because float's precision error,So I make some improve
    for it. This function will be useful in doTrimming.
-   link the innerNode in BANode's BBoxing of uv by call the function
    inline bool TrimLoop::linkOnTrimNode(TrimNode\* pre,TrimNode\* next)

### 30 June 2012

-   continue to implement BVNode<BV>::doTrimming function in
    opennurbs_ext.cpp.
-   deal with a special situation: the BVNode covers some trimcurve's
    bboxing which is remarked as m_checkTrim, however, the BVNode has
    no intersections with any trimcurve. the method which I use may is
    not precise enough,So I'll try to make a better one.
-   add two functions for BANode for judging if a point is contained in
    a BANode

` bool containsUV(const ON_2dPoint& uv);`
` bool containsUVClose(const ON_2dPoint& uv);`

-   debug for doTrimming() by subdivide plane surface manually in
    BBNode\* SurfaceTree::subdivideSurface()

## *Week 7*

### 2 July 2012

-   continue to implement BVNode<BV>::doTrimming function in
    opennurbs_ext.cpp.
-   deal with a special situation: if a trimcurve is collinear with a
    edge of BBNode's uv region and a endpoint of the trimcurve is just
    on the uv region's conner, the conner point will not to be the
    intersection.
-   add a flag 'unTrimmed ' in 'TrimLoop' to mark if a BBNode's uv
    region has been trimmed, situation of trimcurve lies on edge,
    endpoint just on edge are included;

### 4 July 2012

-   insert adjacent subdivide hit into every BBNode's uv region.
-   add member var into class BVNode<BV> and assign these member when
    subdividing surface

`    BVNode`<BV>`* north;`
`    BVNode`<BV>`* south;`
`    BVNode`<BV>`* west;`
`    BVNode`<BV>`* east; `
`    BVNode`<BV>`* parent;`

-   add member function into class BVNode<BV> to get adjacent node

`    BVNode`<BV>`* getAdjacentNorth();`
`    BVNode`<BV>`* getAdjacentSouth();`
`    BVNode`<BV>`* getAdjacentWest();`
`    BVNode`<BV>`* getAdjacentEast();`

-   add member function into class BVNode<BV> to insert adjacent
    subdivide hit

`    void insertAdjacentHit();`

### 6 July 2012

-   add a trimcurve for ell.brep and hyp.brep manually to test trimming
-   ell:left:top view,right:left view

![](/wiki/user/img/Ell1.png)
![](/wiki/user/img/Ell2.png)

-   ell:left:local view,right:uv region

![](/wiki/user/img/Ell3.png)
![](/wiki/user/img/Ell4.png)

-   hyp:

![](/wiki/user/img/HYP1.png)
![](/wiki/user/img/HYP2.png)
![](/wiki/user/img/HYP3.png)
![](/wiki/user/img/HYP4.png)

### 8 July 2012

-   continue to debug 'doTrimming'.There exists a situation that some
    trim leafs' bboxings overlap and it is difficult to find the nearest
    trim leaf above a surface leaf's bboxing in uv. Function 'prepTrim'
    mark the surface leaf in such situation as 'm_checkTrim = true'.But
    in some cases, the surface leaf is trimmed out.I changed the
    subdivision depth to 10 manually and tested the rhino0.s in
    mged.Some surface leaves which should be trimmed out are still
    remain.So, need a more accuracy method to check it.
-   image: some BBoxing in uv which should be trimmed are still
    remain(right bottom conner).

![](/wiki/user/img/rhino.png)
![](/wiki/user/img/rhino1.png)

### 10 July 2012

-   find a algorithm for 'TrimLoop' triangulation,algorithm has the
    steps below:

a\) make the node in 'TrimLoop' to form a linked list.

b)for each triangle form by p0,p1,p2 successive in linked list,calculate
the minimum inside angle.

c)find the triangle which has the max minimum inside angle, then record
the triangle and remove the point p1 in the triangle

d)come to (a) until there only exists three points in the linked list

### 12 July 2012

-   Update my patches.

## *Week 10*

### 1 Augest 2012

-   because of pressure of my paper schedule, I need to leave for a long
    time.I must

say sorry that I will not complete the final-evaluation for gsoc.

## *Week 11*

### 6 Augest 2012

-   I'v package my patch into three part after cleaning up and adding
    some comments.

I think the subdividion is OK some more test must be done to ensure my
trimming algorithm is accurate enough.

-   because of large amount of code need to be cleaned up and test but
    time is up, I decide to handle my paper firstly.
-   But I will come back and complete my work finally.
