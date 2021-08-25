\- Title: Massive Code Reduction - -- Personal Information -- -- Brief
Background info -- -- Brief summary -- -- Detailed project Description
-- -- What else I plan on doing -- -- Deliverables -- -- Timeline -- --
Availability -- -- Why us -- -- Why me -- -- Anything else --

\- Title: Massive Code Reduction - -- Personal information --

`  Name (in full): Nde Wisdom Nji`
`  E-mail address: wisdomnji@gmail.com`
`  IRC username: Sherl0ck`

-- Brief Background info --

`  I'm a freshman at the Catholic University of Bamenda (CATUC), studying Computer science. I've had 3 years of coding experience and have participated in some major codes development for my school and organizations in my vicinity.`
`   I'm proficient in c/c++ and Java (I also do some preliminary work in python and just begin working on some c#).`

--Brief summary --

As it's stated on the wiki, this project entails identifying common
patterns of duplication throughout the code, but with a method I call
"Massive Code Reduction (MCR)", I plan on utilizing for optimum
refactoring.

-- Detailed Project Description --

I plan on working on not only reducing the codes, but on also taking out
un-used variables and "recycling" some variables, with great accuracy
and optimization, while mantaining optimum functionality. As stated in
the wiki, tools are already at the availability for such task (problem
is such tools might be general purpose tools and constructed for general
programming), but I propose on developing my own tools specific for the
BRL-CAD framework codes. How would my own tool be better you might ask;
the answer is pretty simple, I'd spend a considerable amount of time,
recoginizing the unique pattern/format used in the codes of BRL-CAD and
formulate a standard algorithm. With that, I can implement my massive
code reduction technique on the my algorithm and behold would be BRL-CAD
refactoring tool.

How I plan to do that:

`- Templates: For source files which are almost doubled but just maintain differences in their data types, implementating a standard template for that would utilize not only the lines of codes, but amount of source files itself.`
`- Functions: Eliminate every trace of reoccuring code, using functions, in source files.`

`So my plan of action is: Templates, for reducing source files and functions, for reducing lines of code. Now every other refactoring would be variable allocation and common programming styles.`

`e.g `
`//reading from a file....`
`ifstream read("myfile.txt");`
`string temp;`
`read >> temp;`
`bool flag = false;`
`while(flag == false)`
`{`
`   read >> temp;`
`   if(temp.empty() == true) flag = true;`
`}`

but this could be reduced to...

`   ifstream read("myfile.txt")`
`   while(read.eof() == false)`
`   {`
`       string temp;`
`       read >> temp;`
`   }`

The above is just a dummy example of line reduction, which leaves space
for more accurate checking! Due to long hours dedicated to finding code
bugs and resizing code to optimize memory usage, I'm confident to say,
BRL-CAD would be an awesome project to utilize the skills.

-- What else I plan on doing -- Since making the refactoring won't take
in lots of hours, I would optimize the remaining time for testing! To
make sure the code is optimum for use on the BRL-CAD. As I always say,
testing with the worst case scenerio makes the normal case scenerio
accurate! Reading and writing is optimum for this project, not just
pouring hours of coding to develop generalized tools! I'm very skilled
at both and propose my skills be utilized for this project.

-- Deliverables --

-- Timeline --

May 25th to June 1st:

`   - Extensive study of BRL-CAD code formats (Beginning of research phase).`

June 2nd to June 7th:

`   - Development and Coding of MCR`

June 8th to June 15th:

`   - Finalization of MCR and testing on BRL-CAD framework begins.`

June 16th to June 20th:

`   - Testing of code on BRL-CAD framework and debugging of MCR`

June 21th to June 25th:

`   - Uploading of code for standard review.`

June 26th to July 6th:

`   - Creating documentation for first phase of code.`

July 7th to July 14th:

`   - Further extensive research on BRL-CAD code to build on already collected data.`
`   - Development further advanced algorithm`
`   - Test algorithm`

July 15th to July 21st:

`   - Coding of newly developed algorithm.`
`   - Standard testing begins`

July 22nd to July 29th:

`   - Finalize codes and begin full test of code on BRL-CAD framework.`
`   - Focus on amount of refactoring is taken place.`
`   - Test for maintainability of refactored codes.`

July 30th to August 4th:

`   - Final cleaning up.`
`   - Creation of final documentations and wikis`

August 5th:

`   - Submission of work`
`   - Sitting back to hope for the best!`

-- Time availability for each project --

7 hours Mon - Fri 3 hours Weekends. Total of 55 hours per week.

-- Why us -- BRL-CAD has a massive framework of source codes, as the
developing team is huge. Factoring code for such such an organization
would boost my motivation and I'll finally have a contribution to the
open-souce community (BRL-CAD for that matter).

-- Why me -- I'm very skilled at reading, writing, and developing
algorithms and codes. This project isn't technically difficult, but
requires a great deal of time input and motivation. Most programmers
prefer developing the testing, that's why after a few weeks of coding,
they loss motivation, but I'm dedicated to testing and developing (the
science spirit), which means the more I work on refactoring for the
BRL-CAD, the more motivated I'll become to not give up. My skill would
be of great use to the team.

-- Anything else -- From the dates stated till September, I'll have no
engagements and as such would dedicate my time to working on the BRL-CAD
project, and do some xbox gaming on Sundays!