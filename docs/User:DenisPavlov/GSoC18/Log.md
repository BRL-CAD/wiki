-   Community Bonding Period
    -   Read a few mged tutorials and documentation.
    -   Set up an Eclipse project for BRLCAD, tested debug and release
        builds.
    -   Looked through 'librt', 'libged', 'mged' source code.

<!-- -->

-   Week 1
    -   Looked how ged commands are implemented in mged. Created dummy
        'apprt' command ( = added it to 'mged_cmdtab') and tested it in
        mged.
    -   Figured out how to get database filename and view data.
    -   Have been trying to handle Appleseed dependencies and solve some
        problems with c -&gt; c++ calls.
    -   Finally solved the problem and fixed a coresponding
        CMakeLists.txt.
    -   Created a separate binary executable file (like other
        applications in brlcad) for the Appleseed plugin c++ code.
        Called it 'rtapprt', since it's in the 'rt' package for now.

<!-- -->

-   Week 2
    -   Managed to call the binary file from "apprt" callback function
        and get back the output (a naive approach with system() for now,
        will change it to brlcad's pipeline later).
    -   Added a few parameters (like the database filename and names of
        the objects to draw) to the call. Created a small parsing
        routine for it.
    -   Rendered the first image with default materials using Appleseed.
        Image is being saved in the filesystem (current directory).
    -   Separated the plugin's logic into several files, changed a bit
        the intersection function so that it allows to assign materials.
    -   Looked through the rt source code, especially structures related
        to ray intersections and operations with database, like
        "application/partition/region/e.t.c.".

<!-- -->

-   Week 3
    -   Figured out how to properly assign materials using the
        "mater_info" (partition -&gt; region -&gt; mater_info)
        structure from intersections.
    -   Wrote a small routine that checks the shader name, color of the
        region and assigns some Appleseed material.
    -   Tested it on tank_car model using different brdfs: Lambertian,
        Oren-Nayar, Ashikhmin-Shirley, e.t.c.
    -   Have been looking for an efficient way to parse all the
        materials from the database file beforehand and experimenting
        with Appleseed materials trying to figure out the best way to
        translate brlcad's materials to Appleseed's ones.