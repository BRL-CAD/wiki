# Embedding a framebuffer window

In the past month I started working at the Embedding a framebuffer
window project. Like last year, I was really excited about participating
in Google Summer of Code for BRL-CAD.

The project can be split into two main parts:

-   Creating a new Qt framebuffer
-   Embedding a framebuffer window

As expected, I started by creating a new cross-platform Qt framebuffer.
Firstly, I studied the existing framebuffer implementation, especially
the X24 framebuffer. The second step was to create, just like in the
display manager's case, a text framebuffer that just logs function
calls. Being familiarized with the code and with BRL-CAD's libraries
made this task a lot easier than it was last year.

After having a new framebuffer interface, even though it was a simple
one, I was able to integrate the framebuffer so that in can be used by
the rt command. At this point, it was the time to start implementing the
open and close functions. Having last year's experience, made the
integration of Qt in cmake a lot easier and also the creation of an
empty Qt window (which basically is what the open function does). I was
really excited when the window was created, but having an empty window
isn't really helpful. So, I started working at the write function so
that it can display raytraced content. After some struggle with some bad
drawing, I managed to successfully display content:

<http://i.imgur.com/BqYS7Mr.png> <http://i.imgur.com/kFaMQk9.png>

As seen from the above pictures, the new framebuffer is integrated with
the raytracer and it can successfully display raytraced models. However,
there still are things that need to be done such as using, reading and
writing a colormap or adding the keyboard and mouse functionality. In
order to implement this, I have to do a little more research so that I
could find the best approach.

Since at this time I am a little bit busy with my final paper and I
can't say I am really eager to do more research, I decided to change a
little bit the original schedule and start working at embedding a
framebuffer window. I have done this because I have a more clear idea on
what to do and the missing functionality of the framebuffer shouldn't
interfere with this task.

So, in the following week or two I hope to have the embedding done so I
could start working at the missing features. Even though, I changed a
bit the implementation order, I am on track with the original schedule
and everything should be done as expected.

As it comes to the actual code, until now I've written about 750 lines
of code and almost all of it can be found in libfb/if_qt.cpp. In order
to have a fully functional framebuffer, I think it would take another
700-800 lines. What I really like at this project and what keeps me
motivated is the fact that I can have visual feedback, which is
different from other projects I have recently worked at.