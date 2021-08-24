### Bio

I’m Andrei, a CS undergraduate at Polytechnic Univ. of Bucharest,
current in the 4th and last year.When I’m not coding, I’m playing
basketball, going to the gym or just hanging out. I’ve been with BRL-CAD
for GSoC 2012 and Code-in ’13. In my opinion, those projects offer me a
much better view on this and how I should tackle situation, it’s been a
great learning experience.

In the past two years, I’ve been working(mostly open source) as well as
improved my CS knowledge all around. While I’m not an avid CAD user and
there’s no secret behind this, I do like the software development
aspects of BRL-CAD(on short, I find writing code for CAD applications
interesting as it involves several areas like math, os, oop etc) and the
community which, even if small, it’s enthusiastic and willing to help.

Regarding my proposal, I’ll avoid ‘advertising talk’ and be as honest
and upfront as I can. Also, I was rather short on the Bio as I believe
it’s no point reiterating known data all over again.

E-mail: popescu.andrei1991@gmail.com

Full name: Popescu Andrei-Constantin

Timezone: UTC +2:00

Communication availability: IRC/Mail/Skype/phone, anything will do

## Project abstract

Implementing a geometry engine from scratch involves a tremendous amount
of work. BRL-CAD's geometry kernel relies on the already existing
implementation that's found in the BRL-CAD binaries. After doing some
research through code, IRC and commit logs, my understanding is that the
existing code is written in 'OOP C' except for Nurbs which are already
written as OOP C++.

BRL-CAD's engine(core interface) already has several primitives
implemented, as well as database handling. My whole GSoC project is
split into two main parts. The main part is completing the primitives
list, Geometry engine tuning is something to be discussed and there's no
certain plan towards it, I will work on it only if the community decides
so.

### I) Geometry engine tuning

Right now, this is a generic part and there's no technical planning on
it.

### II) Enhancing geometry engine with additional primitives

With the increasing number of implemented primitives in core interface,
increases the usability and external development interest towards the
geometry engine. Primitives where chosen based on how important they are
and how difficult it is to implement them. The goal is to tackle as many
primitives as possible, starting with the easiest ones. Some items from
the list are rec, rcc, ellg, sph etc.

Project details & deliverables

I already have commit access, a somewhat decent understanding of BRL-CAD
concepts and where to look in the source code. This allows me to skip
the ‘obtaining commit access’ step.

## I) Geometry engine(core interface) tuning

Additional actions will be taken to facilitate API usage for
applications, I don't have a view on what type of applications use it
and what environment it is usually used under. This is a
generic(currently unknown) part of my proposal. It depends on what the
'easy-to-deploy' definition the mentor/community have. This part should
be finished before coding starts, or at worst a couple of weeks into
coding, if exceptional circumstances occur.

Deliverables: Undefined

## II) Enhancing geometry engine with additional primitives

# General OOP design aspects

All primitive classes will only inherit Object, regardless of
similarities between one another. For example, sph will not inherit
anything from ell although sph is a form of ell with additional
constraints.

The class design will be decided based on community feedback because, in
my opinion, I lack the experience to take the decision by myself, you
can, however, see my intended approach . Only after the class
interface(actually, abstract class, as C++ does not have an interface
keyword) has been sketched will I begin implementing it. This will be
done in an overlapping manner, testing class1 and designing class2 will
take place in the same period of time, to avoid coding downtime.

# Approach & Implementation plan

A general, natural approach is to take the structure members and convert
them to class members and the functions to methods. Obviously this will
not be a 1:1 transformation in all cases and code refactoring will
happen on the OOP end to avoid duplicated code, breaking OOP principles.
On short, the idea is to do cleanup when designing the class, so we
respect hacking as well as keep the code quality as high as possible.

Obviously, fields & constructors will be implemented first, then pairing
each method with a test, so I don't end up with a period when I have to
do only testing. Also, if I am stuck on a method, I could switch to
testing an already implemented one. I can't write this on the timeline
since I don't know the exact days, but the 'testing' period at the end
of each class is not meant to happen all after the class is fully
written. Another positive aspect of this idea is that it will keep me
from burning out or getting bored/frustrated with issues, since I can
bounce around to different types of activities.

# Primitives

Each of the below mentioned primitives exists in librt, has a well
defined behavior and structure. The idea is to adapt that behavior to a
class, taking the OOP concepts into consideration. Additionally, some
primitives have a more generic version already implemented (rcc has tgc
and sph has ell) so I will use that as a starting point.

The complete list, in chronological order is this : rcc,rec , ellg, sph,
sketch, vol, ars, extrude, bot, pipe and hrt.

If possible, the list will be discussed in the review period and changed
according to how the implementation is going and of mentors' view upon
it.

1\) rcc (right circular cylinder)

Rcc is a primitive that can be used to draw wheels, rods, posts. It is,
in fact, a special case of tgc and as such it's class design will mimic
the tgc with respect to the additional constraints. The main reason rcc
is the first one to be implemented is to practice class design on it.

Deliverables

\- fully functional rcc class with behavior similar to librt one

-tests(probably unit tests) for it

2\) rec( righ elliptical cylinder)

Similar to rcc, rec is a special case of tgc.

Deliverables

-fully functional rec class with behavior similar to librt one

-tests(probably unit tests) for it

3\) ellg

special case of ellipsoid, similar to sph it will mimic Ellipsoid
implementation.

Deliverables

-fully functional ellg class with behavior similar to librt one

-tests(probably unit tests) for it

4\) sph (optional, depending on progress)

similar to rcc – tgc situation, sph is, in fact, a special case of ell.

Deliverables

-fully functional rcc class, with behavior similar to librt one

-tests(probably unit tests) for it

5\) sketch

2D outline

Deliverables

-fully functional sketch class, with behavior similar to librt one

-tests(probably unit tests) for it

6\) vol

A voxel represents a value on a regular grid in three-dimensional space.
Voxel is a combination of "volume" and "pixel" where pixel is a
combination of "picture" and "element" (Wikipedia)

Deliverables

Functional voxelize algorithm

tests(probably unit tests) for it, perhaps other testing (i.e.
profiling)

7\) extrude

extrude face distance mged command; uses arb data, implementation might
differ from others.

Deliverables

-Extrude implementation

-Tests

8\) bot (bag of triangles)l

According to BRL-CAD wiki, The “Bag o’ Triangles” is a CAD primitive
object used for representing triangle mesh objects. BoT objects may be
surfaces or solids, topologically closed or open, clockwise or counter
clockwise.

Deliverables

-fully functional bot class, with behavior similar to librt one

-tests(probably unit tests) for it

9\) pipe

An interesting example of a pipe usage is generating a coil. I consider
that this primitive can be more challenging, so it has been added after
two were already implemented. Based on that, I should have a better
understanding of the process, as well as class design experience.

Deliverables

-fully functional pipe class, with behavior similar to librt one

-tests(probably unit tests) for it

10\) ars (arbitrary rectangular solid)

I decided to implement this primitive because, to me, it seems a very
usable primitive(because of the waterlines), it can be easily shaped
into many complicated forms. Having arb8 already implemented, I have an
example of a non-curvature shape primitive.

Deliverables

-fully functional ars class, with behavior similar to librt one

-tests(probably unit tests) for it

As you know, GSoC is flexible regarding project scope. If this proposed
project is under scoped, we will discuss additional classes to
implement. Similarly, if things take longer than expected due to
unforeseeable factors, primitives will be prioritized. If finished
early, hrt primitive will be implemented.

# Time availability & timeline

There will be work done between 21 March and 21 April, however, not 40
hours a week. This will be discussed in detail via IRC/mails. The
timeline assumes zero work is done until then. During coding period, the
standard 40 hours will be maintained, with the possibility to extend to
48 if there is need.

Each interval is to be read like this: \[Start, finish)

21st April –28th April

Discuss rec and rcc class design, begin basic class implementation

28th April – 5th May

Finish rec and rcc implementation; cleanup; testing; sph and ellg design
discussion;

5th May – 12th May

Sph & ellg implementation; cleanup; doc/testing;

12th May – 19th May

Univ Tests period, sketch design discussions. (probably 15-20h) basic
sketch implementation;

19th May - 26th May

Sketch implementation;

26th of May - 2nd June

Sketch cleanup/testing; vol implementation; extrude discussion

2nd June – 9th June

Extrude implementation

9th June – 16th June

Extrude cleanup/testing/doc; discussion of bot primitive;

16th June – 23rd June

Bot implementation;

23rd June – 30th June

Mid term; break; bot implementation; Limited availability (10 – 20
hours)

30th June - 7th July

Bot cleanup/testing; pipe discussion; sketching class, writing
constructors.

7th July – 14th of July

Pipe implementation;

7th July – 14th of July

finishing pipe implementation; pipe cleaup/testing; ars class discussion

14th of July – 21st July

Ars implementation;

21st of July – 28th July

Finish ars implementation; class testing and cleanup.

1st of August – 11th August

Finishing ars class(testing & cleanup), hrt design discussion

11th – 18th of August

Hrt implementation; clean up, writing doc, testing

The timeline will be adjusted upon discussions with mentors and based on
progress.

Motivation

# Why me?

You know a bit more about me than about newcomers so this question my
seem useless. My impression is that over time I’ve gotten the reputation
of an underachiever as I always start out strong and fall of some time
after. It’s happened with GCI 2014, last part of 2013 and a part of GSoC
2012.

Being honest, I think the best way to figure out if you should pick me
or not(aside the proposal, obviously) is to look at how the period until
taking decisions is spent. I can’t guarantee that I won’t “fall off
again”, but this time I am much more determined, as you will see below.

`         I’ve improved my general CS knowledge considerably from ago two years, that project was much more for me, than for the real benefit of BRL-CAD. I want to change that now,  I want this GSoC project to actually make a difference. So I/you could show the difference between the two projects. Actually, now, I am a bit surprised that I was accepted back then, but nevertheless that lead to this.`

`         Previously, I applied with two proposals, but not this year. My goal is not only to get accepted (as it was) but do this project, this is what I want to do and nothing else. If I don’t get selected, that’s alright, it can happen, but I want to work on this project and none other. I’m saying this because it’s a project that I find extremely interesting for many reasons: making the transition from procedural to OOP, designing classes when you don’t know the exact, full usage of your class, shaping geometry entities into objects.`

# Why BRL-CAD?

Initially, I tried other orgs because I was pursuing a C++ project that
involved compilers aswell( like llvm, lttng, gcc etc) so that’s why I
arrived a bit late around here.

As I am not an CAD expert (or avid user, even) I didn’t want to stay
here just cause it’s easier to get accepted(because I know the process,
what I have to do etc)

So far, I’ve just said why not BRL-CAD. My opinion is that CAD software
is one of the toughest categories of software there is, while I’m not
attracted that much to using it, I find it’s structure, constraints and
general concepts extremely interesting. I simply like how it works more
than what it does.

Another reason for this, except of the project(which I mentioned I’m
interested in probably around 7 times) is the community. For such a
small organization, there’s so much drive in the community (GCI, GSoC
etc), I got to know you folks and it would really be awesome to continue
working with you.

All in all, I believe this project would be a meaningful progress from
my first contact with BRL-CAD.

This is a long shot, but I’d love taking part as a GSoC mentor on the
follow-up of this project next year.