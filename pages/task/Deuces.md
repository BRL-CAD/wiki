Below are tasks that are a great starting point for anyone interested in
contributing to BRL-CAD. Most tasks can be completed in just a couple
hours! ***No prior experience with BRL-CAD is required.***

Some tasks may take longer if you aren't set up or haven't done that
type before, but all they all require about the same amount of
experienced effort. Each task has a description, references, and list of
files you'll probably need. Can we make it any easier? [Let us
know](https://brlcad.zulipchat.com).

# Get Set Up

We suggest you [compile BRL-CAD](../doc/Compiling.md) yourself or, if
you have trouble with that, there's a virtual image with everything
preconfigured, ready to go:

1.  [Download our BRL-CAD Virtual Machine (VM) disk
    image.](https://sourceforge.net/projects/brlcad/files/BRL-CAD%20for%20Virtual%20Machines/)
2.  [Install VirtualBox.](https://www.virtualbox.org/wiki/Downloads)
3.  Import the disk image, start the VM, and log in (password is
    "Brlcad!" without quotes).
4.  Run "svn up brlcad-svn-trunk" and
    [compile](../doc/Compiling.md#Configure_your_Build).

# Pick a Task

Once set up, select any task that sounds interesting, read the
references, and [talk with us](https://brlcad.zulipchat.com) for help.
Don't worry if some words are confusing. You got this. All tasks can be
completed by ***anyone*** but are grouped into the following five
interest categories:

-   Code (programming)
-   Documentation and Training (technical writing)
-   Outreach and Research (graphics, marketing)
-   Quality Assurance (testing)
-   User Interface (usability, design)

__TOC__

## Code

*Tasks related to writing or refactoring code*

See the When You're Done section above for details on submitting your
changes.

<table>
<tbody>
<tr class="odd">
<td><h3 id="close_mged_only_when_both_windows_are_closed">Close MGED only when both windows are closed</h3>
<p>BRL-CAD has an interactive geometry editor called MGED. It's often the starting point for beginners and allows creation and manipulation of models using commands. When <em>mged</em> is run, it creates 2 windows: a text console for commands and an interactive graphics window. Currently, if you close the graphics window, it quits the application.</p>
<p>This task involves change behavior so that MGED exits only after closing <em>both</em> windows. Closing just the graphics window or text console should not quit MGED.</p>
<p>Code:</p>
<ul>
<li>src/mged/mged.c</li>
<li>src/tclscripts/mged/openw.tcl</li>
<li>src/tclscripts/mged/bindings.tcl</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="implement_a_primitive_centroid_function">Implement a primitive centroid function</h3>
<p>BRL-CAD provides more than two dozen types of geometry "primitives" such as ellipsoids, boxes, and cones. Every primitive is described by a collection of callback functions, for example rt_<strong>ell</strong>_bbox() returns the bounding box dimensions for an <strong>ell</strong>ipsoid. Wikipedia, Wolfram Mathworld, and various other math sites (and research papers) around the web include the equations for most of our basic primitives while others are more tricky to compute.</p>
<p>This task involves writing a new callback function that takes an rt_db_internal object and calculates its centroid (as a point_t 3D point). There are numerous examples in our code where we compute centroids for other primitives. The primitives that do not already have a centroid callback are itemized in following.</p>
<p>References:</p>
<ul>
<li><a href="http://en.wikipedia.org/wiki/Centroid">http://en.wikipedia.org/wiki/Centroid</a></li>
<li><a href="http://mathworld.wolfram.com/">http://mathworld.wolfram.com/</a></li>
<li>include/raytrace.h: See ft_centroid callback defined in the rt_functab structure</li>
</ul>
<p>Code:</p>
<ul>
<li>src/librt/primitives/table.c</li>
<li>src/librt/primitives/[PRIMITIVE]/[PRIMITIVE].c</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="implement_a_primitive_curvature_function">Implement a primitive curvature function</h3>
<p>BRL-CAD provides more than two dozen types of geometry "primitives" such as ellipsoids, boxes, and cones each described by a collection of callback functions, for example rt_<strong>sph</strong>_bbox() returns the bounding box dimensions for a <strong>sph</strong>ere. Wikipedia, Wolfram Mathworld, and various other math sites (and research papers) around the web include the equations for most of our basic primitives while others are a little more tricky to compute.</p>
<p>This task involves writing the callback function rt_xxx_curve() that computes the curvature at a given point on the surface of a primitive such as;</p>
<ul>
<li>superell</li>
<li>cline</li>
<li>extrude</li>
<li>grip</li>
<li>metaball</li>
<li>hrt.</li>
</ul>
<p>There are numerous examples in our code where we compute the curvature for other primitives like the ellipsoid, sphere, elliptical parabola, etc.</p>
<p>References:</p>
<ul>
<li><a href="http://en.wikipedia.org/wiki/Curvature">http://en.wikipedia.org/wiki/Curvature</a></li>
<li><a href="http://en.wikipedia.org/wiki/Radius_of_curvature_(mathematics)">http://en.wikipedia.org/wiki/Radius_of_curvature_(mathematics)</a></li>
<li><a href="http://mathworld.wolfram.com/">http://mathworld.wolfram.com/</a></li>
<li>include/raytrace.h: See the data structure that holds the curvature of a surface at a point (from Line 296) as well as the prototype for ft_curve() callback function defined in the rt_functab structure ( Line 2078).</li>
</ul>
<p>Code:</p>
<ul>
<li>src/librt/primitives/table.c</li>
<li>src/librt/primitives/[PRIMITIVE]/[PRIMITIVE].c</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="implement_a_primitive_uv_mapping_callback">Implement a primitive UV-mapping callback</h3>
<p>BRL-CAD provides more than two dozen types of geometry "primitives" such as ellipsoids, boxes, and cones. Every primitive is described by a collection of callback functions, for example rt_<strong>ell</strong>_bbox() returns the bounding box dimensions for an <strong>ell</strong>ipsoid. One of those functions describes a UV mapping of the object's surface, which is used for things like texture and bump mapping. An example of this is rt_ell_uv() in the src/librt/primitives/ell/ell.c source file for an ellipsoid. Several of our more complex primitive types (such as BoT, NMG, and BREP/NURBS) do not presently implement a UV-mapping function leading to unexpected runtime behavior.</p>
<p>This task involves implementing a UV-mapping callback for any of the primitives that do not already have a functional UV-callback defined. Note that this is an advanced task that might take you more than a couple hours if you don't have solid coding skills, but it's ultimately just a few lines of code. See other primitives that already implement a UV-mapping callback for reference.</p>
<p>References:</p>
<ul>
<li><a href="http://en.wikipedia.org/wiki/UV_mapping">http://en.wikipedia.org/wiki/UV_mapping</a></li>
<li>src/librt/primitives/[PRIMITIVE]/[PRIMITIVE].c, search for rt_*_uv() functions</li>
</ul>
<p>Code:</p>
<ul>
<li>src/librt/primitives/extrude/extrude.c</li>
<li>src/librt/primitives/table.c</li>
<li>include/rtgeom.h</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="fix_elliptical_torus_triangulation">Fix elliptical torus triangulation</h3>
<p>BRL-CAD has many 3D object types, one of them being an "Elliptical Torus". If you create a new MGED database and run this sequence of commands, it'll crash due to excessive recursion:</p>
<pre><code>make eto eto
tol norm 1
facetize eto.bot eto</code></pre>
<p>This task's goal is to reproduce, identify, and fix the bug so that detailed eto tessellation completes successfully. To get started, see the rt_eto_tess() function in src/librt/primitives/eto/eto.c and the facetize command logic in libged.</p>
<p>Code:</p>
<ul>
<li>src/librt/primitives/eto/eto.c, &lt;- you'll probably need to modify this file</li>
<li>src/libged/facetize/facetize.cpp</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="implement_a_function_that_evaluates_volume_with_spherical_sampling">Implement a function that evaluates volume with spherical sampling</h3>
<p>Implement this function:</p>
<p><code>??????int??estimate_volume(struct??db_i??*dbip,??</code><br />
<code>??????????????????????????????????????????????struct??directory??*dp,</code><br />
<code>??????????????????????????????????????????????size_t??min_samples,</code><br />
<code>??????????????????????????????????????????????double??confidence);</code></p>
<p>For this function, you'll want to read up on some of BRL-CAD's basic data structures by looking at headers in the include/rt directory or by reading our <a href="https://brlcad.org/docs/api/">API documentation</a>. Calling rt_db_internal() and rt_bound_internal() will get you the bounding box around geometry from which you can calculate a bounding sphere. Once you have the bounding sphere, randomly generate a set of min_samples*2 points on the surface of the sphere. Shoot a ray through those points using rt_shootray(), as in the ray tracing <a href="Example_Application" title="wikilink">example</a>. Keep track of a volume estimate and keep shooting sets of min_samples rays until the estimate is less than the specified confidence value. Volume of a sphere is (4/3 * pi * r^3) so dividing that by num_samples will give a per-ray factor and multiplying all hit thicknesses by that factor will give a running volume estimate.</p>
<p>References:</p>
<ul>
<li><a href="https://brlcad.org/docs/api/">https://brlcad.org/docs/api/</a></li>
<li><a href="https://brlcad.org/wiki/Example_Application">https://brlcad.org/wiki/Example_Application</a></li>
<li><a href="https://stackoverflow.com/questions/9600801/evenly-distributing-n-points-on-a-sphere">https://stackoverflow.com/questions/9600801/evenly-distributing-n-points-on-a-sphere</a></li>
<li><a href="https://karthikkaranth.me/blog/generating-random-points-in-a-sphere/">https://karthikkaranth.me/blog/generating-random-points-in-a-sphere/</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="implement_a_function_to_return_an_objects_color">Implement a function to return an object's color</h3>
<p>CAD geometry can have colors specified in a number of ways including directly on that object, in a parent object, and in a lookup table. For this task, you're going to implement a function that reports the color of an object given a path to that object:</p>
<p><code>??????int??get_color(struct??db_i??*dbip,??const??char??*path,??struct??bu_color??*rgb);</code></p>
<p>You'll need to iteratively consider each object named on the specified path (e.g., "/car/wheel/tire.r/torus") starting with "car" and working your down the path (i.e., 'wheel', 'tire.r', and then 'torus') to 1) see if a color is set on that object and 2) see if that color overrides lower-level colors (i.e., is inherited down the path), and 3) if it's a region object, whether there is a color set in the region table. You'll need to db_lookup() each object on the path to get access to its data.</p>
<p>For this function, you'll want to read up on some of BRL-CAD's basic data structures by looking at headers in the include/rt directory or by reading our <a href="https://brlcad.org/docs/api/">API documentation</a>. This task may seem complicated if you're not familiar with C/C++ APIs, data structures, or hierarchical paths, so don't be shy <a href="https://brlcad.zulipchat.com">asking</a> questions.</p>
<p>References:</p>
<ul>
<li><a href="https://brlcad.org/docs/api/">https://brlcad.org/docs/api/</a></li>
</ul>
<p>Code References:</p>
<ul>
<li>src/libged/display_list.c</li>
<li>src/libged/color/color.c</li>
<li>src/librt/prep.c</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="stub_in_an_openvdb_object">Stub in an OpenVDB object</h3>
<p>BRL-CAD has dozens of distinct primitive object types. For this task, you're going to implement the bare minimum to necessary to create a new object with the "make" command in MGED.</p>
<p>The best way to achieve this task is by searching for a keyword for another primitive (e.g., 'grep -r -i superell .') and implementing your new object the same way. Start with the 'make' command itself in src/libged/make/make.c and add "vdb" alongside where you find one of the other primitive types (e.g., superell). To get that to compile, you'll have to add new symbols you've defined into header files (e.g., include/rt/rtgeom.h). You'll eventually need to implement barebones logic in src/librt/primitives/vdb too.</p>
<p>Code:</p>
<ul>
<li>include/rt/defines.h &lt;- needs an ID</li>
<li>include/rt/geom.h &lt;- needs an "internal" i.e., in-memory structure</li>
<li>src/libged/make/make.c &lt;- needs to recognize "vdb" as a valid type</li>
<li>src/librt/primitives/table.cpp &lt;- needs an entry</li>
<li>src/librt/primtiives/vdb &lt;- needs a dir</li>
<li>src/librt/primitives/vdb/vdb.c &lt;- needs _import5/_export5 callbacks, maybe _describe too</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

## Documentation and Training

*Tasks related to creating/editing documents and helping others learn
more about BRL-CAD*

<table>
<tbody>
<tr class="odd">
<td><h3 id="add_missing_documentation_for_any_one_command">Add missing documentation (for any ONE command)</h3>
<p>BRL-CAD is an extensive system with more than 400 commands and more than a million pages of documentation, but there are approximately 120 commands that are entirely undocumented:</p>
<p>a-d archer asc2g asc2pix bot-bldxf bottest brep_cube brep_simple brickwall btclsh burst bw-a bw-d bwish c-d chan_add clutter contours d-a damdf dauto dauto2 d-bw dconv ddisp d-f dfft d-i dmod double-asc dpeak dsel dsp_add dstat d-u dwin euclid_format euclid_unformat fbgammamod f-d fence fhor f-i g-adrt g-euclid1 g-jack globe g-off i-a i-d i-f ihist imod istat jack-g kurt lowp molecule nmgmodel nmg-sgp off-g pipe pipetest pix2g pix3filter pixcount pixelswap pixembed pixfields pixfieldsep pixflip-fb pixpaste pix-spm pix-yuv plstat pyramid rawbot remapid rlesortmap rletovcr room rtcell rtexample rtfrac rtrad rtsil rtsrv script-tab sketch solshoot sphflake spltest spm-fb ssampview syn tea tea_nmg testfree texturescale torii ttcp tube txyz-pl u-a u-bw u-d u-f umod ustat vcrtorle vegitation wall wdb_example xbmtorle xyz-pl yuv-pix</p>
<p>This task involves writing basic documentation for <strong>JUST ONE</strong> of those commands in the Docbook XML format. The command documentation should provide a one-sentence description, a detailed paragraph description (200+ words), explanation of <strong>all</strong> available command-line options, and one or more examples on how to use the command.</p>
<p>Code:</p>
<ul>
<li>doc/docbook/system/man1/en/Makefile.am</li>
<li>doc/docbook/system/man1/en/*.xml</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="complete_our_intro_to_brl_cad_modeling_tutorial_and_extend_it">Complete our "Intro to BRL-CAD Modeling" tutorial and extend it</h3>
<p>We've developed two short and simple tutorials for introducing new users to modeling with BRL-CAD.</p>
<p>This task involves doing one of the tutorials (they take about an hour) and then extending it with a new section or making some other improvement. At the end of the tutorial are several optional advanced "exercise left to the reader", for example. Write a half-page step-by-step for one of the exercises left to the reader. Include screenshots and images to make it look nice so the reader is not bored.</p>
<p>Reference:</p>
<ul>
<li>Come <a href="https://brlcad.zulipchat.com">talk with us</a> to make sure you get a copy of the latest version.</li>
<li><a href="https://brlcad.org/w/images/9/90/Intro_to_BRL-CAD.pdf">https://brlcad.org/w/images/9/90/Intro_to_BRL-CAD.pdf</a></li>
<li><a href="https://brlcad.org/w/images/c/cf/Introduction_to_MGED.pdf">https://brlcad.org/w/images/c/cf/Introduction_to_MGED.pdf</a></li>
<li>... there's another new one, but you have to ask for it ...</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="translate_contributors_guide_to_brl_cad_to_any_language">Translate "Contributors Guide To BRL-CAD" To Any Language</h3>
<p>People interested in improving BRL-CAD sometimes find themselves lost in a sea of information. In all, BRL-CAD has more than a million words of documentation across hundreds of manual pages, dozens of tutorials and examples, hundreds of wiki pages, dozens of technical papers, and other resources. There are literally thousands of features and this can sometimes pose problems.</p>
<p>In 2013, a team of contributors got to California and worked on an entire book titled "Contributors Guide To BRL-CAD" in just a few days. This great resource needs to be translated to other languages to attract developers from other lingual backgrounds (who don't read English ) to contribute to BRL-CAD.</p>
<p>This task involves translating the chapters/sections of the "Contributors Guide To BRL-CAD" into a language of your choice such as Mandarin, French, Chinese, Spanish, German, Hindi, Arabic, Russian, etc. Chapters/Sections include</p>
<ul>
<li>Feature Overview</li>
<li>Working with our Code</li>
<li>What code to work on</li>
<li>How to contribute</li>
<li>.... (Just to name a few )</li>
</ul>
<p>The output of this task can be a pdf, html, doc, odt or any other document file that contains the translated article.Images in the original document (see link in Reference below) should not be changed ! only text should be.</p>
<p>Reference:</p>
<ul>
<li><a href="http://en.flossmanuals.net/_booki/contributors-guide-to-brl-cad/contributors-guide-to-brl-cad.pdf">http://en.flossmanuals.net/_booki/contributors-guide-to-brl-cad/contributors-guide-to-brl-cad.pdf</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="write_a_brl_cad_commands_quick_reference_document">Write a "BRL-CAD Commands Quick Reference" document</h3>
<p>There is already a command quick reference for BRL-CAD's MGED geometry editing tool, but there is not a similar document for BRL-CAD's 400+ command-line commands.</p>
<p>This task involves writing a quick reference document similar to <a href="http://brlcad.org/w/images/5/52/MGED_Quick_Reference_Card.pdf">the MGED quick reference</a> but for BRL-CAD commands. The sheet should minimally include the following commands:</p>
<p><code>mged,??rt*,??*-g,??g-*,??fb*,??*fb,??nirt,??remrt,??rtsrv,??asc2g,??g2asc,??dbupgrade,??pix*,??*pix,??*-*,??brlman,??benchmark</code></p>
<p>References:</p>
<ul>
<li><a href="http://brlcad.org/wiki/Documentation">http://brlcad.org/wiki/Documentation</a></li>
<li><a href="http://brlcad.org/w/images/5/52/MGED_Quick_Reference_Card.pdf">http://brlcad.org/w/images/5/52/MGED_Quick_Reference_Card.pdf</a></li>
<li><a href="http://appletree.or.kr/quick_reference_cards/CVS-Subversion-Git/git-cheat-sheet-large.png">git example</a></li>
<li><a href="http://www.stdout.org/~winston/latex/latexsheet-0.png">latex example</a></li>
<li><a href="http://img.docstoccdn.com/thumb/orig/524314.png">another example</a></li>
<li><a href="http://www.inmensia.com/files/pictures/internal/CheatSheetDrupal4.7.png">drupal example</a></li>
<li><a href="http://www.phpmagicbook.com/wp-content/uploads/2010/06/php-reference-card.jpg">php example</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="doxygen_cleanup">Doxygen cleanup</h3>
<p>BRL-CAD uses Doxygen for most API documentation but the comment blocks are not optimally set up for Doxygen output.</p>
<p>This task involves cleaning up the Doxygen comments in the library so that useful reports and API documentation automatically generated (correctly, completely, and cleanly). Verify/fix any Doxygen syntax. Verify/fix groups so that functions are organized neatly and all contained within a group. Provide patches that give clean (PDF) output from Doxygen.</p>
<p>References:</p>
<ul>
<li><a href="http://www.jiggerjuice.net/software/doxygen.html">http://www.jiggerjuice.net/software/doxygen.html</a></li>
<li><a href="http://www.stack.nl/~dimitri/doxygen/starting.html">http://www.stack.nl/~dimitri/doxygen/starting.html</a></li>
<li><a href="http://www.stack.nl/~dimitri/doxygen/">http://www.stack.nl/~dimitri/doxygen/</a></li>
</ul>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="doxygen_cleanup_for_libbu_1">... doxygen cleanup for LIBBU</h4>
<p>There are approximately 300 documented API function calls in LIBBU.</p>
<p>Code:</p>
<ul>
<li>include/bu.h</li>
<li>src/libbu</li>
<li>misc/Doxyfile</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="doxygen_cleanup_for_libwdb_1">... doxygen cleanup for LIBWDB</h4>
<p>There are approximately 100 documented API function calls in LIBWDB.</p>
<p>Code:</p>
<ul>
<li>include/wdb.h</li>
<li>include/raytrace.h</li>
<li>src/libwdb</li>
<li>misc/Doxyfile</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="doxygen_cleanup_for_librt_1">... doxygen cleanup for LIBRT</h4>
<p>There are approximately 1000 documented API function calls in LIBRT.</p>
<p>Code:</p>
<ul>
<li>include/raytrace.h</li>
<li>src/librt</li>
<li>src/librt/primitives</li>
<li>src/librt/comb</li>
<li>src/librt/binunif</li>
<li>misc/Doxyfile</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="add_images_to_our_wiki_page_on_volumetric_objects">Add images to our wiki page on Volumetric objects</h3>
<p>BRL-CAD provides a couple dozen distinct primitives. Each primitive is defined by a set of parameters. Several of the more complex primitives have a wiki page describing them in more detail with an example on how to create them.</p>
<p>This task involves adding images to our page for the VOL primitive. You'll need to first complete the tutorial and save images for each step. Add the images to the wiki page.</p>
<p>References:</p>
<ul>
<li><a href="http://brlcad.org/wiki/VOL">http://brlcad.org/wiki/VOL</a></li>
<li><a href="http://brlcad.org/wiki/DSP">http://brlcad.org/wiki/DSP</a></li>
<li><a href="http://brlcad.org/wiki/Sketch">http://brlcad.org/wiki/Sketch</a></li>
<li><a href="http://brlcad.org/wiki/EBM">http://brlcad.org/wiki/EBM</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="fix_image_formatting_in_brl_cads_docbook_documentation_any_one_large_document_or_4_smaller_documents">Fix Image Formatting in BRL-CAD's DocBook Documentation (any ONE large document or 4 smaller documents)</h3>
<p>The majority of BRL-CAD's documentation is defined as DocBook files, from which other formats (HTML, PDF, man page, etc.) can be generated. PDF files present a particular challenge, and have some very specific requirements to achieve "good" formatting.</p>
<p>BRL-CAD's DocBook files need to uniformly use a style of image inclusion that is aware of what "role" the image is supposed to serve. A "basic" image inclusion example looks like this:</p>
<mediaobject>
<p><code>??????</code><imageobject><br />
<code>??????????</code><imagedata align="center" fileref="../../lessons/en/images/img.png" format="PNG"/><br />
<code>??????</code></imageobject><br />
<code>??????&lt;caption&gt;</code><br />
<code>??????????</code></p>
<para>
<p><code>??????????????Caption??goes??here.</code><br />
<code>??????????</code></p>
</para>
</caption>
</mediaobject>
<p>This task involves switching image inclusions that use the above style to something like the following:</p>
<mediaobject>
<p><code>??????</code><imageobject role="html"><br />
<code>??????????</code><imagedata align="center" fileref="../../books/en/images/img.png" format="PNG"/><br />
<code>??????</code></imageobject><br />
<code>??????</code><imageobject role="fo"><br />
<code>??????????</code><imagedata align="center" fileref="../../books/en/images/img.png" format="PNG"/><br />
<code>??????</code></imageobject><br />
<code>??????&lt;caption&gt;</code><br />
<code>??????????</code></p>
<para>
<p><code>??????????????Caption??goes??here.</code><br />
<code>??????????</code></p>
</para>
</caption>
</mediaobject>
<p>The "role" flag to imageobject provides the opportunity to specify different image formatting options when the output is HTML (role="html") or PDF (role="fo").</p>
<p>The captions should be preserved as above on mediaobjects that have them, but mediaobjects without a caption should also be converted and there is no need to add a caption in such cases.</p>
<p>Any patch that makes changes to the DocBook sources should result in a successful "make doc" build test. This won't generate PDF documents, but it will validate the XML files and produce HTML - remember that introducing breakage means the patch won't be accepted.</p>
<p>Remember, the tasks are simply to do the above conversion for all images in the file or files, not to introduce PDF specific formatting. Formatting fixes will be needed, but they are very much "case by case" and will take both additional time and a working Apache FOP installation, as well as knowledge of how to enable PDF generation. If all image inclusions have been converted successfully and a student is interested in actually fixing the formatting, please discuss it with us on IRC or the mailing list.</p>
<p>References:</p>
<ul>
<li>doc/docbook/books/en/BRL-CAD_Tutorial_Series-VolumeIII.xml</li>
</ul>
<p>Code:</p>
<ul>
<li>doc/docbook</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="find_5_bugs_in_ogv">Find 5 bugs in OGV</h3>
<p>Online Geometry Viewer is a web based application with which you can see 3D .g models in browser without the use of any plugins. Your task will be to deploy OGV locally and find 5 bugs or errors in it.</p>
<p>Links: <a href="https://github.com/BRL-CAD/OGV-meteor/">https://github.com/BRL-CAD/OGV-meteor/</a></p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

## Outreach and Research

*Tasks related to community management, outreach/marketing, studying
problems, and recommending solutions*

<table>
<tbody>
<tr class="odd">
<td><h3 id="profile_nurbs_prep_performance">Profile NURBS prep performance</h3>
<p>BRL-CAD implements support for rendering of NURBS representation geometry. If you import a solid 3DM or STEP format model into BRL-CAD, it will import as BREP/NURBS geometry. Opening that geometry in BRL-CAD's MGED editor will tell you what objects are available and our 'rt' tool will raytrace it. When geometry is ray traced, it first goes through a "prep" phase and then it starts shooting rays. Our prep phase is entirely unoptimized so we'd like to know where all the time is presently being spent during prep..</p>
<p>This task involves importing some NURBS geometry into BRL-CAD and ray tracing that geometry with a profiler watching our prep performance. Any profiler will do, including gprof, but a performance monitor like oprofile or the Mac "Instruments" application (or Shark) are preferred.</p>
<p>Learning how to use a profiler is beyond the scope of this task, so it make take you considerably longer to provide us with useful information if you've never run a profiler before.</p>
<p>To capture prep performance, you will need to import some fairly complex geometry. You should be able to search google with "filetype:3dm" or "filetype:step" or find something on grabcad.com to import</p>
<p>Running "tops" within mged will tell you what geometry is available for rendering.</p>
<p>Running "rt -o file.png -s32" on the system command line (not inside mged) should minimize the ray overhead or you can specifically isolate the prep phase we care about. Prep is the time between when rt is run where it opens a window until the first pixels are fired and pixels start filling in.</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="continue_investigating_gmp_integration">Continue investigating GMP integration</h3>
<p>BRL-CAD uses a fastf_t typedef for most all math operations that is usually a "double" floating point type. We would like to provide the option for resorting to exact arithmetic if possible by merely redefining fastf_t to a C++ type sufficiently overloaded to behave the same. You should be proficient with C++ operator overloading to take this work on. This task is a continuation of a prior GCI task (read it in full!):</p>
<p><a href="http://www.google-melange.com/gci/task/view/google/gci2012/7946218">http://www.google-melange.com/gci/task/view/google/gci2012/7946218</a></p>
<p>This task involves testing compilation with a C++ class with overloaded operators such that vmath macro calls still work as well as a sampling of LIBBN API function calls without major changes to the original code. A perfect example case study would be creating the class then testing whether bn_dist_pt3_pt3() and bn_mat_determinant() compute correctly for values that cannot be exactly represented with floating point arithmetic.</p>
<p>Building on the previous GCI task work, take it to the next step. Try setting a vector to 1/3, 1/3, 1/3 and 0.1, 0.1, 0.1 and get proper values to print. Change the V3ARGS() macro if needed. If that all works, try to get bn_dist_pt3_pt3() to work. Report and discuss your progress.</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="upgrade_opennurbs_report_issues">Upgrade OpenNURBS, report issues</h3>
<p>BRL-CAD uses a customized OpenNURBS library for advanced geometry but it's out of date. For this task, you're going to download the latest OpenNURBS code and upgrade the sources we bundle. The easiest way is probably to move src/other/openNURBS to src/other/openNURBS.backup, and then put the latest OpenNURBS release into src/other/openNURBS.</p>
<p>Once that's done, you'll need to add the src/other/openNURBS.backup/CMakeLists.txt file and make sure the list of files it has matches the files in src/other/openNURBS. Last but not least, re-run cmake and make sure it compiles. You may need to consult the newer openNURBS makefile to see if there are other edits needed in the CMakeLists.txt file.</p>
<p>Save output from any commands you run because you'll probably encounter an error, and that's okay. Just submit logs of all output so we can figure out next steps.</p>
<p>References:</p>
<ul>
<li><a href="https://github.com/mcneel/opennurbs">https://github.com/mcneel/opennurbs</a></li>
</ul>
<p>Code:</p>
<ul>
<li>src/other/openNURBS &lt;- replace existing with latest openNURBS from github</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="design_a_t_shirt_for_brl_cad">Design a T-Shirt for BRL-CAD</h3>
<p>This task involves designing a T-Shirt for BRL-CAD. Use your designing skills to design a T-Shirt for BRL-CAD. You can use the current BRL-CAD logo, or you may tweak it. Be creative while designing this T-Shirt. It would be good if the design has some special meaning.</p>
<p>Logo References</p>
<ul>
<li><a href="https://brlcad.org/img/logo_color.png">BRL-CAD Logo</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="design_a_coffee_mug_for_brl_cad">Design a coffee mug for BRL-CAD</h3>
<p>This task involves designing a coffee mug for BRL-CAD. Make it look good or at least interesting, and make it in BRL-CAD. Look over some coffee mug designs before starting to work on this. Verify that your mug is valid geometry by running the "rtcheck" command.</p>
<p>Logo References</p>
<ul>
<li><a href="https://brlcad.org/img/logo_color.png">BRL-CAD Logo</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="design_brl_cad_sticker">Design BRL-CAD sticker</h3>
<p>This task involves designing a BRL-CAD sticker. The design should be simple and sleek. The concept of sticker should be clear and also it should be creatively presented. Get inspired from some sticker designs but choose your own imagination while designing the sticker. There is no bound for shape of sticker, it can be rectangular, circular or even irregular. The only thing that matters is that it should look good.</p>
<p>Logo References</p>
<ul>
<li><a href="https://brlcad.org/img/logo_color.png">BRL-CAD Logo</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="design_a_wallpaper_desktop_image_for_brl_cad">Design a wallpaper / desktop image for BRL-CAD</h3>
<p>This task involves designing a desktop background for BRL-CAD enthusiasts. The main idea of your wallpaper should be to showcase one or more features of BRL-CAD. Be intentional and able to defend/describe your choice of color, layout, and other aspects of the wallpaper design.</p>
<p>Try to make sure the wallpaper works across a broad selection of screen resolutions.</p>
<p>Search the web for wallpapers inspiration such as:</p>
<ul>
<li><a href="http://www.smashingmagazine.com/tag/wallpapers/">http://www.smashingmagazine.com/tag/wallpapers/</a></li>
</ul>
<p>Logo References</p>
<ul>
<li><a href="https://brlcad.org/img/logo_color.png">BRL-CAD Logo</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="model_a_lightcycle_in_brl_cad_using_csg">Model a Lightcycle in BRL-CAD using CSG</h3>
<p>The movie Tron is an iconic computer graphics film that used CSG primitives for a majority of the movie's 3D virtual world. The film is famous for "lightcycle" vehicles that were allegedly modeled using 57 primitives and/or Boolean operations. For this task, see if you can recreate the masterpiece in BRL-CAD.</p>
<p>See this lightcycle discussion thread</p>
<ul>
<li><a href="http://www.tron-sector.com/forums/default.aspx?a=top&amp;id=336281">http://www.tron-sector.com/forums/default.aspx?a=top&amp;id=336281</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

## Quality Assurance

*Tasks related to testing and ensuring code is of high quality*

<table>
<tbody>
<tr class="odd">
<td><h3 id="fix_single_precision_floating_point_crash">Fix single-precision floating point crash</h3>
<p>By default, all of BRL-CAD compiles using double-precision floating point arithmetic. We provide a simple typedef, however, that converts almost the entire system over to single-precision floating point. This compilation mode was recently cleaned up and tested, but a bug was found. The problem is reproduced very simply by compiling in single precision mode and running our "rt" ray tracer tool.</p>
<p>To compile in single precision, edit the include/bn.h header file and change the fastf_t typedef from double to float. To reproduce the bug, compile BRL-CAD and write this out to a text file named star.view:</p>
<p><code>viewsize??2.500000000e+05;</code><br />
<code>eye_pt??2.102677960e+05??8.455500000e+04??2.934714650e+04;</code><br />
<code>viewrot??-6.733560560e-01??6.130643360e-01??4.132114880e-01??0.000000000e+00</code><br />
<code>????????????????5.539599410e-01??4.823888300e-02??8.311441420e-01??0.000000000e+00</code><br />
<code>????????????????4.896120540e-01??7.885590550e-01??-3.720948210e-01??0.000000000e+00</code><br />
<code>????????????????0.000000000e+00??0.000000000e+00??0.000000000e+00??1.000000000e+00??;</code><br />
<code>start??0;</code><br />
<code>end;</code></p>
<p>Then run rt feeding it that view script as input. This is an example how to run within the gdb debugger:</p>
<p><code>gdb??path/to/bin/rt</code><br />
<code>...</code><br />
<code>(gdb)??run??-F/dev/X??-M??.cmake/share/db/star.g??all??&lt;??star.view</code></p>
<p>At this point, rt should crash due to an infinite recursion. A backtrace in the debugger will show lots and lots of calls to rt_shootray() and light_hit().</p>
<p>This task involves investigating and preventing the crash. Provide a patch that fixes the bug.</p>
<p>References:</p>
<ul>
<li>man gdb</li>
<li>brlman rt</li>
</ul>
<p>Code:</p>
<ul>
<li>src/librt/shoot.c</li>
<li>src/liboptical/sh_light.c</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="fix_closedb">Fix closedb</h3>
<p>BRL-CAD geometry editor application (mged) has several hundred commands including two very simple commands for opening and closing a geometry database file. While the user rarely ever needs to close the file, as all changes are always immediately saved, it can be of use to scripting applications. However, at some point in the recent past, the <em>closedb</em> command was horked. It's undoubtedly something very simple but we haven't bothered to look due to other priorities. You can fix it. If you run these simple steps within graphical mged, you should see how commands stop working after calling closedb:</p>
<p><code>??mged&gt;??opendb??test.g??y</code><br />
<code>??mged&gt;??make??sph??sph</code><br />
<code>??mged&gt;??l??sph</code><br />
<code>??mged&gt;??closedb</code><br />
<code>??mged&gt;??make??sph??sph</code><br />
<code>??mged&gt;??opendb??test.g</code><br />
<code>??mged&gt;??l??sph</code><br />
<code>??mged&gt;??exit</code></p>
<p>Provide a patch that fixes the bug or tell us which SVN revision introduced the bug. Make sure you can reproduce the bug before claiming this task, which presumes you know how to download/install BRL-CAD from a source distribution.</p>
<p>Code:</p>
<ul>
<li>src/mged/mged.c</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="create_a_utility_library_libbu_api_unit_test">Create a utility library (LIBBU) API unit test</h3>
<p>There are more than 300 library functions in our core LIBBU library. As a core library used by nearly every one of BRL-CAD's tools, testing those functions for correct behavior is important.</p>
<p>This task involves implementing new unit tests for any of LIBBU's source files that do not already have a unit test defined. The test should run all of the public functions and be hooked into our build system. We have lots of existing unit tests to follow as examples.</p>
<p>References:</p>
<ul>
<li>include/bu.h</li>
<li>src/libbu/*.c</li>
<li>src/libbu/tests/*.c</li>
</ul>
<p>Code:</p>
<ul>
<li>src/libbu/tests/[TEST].c</li>
<li>src/libbu/tests/CMakeLists.txt</li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="create_numerics_library_libbn_api_unit_tests">Create Numerics library (LIBBN) API unit tests</h3>
<p>There are more than 300 library functions in our core LIBBN library. As a core library used by nearly every one of BRL-CAD's tools, testing those functions for correct behavior is important.</p>
<p>This task involves implementing new unit tests for any of LIBBN's source files that do not already have a unit test defined. The test should run all of the public functions and be hooked into our build system. We have lots of existing unit tests to follow as examples.</p>
<p>References:</p>
<ul>
<li>include/bn.h</li>
<li>include/plot3.h</li>
<li>include/vmath.h</li>
<li>src/libbn/*.c</li>
<li>src/libbn/tests/*.c &lt;-- check this directory for examples</li>
<li>src/libbu/tests/*.c &lt;-- Note: Also check this too for more examples.</li>
</ul>
<p>Code:</p>
<ul>
<li>src/libbn/tests/[TEST].c</li>
<li>src/libbn/tests/CMakeLists.txt</li>
</ul>
<p><b> Note </b> A valid task will constitute writing a basic test for each function in the following libbn/ files.</p>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="unit_tests_for_libbn_anim.c_1">... unit tests for LIBBN anim.c</h4>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="unit_tests_for_libbn_axis.c_1">... unit tests for LIBBN axis.c</h4>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="unit_tests_for_libbn_qmath.c_1">... unit tests for LIBBN qmath.c</h4>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="unit_tests_for_libbn_rand.c_1">... unit tests for LIBBN rand.c</h4>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<table>
<tbody>
<tr class="odd">
<td><h4 id="unit_tests_for_libbn_vector.c_1">... unit tests for LIBBN vector.c</h4>
<p>??</p></td>
</tr>
</tbody>
</table>
<p>??</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="find_reliably_reproduce_and_report_any_bug_in_archer">Find, reliably reproduce, and report any bug in Archer</h3>
<p>Archer is our new modeling interface and a soon to merge with our long-standing MGED geometry editor. It undoubtedly has bugs. It's your job to find one, but do so in a manner that is so obvious that one of the other devs will be able to instantly reproduce the bug given your specific instructions. Find a way to make archer crash, become unresponsive, or otherwise behave incorrectly. You will have to explore the tool with minimal documentation.</p>
<p>This task involves filing a bug report with verifiable and reproducible steps that clearly demonstrate the bug. It can't be a bug already reported or otherwise documented nor can it be merely behavior you don't like.</p>
<p>References:</p>
<ul>
<li>archer</li>
<li>Introduction to MGED at <a href="http://brlcad.org/wiki/Documentation">http://brlcad.org/wiki/Documentation</a> (many of the mged commands are available in some fashion within archer)</li>
<li>BUGS file in any source/binary distribution</li>
<li><a href="http://sourceforge.net/tracker/?atid=640802&amp;group_id=105292&amp;func=browse">http://sourceforge.net/tracker/?atid=640802&amp;group_id=105292&amp;func=browse</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="reproduce_any_10_unconfirmed_open_bug_reports">Reproduce any 10 unconfirmed open bug reports</h3>
<p>BRL-CAD presently has approximately 75 open bug reports of which 50 are unassigned. Read the comments and status to see if the bug has been confirmed/reproduced.</p>
<p>This task involves going through those reports and REPRODUCE at least 10 of the ones that have not been confirmed. When you can reproduce the issue being reported, you'll comment on the thread to state as much and attach any data you used to reproduce the crash.</p>
<p>References:</p>
<ul>
<li><a href="https://sourceforge.net/tracker/?limit=100&amp;func=&amp;group_id=105292&amp;atid=640802&amp;assignee=100&amp;status=1&amp;submit=Filter">https://sourceforge.net/tracker/?limit=100&amp;func=&amp;group_id=105292&amp;atid=640802&amp;assignee=100&amp;status=1&amp;submit=Filter</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

## User Interface

*Tasks related to user experience research or user interface design and
interaction*

<table>
<tbody>
<tr class="odd">
<td><h3 id="create_an_isst_screenshot_or_animation">Create an ISST screenshot or animation</h3>
<p>Everyone loves to see screenshots and animations of software in action. We use both in our marketing and outreach. See some of the examples below that we already have.</p>
<p>Create an awesome screenshot and/or animation of our 'isst' tool in action. It's an interactive geometry viewer interface. It should be graphically interesting and give some sense of capability. You should import a visually complex and interesting model with LOTS of polygons and detail. Note you may have to go through some or the MGED tutorials (see Docs on our website).</p>
<p>References:</p>
<ul>
<li><a href="https://brlcad.org/gallery/index.php?/category/12">https://brlcad.org/gallery/index.php?/category/12</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="categorize_commands_into_a_spreadsheet">Categorize commands into a spreadsheet</h3>
<p>BRL-CAD is a suite of more than 400 commands, processing tools, image tools, geometry converters, and more. MGED also has a command-line with hundreds of commands too. Help us reorganize one of those command sets.</p>
<p>This task involves creating a spreadsheet that lists all commands and groups them together into a finite set of categories or labels. This spreadsheet will help us identify places where commands can be consolidated, commands we might want to consider removing, common groupings for documentation, etc.</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="design_a_cover_photo_for_facebook_and_other_social_media">Design a Cover Photo for Facebook (and other social media)</h3>
<p>BRL-CAD website and marketing materials are constantly undergoing change. Effective marketing requires well designed and attractive imagery. Imagery ideally should showcase some feature of BRL-CAD, some highlight, something visually interesting and compelling.</p>
<p>References:</p>
<ul>
<li><a href="https://www.facebook.com/brlcad">https://www.facebook.com/brlcad</a></li>
</ul>
<p>??</p></td>
</tr>
</tbody>
</table>

??

<table>
<tbody>
<tr class="odd">
<td><h3 id="create_a_video_for_brl_cad">Create a video for BRL-CAD</h3>
<p>Watching someone else use software is incredibly helpful to some. Create a screen-cast video for BRL-CAD that showcases some feature, goes over steps involved in creating some model, or shows how to accomplish some other task.</p>
<p>You'll need to install BRL-CAD on your computer and use it in the video. Create or import some model and make a recording.</p>
<p>??</p></td>
</tr>
</tbody>
</table>

??

# When You're Done

For non-code, just send us your file(s). For code changes, you will be
expected to [provide a patch file](../doc/Patches.md). Make sure you
*read* your patch file before submitting it. Make sure your patch file
will apply cleanly to an unmodified checkout of BRL-CAD:

`svn??co??`[`https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk`](https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk)`??brlcad.edit`
`cd??brlcad.edit`
`#??make??changes`
`svn??diff??>??~/my.patch`
`#??read??~/my.patch??file??with??text??editor`
`cd??..`
`svn??co??`[`https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk`](https://brlcad.svn.sourceforge.net/svnroot/brlcad/brlcad/trunk)`??brlcad.fresh`
`cd??brlcad.fresh`
`patch??-p0??<??~/my.patch`
`#??submit??your??patch??file??to??our??patches??tracker`

??
