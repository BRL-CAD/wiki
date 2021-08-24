MGED is currently the primary geometry editor in BRL-CAD. By default,
MGED will provide a graphical user interface for modeling, editing,
render, and managing geometry models. MGED can also be run in a
command-line "classic" mode using the "-c" command-line option, which
can also be used for scripting interactions.

MGED does **not** provide a discoverable graphical user interface. Going
through the available tutorials and documentation is ***required*** to
be proficient. MGED is *expert-friendly* with minimal documentation and
feedback inside the application itself.

MGED maintains immediate storage persistence, i.e. automatic and
immediate saves. There is no need to save your file(s) as all
modifications are immediately saved as soon as they are applied.

MGED (and most of the BRL-CAD tools) perform constant validity checking
and will abort early at the first sign of error or corruption detection
in order to minimize or prevent data loss at all costs.

MGED is intentionally a highly modal editor (similar to vi) in that
there are various editing modes and states that you can go to/from while
editing geometry.

MGED will not automatically display the contents of a geometry database
when it is opened/loaded. Unlike other CAD systems, a single BRL-CAD
geometry database can contain an arbitrary number of complete geometry
models. Run the MGED [tops](tops "wikilink") command or use the
Tools-&gt;Geometry_Browser to see the top-level objects in an opened .g
geometry database.

There is extensive documentation and tutorials available for MGED under
[Documentation](Documentation "wikilink").

See also:

1.  1.  (Also available as a )

    2.

2.  [:Category:MGED](:Category:MGED "wikilink")

[category:commands](category:commands "wikilink")