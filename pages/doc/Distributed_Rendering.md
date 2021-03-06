[category:tutorials](category:tutorials.md)

## Distributed Rendering

In order to create a distributed render across many machines using
BRL-CAD, one first needs a 'host' that will serve as the rally point to
where all rendering machines will go to get information needed for the
render.

Typically the host machine would have all the information needed in
order to carry out the distributed render however, that currently
doesn't work right now.

For the moment, all machines must have a copy of the information needed
for a render to be completed. So for example:

'Server' is the host machine in which all computers will report to in
order to get their jobs, and return their jobs to. 'comp1' and 'comp2'
are machines that will connect to 'Server' in order to carry out the
rendering job.

So in order for the whole process to get started, one would have to
access 'Server' and run the remrt command.

For Example:

`$ remrt -s100 Picture.g objects.c`

or: remrt (- options) (.g file) (.c objects in .g file)

would start a server that is going to render a 100 x 100 picture using
geometry from Picture.g with objects.c loaded.

Then for comp1 and comp2 you would run:

`$ rtsrv Server 4446`

or: rtsrv (server's name) (listening port, which defaults to 4446)

to connect to Server, and begin the rendering job. 'Server' will assign
work to 'comp1' and 'comp2' and they will start rendering their lines
for the picture. Typically the workload is that each connected computer
will render a single line of the picture, so comp1 will render the first
line, and comp 2 will render the second, and will continue rendering
until all lines are processed.

The final rendered picture is located on 'Server' in the .pix format.

------------------------------------------------------------------------

## Advanced Commands

*HOWEVER*, this all is pie-in-the-sky simplicity and in reality much
more work has to been done in order for proper distributed rendering to
occur.

Currently, remrt needs many extra values given to it in order for it to
work correctly. This line is an example of the actual information needed
in order for a proper server to be set up:

`$ remrt -M -s4096 -p65 -o Output.pix shape.g object.c 2>> Log.log <`<EOF
 >` viewsize 1.298471982398`
`> orientation 1.1238190283 2.39028130938 3.0129381098309 4.120938019823`
`> eye_pt 2.192310238018 3.120398109283098 4.108312083108`
`> start 0; clean;`
`> end;`
`> EOF`

And the rtsrv has to be run like this:

`$ rtsrv -d Server 4446`

And that will connect your current computer to the server to start
rendering the picture.

One important thing to remember is the .remtrc file, placed on the
server, which holds information on which rendering computers do what and
when.

.remtrc

`host computer1.brlcad.org always cd /tmp`
`host computer2.brlcad.org always cd /geometry`
`host busyserver.brlcad.org night cd /tmp`

This shows 3 computers that will be used in the render, computer1 and
computer2 will render 'always' in their respective directories where the
geometry is, and busyserver will only render at 'night' (6pm - 8am),
keeping busyserver from becoming even more busy during normal working
hours.
