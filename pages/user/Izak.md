## PROJECT PROPOSAL

## PERSONAL INFORMATION

Name: Isaac Kamga.

E-mail: u2isaac@gmail.com.

Internet Relay Chat Username: Izak.

Brief Background information.

I am a final year Master of Science in Computer Science student at the
University of Buea , Cameroon , Africa holding a Bachelor of Science
degree in Mathematics.I have worked on various data structuring,
algorithmic and compiler-related individual and team projects in the
University community which I really enjoyed.By June , I expect to be
done with the writing of my thesis and will be available for 40+ hours
weekly to implement a heart surface primitive for BRLCAD software.If I
am not done with the thesis or I am given more work,I will work on the
thesis writing during the day and allocate time to work on the BRL-CAD
software during the night hours making sure I dedicate atleast 40 hours
each week.

## PROJECT INFORMATION

PROJECT TITLE: Implementation of a heart primitive.

## PROJECT SUMMARY

In our world today , we observe that all solid objects are simply
combinations of basic ones like cubes,spheres,cones,etc and we
frequently have to manipulate objects which have surfaces such as
gadgets and devices . With the explosion in ubiquitous technology,
Computer-aided design (CAD) software help us create digital content in
adverts and movies as well as visualize some solid objects like perfume
bottles and shampoo before they are actually manufactured. In this
project, we propose that BRL-CAD, which aspires to be the best CAD
software, should incorporate a heart, a symbol of love, into its core
functionality as one of its basic solid objects in order to increase its
customer base and differentiate itself amongst its competitors. Indeed,
this heart structure ( also called a heart primitive ) shall be used by
those producing cartoons and designing electronic cards, gifts and
presents during celebrations such as birthdays, weddings,family
reunions, anniversaries and Valentine's day which deeply appeals to many
individuals,families and communities.So during the summer, this heart
primitive will be included into the raytrace library as a set of
routines with corresponding support added to other parts of the source
code.

## PROJECT DESCRIPTION

In this section of this proposal, I give a detailed description of how I
am going to implement the heart primitive. In order to implement a heart
primitive for the BRL-CAD software, we have to write a set of
routines.These routines will be stored in the hrt.c file that help for
ray intersection, geometric representation and analysis of the a heart
as well as the combination of regions using boolean operations which
assist BRLCAD users in constructive solid geometry (C.S.G.) modeling.

--hrt.c Here, we implement ray intersection , geometric analysis ,
geometric representation and combine several elliptical paraboloids to
form a heart. This hrt.c file is the heart of the heart primitive. We
include common.h for portability , system headers like stdio.h, math.h
and stddef.h, db.h for database interactions, raytrace.h and rtgeeom.h .

The sextic equation given below by the formula

F(x,y,z)=0 ------- (1)

where F(x,y,z) = (x^2 + 9/4\*y^2 + z^2 - 1 )^3 - x^2\*y^3 - 9/80 \* y^3
\* z^3

defines the surface of the heart and it happens to be symmetric along
the x-axis. We need to Solve this equation for x^2 inorder to enable us
plot the heart curve in three dimensions. To do this, we rewrite the
equation into a function of two variables P(y,z) which yields Q(x,y). We
get x = Q(y,z) = sqrt(P(y,z)). The sextic equation above gets sinplified
to the formula

(a + 9/4\*y^2 + z^2 - 1)^3 - a\*y^3 - 9/80\*y^3\*z^3 = 0 ---------- (2)

by a = P(y,z) = x^2.

This gets reduced to a cubic (of power 3) polynomial given below

a^3 + b\*a^2 + c\*a + d = 0-------------(3)

where

b = P1(y,z) = 27/4 \* y^2 + 3 \* z^2 - 3. c = P2(y,z) = 405/16 \* y^4 -
27/4 \* y^2 + z^4 + 9/2 \* z^2 \* ( y^2 + 1) + 1. d = P3(y,z) =
729/64\*y^6+243/16\*z^2\*y^4+27/4\*y^2\*z^4-27/4\*y^2\*z^2-81/4\*y^4+9/2\*y^2+z^6-z^4
+ z^2-1.

The cubic equation in (3) can be solved algebraically using a division
method or a decomposition as referenced in the research articles below
(See "Links to code and algorithms you intend to use" section in this
proposal). The roots of the equation will be Q(x,y) =
{a1,a2,a3,a4,a5,a6} where ai = Q(x,y) for i in {1,2,3,4,5,6}. We are now
able to plot the heart curve in 3D.

Ray tracing

Now we go over to how I intend to evaluate a ray against the sextic
equation in (1).

First of all , I will parametrize the sextic surface equation in (1) by
converting it into the form

x = F1(u,v) ----------- (4)

y = F2(u,v) ----------- (5)

z = F3(u,v) ----------- (6)

I intend to compute the normal vector (ray) using the cross product of
the partial derivatives of the coordinate functions. That is,

F1u(u,v) = partial(F1(u, v)) / partial(u) ------------- (i)

F1v(u, v) = partial(F1(u, v)) / partial(v) -------------(ii)

F2u(u, v) = partial(F2(u, v)) / partial(u) -------------(iii)

F2v(u, v) = partial(F2(u, v)) / partial(v) -------------(iv)

F3u(u, v) = partial(F3(u, v)) / partial(u) --------------(v)

F3v(u, v) = partial(F3(u, v)) / partial(v) --------------(vi)

where the vectors

tu(u, v) = &lt;F1u(u,v), F2u(u,v) , F3u(u,v)&gt; and tv(u, v) =
&lt;F1v(u,v) , F2v(u,v) F3v(u,v)&gt; are tangents to the surface. Thus,
we obtain the vector perpendicular to the tangent ( the normal to the
surface) which is N(u, v) = p(u, v) / \|\| p(u, v) \|\| where p(u, v) =
tu(u,v) X tv(u,v). The normal to the surface N(u,v) is the ray touching
the heart from a particular point in 3D.

Rendering

Here, I discuss how I intend to do visualization (geometric
representation and analysis). I intend to do this by finding the
intersection points between the line (light ray ) and the heart. We
simply will write a line-heart test which tells us if a point on the
heart surface intersects with the heart. The points of intersection are
those that satisfy the line equation and the equation for the surface of
the heart at the same coordinates x, y, z. Here , we equate (1) and the
equation of the line given below by

X = o + dL --------------- (7)

where d &gt; 0 , X = (x,y,z) is in R^3 and L is the direction of the
line.

To search for points that are on the line and on the heart means
combining the equations and solving for d. When equations are combined ,
expanded and rearranged , we get a quadratic equation

a\*d^2 + b\*d + c = 0 ---------------(8)

which can be solved using the quadratic formula.

d = -b + sqrt(b^2 - 4 \* a \* c) / 2\*a and d = -b - sqrt(b^2 - 4\*a\*c)
/ 2\*a.

If the value of b^2 - 4\*a\*c is less than zero, then it is clear that
no solutions exist, that is, the line does not intersect the heart.If it
is zero, then exactly one solution exists, that is, the line just
touches the heart in one point.If it is greater than zero, two solutions
exist, and thus the line touches the heart in two points (the entry and
exit point).

Boolean operations

Intersection In order to write the intersection of different primitives
with the heart primitive , I will solve for the 3D surface R(x,y,z)
using the method given above (Equating (1) and the equation of the given
primitive).

We create bounding box for the heart.

We transform the points on the heart to points on a heart centered at
the origin, with a height along the the positive Z axis and a vertex V.

We find the point of intersection W of a line with the surface of a
heart and the vector normal to the tangent plane at the point of
intersection.

We write routines to interact with the values of the heart in the
database.For example, routine to free the database storage of he heart,
change database formats and export the heart from the database.

We then write routines to compute the volume, surface area and centroid
of the heart. Routines to print the heart , get curve points, plot the
heart and tesselate will be written.

We write routines to return the normal, entry and exit points of a ray .

### LINKS TO CODE OR ALGORITHMS WHICH YOU INTEND TO USE

Research papers

1.Taubin, G. "An Accurate Algorithm for Rasterizing Algebraic Curves."
In Second ACM/IEEE Symposium on Solid Modeling and Applications
Proceedings. 221-230, May 1993.

2.Nordstrand, T. "Heart." <http://jalape.no/math/hearttxt>.

3."A Generalization of Algebraic Surface drawing" by James F. Blinn.

4.Wolfram mathworld's sextic
equation:<http://mathworld.wolfram.com/HeartSurface.html>

5.Solving sextic equations by division , Raghavendra G. Kulkarni.

6.Solving sextic equations by decomposition , Raghavendra G. Kulkarni.

Pictures

1.Three dimensional heart with sextic equation:

<http://www.google.cm/imgres?imgurl=http://upload.wikimedia.org/wikipedia/commons/thumb/f/f5/Heart3D.png/400px-Heart3D.png&imgrefurl=http://en.wikipedia.org/wiki/Heart_%28symbol%29&usg=__XN7WVIXRvY-U2iWfJEUScKLec3w=&h=431&w=400&sz=46&hl=en&start=7&zoom=1&tbnid=kE8CeD2yTcfjQM:&tbnh=126&tbnw=117&ei=wv5_UY7cFqbk4QTGwIHIDQ&itbs=1&sa=X&ved=0CDcQrQMwBg>

2.Two dimensional heart with sextic equation:

<http://www.google.cm/imgres?imgurl=http://image.spreadshirt.com/image-server/v1/compositions/3874833/views/1,width%3D280,height%3D280,appearanceId%3D1.png/yellowibis-com-mathematics-toddler-t-heart-surface-white_design.png&imgrefurl=http://yellowibis.spreadshirt.com/yellowibis-com-mathematics-toddler-t-heart-surface-white-A3491939&usg=__RGCh-_OLatg54LA5YvW6RlD4Hr8=&h=280&w=280&sz=40&hl=en&start=11&zoom=1&tbnid=EAbPmsQpWM9CeM:&tbnh=114&tbnw=114&ei=wv5_UY7cFqbk4QTGwIHIDQ&itbs=1&sa=X&ved=0CD8QrQMwCg>

3.Three dimensional heart centered at origin according to Taubin,G:

<http://www.google.cm/imgres?imgurl=http://www.maa.org/mathland/pic03563.jpg&imgrefurl=http://www.maa.org/mathland/mathtrek_02_11_02.html&usg=__DBx2PqQ_2PQIprMydn8zBX5VS60=&h=200&w=200&sz=6&hl=en&start=4&zoom=1&tbnid=qBdMD9--k5-pOM:&tbnh=104&tbnw=104&ei=DQGAUdCmO4HX4ASa9YGoDQ&itbs=1&sa=X&ved=0CDEQrQMwAw>

Code patch

<http://sourceforge.net/p/brlcad/patches/174/>

## DELIVERABLES

Pre mid term evaluation period

-   Ray intersection with heart.
-   Geometric analysis and representation
-   Compute heart metrics like surface area and volume of heart.
-   Testing of hrt.c.

Post mid term evaluation period

-   Combinations and regions using booolean operations.
-   Database interactions.
-   Intersections with other primitives.
-   Integrating and documenting heart primitive into BRLCAD

## DEVELOPMENT SCHEDULE AND TIMELINE

May 27th : Community bonding period

(3 weeks)

-   Study BRL-CAD manuals,tutorials series and documentation concerning
    hacking.

<!-- -->

-   Compile BRL-CAD source code ,Study code base and remove bugs.

<!-- -->

-   Discuss with other developers and BRL-CAD mentors to refine
    mailing-list etiquette.

<!-- -->

-   Study the src/librt/primitives/\*/\* and /include libraries.

<!-- -->

-   Acquaint myself with necessary software like svn

June 17th to July 26th : Work period (Pre-mid term evaluation)

(1 week)

-   Ray intersection with heart.

<!-- -->

-   Testing and debugging routines.

(2 weeks)

-   Geometric analysis and representation.

<!-- -->

-   Testing and debugging routines.

(1 week)

-   Compute heart metrics like surface area and volume of heart.

<!-- -->

-   Testing and debugging routines.

(2 weeks)

-   Testing routines in hrt.c code.

<!-- -->

-   Submission of hrt.c to mentors for corrections.

June 29th to August 2nd : Mid-term evaluation

(1 week)

-   Submission of preliminary hrt.c to Google.

Aug 5th to Sept 13th : Work period (Post mid-term evaluation)

(2 weeks)

-   Combinations and regions using

<!-- -->

-   -intersection operation.

<!-- -->

-   -union operation .

<!-- -->

-   -exclusion operation.

(2 weeks)

-   Database interactions.

<!-- -->

-   Intersections with other primitives.

(2 weeks)

-   Testing and debugging of hrt.c.

Sep 16th to Sep 27th: Testing and Documentation period

(1 week)

-   Integrating heart primitive into BRL-CAD.

<!-- -->

-   Final testing and debugging of src/librt/primitives/hrt/hrt.c code.

<!-- -->

-   Documenting heart primitive in BRL-CAD.

<!-- -->

-   Submit hrt.c code to Google.

(1 week)

-   Final submission of hrt.c code to Google.

## TIME AVAILABILITY.

I am at the last phase of my M.Sc. research and will be done with the
thesis before June. I will have ample time to code full time for 40+
hours weekly till the end of the summer holidays.My thesis defense will
take place after the summer holidays in November . If I am done with my
thesis in June, while awaiting defense and graduation in December 2013
after the summer , I will be available for some months to do any
polishing and maintenance work given to me by BRL-CAD mentors.If I am
not done with the thesis or I am given more work, I will work on the
thesis writing during the day and allocate time to work on the BRL-CAD
software during the night hours making sure I dedicate atleast 40 hours
each week.

## WHY BRL-CAD?

First of all, I really believe that software can change the world by
providing new technologies and that software should be free. I choose
BRL-CAD because it is a not-for-profit technology organization which
offers me the opportunity to assist the United States Army Research
Laboratory with tools which help them simulate and visualize their
combat vehicle systems and war events. Working with BRL-CAD also helps
me contribute over the long-term and gain status within the hacker
community based on my mathematical/Computing background and academic
interests. Although I have not contributed before to opensource ,I see
implementing a heart surface primitive as a long-awaited opportunity to
provide more primitive options (adding a heart to the raytrace library
which is the heart of BRL-CAD) for the BRL-CAD software and a jumpstart
to my continued contribution to open source software through
BRL-CAD.This project will also help BRL-CAD users to build
three-dimensional models related to the heart and love - a virtue we
really need in our world today.

## WHY YOU?

I am a final year M.Sc. student in Computer Science at the University of
Buea (www.ubuea.net) , Cameroon , Africa and a holder of a B.Sc. in
Mathematics & Computer Science. I am currently rounding up with my
research thesis on business process compliance. I have a good background
and intuition in Mathematics and algorithms as well as C/C++
programming. In the past , I worked on various data structuring and
algorithmic individual and team projects in the University community
which I really enjoyed. For example , I built mini-compilers flex/bison
to reason about and infer the regulatory compliance in associated
business process graphs . Also , I worked within a team to implement red
black trees and variants like order statistics trees , interval trees
and persistence trees (over 6000 lines of C code). I was enthused
collaborating in teams with other bright thinkers . I was the best on
some projects and mediocre on some others - but I really learned the
importance of communicating and working in teams with other smart
individuals. I was born into an extended family of researchers in
Research institutions and Universities under the Cameroonian
government.This gave me the passion to become a researcher for
not-for-profit organizations and contribute to the open source
community. With this upbringing ,background and experience, I think I
have the necessary skills to implement a heart surface primitive for the
BRL-CAD software. I am familiar with various open source software
engineering tools like svn, gcc, gdb ,emacs ,etc and switched to Linux
distributions ( using Red Hat and Ubuntu ) since 2010. Also, I am at the
last phase of my research and will be done with the thesis before June.
I will have ample time to code away the summer holidays .If I am not
done with the thesis or I am given more work,I will work on the thesis
writing during the day and allocate time to work on the BRL-CAD software
during the night hours making sure I dedicate atleast 40 hours each
week. Lastly , I will make sure I communicate my progress , problems
encountered and further work to my mentors in Weekly reports to
facilitate the supervision and management of the project. I will discuss
with mentors real time for short clarifications on IRC chat and demand
long clarifications on the mailing list.

## ANYTHING ELSE?

I think it would be great for BRL-CAD to select me for various reasons.
Firstly , it will greatly encourage the programmers around my community
and country to come up to hackerdom standard and contribute to open
source projects. It will also attract and encourage a lot of young ones
in my country and continent towards the computing field as a whole.
Also, BRL-CAD will gain the reputation of encouraging equal opportunity
and ethnic diversity by helping to groom more hackers from
underrepresented minority backgrounds in computing like Africa.

## DEVELOPMENT REPORT

You want to read my [diary](GSOC_2013_logs.md) to know the status of
my work.
