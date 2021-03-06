BRL-CAD's graphical applications (MGED and Archer in particular) make
use of the Tcl/Tk toolkit to describe their interfaces. Tk has some
limitations when it comes to complex cross-platform application
development, and we are looking to migrate our graphical interface codes
from Tk to the Qt toolkit.

There are two major "directions" that can be attempted:

-   Re-create MGED as a Qt application. MGED is our current "production"
    geometry editing and viewing interface.

<!-- -->

-   Re-create (some of) Archer as a Qt application. Archer is our
    "next-generation" MGED application.

Most likely recreating one of these interfaces in its entirity is well
beyond the scope of GSoC (although we certainly won't complain if you
manage it!) A better strategy is to identify and tackle one aspect of
the problem with an eye towards creating a Qt widget that can be reused
in subsequent applications. If you complete that task, you can build
from there.

Easily the most important "missing" component at this point is the 3D
interactive viewing widget - the centeral widget in Archer's interface
and the "3D display" window in MGED. A good starting point would be to
create a "Qt viewer widget" that can load and display a libdm 3D
context. You will need to handle Qt's OpenGL widget and its interactions
with libdm/libfb, set up key bindings using our existing Tk bindings as
a guide, and ensure that multile views can work successfully (the quad
view mode).

Another major and important piece of the interface is the tree widget
(Archer's is the example to study, and a read-only version has been
implemented in the experimental qged code - the challenge will be to
first get it updating in response to geometry changes in the database.
After that there are any number of additional features needed...)

We're also constructing a custom CAD terminal widget, tailored to the
needs of our CAD system. We have a basic implementation in our
experimental qged GUI, but it needs work - text selection doesn't span
command outputs, we need a way to auto-hide long outputs that aren't the
current output in the history and allow them to expand/contract via some
user mouse interaction, we need an "in-process" graphic for commands
that have launched but haven't yet completed, ideally with a way to
abort them as well (this will require some delving into QThreads and
launching libged commands in separate threads, as well as a limited
control-the-view terminal mode while some potentially database altering
command is running.)

Anyone wanting to tackle this project should have a good familiarity
with things like the Qt event and signals/slots systems as well as the
generic widget systems (most of the pre-packaged Qt widgets aren't going
to be quite what we need, which usually means creating custom widets
with the more general parent classes.) See the qged sources below for an
idea of the approach.

Proposals here should be detailed and demonstrate a firm grasp of the
issues. Qt 5.6 or higher should be used (that is the assumption made in
the existing code, and if you require a newer Qt for some feature or
issue that should be fine - supporting older Qt releases is not
something we're going to spend effort on at this early stage.

# References

-   <http://sourceforge.net/p/brlcad/code/HEAD/tree/brlcad/branches/qtged/src/qged/>
-   <http://qt-project.org/>

Requirements:

-   Familiarity with C/C++/Qt
-   Sufficient familiarity with Tcl/Tk to be able to read and understand
    the intent of the code (key bindings, for example.)