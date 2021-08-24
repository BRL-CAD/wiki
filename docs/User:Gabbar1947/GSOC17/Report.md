## **Annotations: Implement support for 2D annotations \| Project Report**

The project was divided into two parts:

-   Creating a new primitive for annotations
-   Rendering the primitives to the wireframe view
-   Support for the screen projection

### **Creating a new primitive for annotations**

-   What was basically required was a container to hold things together

`  `[`https://sourceforge.net/p/brlcad/patches/469/#ea23`](https://sourceforge.net/p/brlcad/patches/469/#ea23)
`  `[`https://sourceforge.net/p/brlcad/patches/469/#34f1`](https://sourceforge.net/p/brlcad/patches/469/#34f1)

### **Rendering the primitive on screen**

-   The next part was to add support for the visualization of the
    primitive
-   Input for the primitive also handled through the 'in' command in the
    patches mentioned below

` `[`https://sourceforge.net/p/brlcad/patches/471/#97f3`](https://sourceforge.net/p/brlcad/patches/471/#97f3)
` `[`https://sourceforge.net/p/brlcad/patches/471/#4b72`](https://sourceforge.net/p/brlcad/patches/471/#4b72)

### **Support for the 3D-&gt;2D projection**

![](Example_annot.png "Example_annot.png")

-   Annotations always remain in the plane of the screen
-   Modifying the projection matrices for all the display managers was
    another task
-   Scaling the annotations was another issue
-   All of this was handled by the patches mentioned below

`  `[`https://sourceforge.net/p/brlcad/patches/471/#cd2e`](https://sourceforge.net/p/brlcad/patches/471/#cd2e)
`  `[`https://sourceforge.net/p/brlcad/patches/471/#acd7`](https://sourceforge.net/p/brlcad/patches/471/#acd7)

Here is the link to my
[Proposal](https://brlcad.org/wiki/User:Gabbar1947) The tasks mentioned
in the proposal are completed, just the extension ideas need to be
worked upon.

**Project Extension**

-   These are some of the tasks that I aim to work on in the near
    future:

<!-- -->

-   -   Functionality to set up the annotation properties for the
        primitive( the annotate command)
    -   Features related to the coordinate system like the annotation
        scaling
    -   Algorithm to provide a bounding box for the text using the
        relative coordinates
    -   Editor for the annotations just like the sketch primitive has

**Documentation**

-   Documentation has been provided
    [here](https://brlcad.org/wiki/Annot).
-   [Link](https://rathoresaab.wordpress.com/gsoclogs) to my daily logs.