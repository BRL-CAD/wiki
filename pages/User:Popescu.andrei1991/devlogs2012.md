## Personal Info

Hello, my name is Andrei - Constantin Popescu, I usually go by Andrei. I
am a second year undergraduate at Polytechnic University of
Bucharest,studying at the computer science department.

## Contact

I can usually be found on IRC on \#brlcad - freenode, I have various
nicknames, depending on availablity : andrei, andrei_, andrei__. The
quickest way to reach me on e-mail is the address:
popescu.andrei1991@gmail.com - I read emails on this several times a
day. My github account is : <https://github.com/pandrei>

I will use this page to keep track of my progress on a daily basis.

## Project Summary

Firstly, here can be found my official proposal.
<https://google-melange.appspot.com/gsoc/proposal/review/google/gsoc2012/popescuandrei/4002>

The purpose of a package managing library ( or tool) is to pass around
packages containing data from brlcad tools. The packages are sent via
TCP and as a result are using TCP header. TCP --
<http://en.wikipedia.org/wiki/Transmission_Control_Protocol>

My current knowledge is that the TCP Payload\[1\] has a size of 64kb, at
least in the linux kernel. There has been a reported incident where
libpkg fails to send 24k+ packages. \[1\] Payload - TCP field
containinig effective data (user data, for example).

I believe this is the reported incident :
<http://permalink.gmane.org/gmane.comp.cad.brlcad.devel/959>.

Tpkg will be used for testing the package issue. I am currently
researching dstat and ifstat, found via apt-cache search ifstat dstat -
versatile resource statistics tool ifstat - InterFace STATistics
Monitoring

The curent state of brlcad libpkg is a basic client-server protocol.

## GsoC 2012 progress

So far I have managed to compile and install brl-cad on a 32-bit
Archlinux. I am focusing on the tpkg command to see what exactly happens
and properly submitting the global removal patch.

Tests have been run 3D version on a remote machine. The graphics are
present on here on the log. However, after more discussion it was
decided there is too much noise in 3d mesh.

Currently, tests have been performed for package size from 2048 to
4194304 ( 2048 ^ 2 ). Tests have been performed on a 8M file. This is
the graphic obtained by testing : <http://i.imgur.com/H5Q2u.jpg>

TODO : add some github link with files and numerical values.

There is a second test, running package size from 1 to 2048 on a 8M
test. It has not finished at the moment of writing. However, a graph was
drawn with some partial data ( 1 - 95 package size ). It's correctness
needs to be checked but it does seem to look like an exponential curve.

TODO : add details and graphics when the script finishes.

I m currently working on fixing the unit test.

## Performance measuring

The 3d graphics have finished.

File size increase as powers of two series from 1 to 8MB

Package size 1 - 2048

<http://i.imgur.com/OPum5.png>

Package size 2048 - 4194304

<http://i.imgur.com/fH4rL.png>

Package size 1 - 4194304

<http://i.imgur.com/AXUpN.png>

After converting data into CSV format and using GNU plot I have obtained
the following graphics :

1 - 2048 : <http://i.imgur.com/tnWAa.png>

2048 - 4194304 : <http://i.imgur.com/isNXL.png>

Currently I m working to see if I can combine the two files. From what I
read so far this seems rather complicated.

## Daily development log

## Weeks 1 - 3

21th May - 8th of June - exams period, minor work on tpkg patch and on
the red - black tree test unit.

9th June - working on obtaining commit access asap. Currently developing
the performance shell script.

10-11th June - not much work , documenting regarding bash programming.

## Week 4

12-13th June -finishing the shell script, applying feedback given by
Erik on the tpkg parameter patch.

14th June - submitting the final version of the shell script.

15-17th of June - learning K&R indentation, learning about POSIX.
Finishing the tpkg script and the tpkg.c modifications.

18th of June - unsuccesful attempts to sync the server and client ( To
start the client only after server started) using signal handling,
docummenting about signal handling

19th of June - unsuccesful attempts to achieve the above by using
inter-process communications, understanding thread concepts,
docummenting about the basics of fork() , pthreads_

## Week 5

20th of June - sync the server with the client by using a loop to detect
a key string (while "Server_ready" isn't found in the log_file the
client does not start. Having issues with redirecting output from a
background process

21st of June - finished tpkg script for localhost ( both client and
server are on the same machine), developing the remote one. (Using two
different machines)

22nd of June - getting some hints from \#bash, reading about ssh,
working on the ssh remote script(password-less ssh login process).
Having issues with the ssh session not exiting properly.

23rd of June - script finished, full functional started script on two
machines setting up log files / reading a bit about sampling necessary
for graphic( how many points are enough )

24th - 25th of June - scripts running time, realized I could have done
them a lot better and faster. No notable work done in these days. ( a
script using small files ran twice and one using large files( up to 700
mb ) ran once.

26th of June the total dimension for the log files was 8.4Gb on server
machine as well as on client ( minor difference) purging the files from
irrelevant data. read about sed and awk. Compared the first two tests(
which use identical parameters) and found no notable difference.
Starting to read about and write the octave script. Reading about
interpolation and how can I use it if I don t know what points am I
missing.

27th of June - asked for some mathematical hints on \#octave - freenode.
Finished graphs currently without interpolation. Looking up bu_bomb.log
but they are empty. Re-run the script for a small number of iterations
still found no error.

## Week 6

28th of June - uploaded data. upated logs.

29th of June - Reading about google test, planning on what testing
framework to use for libpkg client - server.

30th of June - still stuck with the OOP from google test.

1st of July - learning / understanding how to use google test for this
was taking too long, finding another way.

2nd of July - initially created the unit test as a shell, after further
digging, decided to change the plan and make it a .c unit test.

3rd of July - finished unit testing. uploaded unit test on sourceforge.

4th of July - minor work, mostly look up things I already did and see
where and what I can improve.

## Week 7

5th of July - Issue with wallclock, script was modified to counter the
wallclock instability. Single variable tests were run.

6th of July - issues with the script, for some reason ssh was not
working. Adjusting that. Finished all the issues with the scripts /
tpkg. Started 2d graphics ( 1 - 2048 ) and ( 2048 -&gt; 2048^2).

7th of July - 2048 -&gt; 2048^2 testing finished, graph drawn. Minor
analysis on it. Drawn a graph with the partial data from 1 - 2048 one,
does seem incorrect. Will be reworked.

8th of July - Restarted 1 - 2048 test. Discussing further tests and how
I should proceed. Minor reading about unit tests in networking

9th of July - Scripts still running, wrote unit test. Received feedback
started applying it. Monitoring the values obtained from the tests. The
" 3D graphic " test failed ( script execution ended ). It was an script
error not a tpkg error. Fixed it and resumed tests.

10th of July - working on the test unit, running tests.

11th of July - Graphed the results of one test

## Week 8

12th of July - discovered an error in testing. Previously calculated
average was taken into consideration when it should have not, restarted
scripts. Got two more machines ( installing archlinux + brlcad on them )

13th of July - fixing HACKING issues on previous patches. Providing
1-2048 Graph.

14th - 15th of July - minor work, waiting for tests mainly.

16th of July - finished tests, graphed results. TODO:// Complete with
rest

17th of July - obtain data in CSV format, attempt to check scripts
correctness, minor reasearch about gnuplot

18th of July - plotting data in a single file, taking a look into pkg.c
and pkg.h to decide what unit tests to write

## Week 9

19th of July - didn't manage to work anything at all, had
somehardware(hdd)failure, reinstalled OS.

20th of July - started working on test_pkg_permserver, some
documentation regarding unit tests.

21th of July - finished test_pkg_permserver, minor HACKING reedit,
started working on test_pkg_getclient.

22th of July - trying to solve issues with blocking calls. Document
about potential solutions such as threading / signal handling or select
()

23th of July - abandoned test_pkg_getclient for the moment, moving to
test_pkg_open, had some issues. Pkg_open was not exiting correctly.

24th of July - finished test_pkg_open. Moved to test_pkg_stream,
almost finished but there are some issues with the structure of the
test. ( checking only pkg_conn header)

25th of July - Clean-up on the current test units, searching for other
potential candidates. Taking a look into pkg_send and pkg_send2.

## Week 10

26th of July - asked for guidance on IRC, uploaded on sourceforge.

27th of July - None

28th of July - still searching for methods to escape a blocking call,
none found using stdout as file descriptor. finished writing
test_pkg_getclient

29th of July - fixing indent issues and such on test_pkg_getclient,
started working on test_pkg_stream. finished coding test_pkg_stream.

30th of July - fixing minor issues with test_pkg_stream. started
working on test_pkg_flush. Finished working on test_pkg_flush( tho
there are some issues)

31st of July - started working on pkg_block and pkg_suckin,
investigating some issues regarding pkg_conn

1st of August - finished pkg_block / pkg_suckin, checking out
contributor quickies in order to obtain commit access

## Week 11

2nd of August - done test_pkg_close and started working on
test_pkg_waitfor

3rd of August - finished working test_pkg_waitfor. reading
/understanding pkg_send.

4th of August - worked on test_pkg_send. Finished it. Minor work on
pkg_2send.

5th of August - finished working on pkg_2send.

6th of August - taking a look into pkg_bwaitfor, no other work done.

7th of August - started working on pkg_bwaitfor, finished it. however
still some minor issues with it

## Week 12

8th of August - None

9th of August - Minor programming issues. None other

10th of August - read pkg.c code, attempted to fix fail cases discovered
in unit tests.

11th of August - continued to work on fixing fail cases ( difficulty in
finding out which ones are legit and which ones I should fix ) PKG_CK
for example, aborts execution.

12th of August - cleaning up unit tests, making them ready for upload

13th of August - Converting tests into patch format and uploading them ,
fixed some more fail cases, adjusting code.

14th of August - issues with a segmentation fault in pkg.c code, working
on fixing it.

## Week 13