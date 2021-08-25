## Installation

### From SVN

<code> svn checkout <svn://svn.code.sf.net/p/brlcad/code/brlcad/trunk>
brlcad-svn-trunk

cd brlcad-svn-trunk

cmake ../ -DCMAKE_BUILD_TYPE=Debug -DBRLCAD_BUNDLED_LIBS=Bundled
</code>

### Ubuntu

`sudo apt-get install brlcad`

## Getting Started

-   Start mged from the command prompt, and create a new file for
    storing CAD design data (BRL-CAD calls these files **geometry
    databases** and uses the .g file extension by default)
    -   `mged your_desired_filename_here.g`

### Radio example

-   The following lines of code will produce something that looks like a
    walkie-talkie style radio.
-   It uses BRL-CAD's *Solid Primitive Shapes*
-   At the mged interactive command interpreter window, type the
    following:
    -   `in body.s rpp 0 16 0 32 0 48`
    -   `in btn.s rec 8 30 36 0 3 0 4 0 0 0 0 2`
    -   `in btn2.s ell1 8 33 36 4 0 0 2`
    -   `in spkr.s tor 16 16 16 1 0 0 12 1`
    -   `in ant.s rcc 2 2 46 0 0 48 1`
    -   `in knob.s rcc 4 4 40 8 0 0 5`
-   Pasting or typing those lines should look like this:

![](/wiki/user/img/Mged_radio_view1.png)

-   Press enter if you haven't already
-   If you don't see a window with an image open up, click mged's
    **Tools** menu, then **Graphics Window**

![](/wiki/user/img/Mged_radio_graphic_view1.png)

-   Pressing the keyboard **CTRL** button along with the **left
    mouse-button** will pan around the displayed image
-   Pressing the keyboard **SHIFT** button along with the **left
    mouse-button** will move the view away from or toward the center
    (where the cartesian plane X,Y,Z are 0,0,0)

![](/wiki/user/img/mged_radio_graphic_window.gif)

## Primitive Examples

### tgc

Truncated general cone

Handled by

-   in make form create

Arguments

-   vertex, vectors H A B, magnitudes of vectors C D

![](/wiki/user/img/TGC_mged_brlcad.png)

#### RCC example via TGC

-   An rcc primitive is a special form of a tgc, you can reproduce a
    right-circular-cylinder at vertex 0,0,0 with height 10, and a base
    and top of radius 1 (both in the XY plane):
    -   `in aaa.s tgc 0 0 0 0 0 10 1 0 0 0 1 0 1 1`

<!-- -->

-   increasing the radius of the base and top to 5:
    -   `in aaa.s tgc 0 0 0 0 0 10 5 0 0 0 5 0 5 5`

#### breaking down the command

-   `in `<name of primitive>` tgc (base X, Y, Z) (height vector X,Y,Z) (ellipse base radius part A vector X,Y,Z) (ellipse base radius part B vector X,Y,Z) (top radius scalar C, restricted to same plane active in base part A) (top radius scalar D, restricted to same plane active in base part B)`

#### elliptic cones in either X or Y directions

-   5 in the X direction, 10 in the Y (same at the top)
    -   `in aaa.s tgc 0 0 0 0 0 10 5 0 0 0 10 0 5 10`
-   10 in the X direction, 5 in the Y (same at the top)
    -   `in aaaa.s tgc 0 0 0 0 0 10 10 0 0 0 5 0 10 5`
