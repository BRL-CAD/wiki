# Project title

Code Reduction

# Brief summary

BRL-CAD has the really huge project. There are a lot of libraries and
different files, so there is such problem as code duplication. The
sources must be cleaner and smaller. The code must be easy to read and
understandable. This reduction will help new developers to make their
work more effective and faster. So, the main aim is to shorten the count
of lines of code without disrupting the project. Special tests will help
not to disrupt the project after reduction.

# Detailed description

I decided to choose this project, because, I am sure, I have enough
knowledge in c/c++ for doing it. I've been working with it since
19.03.2012. Unfortunately, I have a lot of subjects (about 12) this
year, so I don't have enough time for working with BRL-CAD and patches
every day now. Nevertheless, after the 1-5 of May I will be absolutely
free and ready to work hard.

## Proposes for reduction

BRL-CAD has quite useful Virtual Machine, which helped me to do my first
steps with it. Mentor Sean helped me to become quite familiar with it.
After several tests with "Simian" I understood that the work for
reduction will be really huge. There are a lot of duplications (e.g.
just copy-pasts). After testing I can propose such ideas:

-   Duplication in one file.

Example:

................

`if (!invert) {   `
`   for (line = file_height-1; line >= 0; line--) {      `
`      unsigned char *op;        `
`      vp = &vert_buf[line*3];      `
`      op = &horiz_buf[(file_width*3)-1];`
`      while (op > horiz_buf) {`
`         *op-- = vp[2];`
`         *op-- = vp[1];`
`         *op-- = *vp;`
`      }`
`      ret = write(1, horiz_buf, file_width*3);`
`      if (ret < 0)`
`          perror("write");`
`   }`
`} else {`
`/* Inverted: top-to-bottom. Good with cat-fb */`
`   for (line=0; line < file_height; line++) {`
`      unsigned char *op;        `
`      vp = &vert_buf[line*3];      `
`      op = &horiz_buf[(file_width*3)-1];`
`      while (op > horiz_buf) {`
`         *op-- = vp[2];`
`         *op-- = vp[1];`
`         *op-- = *vp;`
`      }`
`      ret = write(1, horiz_buf, file_width*3);`
`      if (ret < 0)`
`          perror("write");`
`   }`
`}`

..................

This part is situated in file src/util/picbackgnd.c. We can see that the
code in the first "for" is the same as in the second. So I propose to
write the function with all necessary parameters which will contain this
code:

`void`
`my_reduction (unsigned char *horiz_buf, unsigned char *vert_buf, unsigned char *vp, ssize_t ret, int line)`
`{`
`    unsigned char *op;`
`    vp = &vert_buf[line*3];`
`    op = &horiz_buf[(file_width*3)-1];`
`    while (op > horiz_buf) {`
`       *op-- = vp[2];`
`       *op-- = vp[1];`
`       *op-- = *vp;`
`    }`
`    ret = write(1, horiz_buf, file_width*3);`
`    if (ret < 0)`
`       perror("write");`
`}`

The function call will have such view:

..................

` if (!invert) {`
`    for (line = file_height-1; line >= 0; line--) `
`        my_reduction(horiz_buf, vert_buf, vp, ret, line);`
` } else {`
`    for (line=0; line < file_height; line++) `
`        my_reduction(horiz_buf, vert_buf, vp, ret, line);`
` } `

.................

We can see that the code would be more understandable and short

-   Duplication in one directory but different files

In such situation I suggest to make file like "utils.c" which would be
common for this directory. I have already done the patch for such
situation: [my first
patch](http://sourceforge.net/tracker/?func=detail&aid=3512039&group_id=105292&atid=640804)

-   Duplication in different directories

Such duplication must be the most careful and difficult, because every
change can influence working the whole project. Common functions will be
situated in the libraries.

## Tests and patches

I am sure, it is necessary to make tests as much as possible to avoid
mistakes or to find them before big changes. I think that simple unit
tests would be the best way in this situation.

As for patches, I think, they must be doing very often during the whole
period of working for the same reason as tests.

## Simian

I think the tool "Simian" is really useful and easy in use. Also it
works rather fast. If I am involved into this project I want to use it
specifically. But, of course, if my mentor advises me something else, I
will improve my skills in other tool

# Deliverables

The main expectation is much clearer code with much fewer lines with no
bugs or errors after reduction. My personal aim is getting useful
experience and knowledge which could help me in my future and, maybe,
would give me a chance to work with this company even after this project

# Development schedule

-   before 23.04 - continuing to get familiar with project
-   23.04 - 21.05 - active communication with mentor(s), asking
    questions, getting ready for start
-   21.05 - 15.06 - coding. Complete reduction of the duplications that
    take place in one file.
-   15.06 - 3.07 - Reduction of as large as possible number of files
    that contains duplications (duplications in different files, the
    same directory). Writing some tests
-   3.07 - 9.07 - bugs fixing, review to be ready for submitting
-   9.07 - 13.07 - submitting, some more review if it is necessary
-   13.07 - 23.07 - reduction of the reminder of duplication in
    different files and tests.
-   23.07 - 13.08 - coding the last part of the project, removing
    duplications in files that contains in different directories, making
    necessary tests and libraries.
-   13.08 - 20.08 - bugs fixing, review to be ready for submitting the
    final result

# Time availability

I will not have any other jobs or project during participation in the
project. My exams ends on the 18th of May because of EURO-2012, so I
will have a lot of free time. All trips or vocations I am going to have
in the end of August (after GSoC). I am going to work almost every day
(6 days per week; not 7 - because, I am sure, every person must have a
weekend for effective working) and 8 hours per day (for example: 8-00 -
14-00 and 19-00 - 21-00). If it is necessary for me to go somewhere
during working on the project, I will work longer and harder before it
to compensate this time.

# Why BRL-CAD

Recently, I have started being interested in computer graphic and
modeling, so I would like to improve my skills with the help of this
company. But I am not so good at these things yet, so I decided to try
to take part in the project where my skills are better. Also it is
really pleasantly that I always get sensible answers from mentor (Sean
Morrison) for my questions. All the responses are totally complete. It
seems people are interested in success of their project, therefore,
there is also a moral reason of my desire to work with BRL-CAD.

# Why me

I would not like to tell that I am "excellent" programmer or something
like that. I want only to say that I am ready to work hard and to study
new important knowledge. And I hope, BRL-CAD will help me with it.
Studying and getting experience are on the first place of this period of
my life.