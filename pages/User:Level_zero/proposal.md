# Personnel Information

|                     |                                                    |
|---------------------|----------------------------------------------------|
| **Name**            | Mohit Daga                                         |
| **Email Address**   | <mohit.daga@ieee.org>                              |
| **IRC(nick)**       | zero_level                                        |
| **Phone Number**    | +91 9783582684                                     |
| **Mailing Address** | E\#221 Ram Path, Shyam Nagar, Jaipur – 302019.(IN) |
| **Time Zone**       | UTC +0530                                          |

## Brief Background

I am an Undergraduate Student in Computer and Communication Engineering.
Currently in my pre-final year, I have done diverse range of projects
varying from Computer Systems, graphics, Image Processing and Learning.

# Project Information

## Project Title

Consolidating and Adding the Image Processing Functions to LIBICV

## Brief summary of Project

BRL-CAD has a number of image processing tools. Currently all the tools
are implemented in a modular fashion where in each tool is accessed as a
module. The primitive task of this project is to combine the image
processing functionalities of these tools to a library. This task will
ensure the re-usability of these functionalities by the application
programmer through relevant API calls in the code and thus will be
useful for building a proper GUI for BRL-CAD and helpful in other new
tools/functions to be added to BRL-CAD in future.

## Project Description (Detailed)

### Introduction

-   This project aims at consolidating the functionalities of the Image
    Processing Tool (IPT) (around 100 in number) under a library
    (already initiated as LIBICV in BRL-CAD).
-   Additionally this project will emphasize its focus on the usability
    of the image processing functions.

### BRL-CAD’s IPT(s) Information and Current Status

Currently these tools are implemented as standalone applications where
in each tool is a separate program and separate executable are compiled
through these programs. To run any tool, currently we pass command line
arguments to the executable file (separate for each tool) and the return
arguments are received on standard output buffers or it could be done by
saving the output at BRL-CAD’s IPT(s) are extensively written for
various Image Processing task. Apart from the other formats, it has
support for the BRL-CAD pioneered **.pix** format and the UNIX plots.
Thus BRL-CAD cannot use any other third party library for Image
Processing without altering them. Therefore work is underway in
strengthening and Consolidating BRL-CAD’s image Processing Library and
adding various Image Processing functionalities in it.

### Consolidating IPT(s) under LIBICV

This is the primary task of this project wherein the image processing
functionalities of the current tools are to be arranged and consolidated
to a library lib_icv. It is possible to create our own library of
function by writing the functions as subroutines and compiling them to
link to a shared library.

Any API caller just needs to include the said library and thus has
access to the implemented functions of image processing.

Among the current tools, image processing functions and there common
groups will be identified which could enhance the usability of the
tools. Proper Documentation will be done as discussed in later sections.

### Formats of Image to be supported

The current status of icv.h defines
.PIX,.BW,.ALIAS,.BMP,.CI,.ORLE,.PNG,.PPM,.PS,.RLE,.SPM,.SUN,.YUV and
looking at the conversion tools among the IPTs in src/util folder these
seem to be the only relevant formats for BRLCAD. Very few formats among
them are currently implemented for loading and saving of the images.
This project will create functions for loading and saving of all these
formats.

### Categories of Image Processing Functions

On analyzing the current status of the IPTs they involve usage of the
following categories of image processing functionalities.

-   Crop or Rect
-   Differences and other arithmetic operations
-   Filters,
-   Histograms and Equalizations
-   Rotate
-   Scale or Shrink
-   Stats
-   Thresh
-   Interpolate
-   Dimensions and Image Information
-   Background
-   Borders
-   Fading
-   Merge or Split
-   Saturation
-   Morphing

In this project, I propose to add these functionalities in the ICV
library. Further analysis will be done to identify other functionality
(enough time is given for this in schedule). During the initial working
stage details of these functions will be worked on, to identify the
input and output arguments, usability and different methods to be
incorporated in the functions.

### Implementation

The current tools present in the /src/util include usage of most of the
above mentioned functionalities and the image format. The implementation
task will include extracting these functionalities, finding common
attributes to arrange them in common groups, improve usability and add
multiple available methods.

### Use of image containers and structures

The current structure for used in the icv library, for image details is
as follows:

`   struct icv_image_file {`
`   uint32_t magic;`
`   char *filename;`
`   int fd;`
`   int format;         /* ICV_IMAGE_* */`
`   int width, height, depth;   /* pixel, pixel, byte */`
`   unsigned char *data;`
`   unsigned long flags; `
`   };`

Like any other image processing library there will be a need of
containers to keep the points, arrays etc. No, judgment is made at this
stage about these structures. In the working schedule special time is
devoted for this purpose. On discussion with the mentors and other
developers decision will be taken about deciding the image container and
other structures needed for this library.

## Sample Codes and Tools

-   Code Patch (A code containing functions to load .png, .bw and .pix
    files). <https://sourceforge.net/p/brlcad/patches/176/>
-   Tools of Image Processing in /src/util.
-   gprof for Performance Analysis

### After Application Deadline

Added a more robust patch which uses functions to implemneted load
functions and thus converts to files from one format to other.

#### Details of Patch

<https://sourceforge.net/p/brlcad/patches/178/>

## Documentation

For any library the documentation defines the way it will be used by the
users and other hackers. As per the current practice, Doxygen Markups
will be added to the files in the library. This will include the input,
output arguments. Details of the various methods in the functions. In
detail documentation about method could also be done on BRLCAD wiki.

## Deliverables

A robust image processing library.

## Working Schedule

### upto June 17 (Analysis and Design Period)

-   Exploring the code.
-   Make a short rough bio about each tool - *the way they work*.
-   Find the Image Processing functionalities used in them. Look at
    duplication in the functionalities.


(5-10 tools/day depending on varied length.

-   Preparation of rough ideas of each functionalities and the way they
    will be implemented with additional improvements in usability.
-   Discuss with mentor and other developers about the final plan for
    the design of the library. This includes :
    -   the possible formats to be supported (In addition to the already
        started in include/icv.h)
    -   Addition of Different functionalities and there usability
        improvements.
    -   Discussion about common groups identified for different
        functionalities.
-   Learning usage from BRLCAD libraries like common.h libbu libbio

At the end of this period : **A finalized plan to proceed for the
development of the library**.

### June 17 - Sep 2 (Development Phase)

#### June 17 - July 1 \[\~2 Week\]

-   Implementation of various Structures of the new library
-   Deciding about the functions to be included in different files based
    on categories.
-   Deciding the input parameters and return type of each function.
-   Identify error handling in each Function.
-   Witting Documentation of all the structures included. PDF+Wiki
-   Creating Patches all together.

#### July 1 - Aug 19 \[\~7 Week\]

-   Implementation of image processing functionalities focusing on
    categories identified during project analysis period.
-   Enough Time is allotted to this to follow up the implementation as
    decided during analysis step.
-   Implementation of 3-4 functions a week which includes unit-level
    testing and code coverage.
-   Documentation of the functions including input output
    arguments/methods etc.

To implement the image processing functionalities common groups have
been identified details of which are given at
<http://brlcad.org/wiki/User:Level_zero/GSOC13/ImplemnetationDetails-1>
.Further these groups have varied implementation load, Thus to balance
the load for a particular following weekly plan has been chalked in.

##### Sub Division

-   WEEK-1
    -   Crop or Rect (GROUP\#1)
    -   Differences and other arithmetic operations (GROUP\#2)
-   WEEK-2
    -   Filters, (GROUP\#3)
-   WEEK-3
    -   Histograms and Equalizations (GROUP\#4)
    -   Stats (GROUP\#6)
-   WEEK-4
    -   Scale or Shrink (GROUP\#5)
    -   Interpolate/Decimate (GROUP\#8)
-   WEEK-5
    -   Thresh (GROUP\#7)
    -   Background and Border (GROUP\#9)
-   WEEK-6
    -   Merge or Split (GROUP\#10)
-   WEEK-7
    -   Morphing and other Misc (GROUP\#11)

#### Aug 19 - Sept 2 \[\~2 Week\]

-   Implimentation of Import/Export Modules.
-   Testing these Modules.
-   Documentation of these modules

### Sep 2 - Sep 27 (Final Wrap UP and Cleaning)

#### Sep 2 - Sep 9 \[\~1 Week\]

-   Code Cleaning
-   System Level testing for the library.
-   Giving final structure to the documentation.

#### Sep9 - Sep16 \[\~1 Week\]

-   Creating Demos For each functionality and Final cleaning

#### Sep 16 - Sep 27 \[\~1 Week\]

-   Performance Analysis using gprof for different data.
-   Final code submission with Google.

## Time Availability

-   During summer holidays I am completely free. I like working infront
    of screens and reading all types of books.
-   I can devote 40-50 hrs/week .
-   Besides this I may have to take a weeks off for a meditation seminar
    and the dates are still not known. Even if this happens I have
    ability to work for late hours to complete work at hand.

## Why BRL-CAD?

In my final year at the university, I am due to work on my Under
Graduate thesis. As per my background, my university has assigned me a
faculty dealing in graphics and Image Processing. This motivates me to
utilize my summer holidays working with BRLCAD due to their large code
base dealing with Image Processing and Graphics and thus becoming a
regular contributor with it in my final year which would help me to
complete my thesis.

## Why you?

I am good in c, c++. I will not say that I possess excellent coding
skills. But I have enough to work on this project. Besides this I am
dedicated and have an inquisitiveness to learn new things.