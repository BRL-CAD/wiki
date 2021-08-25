-   **Name:** Suraj

<!-- -->

-   **IRC nick:** SurajDadral

<!-- -->

-   **Blog:** <https://hacksj4u.wordpress.com>

<!-- -->

-   **GitHub profile:** <https://github.com/SurajDadral>

**Brief Background Information**

I am B.Tech. (2nd year), Computer Science student of Guru Nanak Dev
Engineering College, India. Practiced in writing code in C/C++, Python
and used Git, Qt, Django, Make, Jekyll and PySide.

I solved an
[issue](https://github.com/amrit3701/FreeCAD-Reinforcement/issues/10)
with Rebar Addon and here is merged PR:
<https://github.com/amrit3701/FreeCAD-Reinforcement/pull/11>

I worked on GeoData workbench of FreeCAD and added support for links
from popular maps to import OSM (OpenStreetMap) using core functionality
of GeoData workbench.

Related discussion:
<https://forum.freecadweb.org/viewtopic.php?f=3&t=27803>

Merged PR: <https://github.com/microelly2/geodata/pull/10>

# Project Information

# Project Title: Automate Reinforcement Process in FreeCAD

# Brief Project Summary

My project is to automate Reinforcement process by using Rebar Addon in
FreeCAD. The idea is to create UI and functions on top of the current
implementation to combine different types of Rebars in a single Dialog
Box as per the user requirements. For example, combine Stirrups and
Rebars (different types of rebars) in case of Beam Reinforcement.

# Detailed Project Description

**Current Scenario in FreeCAD**

1.  There is no provision to create straight rebars in a circular column
    as discussed here:
    <https://forum.freecadweb.org/viewtopic.php?f=8&t=22760&start=230#p186507>
2.  To create Reinforcement in a single Beam or Column, user needs to do
    a lot of work like creating Stirrups, Rebars and perform all
    calculations involved manually.
3.  If user decides to make changes in any parameter of Beam/Column
    Reinforcement like Cover of Stirrup, he/she needs to manually adjust
    Cover and Spacing of all Rebars provided. Doing so manually needs
    efforts never less than applying Reinforcement from Scratch and
    involves lots of calculations. And obviously, there are going to be
    number of Beams/Columns in a building and no one wants to apply
    Reinforcement to all Beams/Columns manually. So, this is a very time
    consuming task.</br>
    Example: You can see below how the things went wrong after modifying
    covering of Stirrup.
    ![](/wiki/user/img/ModifyCoverofStirrup.png)

Example: In case of Beam Reinforcement

1.  To create reinforcement in a Beam, user has to do following steps:
    -   Select face of the beam and create stirrups.
        ![](/wiki/user/img/BeamReinforcementImage1.png)
        ![](/wiki/user/img/BeamReinforcementImage2.png)
    -   To create rebars, first user needs to select one of the face,
        perpendicular to previously selected face and then calculate
        ‘Front Cover’ and ‘Top/Bottom Cover’ based on the values of
        Rounding and Top/Bottom/Left/Right Cover of the stirrups. And
        this should be done for all four sides. And this will produce
        single layered Reinforcement in Beam as follow:
        ![](/wiki/user/img/BeamReinforcementImage3.png)
        ![](/wiki/user/img/BeamReinforcementImage4.png)
2.  To create multi-layered Reinforcement in a Beam, user needs to do
    following steps:
    -   Create Reinforcement as discussed above.
    -   Create Spacer Reinforcement for new layer. While creating this,
        user needs to perform calculations to adjust cover and spacing
        of Spacer Rebars.
        ![](/wiki/user/img/BeamReinforcementImage5.png)
    -   Create Rebars of new layer:
        ![](/wiki/user/img/BeamReinforcementImage6.png)
    -   Now to create each new layer of Reinforcement, user needs to
        repeat Step II and III and perform all calculations manually.
        ![](/wiki/user/img/BeamReinforcementImage7.png)

**Proposed solution to the problem**

To solve above mentioned issues, an interactive UI will be developed on
top of the current implementation of Rebar Addon in FreeCAD.

-   Dialog Box will be developed where user will input the required data
    as per the design requirements.
-   When the user will press apply button, this input data will be
    passed to functions makeStirrup(), makeStraightRebar(),
    makeLShapeRebar(), makeUShapeRebar() etc. of the Rebar Addon as per
    the requirements.
-   The Reinforcement will be created using core functionality of the
    Rebar Addon.
-   To edit Reinforcement provided, user will double click on created
    Reinforcement object. Then he/she will be shown same Dialog Box as
    while creating Reinforcement. And then user can make changes and
    apply them as did before.
-   There will be a Dialog Box, using which user can create straight and
    L-Shaped rebars in a circular column.

So, the developed UI will contains following features:

1.  User will add only basic details for Reinforcement and all the
    calculations (like for cover and spacing of rebars) will be done by
    script.
2.  User can create different types of Rebars in single step. Like
    creating Stirrups and Rebars (of different types) for Beam or
    Rectangular Column.
3.  User can add number of layers and number of Rebars in each layer in
    beam.
4.  User can create reinforcement for circular column in one step.
5.  For Column Reinforcement, user will be presented with a list of
    prototypes of some default configurations, which we will choose from
    “SP 34: Handbook on Concrete Reinforcement and Detailing” as present
    here: <https://archive.org/details/gov.in.is.sp.34.1987/page/n95>
    </br> Due to time constraints of GSoC, I will implement following
    prototypes, but will keep on adding even after GSoC.
    ![](/wiki/user/img/ColumnPrototypes1.png) I also
    implemented above prototypes manually and can be found at
    <https://github.com/SurajDadral/FreeCAD-Examples>

**Input parameters**

Input parameters for Beam Reinforcement are categorised into two groups
that forms two different tabs in Stirrup Reinforcement as following:

1.  Stirrup parameters
2.  Rebars distribution
    -   Top Rebar
    -   Bottom Rebar
    -   Side Rebar

Dialog Box will contain similar input parameters which are present in
Reinforcement table of STAAD.Pro output file. For example, Reinforcement
for Beam in STAAD.Pro file is present as:

&lt;p align=center width:80%&gt;<b>SUMMARY OF PROVIDED REINF. AREA</b>

<table style="width:80%;" align="center">
<tr>
<th>

SECTION

</th>
<th>

0.0 mm

</th>
<th>

2000.0 mm

</th>
<th>

4000.0 mm

</th>
<th>

6000.0 mm

</th>
<th>

8000.0 mm

</th>
</tr>
<tr>
<td>

TOP</br>REINF.

</td>
<td align=center>

2-20í</br>1 layer(s)

</td>
<td align=center>

2-20í</br>1 layer(s)

</td>
<td align=center>

3-20í</br>1 layer(s)

</td>
<td align=center>

2-20í</br>1 layer(s)

</td>
<td align=center>

2-20í</br>1 layer(s)

</td>
</tr>
<tr>
<td>

BOTTOM</br>REINF.

</td>
<td align=center>

2-25í</br>1 layer(s)

</td>
<td align=center>

4-25í</br>1 layer(s)

</td>
<td align=center>

5-25í</br>2 layer(s)

</td>
<td align=center>

4-25í</br>1 layer(s)

</td>
<td align=center>

2-25í</br>1 layer(s)

</td>
</tr>
<tr>
<td>

SHEAR</br>REINF.

</td>
<td align=center>

2 legged 8í</br>@280 mm c/c

</td>
<td align=center>

2 legged 8í</br>@280 mm c/c

</td>
<td align=center>

2 legged 8í</br>@280 mm c/c

</td>
<td align=center>

2 legged 8í</br>@280 mm c/c

</td>
<td align=center>

2 legged 8í</br>@280 mm c/c

</td>
</tr>
<tr>
</table>

For Top Reinforcement, ‘2-20i 1 layer(s)’ represents 2 Rebars of
diameter 20 mm present in one layer. So, Dialog Box will contain input
fields for:

-   Layer Information
-   Number of Rebars
-   Diameter of Rebar

Benefit of doing so is discussed in [future
scope](#Future_Scope.md) of project.

**Enhancement**

<b>Master Configuration:</b>Instead of setting default values in UI as
in below image: ![](/wiki/user/img/CreateColumn1.png) We will
have Master Configuration file, in which user can set default values for
Rebar Addon like:

-   Diameter of Stirrups
-   Diameter of Rebars
-   Diameter of Ties
-   Span Length of Rebars
-   Offset for Rebars
-   Clear Covers (Left, Right, Front, Top, Bottom) for Stirrups
-   Bent Angle of Stirrups
-   Bent Factor of Stirrups
-   Rounding of Stirrups

**Proposed UI wireframe**

<dl>
<dt>

**Initialization**

</dt>
<dd>

![](/wiki/user/img/RebarAddonInitializationMenu.png)

</dd>
<dt>

**Dialog Box I:** For Reinforcement details in Beam

</dt>
<dd>

![](/wiki/user/img/CreateBeam1.png)
![](/wiki/user/img/CreateBeam2.png)
![](/wiki/user/img/CreateBeam3.png)
![](/wiki/user/img/CreateBeam4.png)

</dd>
<dt>

**Dialog Box II:** For Reinforcement details in Column

</dt>
<dd>

![](/wiki/user/img/CreateColumn1.png)
![](/wiki/user/img/CreateColumn2.png)

</dd>
</dl>

**Implementation**

-   An icon for Beam and Column Reinforcement will be made and
    integrated in drop down menu of Rebar Addon. Integration in drop
    down menu can be done by modifying RebarTools.py file of Rebar
    Addon.
-   The dialog box will be developed using QtDesigner. User will provide
    input through this dialog box.
-   The inputs provided by the user will then be passed to prebuilt
    functions of Rebar Addon. Below is the list of that functions:
    -   makeStraightRebar(f_cover, coverAlong, rt_cover, lb_cover,
        diameter, amo unt_spacing_check, amount_spacing_value,
        orientation = "Horizontal", structure = None, facename = None):
        Adds the straight reinforcement bar to the selected structural
        object.
    -   makeUShapeRebar(f_cover, b_cover, r_cover, l_cover,
        diameter, t_cover, rounding, amount_spacing_check,
        amount_spacing_value, orientation = "Bottom", structure =
        None, facename = None): Adds the U-Shape reinforcement bar to
        the selected structural object.
    -   makeLShapeRebar(f_cover, b_cover, l_cover, r_cover,
        diameter, t_cover, rounding, amount_spacing_check,
        amount_spacing_value, orientation = "Bottom Left", structure =
        None, facename = None): Adds the L-Shape reinforcement bar to
        the selected structural object.
    -   makeStirrup(l_cover, r_cover, t_cover, b_cover, f_cover,
        bentAngle, bentFactor, diameter, rounding,
        amount_spacing_check, amount_spacing_value, structure =
        None, facename = None): Adds the Stirrup reinforcement bar to
        the selected structural object.
    -   makeHelicalRebar(s_cover, b_cover, diameter, t_cover, pitch,
        structure = None, facename = None): Adds the Helical
        reinforcement bar to the selected structural object.
-   To implement Master configuration:
    -   An icon will be made and integrated in drop down menu of Rebar
        Addon by modifying RebarTools.py file of Rebar Addon.
    -   The master configuration file will be created and supplied with
        Rebar Addon.
    -   When user will click on icon, the FreeCAD function
        “FreeCADGui.open(<file_location>)” will be called with
        appropriate file_location. This will open file in FreeCAD for
        editing.
    -   Note: The open() function of FreeCAD does not support ‘.txt’
        files, and thus file will be Python file with extension ‘.py’.
    -   The master configuration will be imported into other files and
        used for setting default values for Rebar detailing.

# Timeline

As an overview, out of beam and column reinforcement, reinforcement for
column is more simpler and will be completed in the first phase before
the first evaluation.

-   **Community Bonding Period (6 May - 27 May)**
    -   Having interaction on mailing list and IRC regarding important
        aspects of project.
    -   Get to be more familiar with the code and workflow of FreeCAD
        and Rebar Addon.
    -   Learn more about PySide, STAAD.Pro file format and reinforcement
        in beams and columns.
    -   Learn Doxygen syntax and inkscape.
-   **27 May - 20 June (25 days)**
    -   Create UI for beam reinforcement.
    -   Implement beam reinforcement detailing function for passing user
        input to prebuilt Rebar Addon functions.
-   **21 June - 23 June (3 days)**
    -   Backup days for any backlog or pending task and preparation for
        phase I evaluation.
-   **24 June - 28 June (5 days, Phase I evaluation)**
    -   Developers documentation using Doxygen.
    -   Submitting all the work to mentor.
-   **29 June - 18 July (20 days)**
    -   Implement UI for circular column reinforcement.
    -   Implement circular column reinforcement detailing function for
        passing user input to prebuilt Rebar Addon functions.
    -   Create required images and icons using inkscape.
    -   Integrate UI with Rebar Addon UI.
-   **19 July - 21 July (3 days)**
    -   Backup days for any backlog, pending task, bug fixes and
        preparation for phase II evaluation.
-   **22 July - 26 July (5 days, Phase II evaluation)**
    -   Developer documentation using Doxygen.
    -   Submitting all the work to mentor.
-   **27 July - 11 August (16 days)**
    -   Create UI for square/rectangular column reinforcement.
    -   Implement square/rectangular column reinforcement detailing
        function for passing user input to prebuilt Rebar Addon
        functions.
-   **12 August - 18 August (1 week)**
    -   Work on UI enhancement to improve user experience.
    -   Work on backlogs and bug fixes.
-   **19 August - 26 August (8 days, Final evaluation)**
    -   Developer documentation using Doxygen.
    -   User documentation through detailed tutorial and post on FreeCAD
        wiki with screenshots.

# Future Scope

Since, we are taking similar input parameters which are present in
STAAD.Pro output file, so in future we can implement that user will
import output file of STAAD.Pro in FreeCAD and it will automatically
create Reinforcement detailing. This will enable us to create
Reinforcement for entire building using output from STAAD.Pro file. And
I will be interested to implement this.

**Implementation**

-   The output file of STAAD.Pro will be imported in FreeCAD using a
    button in Rebar Addon.
-   This file will be parsed through a script.
-   Script will extract required Reinforcement details from file and
    automatically fill the input values in Rebar Addon’s dialog box.
-   Now user can modify any value if required and will press OK button
    to create Rebars.

For Column Reinforcement, we can have following prototypes also and much
more as in <https://archive.org/details/gov.in.is.sp.34.1987/page/n95> :
![](/wiki/user/img/ColumnPrototypes2.png)

# Time Availability

I will be able to dedicate 40 hours per week. During regular days from
Monday to Friday, my college timings are 8:00 am to 4:00 pm IST. So, in
these days I am available for 5 hours after my college and can manage to
get 2 hours in my college timing. I am free on weekends during which I
am free to work. In the month of May, I have my final exams during which
there are 3 to 4 holidays before each exam. So, I can spend 2 of 4 days
working on my project. Since, actual coding part will start from 27 May
2019, so my final exams will not going to be a barrier in my project
work. In the month of June, I have industrial training from 3rd June to
3rd July during which I will be full time available to work on my
project. In the month of July, there will be holidays from 4 July to 15
July, during which I will also be available full time. My new semester
will start from 16 July and therefore I can contribute 4 hours per day
as mentioned above for July and August.

# Why FreeCAD?

I have always been fascinated by operation of CAD softwares. I’m an open
source enthusiast and FreeCAD is the only CAD software I have ever used.
There are several workbenches included in it and third party workbenches
are also available from within the FreeCAD Addon manager is very
interesting feature. FreeCAD has a well established community of great
developers and this project will give me an opportunity to work with
them. So, this project will turn out to be a great learning experience
for me.

# Why you?

I found myself fit to this project according to my skill set and
interest. I always try to explore and learn new things. I have keen
interest and good coding skills in Python, C/C++ and bash scripting. I
will also actively contribute and maintain the code even after GSoC.

# Reference Links:

Related Discussion:
<https://forum.freecadweb.org/viewtopic.php?f=8&t=35077>

Github Repository:
<https://github.com/SurajDadral/FreeCAD-Reinforcement/tree/automate>
