# Embedding a framebuffer window

The project can be split into two main parts:

-   Creating a new Qt framebuffer
-   Embedding a framebuffer window

I started by creating a new cross-platform Qt framebuffer which was
implemented almost completely until midterm evaluation. More information
about my work in that period can be found [here](Midterm.md).

In the second part I worked at embedding a framebuffer window in the
existing Qt display manager. Even though I encountered quite a lot of
unexpected problems (bad drawings, drawings that disappeared) in the end
I managed to successfully embed a framebuffer window. I can say that
when I saw correct and permanent drawings made in mged I was really
relieved and also really excited.

Apart from embedding a framebuffer window, I also added support for
keyboard and mouse events and for using, reading and writing a colormap
to the framebuffer.

When it comes to the actual code, it can almost all be found in
libfb/if_qt.cpp and libdm/dm-qt.cpp. As I predicted in the first part,
in order to embed a frambuffer window another 800 lines of code were
necessary.

# Results

As you can see from the below pictures the framebuffer is integrated
with the raytracer and it can successfully display raytraced models.

<http://imgur.com/hOIryrt.png> <http://imgur.com/h3TLREb.png>

When it comes to embedding a frambuffer window, I tested the behavior in
both mged

![](img/Mged_fb.png)
![](img/Mged_fb4.png)

and archer

![](img/Archer_fb.png)
![](img/Archer_fb2.png)

More infos about the development process can be found on the [log page](Logs.md)
