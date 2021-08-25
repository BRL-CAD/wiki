## **Annotations: Implement support for 2D annotations, labels that can be added to geometry**

The project is divided into two parts:

-   Creating a new primitive for annotations
-   Rendering the primitives to the wireframe view

### **Creating a new primitive for annotations**

-   Annotations comprise of:
    -   Notes and Labels : Single line or Multiline text
    -   Leader Lines (includes GD&T)

<!-- -->

-   The primary goal is to implement simple leader lines, so that we
    have a basic frame for further amendments.
-   Support for view Independent annotations: This is resolved by using
    a separate coordinate system in two dimensions for the labels. This
    coordinate system has a direct mapping with the original 3D
    coordinate system that comprises of the wireframes.
-   Coordinate system is nothing but a transformation matrix. This
    matrix projects all the points in the 3D coordinate system to the 2D
    coordinate system that will contain the annotations.
-   The plan of action comprises of the creation of a new primitive
    “annotation”. The basic workflow can be related to that of the
    sketch primitive.
-   The annotation primitive will comprise of various parameters that
    define the labels.
-   Here we are aiming for manual annotations. The parameters will be
    provided by the user through the command line. ”in” followed by
    various parameters some of which are:
    -   Position
    -   Text - leader line
    -   Additional object reference name

**Container for annotations**

-   The container for annotations will be defined in geom.h or other
    desired location.
-   The container will comprise of structs, each of which will
    correspond to an annotative identity.
-   The structs to be included are(subject to modification after further
    discussions):
    -   struct line_seg
    -   struct curve
    -   struct carc_seg
    -   struct text_label
    -   struct linear_dimen
    -   struct angular_dimen

\[ linear_dimen & angular_dimen: Not a priority, may be added later
on\]

-   Once we have a fully functional primitive comprising of arcs,
    segments and text, beizer_seg and nurb_seg will be also ported.
-   The final struct will be of the annotation_internal that contains:
    -   The point in the 3D coordinate system that maps to the origin in
        the 2D annotation coordinate system.
    -   The curves of the primitive.
    -   Some other required parameters and flags.
-   Next step would be to define annotations.c
-   The annotations.c will comprise of various functions:(these
    functions basically append the annotations according to the details
    found in the internal object)
    -   Annotation_validation function
    -   Functions for appending the line with text and corresponding
        parameters.
    -   Returning the appended annotation details though an external
        return object

**Properties**

-   Provision for altering the properties of the annotation created
    through the command line, if time permits. \*Otherwise this is
    something that is to be done once we have a basic frame ready for
    the annotations. The properties can be changed using the annotation
    keyword in the command line.
-   These properties include(subject to change after discussion) :
    -   Font
    -   Color
    -   Line Width
    -   Text alignment and placement
    -   Some other parameters

### **Representation in the 3D view**

-   The second part of the project is to render the annotation object
    formed.
-   As mentioned before, we aim for view-independent annotations.
-   For this to be accomplished we cannot define the annotations in the
    primitive coordinate system as on rotation or zoom the annotations
    remains of no use to the viewer.
-   coordinates from the primitive -&gt; 3D world coordinates -&gt; 2D
    plane (e.g. with a perspective) -&gt; 2D screen coordinates\[working
    on this\]
-   So a new coordinate system needs to be defined for the annotations.
-   This coordinate system unlike the other is two dimensional.
-   By a new coordinate system we mean the existence of a transformation
    matrix that maps all points of the 3D system to the 2D one.
-   The process is quite similar to calibrating a camera.
-   For the rendering part, rest is the same as that for other
    primitives only thing being that no ray tracing takes place here (as
    of now).
-   If time permits the project, I will provide functionalities to
    portray the annotations on a rendered image.

**Project Extension**

After discussions with the mentors, some extension ideas came up:

-   Functionality to set up the annotation properties for the primitive
-   Extension for the geometric shape of the annotation
-   Common functionality for the annotation and the sketch primitive in
    order to reduce redundancy
-   Features related to the coordinate system like the annotation
    scaling
-   Algorithm to provide a bounding box for the text using the relative
    coordinates

### **Timeline**

As per the Google Summer of Code guidelines, work is supposed to begin
on May 5, 2017 upto August 21,2017. This is a tentative timeline, as I
am not sure regarding the time to be taken by some parts of the project.
Results are to be announced on May 4, so schedule goes accordingly. I’ll
start working from April itself, and try to improve my proposal as much
as I can till the start of community bonding period, irrespective of the
project selection.

**Deliverables** :

Community bonding period

\[ May 5 - May 20 \]:Review the pipeline Take inputs from the community
Gain insight into the on screen rendering of the primitive

Coding period ( I aim to start coding from May 21 onwards)

-   \[May 21 - June 1\]:Define the annotation container with all the
    basic forms( line, curve)

<!-- -->

-   \[June 1 - June 20\]:Start writing functions in annotation.c

<!-- -->

-   \[June 20 - June 26\]:Tests for the written functions


Clear any backlog if present

-   1st Mid Term Evaluation\[June 27 - June 30\]

<!-- -->

-   \[July 1 - July 20\]:Implement support for the new coordinate system
    and port the functions left

<!-- -->

-   \[July 20 - July 24\]:Write the tests and solve any issue if arises

<!-- -->

-   2nd Mid Term Evaluation\[July 25 - July 27\]

<!-- -->

-   \[July 28 - Aug 5\]:Support for rendering the primitives

<!-- -->

-   \[Aug 5 - Aug 15\]:Overlay rendered image with annotations

<!-- -->

-   \[Aug 15 - Aug 20\]:Write tests and clear any issue if arises

<!-- -->

-   \[Aug 20 - Aug 25\]:Documentation support for the written primitive

<!-- -->

-   Final Evaluation\[Aug 25 - Aug 29\]


\[ If the work does not complete in the period by any chance, then I’ll
work even after the coding period ends. The timeline is subject to
change after discussion with the mentors\]

### **Milestones**

-   Fully functional annotations for basic leader line callouts.
-   Fully functional annotations for GD&T labels.
-   Tests for those annotative elements
-   Documentation Support

### **Why BRL-CAD ? Why me?**

I love the way the community members encourage a person to work. I was
looking for a project that could match my research interests and BRL-CAD
provided me with the project. I was always helped by the community
members while I was working on my first patch, even if I was going
totally wrong. I thought of applying last year itself but resisted,
because I felt the need to gain more experience in this field and this
is the last opportunity for me to be a part of the organization and I
simply don’t want to miss it.

Open source has been a part of my life, since I joined college. I have a
decent number of contributions to Joomla! and The Processing Foundation.
Later on I started working in the field of Computer Vision. I started
working on modeling systems as a part of my research. I was looking for
something that could match my research interest as well as preserve my
interest for open source. After gaining enough knowledge in this area I
thought of finally applying with BRL-CAD. I have submitted three patches
till now and will continue to do so in the near future. Development
process is something with which I’m familiar. I am active on irc and as
well as the mailing list and am in contact with the mentors and will do
the same in the coming time.

### **Personal Details**

-   **Name** : Shubham Rathore

<!-- -->

-   **Country** : India(UTC+5.30)

<!-- -->

-   **Contact Details**
    -   Email : shubhamrathore1947@gmail.com
    -   University Email : shubham.rathore@students.iiit.ac.in
    -   IRC Nick : gabbar1947

<!-- -->

-   **Education**
    -   Centre for Visual Information Technology(CVIT)\[1\],
    -   International Institute of Information Technology,
        Hyderabad(IIIT-H), India

<!-- -->

-   **Github**:GABBAR1947