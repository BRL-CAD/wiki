<b>Name:</b> Priyanka Kapoor
<b>Email Address:</b> anjalicool.kapoor444@gmail.com
<b>IRC Username:</b> priyanka
<b>Brief Background Information:</b>
Final year B. Tech student of Information Technology at Guru Nanak Dev
Engineering College, Ludhiana, India.
Had worked on LibreCAD, BRL-CAD, C/C++ and Qt
<b>Phone number:</b> +91 988 890 3138

<b>Project Information</b>

<b>Project Title:</b> Multi-Naap Parser (Support for Multiple Measuring
Units)

<b>Brief Summary:</b> This project aims to make LibreCAD supportive for
various measuring system. In current status, LibreCAD draws entity in
only one unit. In proposed project, it will be able to take user input
for dimensions in the form of expression like one foot 12 inch. For
this, at back-end, whole expression will be parsed and interpreted and
then converted to unit used in LibreCAD.

<b>Detailed Description:</b>

<b>Approach:</b>

I will divide the project into two parts. Firstly GUI part that will
contain all necessary drop downs with various units as options to be
used by the user. Secondly coding part that will do pre-parsing,
interpreting and evaluating the expressions of mixed units and then
passing to mu-parser.

Detailed procedure is:

1\. Change the layout of dimension dialog box to add necessary drop
downs.
2. Making switch cases for various symbols used for specifying measuring
units.
3. Just like, if we have 1’ + 2”
4. Break the string by using arithmetic operators as delimiter and store
operator in stack. Now you find symbol of units by checking ASCII code
for that.
5. Compare ’ with foot symbol, if true, multiply the operand with 0.3048
(if unit used in LibreCAD is metre)
6. At end, apply all the operators stored on stack one by one on
consecutive last two operands and passing on to mu-parser for further
arithmetic evaluation.
<b>Development Schedule:</b>

Firstly reviewing the code of existing measuring units. Understanding
how the expressions are passed to mu-parser for evaluation. Then I will
design a pre-parser that would simplify the expression by converting
mixed units to single units and passing back to mu-parser. Then comes
the major part of optimizing the code and improving it to the fullest,
removing all warnings and bugs if any.

<b>Challenges:</b>

Need to discuss the flowchart of working of pre-parser. All its input,
processing and output.

<b>Milestones:</b>

<b>21 April - 19 May</b> Making work flow and to-do lists. Discussion
with Mentors.

<b>19 May - 23 June</b> Starting with coding part implementing various
symbols recognition, tyeing up with the factors to be multiplied with,
re-building the expression in one unit form and then passing to
mu-parser.

<b>24 June - 15 July:</b> Discussing with mentors any error, wrong track
if any. Unit testing the code.

<b>16 July - 23 July:</b> Pushing the changes to LibreCAD for user
testing and evaluations.

<b>24 July - 25 July:</b> Back up days, for any backlogs or pending
tasks.

<b>26 July - 29 July:</b> Any pending tasks. Final go through, and
preparation for final evaluation.

<b>3 August – 9 August:</b> Fixing bugs, implementing suggested changes,
testing.

<b>9 August – 12 August </b> Starting documentation (using LaTeX or any
other tool recommended) including developers documentation, user’s
documentation.

<b>Future work/Scope (Post GSoC):</b>

Making it more precise in floating point conversions. It can be extended
to much more units. We can make LibreCAD's own parser for evaluating
mathematical expressions.

<b>Time Availability:</b>

I will be available 35 hours/week, if needed can spend more. No
restriction of time.

<b>Why LibreCAD?</b>

LibreCAD is in C++ and Qt which is a source of attraction for me.
Moreover LibreCAD code is much more easy to understand and Mentors are
much more supportive and helpful. LibreCAD is doing wonders in 2-D CAD.
Its much demandable especially for mechanical and civil. Being a
Software Engineer, it would be great to help/contribute this software so
that it flourish more and more.

<b>Why me?</b>

Programming is my passion. I have good knowledge of C++ and I love maths
too. Moreover its my dream to get involve in Google Summer Of Code.
Working for my dream would be a much enjoyful and enthusiastic for me.
It would be great to interact and work under superior mentors. I will
work hard and will surely complete the project under the super guidance
of LibreCAD mentors.