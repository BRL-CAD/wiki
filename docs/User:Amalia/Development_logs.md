# Introductions

This page is a diary dedicated to the work I have been honored to do
with LibreCAD this Google Summer of Code 2015 period.

## COMMUNITY BONDING PERIOD

# Community Bonding Week 1

-   Celebrated my acceptance into Google Summer of Code 2015 with my
    friends at the Limbe Semme beach

<!-- -->

-   Getting to know other students in Buea selected for GSoC.

<!-- -->

-   Updated my repository on
    [github](https://github.com/Ngassa/LibreCAD).

# Community Bonding Week 2

-   Filled Student Foreign Certification Tax Form

<!-- -->

-   Discussed with my mentors the possibility of a wire transfer for
    work during the bonding period. No channels were open apart from
    Paypal.

<!-- -->

-   Updated my repository on
    [github](https://github.com/Ngassa/LibreCAD)

# Community Bonding Week 3

-   Looked at the lc_splinepoints code in
    librecad/src/lib/engine/lc_splinepoints.\*

<!-- -->

-   Worked feverishly and biased my efforts on my final year Management
    project ( meetings with supervisor, Writing Theoretical and
    Literature review, conceiving and administering questionnaires, etc
    ) which ate up the next fortnight.

<!-- -->

-   The intention was to go furthest as possible with Final year School
    Project so that when GSoC coding begins, I can concentrate more on
    my LibreCAD project.

# Community Bonding Week 4

-   Discovered a Paypal account at the end of the Community bonding
    period.

## CODING PERIOD

# Week One

# Monday May 25th

-   Had a meeting with Women Techmakers Arm of GDG Buea organizing
    upcoming [Google I/0 Extended
    2015](https://plus.google.com/u/0/events/cdl24bk07spiac2o2fduaan9d24)
    at my University.

<!-- -->

-   Reading Documentation on [Conics Sections in
    LibreCAD](https://drive.google.com/file/d/0B-pwKjF4CzPzc3UzZlFnNEtiWDQ/view?usp=sharing)
    given to me by my mentor Dongxu Li.

# Week Two

# Thursday June 4th

-   Hurray! My Google Summer of Code finally package arrived my
    University today and I was called to come and collect it.

# Friday June 5th

-   Had a meeting with the Mentor for Google Developer Groups in
    Cameroon. He cautioned me on the importance of communication and
    daily coding on my project.

<!-- -->

-   Almost done with my Final year Research Project.Was working on
    corrections given by my supervisor the whole day.

# Saturday June 6th

-   Updated my github repository today.

# Week 3

# Monday June 8th

-   Synced my github [repository](https://github.com/Ngassa/LibreCAD)
    with LibreCAD's.

<!-- -->

-   Installed and ran LibreCAD from source.

<!-- -->

-   Studying RS_Ellipse::getTangentPoint() and
    LC_SplinePoints::getTangentPoint() to help create
    RS_Hyperbola::getTangentPoint().

# Tuesday June 9th

-   Hyperbolas are unbounded and disconnected too. Investigating how
    finding the tangential points of splines can help the case of
    hyperbolas.

<!-- -->

-   Read articles by www.qcad.org on
    [splines](http://www.qcad.org/doc/qcad/3.1.0/reference/en/scripts/Draw/Spline/SplineControlPoints/doc/SplineControlPoints_en.html).
    Each branch or arm of a hyperbola can be seen as an open quadratic
    spline.

# Wednesday June 10th

-   Discussed with my mentor in IRC today and he gave me [wiki
    link](http://wiki.librecad.org/index.php/LibreCAD_users_Manual) for
    LibreCAD.

# Thursday June 11th

-   Re-established contact with my co-mentor Ries.

<!-- -->

-   Discussed with mentor dli_ on \#librecad.

<!-- -->

-   Understood what class RS_VectorSolutions is.

<!-- -->

-   Working on [math algorithm](https://paste.kde.org/pir5jd87w) for
    finding tangential points from a given point outside a hyperbola.

# Friday June 12th

-   Awaiting mentors' response to my question on IRC channel on [math
    algorithm](https://paste.kde.org/pir5jd87w).

<!-- -->

-   Using calculus to solve the above math problem. It's quite
    cumbersome and I'm having a hard time.

# Saturday June 13th

-   Continued work on cumbersome algebra and calculus on tangential
    points to the hyperbola. I'm excited that my thinking was the same
    as
    [this](http://math.stackexchange.com/questions/214977/general-equation-of-a-tangent-line-to-a-hyperbola?rq=1)
    except that my hyperbola is centered at (xo,yo) rather than (0,0).

<!-- -->

-   Succeeded to have a general formula to obtain the intersection point
    (h,k) of the tangent line and the hyperbola. That was quite tedious.

<!-- -->

-   My mentor asks for Proof of concept code on a daily basis.

<!-- -->

-   Next task is implementing the math algorithm which I developed.

# Week 4

# Monday June 15th

-   Discussed my math algorithm with my mentor dli on \#librecad.

<!-- -->

-   Started doing some [minor changes](http://pastebin.com/TmWXQhEh) to
    my LibreCAD [repository](http://pastebin.com/x3tBUBw6) today.

# Tuesday June 16th

-   Today I had my final year project defense in school.Thus, I couldn't
    do any work on GSoC LibreCAD project today.

# Thursday June 18th

-   Studying lc_splinepoints code to finish writing the getTangentPoint
    of a hyperbola

# Friday June 19th

-   Developed a heuristic to solve the getTangentPoint() of a hyperbola.

<!-- -->

-   Emailed the [paste](https://paste.kde.org/p9sw0q6lb) to my mentors
    for review.

# Saturday June 20th

-   Awaiting my mentors review of the heuristic before proceeding.

<!-- -->

-   Attended the Silicon Mountain Conference today.

# Week 5

# Sunday June 21st

-   Adjusting the getTangentialPoints() algorithm for a unit hyperbola
    based on my mentor's corrections.

# Monday June 22nd

-   Sent [adjustments](https://paste.kde.org/px1krxfhc) to
    getTangentpoint() member function algorithm over to my mentor for
    review.

<!-- -->

-   Been having discussions with my mentor on code snippets like
    [this](https://paste.kde.org/pa1axlysg). Hustling towards a working
    prototype.

<!-- -->

-   Showed my mentor some [code
    snippets](https://paste.kde.org/pzvmlq1yc) that compile today.

# Tuesday June 23rd

-   My mentor gave feedback and corrections to the code snippet I
    tunrned in yesterday.

<!-- -->

-   Have done some [corrections](https://paste.kde.org/pxz2wpd9o) to the
    code snippet.

<!-- -->

-   My mentor proposed a much more concise and [maintainable
    algorithm](http://www.texpaste.com/n/u6dkvzc0) which I'm
    incorporating into the Hyperbola code.

<!-- -->

-   LibreCAD Build is [broken](https://paste.kde.org/pnpgabtyj).
    Downloading Qt5 to run LibreCAD with while Lead developers fix this
    issue.

# Wednesday June 24th

-   Upgraded to qmake-qt5, updated my LibreCAD repository and build it.

<!-- -->

-   Awaiting review from my mentor for the
    [improved](https://paste.kde.org/pq37vefit) the code snippet.

# Thursday June 25th

-   Did not do any work today due to housekeeping.

# Friday June 26th

-   More critique on code from my mentor.

<!-- -->

-   Improved [code](https://paste.kde.org/pq4vt14lx) based on
    corrections discussed on IRC.

<!-- -->

-   Chatted a little with brlcad on \#brlcad and ries on \#librecad
    today.

# Saturday June 27th

-   Today was a lazy day for me. Did not code.

# Mid-term Evaluation Week(Week 6 )

# Monday June 29th

-   After a deeper look at my logic of getTangentPoint(), I overhauled
    my code to have [this](https://paste.kde.org/pkt2o2ifh).

<!-- -->

-   My mentor has confirmed that my logic is a step int the right
    direction and has suggested that I use github and email more
    including IM/IRC.

<!-- -->

-   Starting to design unit tests for this getTangentPoint() function.

# Tuesday June 30th

-   Filled Student evaluation form today.

<!-- -->

-   Working on unit test for getTangentPoint() member function.

<!-- -->

-   Some work in progress available
    [here](https://paste.kde.org/pvnynjgvt)

# Wednesday July 1st

-   Sick day:I have not been able to do any work because of the symptoms
    of malaria I've been experiencing since morning.

<!-- -->

-   I've developed the unit tests for the getTangentPoint() in
    librecad/src/main.cpp and LibreCAD builds well.

<!-- -->

-   Next step is running the code to see the results from the function.

# PRE MIDTERM EVALUATION SUMMARY

I was rather off to a slow start for GSoC 2015 coding due to my final
year management project. However, I've written the getTangentPoint()
member function for the LC_Hyperbola and I am currently designing
appropriate test cases to ascertain the effectiveness of
getTangentPoint() function. When I've perfected these test cases, anyone
will be able to run these tests after compiling LibreCAD by ./lc on the
command line in the unix/ directory.

# Thursday July 2nd

-   Sick day: Have not done any work today. Currently on medications.

<!-- -->

-   Managed to post my pre midterm evaluation summary to my development
    logs, BRL-CAD mailing list and cc'ing my mentors in LibreCAD and
    BRL-CAD.

<!-- -->

-   Updated my LibreCAD
    [repositories](https://github.com/Ngassa/LibreCAD) too.

# Friday July 3rd

-   Sick day: Haven't been able to do any work due to illness.