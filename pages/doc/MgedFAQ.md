-   See this [page](../misc/Msgid1010480.md) for the history of the
    following data.

## Editing, viewing, and correcting objects

**Q1:**


I am trying to create case walls for ammo, gun tubes, etc. and the

way I'm doing it is by making inner and outer walls using rcc and trc

primitives, and I have figured out that I need to make a combination

of the two, then hide the primitives and draw the comb, and then do *rt*

to see the finished product. That's fine. But if I

translate or rotate the inner wall, for example, away from the point

of creation, I cannot seem to figure out a way to restore it to its

original point so that it perfectly lines up concentric with the outer

wall. Can this be done with the mouse, or must I use the keyboard and

editing commands?

**A1:**


There are *reset* and *apply* options on the Edit menu when you're

in an edit mode on a primitive. The intent is that you incrementally

apply/accept changes as you are happy with them or reject/reset them

if you are not. As for your create -&gt; hide -&gt; draw steps, you can

collapse those with a "B objectname" which will erase everything else

and draw 'objectname' in one step.

------------------------------------------------------------------------

## Matrix editing objects

**Q2:**


Once I create a combination, is the proper way to modify the

combination via matrix edits, or is there some other way? I understand

that matrix edits really mean applying the same change to all elements

of an entity (primitives within a comb, for example), and then pushing

the common change to all elements.

**A2:**


Presuming you mean 3D manipulations (translation, rotation,

scaling, etc) instead of structural (adding new CSG elements), then

yes--matrix edit (aka "object edit") is the means to modify. Matrix

edit doesn't have to be on everything in a given combination, but it

is a hierarchical tree so if you apply a matrix to object A that

references objects B and C, the matrix applies to that entier

hierarchy. Whether you push the matris is a modeling design decision,

which I personally do not like performing so that editing operations

retain a useful local coordinate systems. Others have different

preferences for different reasons.

------------------------------------------------------------------------

## Resetting object vertex (V)

**Q3:**


When I move an rcc or trc, I want to reset where V is, but there

seems to be no command that allows me to reset V to 0 0 0. Is there

one?

**A3:**


Select translate on the Edit menu and then type:

`mged>??p??0??0??0`

------------------------------------------------------------------------

## Editing general cone radii

**Q4:**


Is there a way to modify the radius of rcc's and trc's? I can't

find a 'set R' command in the prim selection menu anywhere.

**A4:**


rcc's and trc's are all fundamentally a generalized cone

represented by two vectors at both ends of the cone. To change the

radius, select either the "Set A,B" or "Set C,D" menu option, and

type:

`mged>??p??###`


for whatever \#\#\# size you want to set it to.

------------------------------------------------------------------------

## Editing solid parameters A and B

**Q5:**


When I try to set A and B at the same time, thinking if I make

them the same, the radius will be uniform, but it tends to squash

them to a single point. This leads me to believe that I am setting A

and B to the same coordinates in space, not the same length (radius).

<!-- -->


Is this a true statement? (I tend to think of geometries in terms of

their respective dimensions but it seems like with MGED, you have to

know exactly where in space everything is, and that is not really

desirable for me most of the time.)

**A5:**


Sounds like the size value you're using is way too small. It

should be the absolute size using whatever units you're operating

with, just a single value (e.g., "p 1000"), not multiple values for A

and B. Doing "Set A,B" basically means "keep the base circular"

instead of ellipsoidal.

------------------------------------------------------------------------

## Picking combination and primary objects

**Q6:**


I see that you can pick which combs you want to modify under the

comb editor, but the same does not apply for the prim editor. The

prim editor seems to be only or generating new prims. Is that a true

statement?

**A6:**


No, it's not true that it only generates new primitives. It's

just lacking a drop-down box because there are generally **way** too

many primitives for that to be a useful selection mechanism with any

real model and its use is often discouraged for other reasons (it's

**very** susceptible to human error that in ways that are difficult to

recover from--use with caution). Type the name of the primitive

you wish to edit into the 'Name:' field and hit enter. The values

should update to show that primitive.

------------------------------------------------------------------------

## Translating objects

**Q7:**


When trying to translate a combination, where is the 'Z move'? I

see only 'X move', 'Y move', 'XY move'. Answer: You may have to select

the combination and use the *translate* or *tra* commands to reposition

the object.

**A7:**


Very good question! The naming convention used on the labels

should be clarified, but it's trivial "once you know". The X and Y

don't refer to the 3D coordinates but rather to the 2D view.. So if

you are looking at front, left, right, or rear views, then the z axis

runs up and down the graphics window vertically, so selecting the "X

Move" option will translate up and down the Z axis. Similarly, if

you're looking from a more complex/arbitrary view, doing an X Move or

Y move will perform more complex movements than just constrained to a

given coordinate axis. The labels should probably say something like

"Pan object horizontally" and "Pan object vertically" for X Move and Y

Move respectively with the XY Move meaning something like just "Pan

object".

------------------------------------------------------------------------

## Copying text from the command window ('journal')

**Q8:**


Is there a way to block-copy text from the command window, or save

it as a buffer/text file, in case you want to record the steps it

took you to do something?

I tried using the journal command and even tried to view the file

while a session was open but it was a zero-length file with none of

my session saved.

**A8:**


The journal command only begins recording from the moment you type

journal, and presently doesn't write out the journal entries until

you close your session. It's a limitation of the implementation.

You should also be able to copy/paste any text in the command window

using usual copy/paste methods (select region and click middle mouse

button in a text buffer in another xterm window, for example).

------------------------------------------------------------------------

## Fitting view to window

**Q9:**


Is there a 'fit to window' zoom feature?

**A9:**


The autoview command automatically resizes geometry when it is

loaded and it's intentionally 50% the bounding of your display size

so that it's guaranteed to be fully displayed at any orientation.

You can 'zoom 2' to make it fit more tightly, and can similarly wrap

those two commands into a proc of your own. autoview can be run on-

demand and is automatically run whenever you 'e' or 'draw' something

among a variety of other commands.

------------------------------------------------------------------------

## Cutting a solid to make a combination

**Q10:**


How do you use a plane to slice part of a solid to make a

combination (e.g., a plane cutting a box at an angle and just using

the resulting portion of the box)?

**A10:**


The recommended approach is to create an arb8 or similar *box*

shape that is positioned exactly how you want it and subtract or

intersect as desired. You can also use a "half" primitive, which

stands for halfspace (which is an infinite plane where half the space

is solid the other half is empty) though the performance is

non-optimal for real models.

------------------------------------------------------------------------

## Panning the view

**Q11:**


Can you pan the view before you raytrace so that you can see more

of the geometry in the rt window (fb) but without having to physically

move the geometry around?

**A11:**


Not sure I understand this question fully, but it sounds like the

answer is "yes". You can raytrace from any azimuth/elevation as well

as from any arbitrary view whether *panned* or not. By default in

mged, when you run ''rt', it will invoke the raytracer with a view that

matches the geometry window's view so if you're not in an edit mode,

you can change the view to whatever you want without editing or

modifying geometry.

------------------------------------------------------------------------

## Translating objects away from visible axes

**Q12:**


When you change (translate) the body away from the blue xyz axes,

does that actually change the coordinates as well, or is that only a

visual change (i.e. now your coordinates referenced to the origin are

totally different than from when you started)?

**A12:**


Depends whether you're in an edit mode. The blue axes you're

referring to, I presume, are the "View" axes which only refer to the

orientation of the view and which is always at the center. The green

axes are the model axes, which indicate where an object is at, and

when coupled with the white edit axes, show you how edits are being

performed.

------------------------------------------------------------------------

## Interrogate *mged* for axis changes

**Q13:**


Is there any way to interrogate MGED and find out where your new

(translated) xyz axes are relative to the original origin if you

moved the object geometry around (i.e. new 0,0,0 =3D old x,y,z +

translation matrix)?

**A13:**


Yes, turn on the Faceplate option on the Misc menu.. that option

really should be set by default. Be sure to run File-&gt;Create/

Update .mgedrc so that it keeps your settings between runs of mged.

------------------------------------------------------------------------

## Creating a plane (2D) object

**Q14:**


How can you create just a plane, triangle, etc. if you need one?

Do you just make a 3D primitive with zero thickness?

**A14:**


This one is somewhat philosophical. BRL-CAD is predominantly a

3D solid modeler so creating 2D or 1D objects is not only highly

discouraged but generally rather complicated. That said, halfspaces

work well instead of planes, arb5's instead of triangles, and spheres

instead of points. Alternatively, in the 2D realm, you can use the

sketch primitive and the sketcher to make purely 2D objects, though

the use of those are generally limited to extrusions. There is a way

to manually create triangles and meshes, but it's non-trivial and

similarly limited in use until you form a closed 3D shape.

------------------------------------------------------------------------

## Creating a non-smooth surface

**Q15:**


How do you make a non-smooth surface such as a corrugated circular

surface surrounding a cylinder?

**A15:**


There are two methods to achieve that, both with their tradeoffs.

The CSG approach would have you create a cylindrical pattern that

matches your corrugation pattern. For example, you can make something

like corrugated duct tubes by subtracting a linearly translated

pattern of torii from a cylinder--create a similar smaller version

to hollow out the middle. Alternatively, you could use a 2D extrusion

approach for something as simple as a cylinder where you model the

shape in 2D using a *sketch* primitive and combine that with an

*extrude* operation, and you'd have it. You can see an example of the

CSG approach using the pattern tool at <http://ftp.brlcad.org/tmp/gear/>

where I create a simple 6-tooth gear using a relatively simple tooth

shape.

------------------------------------------------------------------------

## Constraining angles of rotated components

**Q16:**


How do you set the angle that an articulated rotating component

may sit at (e.g., a hinged part or arm)? Is such a thing possible?

**A16:**


It is possible, but frankly not a strong point of the package.

You'd use a joint/constraint system and have it solve for various

angles. It's quite difficult to use frankly, and generally easier to

perform the rotation using one of several rotation commands (see the

MGED Quick Reference cheat sheet)--at least one of those is dedicated

to rotation via angles. You cannot set the angle as an automatically

resolved constraint at the moment.

------------------------------------------------------------------------

## Repeating construction of an object (pattern editing)

**Q17:**


If you wanted to distribute a common structure on the inside of a

cylinder at a fixed spacing, how would you go about doing something

like that (e.g., a structural stiffener)?

**A17:**


If I understand the question correctly, the pattern tool should

do the trick (on the Tools menu). Probably a cylindrical pattern

with some periodic/fixed spacing. Basically the same as the gear I

mentioned above, but with a different base object being duplicated.

------------------------------------------------------------------------

## Batching or scripting *mged* commands

**Q18:**


Can you take a series of MGED commands to build a geometry and

batch-file it and just have MGED run the batch file in order to

autocreate geometries?

**A18:**


Yes! Create your text file and run mged using the -c option for

command/classic mode. You can do something like

`$??mged??-c??file.g??<??my_transcript.txt`


or here now documents like:

`$??mged??-c??file.g??<`<EOF >`??my_log.txt??2>&1`
`` `cat??my_transcript.txt` ``
`EOF`


and more. You can also use the -c option to run any individual mged

command without it bringing up the entire mged environment, e.g.,

`$??mged??-c??myfile.g??tops`

------------------------------------------------------------------------

## Lighting and the *mater* command

**Q19:**


I have used the mater command to make a combination white but it

shows up gray in rt. How do I fix that? Is that a lighting property?

What about the fact that the wireframe in the regular MGED graphics

window is always red?

**A19:**


That is a lighting property and is dependent upon the lights in

the scene. If you define no lighting sources, rt creates default

lights for you. First, make sure you really are looking at what you

think you're seeing by setting the object's color to green or blue

instead of white. If you don't, then you're doing something else

wrong. The mater command is supposed to be used on regions, which

gets into a whole hierarchy discussion that is far beyond this forum

and better explained over the span of the tutorial series. The fact

that you set a color on a non-region is probably why the wireframe is

still red.

------------------------------------------------------------------------

## Translating and rotating objects

**Q20:**


When I shift and rotate geometry around so that it fits into the

viewing area (a) does that actually reposition the geometry to a new

place, or is that just visual; (b) is there a 'reset' or 'undo'

command to reset the geometry to its original position; and (c) is there
a way

to precisely re-zero the geometry?

**A20:** This sounds a lot like question 13 and the answer depends on
whether you're in an edit mode or not. If the edit menu lists a bunch of
editing options, along with options to Accept/Apply/Reset/Reject, then
you are in an edit mode and changes to the geometry window may be actual
edits (it depends what buttons you press--see the cheat sheet on the
main website documents section). If you don't see
Accept/Apply/Reset/Reject options then nothing you do in the graphics
window will edit geometry, you're only affecting the view orientation.
If you do see then, then those aforementioned Edit menu options of Reset
and Reject are there to help. To precisely select a view, either use the
View menu or type one of the key-bindings in the graphics window (e.g.,
'f' for front, 't' for top, '3' for 35/25, '0' to stop it from spinning
if you hit xyzXYZ).

------------------------------------------------------------------------
