## POV-Ray Export and LinuxCNC StepConf improvement

**Name:** Gurwinder Singh Bains

**E-mail Address:** gswithbains@gmail.com

**IRC Username :**Gurwinder

## Background

B.Tech final year student of Computer Science at Guru Nanak Dev
Engineering College, Ludhiana, India. In my free time I love to draw
portraits with graphite and charcoal. I'm a weightlifter under SAI(
Sports Authority of India) from past two years.

## Brief Summary

## POV-Ray Export

Geometry conversion is a very important aspect for every CAD software as
it is the basis for CAD data exchange between various CAD softwares.
BRL-CAD has dozens of importer and exporters but this does not include
support for g to POV-Ray file converter. So am going to write a POV-Ray
exporter in this summer.

## LinuxCNC StepConf improvements

LinuxCNC is open source software system for numerical control of
machines such as milling machines, lathes, plasma cutters, routers,
cutting machines, robots and hexapods. It can control up to 9 axes or
joints of a CNC machine using G-code (RS-274NGC) as input. For
configuring LinuxCNC with machines there is a GUI, StepConf written in
Python. So am going to add missing features in it.

## Description:

## POV-Ray exporter

POV-Ray, is a ray tracing program which generates images from a
text-based scene description, and is available for a variety of computer
platforms. It was originally based on DKBTrace, written by David Kirk
Buck and Aaron A. Collins for the Amiga computers. Many methods for
generating the 3-D models are used, including a companion program
"moray" for interactive modeling. BRL-CAD has many exporters and
importers which are used as a way of sharing data between BRL-CAD and
other CAD softwares. They all are written well. BRL-CAD require g to
POV-Ray converter from last two three decades and I'm going to write a
code of POV-Ray exporter for BRL-CAD in this GSoC. Currently I have
submitted code for sphere and torus which is working successfully. In
all these, database is parsed and by using that parsed data using librt
library it exports those primitives into POV-Ray file format. I have
written tgc code and cylinder which requires some improvement. Moving
further in exporter I am going to convert some primitives upto the
Mid-Term Evaluation. I have to make macro which converts BRL-CAD's
primitives into POV-Ray. POV-Ray has different way of representing its
own primitives. So it require more focus on macro logics. I will work
for BRL-CAD's POV-Ray exporter upto the Mid-Term Evaluation.

## LinuxCNC StepConf Improvements

LinuxCNC is an open source software which is used with many machines
like milling machines, lathes, plasma cutters, routers, cutting
machines, robots and hexapods. Its used for numerical control of
machines. After Mid-Term Evaluation, am going to work for LinuxCNC in
addding new features on StepConf( Stepper Configuration Wizard ). As its
a program for generating configuration files for specific class of CNC
machines so it requires more features to be added. So I'm going to work
on it in this GSoC after Mid-Term Evaluation and write those features
upto the Final Evaluation

My whole GSoC is divided into two parts. Before Mid-Term Evaluation, I
have to submit POV-Ray exporter in which I will convert some remaining
BRL-CAD's primitives. And after Mid-Term Evaluation I am going to work
on LinuxCNC in adding new features in Stepper configuration Wizard upto
Final Evaluation.

## Development Schedule and Timeline

Upto 25th May: Community Bonding

I will do 1 to 2 hrs/day work on 26 and 27 May as I have my final
project exam. I will be totally dedicated to gsoc after exams. I will be
in Communication with my mentor, familiarize with POV-Ray and BRL-CAD,
understand parsing of file and understand the exporting of different
primitives.

Pre-mid term evaluation( May 26 to Jun 26 )

1st Week:

-   Read particale
-   Export particale

2nd Week:

-   Read ell from database
-   Export ell

3rd Week:

-   Read arb8 from database
-   Export arb8

4th and 5th Week:

-   Read tgc from database
-   Export tgc
-   Start basics of Python

26 June to 3 July: Submitting mid term report

30 June - 3 July (Mid term Evaluation)

After Mid Term Evaluation From 4 July to 17 Aug

-
-
-

## Time Availability

I am not fully available in the month of April and May as I have my end
semester exams from 27th April to 14th May. After May I will work for
40+ hours/week for gsoc( except 5 hours in the evening).

## Why Me

As I contributed in BRL-CAD and submitted g-pov converter to it before
starting of gsoc. So it make me feel proud if I wrote the remaining
primitives conversion code for BRL-CAD.

## Previous Related work

<https://github.com/GurwinderSinghBains/BRL-CAD> I have submitted four
primitive conversion for g-pov converter.

## Why BRL-CAD

I choose BRL-CAD because since I started contributing to this community
I have had the opportunity to learn so much about software and
open-source development and also due to my special interest in computer
graphics.

## Refrences

\[1\] http//:povray.org

\[2\] http//:brlcad.org

\[3\] http//:linuxcnc.org