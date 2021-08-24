## Who I am

My name is Brandon Hinesley. I'm a 27 year old, unemployed, full-time
student in my junior year of a Bachelor of Science in Computer Science.
I live in Bakersfield, CA. My preferred coding environment is in any
\*nix operating system, while using Vim and screen/tmux.

## Contact

-   IRC nick: bhinesley
-   email: [bhinesley@gmail.com](mailto:bhinesley+brlcad@gmail.com)

## Experience

I participated in [GSoC 2011 with
BRL-CAD](#GSoC_2011_Project "wikilink"), under Cliff, my official
mentor. I have 5 years of experience designing [commercial plumbing
systems in
3d](https://picasaweb.google.com/lh/photo/_dWpWLr1esGb16X7_4DlNHMyrgI048JfNwPx7Dl9cn0?feat=directlink),
using AutoCAD. I've also [fooled
around](https://picasaweb.google.com/lh/photo/uy-_CFMyTMVmso32iUyjV9MTjNZETYmyPJy0liipFm0?feat=directlink)
a
[bit](https://picasaweb.google.com/lh/photo/HAuEHnoczzi-NEM0Gs5fM9MTjNZETYmyPJy0liipFm0?feat=directlink)
in
[Blender](https://picasaweb.google.com/lh/photo/RtLNLlTFSzjZHFWkb3lbZtMTjNZETYmyPJy0liipFm0?feat=directlink).
I have experience in C/C++, and Tcl/Tk/Itcl/Itk. For 3 years I was a
system administrator for a Linux/Windows based small business network.

## GSoC 2011 Project

See the [log and timeline](User:Bhinesley/gsoc2011 "wikilink") or the
[official GSoC project
summary](http://www.google-melange.com/gsoc/project/google/gsoc2011/bhinesley/1000)
for details. I migrated MGED commands to Archer/libged, and cleaned up
existing commands. Later in the program, my focus shifted towards adding
new capabilities to the libged oed commands, rather than simply
migrating them.

## GSoC 2012 Project

See my [GSoC 2012 proposal drafts](User:Bhinesley/gsoc2012 "wikilink").

## Misc

### Edit command, TODO

1.  Getting help for the edit subcommands is confusing. ex: 'help
    translate' doesn't work, since translate is really just a subcommand
    of edit. The current workaround is to use 'edit help translate' or
    'translate help'.
2.  It is not possible to use the batch operator '.' as a particular
    coordinate, i.e. 'translate -k -y . -a cube.s sph1.s sph2.s sph3.s'
    will not work. It would increase orthogonality if this were
    supported, although it's not strictly necessary. A workaround for
    the aforementioned example is 'translate -k . -a -y cube.s sph1.s
    sph2.s sph3.s'. It would take some doing to get this working, but it
    could be viewed as an opportunity to refactor some poor design
    decisions along the way.
3.  All testing has been done by hand. There are so many possible
    combinations of options/args, surely some have been overlooked.
4.  Cleanup logic per TODO/FIXME's in edit.c. Minor impact.
5.  The basic commands rotate and scale are not yet implemented
6.  Other subcommands could be written, for example:
    -   **swap** - switch one object out with another
    -   **align** - line several objects up with points on one or two
        axes (besides an intuitive name, it's not clear if this would be
        any better than using translate to perform this task, for ex:
        'translate -k . -a -y cube.s sph1.s sph2.s sph3.s' moves
        sph\[1-3\].s to the same y-coordinate as cube.s, without
        changing x/z positions.)
    -   other ideas?