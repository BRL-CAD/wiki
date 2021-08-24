# GSoC 2014 Project Proposal : LibreCAD Kernel kickoff

## Personal Information

**Name:** Gaganjyot Singh

**Email Address:** thegaganx@gmail.com

**IRC Username:** gaganjyot

**Brief Background Information:**

Studying in second year bachelors degree in computer science and
engineering from Chandigarh Engineering College, Chandigarh, Punjab,
India. Working with CAD softwares like LibreCAD, FreeCAD and BRL-CAD and
CAD formats as DXF, DWG. GSoC 2013 student.

**Phone number:** +91 988 836 2700

**Programming background :**

As it comes to programming languages I prefer C/C++ and Python, in which
I also have more experience (about 2 years in Python and more than 4
years with C/C++). Other programming languages I have experienced: PHP,
Vala, Bash Scripting, Assembly language. Versioning tools: I am quite
familiar with Git (I update my work done on github using git) and SVN
(maintainer of GNU Dr. Geo and commit code using SVN).

## Project Information :

### Project Title: LibreCAD Kickoff

### Brief Summary:

LibreCAD v3 kernel was developed in 2012 by Ries Van Twisk as in
experimental stage using modern technologies and the new C++11 standard
code and libraries. A kernel is the part of any software which stands
the base for software. A CAD kernel is one which manages the various
operations such as scale, move, copy, trim, rotate. It manages the
entities, attributes of entities and the data/information of the entity.
It also manages the way the data is stored in memory and how the data
will be written to a file ( file format ) or storing the values in a
database. This project will extend the new completely rewritten code
base so as to stand as the base for the new LibreCAD.

### Detailed Description:

LibreCAD when started was a fork of QCADv2 community edition. The QCAD
version was only working on QT3 while qt 4 was in the market. So
LibreCAD was forked and ported to Qt4. This fork was about 10 years ago
and hence the codebase is quite old. To overcome this problem, Ries
started developing a new versions of LibreCAD from scratch. This new
version, so called the LCv3 is divided into 3 parts.

1.  The UI
2.  The Kernel
3.  The CAD viewer

The Kernel ( My playground ):

The kernel is the base of this CAD software. It does the operations that
are to be done on any entity. This kernel follows the immutable entity
approach. Every entity in this kernel has its own unique ID. This means
if an entity is created, if any operation is to be performed on it, it
will be deleted and a new entity will be created with the operation
performed on it with the same ID as of the deleted entity. Listed below
are the operations, entities and the intersection pattern which is to be
implemented.

#### Operations :

##### Move:

The implementation of the Move operation involves ( atleast ) an offset.
Offset is the value by which the entity needs to be moved.

For the Line, the move can be implemented as

void move_line ( coordinate offset ) {

start_point = start_point + offset;

end_point = end_point + offset;

}

delete_line(id); // Immutable approach, older gets deleted and a new
will be created.

new_line(start_point, end_point); // values changed above.

For Circle and Arc, the center will be moved by the offset value For the
Ellipse, with the center another attribute will be For the Text entity,
the placement points will be moved by the offset.

This pseudo-code refers to very basic move. While moving the user can
also rotate if he wants. It will look something like, void move_line (
coordinate offset, double angle ) // angle by which the entity needs to
be rotated. Though circle is a special case since it will look same on
rotation.

##### Copy :

Copy includes almost the same code as the code of Move. Even in the
copy, the new copy will be placed at some offset. The only difference
between Copy and move is only that in the move, the older entity is
deleted but in Copy both the entity remain in the document.

Copy also supports rotation while copying. void copy_entity (
coordinate offset, double angle ) // where entity will be replaced by
specific entity name in the entity specific classes.

Copy will support a special feature of multiple copies. void
copy_entity ( coordinate offset, double angle, int copies ) // copies
will be created each at a difference of offset provided in first
argument.

##### Rotate:

Rotate is required for rotating an entity. It could be rotating with
respect to any other special point ( such as the origin ) or may be with
respect to entity it self.

void rotate ( double angle ) {

// Rotation around itself at some angle.

// first the double value will be converted into a coordinate using sin
cos functions for x and y coordinate respectively and then the algo will
be applied to rotate the entity. Which is like

temp_x = x \* angle.x – y \* angle.y // stored in temp since we need
older x value

y = x \* angle.y – y \* angle.x

x = temp

}

#### Entites:

Two entities will be added. 1) Text 2) Dimension

-   Text will have support for the following attributes,

<!-- -->

-   -   Insertion point : The point at wich entity is to be inserted.
    -   SecondPoint : It is used by the aligned fit.
    -   Widthrel : It is the width of reference rectangle around the
        text.
    -   Height : Height of text
    -   Valign : Vertical Alignment of the Dimension value text
    -   Halign : Horizontal Alignment of the dimension value text
    -   Text : Text value held by dimension entity
    -   Style : Style of the text
    -   Angle : If the text is aligned at some angle

<!-- -->

-   Dimension has the following attributes,

<!-- -->

-   -   DefinitionPoint : The point at which dimension is defined
    -   MiddleOfText : Middle of the dimension text
    -   Valign : Vertical Alignment of the Dimension value text
    -   Halign : Horizontal Alignment of the dimension value text
    -   LineSpacingStyle : Spacing style if any for the dimension
    -   LineSpacingFactor : Spacing factor if any
    -   Text : Text value held by dimension entity
    -   Style : Style of the text
    -   Angle : If the text is aligned at some angle

#### Intersection Stuff

The Kernel manages the intersection of two entities. The types of
entities being Arc, Line, Ellipse, circle, point if we create the
functions to check and return intersection between entities, we will get
a number of functions. For example :

intersect_line_line(line, line);

intersect_line_arc(line, arc);

intersect_line_ellipse(line, ellipse);

and so on for every entity.

The quadratic of any entity can be found. Then the quadratic of two
entities can be passed to a common function that just calculates the
intersection points from the two quadratic equations.

quad1 = line.get_quadratic()

quad2 = circle.get_quadratic()

quad3 = ellipse.get_quadratic() // ellipse quadratic equation

get_intersection(quad1,quad2) // will give intersection points of line
and circle

get_intersection(quad1,quad3)// will give intersection points of line
and ellipse

For example,

Approach 1 ( Line Line direct intersection calculation )

void Intersect::visit(shared_ptr<const lc::Line> l1,
shared_ptr<const lc::Line> l2) {

`   `[`geo::Coordinate`](geo::Coordinate)` p1 = l1->start();`
`   `[`geo::Coordinate`](geo::Coordinate)` p2 = l1->end();`
`   `[`geo::Coordinate`](geo::Coordinate)` p3 = l2->start();`
`   `[`geo::Coordinate`](geo::Coordinate)` p4 = l2->end();`

`   double num = ((p4.x() - p3.x()) * (p1.y() - p3.y()) - (p4.y() - p3.y()) * (p1.x() - p3.x()));`
`   double div = ((p4.y() - p3.y()) * (p2.x() - p1.x()) - (p4.x() - p3.x()) * (p2.y() - p1.y()));`

`   // TODO: We properly should add a tolorance here ??`
`   if (fabs(div) > 0.0) {`
`       double u = num / div;`
`       double xs = p1.x() + u * (p2.x() - p1.x());`
`       double ys = p1.y() + u * (p2.y() - p1.y());`
`       `[`geo::Coordinate`](geo::Coordinate)` coord(xs, ys);`

`       if (_method == Method::Any || (_method == Method::MustIntersect && l1->isCoordinateOnPath(coord) && l2->isCoordinateOnPath(coord))) {`
`           _intersectionPoints.append(coord);`
`       }`
`   }`

}

Approach 2 ( First calculate quadratic of entities and then calculate
intersection from quadratic )

void Intersect::visit(const shared_ptr<const lc::Line>& l1, const
shared_ptr<const lc::Line>& l2) {

//getIntersection QList<geo::Coordinate>&&
points=LC_Quadratic::getIntersection(l1-&gt;getQuadratic(),
l2-&gt;getQuadratic()); // Where getQuadratic is a function to calculate
quadratic of lines. if (points.empty() == false )

`   _intersectionPoints.append(points);`

}

References : <http://en.wikipedia.org/wiki/Quadratic_form>

Maths will be taken from LibreCAD2 :

<https://github.com/LibreCAD/LibreCAD/blob/master/librecad/src/lib/math/lc_quadratic.h>

<https://github.com/LibreCAD/LibreCAD/blob/master/librecad/src/lib/math/rs_math.h>

### Deliverables:

The project can be divided in at least 4 parts, so all of this can be
considered a specific measurable goal (one for every feature
implemented). LibreCAD v3 Kernel will be delivered with the support of
following,

1.  Operations:
    1.  Move
    2.  Copy
    3.  Rotate
2.  Entities :
    1.  Text
    2.  Dimensions
3.  Intersection support extended to Arc, Line, Circle, ellipse.
4.  Unit tests so as to test the working of implemented stuff.

### Milestones( or Plan ):

19 May – 27 May: Move will be implemented to all the entities.

28 May – 5 June: Copy will be implemented to all the entities.

6 June – 14 june: Rotate will be implemented to all the entities.

15 June – 25 June: Text entity will be implemented with support for
move,copy and rotate.

26 June - 6 July Dimension support will be added with support for the
operations.

7 July – 27 July Visitor pattern will be implemented in this time. (
Most important and challenging of all tasks so have provided the maximum
time).

28 July – 10 August: Unit tests for copy, move rotate will be added.
Unit test for adding dimension and text will be added.

11 August – 18 August: Code Cleanup, fixing bugs if any and
preparing/submitting final submission.

### Future work / scope (Post GsoC):

-   After the GSoC, the LibreCAD kernel will have functionalities to be
    embedded into the LibreCAD v3 and hence on with the development of
    UI and CAD viewer of LibreCADv3, it will be soon replacing the
    LibreCADv2.
-   Moreover since this is a complete rewrite, this way the license be
    totally on the LibreCAD team and hence we will be able to avoid the
    conflict that is going from about 3 years between the LibreCAD and
    LibreDWG library. This way users will also be able to read the DWG
    files into LibreCAD hence uplifting the status of CAD on opensource
    platforms.

## Time Availability:

I will be available 40 to 48 hours a week, if needed can spend more.

## Why LibreCAD?

My interest in CAD programs. There is no CAD program till now which
satisfies my needs exactly right now on Linux. LibreCAD meets my demands
more than others. Hence I will be making libreCAD do all my work.

## Why me?

I wish to lift up the level of open source CAD and Linux. With previous
Summer of code done with a CAD library, I have gained more experience
about the working of CAD. There is a great need of a person who
basically has knowledge of softwares like AutoCAD, LibreCAD, BRL-CAD,
SolidWorks, NX and knowledge in field of machines, I being a mechanical
engineer and a programmer have undergone rigorous practice for CAD
softwares listed above. Moreover, My recent college project was also
first designed on solidworks and BRL-CAD before bringing it to reality.
I therefore can easily understand user requirements can and bring it to
reality. At last my wish to work for open source/open source CAD and my
passion for programming.