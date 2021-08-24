<div style="text-align:center;">

**Automate Reinforcement Process of Slab and Footing in FreeCAD**

</div>

## Personal Information

**Name:** Shiv Charan

**Email Address:**shivcharanmt@gmail.com

**Gitter:**ShivCharanSharma

**GitHub:**<https://github.com/ShivCharanSharma>

**Blog:**<https://codebuddy.code.blog/>

**Brief Background Information**

I am a B.Tech. (4th year) student of Computer Science at Guru Nanak Dev
Engineering College, India. Practiced in writing code in C/C++, Python,
Java, JavaScript and used Git, Django, Android Development, web
development, Embedded C.

I solved an
[issue](https://github.com/amrit3701/FreeCAD-Reinforcement/issues/10)
with Rebar Addon and here is merged PR:

[<https://github.com/amrit3701/FreeCAD-Reinforcement/pull/144>](https://github.com/amrit3701/FreeCAD-Reinforcement/pull/144)

I have implemented different types of reinforcement in FreeCAD that can
be found at :
[<https://github.com/ShivCharanSharma/FreeCAD-Examples>](https://github.com/ShivCharanSharma/FreeCAD-Examples)

## Project Information

## Project Title: Automate Reinforcement Process of Slab and Footing in FreeCAD.

## Brief Project Summary

This project is to automate Reinforcement process of slab and footing by
using the Reinforcement Workbench in FreeCAD. The idea is to create UI
and functions on top of the current implementation to combine different
types of Rebars in a single Dialog Box as per the user requirements. For
example, combine BentShape and Straight Rebars ( or different types of
rebars) in case of Slab and Footing Reinforcement.

## Detailed Project Description

## Current Scenario

1.  To create Reinforcement in a Slab or Footing, user needs to do a lot
    of work like creating Bent shape rebars, distribution
    rebars/Straight rebars in slab and Stirrup rebars , UShape rebars,
    straight rebars in case of footing and perform all calculations
    involved manually.
2.  If user decides to make changes in any parameter of Slab/Footing
    Reinforcement like covers of bentShape or Distribution rebars (int
    slab) or Covers of Stirrup (in footing), he/she needs to manually
    adjust Cover and Spacing of all Rebars provided. Doing so manually
    needs efforts never less than applying Reinforcement from scratch
    and involves lots of calculations. And obviously, there are going to
    be a number of Slab/Footing in a building and no one wants to apply
    Reinforcement to all Slab/Footing manually. So, this is a very time
    consuming task.

<div style="margin-left:3.016cm;margin-right:0cm;">

Example: You can see below how the things went wrong after modifying the
covering of BentShaped rebar.

</div>
<div style="margin-left:0.635cm;margin-right:0cm;">

![](img/Bent_shape_rebar_side_view.png)

</div>
<div style="margin-left:0.635cm;margin-right:0cm;text-align:center">

Original

</div>
<div style="margin-left:0.635cm;margin-right:0cm;">

![](img/Error_in_one_direction_slab.png)

</div>
<div style="text-align:center">

After Modifying

</div>
<div style="margin-left:3.016cm;margin-right:0cm;">

Example: You can see below how the things went wrong after modifying the
covering of Stirrup (in case of footing).

</div>
<div style="text-align:center;margin-left:1.27cm;margin-right:0cm;">

![](img/Footing_error_img.png)

</div>
<div style="margin-left:0.635cm;margin-right:0cm;">
</div>
<div style="margin-left:0.635cm;margin-right:0cm;">

Example: In case of Slab Reinforcement ( Slab spanning in one direction
).

</div>
<div >

<span style="background-color:#ffffff;">To create reinforcement in a
Slab for </span>slab spanning in one direction
<span style="background-color:#ffffff;">, user has to do following
steps:</span>

</div>

-   Select the face of the slab and create straight rebars (
    Distribution rebars ).

![](img/Config_stright_rebars.png)

<div style="text-align:center;">

![](img/Stright_rebar_in_Slab_one_drection.png)

</div>
<div style="text-align:center;">

Output

</div>

-   To create BentShape rebars, first the user needs to select one of
    the face, perpendicular to the previously selected face and then
    calculate ‘Front Cover’ and ‘Top/Bottom’ based on the values of
    Top/Bottom/Left/Right Cover of the distribution rebars.

<div style="text-align:center;">

![](img/Config_bent_shape_rebars_2.png)

</div>
<div style="text-align:center;">

Note : Bottom cover, Front cover and Anchor Length value are manually
calculated values.

</div>
<div style="text-align:center;">

![](img/Slab_spanning_in_one_direction_(isomatric_view).png)

</div>
<div style="text-align:center;">

Output

</div>

To create upper distribution bars as shown in below figure.

-   User will select face perpendicular to face selected for bentShape
    rebars, then select straight Rebar. Then calculate Front cover, Top
    cover based on Top/Bottom/Right/left cover of BentShape rebars.

![](img/Upper_distribution_rebars_in_slab_one_direction.png)

<div style="margin-left:1.27cm;margin-right:0cm;text-align:center;">

Note : Front cover and Top cover are calculated values.

</div>

-   Then calculate custom spacing for upper distribution rebars.

![](img/Custom_spacing_for_upper_distribution_rebars.png)

<div style="margin-left:1.27cm;margin-right:0cm;text-align:center;">

Note : Here spacing is Manaully calculated values

</div>

Output:

<div style="margin-left:2.54cm;margin-right:0cm;">

Repeat steps IV - V for upper distribution rebars on opposite side.then
final output will be as follows.

</div>

![](img/Bent_shape_rebar_side_view.png)

![](img/Slab_spaning_in_one_direction_final_output.png)

<div style="text-align:center">

Final output&lt;\\div&gt;

<div style="margin-left:2.54cm;margin-right:0cm;">
</div>

Step for Slab spanning in two directions and for different types of the
footing will need more manual calculations.

![](img/Screenshot_from_2021-04-11_15-35-56.png)

<div style="text-align:center;">

Slab Spanning in two direction

</div>

![](img/Screenshot_from_2021-04-11_15-37-19.png)

<div style="text-align:center;">

Column Footing Reinforcement.

</div>
</div>

## How to solve the problem?

To solve above mentioned issues, an interactive UI will be developed on
top of the current implementation of Rebar Addon in FreeCAD.

-   Dialog Box will be developed where users will input the required
    data as per the design requirements.
-   When the user will press apply button, this input data will be
    passed to functions makeBentShapeRebar(), makeStraightRebar(),
    makeStirrup(), makeLShapeRebar(), makeUShapeRebar() etc. of the
    Rebar Addon as per the requirements of Slab or Footing
    reinforcement.
-   The Reinforcement will be created using core functionality of the
    Rebar Addon.
-   To edit Reinforcement provided, the user will double click on the
    created Reinforcement object. Then he/she will be shown the same
    Dialog Box as while creating Reinforcement. And then users can make
    changes and apply them as did before.
-   There will be a separate Dialog Box for footing reinforcements.

So, the developed UI will contains following features:

1.  User will add only basic details for Reinforcement and all the
    calculations (like for cover and spacing of rebars) will be done by
    script.
2.  User can create different types of Rebars in a single step. Like
    creating Bent Shape, Straight rebars in case of slab and Stirrups
    and Rebars (of different types) for footing reinforcement.
3.  User can add number of layers and number of Rebars in each layer in
    slab or footing.
4.  For Slab and footing Reinforcement, user will be presented with a
    list of prototypes of some default configurations, which we will
    choose from “SP 34: Handbook on Concrete Reinforcement and
    Detailing” as present here:

<div style="margin-left:1.27cm;margin-right:0cm;">

For Slab:

</div>
<div style="margin-left:1.27cm;margin-right:0cm;">

<https://archive.org/details/gov.in.is.sp.34.1987/page/n129/mode/2up>

</div>
<div style="margin-left:1.27cm;margin-right:0cm;">

For Footing:

</div>
<div style="margin-left:1.27cm;margin-right:0cm;">

<https://archive.org/details/gov.in.is.sp.34.1987/page/n77/mode/2up>

</div>

Due to the time constraints of GSoC, I will implement the following
prototypes, but will keep on adding even after GSoC.

![](img/Stright_Rebar_Slab_.png)

<div style="text-align:center;">

Straight rebars in Slab

</div>

![](img/U_shaped_rebar_Slab.png)

<div style="text-align:center;">

U-Shaped rebars in Slab

</div>

![](img/LShaped_rebar_Slab.png)

<div style="text-align:center;">

L-Shaped rebars in Slab

</div>

![](img/Slab_spanning_in_one_direction_(isomatric_view).png)

<div style="text-align:center;">

Slab spanning in one direction.

</div>

![](img/Slab_Spanning_in_two_direction.png)

<div style="text-align:center;">

Slab Spanning in Two Direction.

</div>

![](img/Footing_output_img.png)

<div style="text-align:center;">

Column Footing Reinforcement.

</div>
<div style="margin-left:1.905cm;margin-right:0cm;">
</div>
<div style="margin-left:1.905cm;margin-right:0cm;">

<span style="background-color:#ffffff;">I also implemented above
prototypes manually and can be found at
</span>[<https://github.com/ShivCharanSharma/FreeCAD-Examples>](https://github.com/ShivCharanSharma/FreeCAD-Examples)

</div>
<div style="margin-left:1.27cm;margin-right:0cm;">
</div>
<div style="margin-left:1.27cm;margin-right:0cm;">
</div>

## Implementation:

-   An icon for slab and footing Reinforcement will be made and
    integrated in drop down menu of Rebar Addon. Integration in drop
    down menu can be done by modifying RebarTools.py file of Rebar
    Addon.
-   The dialog box will be developed using QtDesigner. Users will
    provide input through this dialog box.
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
    -   makeBentShapeRebar( f_cover, b_cover, l_cover, r_cover,
        diameter, t_cover, bentLength, bentAngle, rounding,
        amount_spacing_check, amount_spacing_value,
        orientation="Bottom Left", structure=None, facename=None).Adds
        Bent-Shaped reinforcement bar to the selected structural object.
    -   makeStirrup(l_cover, r_cover, t_cover, b_cover, f_cover,
        bentAngle, bentFactor, diameter, rounding,
        amount_spacing_check, amount_spacing_value, structure =
        None, facename = None): Adds the Stirrup reinforcement bar to
        the selected structural object.

## Timeline

An overview of working on tasks is as follows.

-   **Community Bonding Period (17 May - 7 June)**
    -   Having interaction on mailing list and IRC regarding important
        aspects of the project.
    -   Get to be more familiar with the code and workflow of FreeCAD
        and Rebar Addon.
    -   Learn more about reinforcement in Slab and Footing.
    -   Learn more about tools that will be used in implementation.
    -   Learn Doxygen syntax and inkscape.

<!-- -->

-   **7 June - 7 July (30 days)**
    -   Implement slab (having Straight , U-shaped, L-shaped rebars)
        reinforcement detailing function for passing user input to
        prebuilt Rebar Addon functions.
    -   Create UI for slab reinforcement (having Straight , U-shaped,
        L-shaped rebars).

<!-- -->

-   **7 July - 12 July (5 days)**
    -   Backup days for any backlog or pending task and preparation for
        phase I evaluation.

<!-- -->

-   **12 July - 16 July (5 days, Phase I evaluation)**
    -   Developer documentation using Doxygen.
    -   Submitting all the work to mentor.

<!-- -->

-   **16 July - 25 July (9 days)**
    -   Implement slab (spanning in one or two direction) reinforcement
        detailing function for passing user input to prebuilt Rebar
        Addon functions.
    -   Implement UI for slab spanning in one and two direction
        reinforcement.
    -   Create required images and icons using inkscape.
    -   Integrate UI with Rebar Addon UI.

<!-- -->

-   **25 July - 9 August (15 days)**
    -   Implement footing reinforcement detailing function for passing
        user input to prebuilt Rebar Addon functions.
    -   Create UI for footing reinforcement.

<!-- -->

-   **9 August - 16 August (1 week)**
    -   Work on UI enhancement to improve user experience.
    -   Work on backlogs and bug fixes.

<!-- -->

-   **16 August - 23 August (8 days, Final evaluation)**
    -   Developer documentation using Doxygen.
    -   Submitting all the work to mentor.
    -   User documentation through detailed tutorial and post on FreeCAD
        wiki with screenshots.

## Future Scope:

For slab reinforcement, we can have the following prototypes also and
much more.

[<https://archive.org/details/gov.in.is.sp.34.1987/page/n137/mode/2up>](https://archive.org/details/gov.in.is.sp.34.1987/page/n137/mode/2up)
: ![](img/Cantilever_slab.png)

<div style="text-align:center;">

Cantilever slab continuous over brick

</div>

For Footing reinforcement, we can have the following prototypes also and
much more.

[<https://archive.org/details/gov.in.is.sp.34.1987/page/n81/mode/2up>](https://archive.org/details/gov.in.is.sp.34.1987/page/n81/mode/2up)
:

<div style="text-align:center;">

![](img/Common_footing_example.png)

</div>
<div style="text-align:center;">

Combined Column Footing

</div>

## Time Availability

I will be able to dedicate 40 hours per week. As this is my training
semester I can dedicate my 6-7 hours per day. And as there will be only
one exam day in this semester which will be completed in May month. So I
will be available full time to work on this project. Also, my graduation
will be completed in June, thus there will not be any time constraint
from college and I can dedicate my full time to this project.

## Why FreeCAD?

The very first reason that makes me curious about FreeCAD is the
flexibility and automation that it provides to its users to create
complex designs efficiently and with a simplified design process. Users
can utilize features from a wide variety of workbenches while working on
a design and can easily switch and manage them. FreeCAD has a
well-established community of excellent coders and engineers of
respective domains and this project will give me an opportunity to work
with them. So, this project will provide me a wide variety of learning
opportunities.

## Why you?

I am a software engineering studententhusiast, and have a good
programming skill in C/C++, Python, Data Structure and Algorithms. I
like to use my skill to bring automation to different tasks and try to
help people to ease their work with automation. I like to do challenging
tasks in programming and explore new things. I will also contribute
actively and maintain the code even after GSoC and will work on adding
new features in FreeCAD.
