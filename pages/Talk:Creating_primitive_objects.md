# Why I created this article

I initially set out to revise the introductory section of the [BRL-CAD
Primitives](BRL-CAD_Primitives.md) article, which used to
briefly discuss the various ways MGED provides for creating such
objects. I was thinking I would flesh out that discussion and also talk
about how the properties of such objects can be viewed and edited. But I
decided that information would make that intro way too long and in any
event properly belonged in separate articles. So I moved the information
on creating primitives here, renamed the articles on viewing and editing
them so all three titles are grammatically consistent (turning the old
titles into redirects), substituted links to them into the primitives
article, and went to work on all three.

As for my changes to the primitive creation information that I moved
here:

-   My experience with the Create command is that it never displays the
    Primitive Editor dialog box. So I removed the claim that "When an
    object is selected from the create menu, you are prompted for a
    name, and then dropped into the primitive editor form; however, if
    the object type has no form, create will do about the same as make."
    Instead, I noted that **make** and **create** do essentially the
    same thing, and are usually immediately followed by editing of the
    created object. If that's wrong, I would really appreciate being
    told why create doesn't open the Primitive Editor when I use it.

<!-- -->

-   I also removed the parenthetical "are there any other ways" comment
    in favor of mentioning object importing and using the TCL put
    command. If I learn of any other methods, I'll add mentions of them
    too.

Instead of putting examples in this article, I'm planning to add them to
the descriptions of the various types of primitives and add appropriate
links here. That will probably make [that
article](BRL-CAD_Primitives.md) too long, so I suspect I'll
split it up at some point (assuming no one objects too strenuously).

[JoelDBenson](User:JoelDBenson.md)
([talk](User_talk:JoelDBenson.md)) 21:09, 27 May 2013 (UTC)

I certainly don't object. Make it better. :)

Your notion of what you observed about **Create** and **make**
essentially being the same thing is accurate. I think the original
writing was perhaps not being precise or, quite possibly, the code has
simply changed since it was written.

You may also want to look at much of the very new content created by our
participation in the Google Code-In project where many of the completed
tasks were helpful documentation:
<http://www.google-melange.com/gci/org/google/gci2012/brlcad>

Much of that will eventually find its way onto our wiki (or already
has), into our XML documentation sources, and integrated with our other
content.

[Sean](User:Sean.md) ([talk](User_talk:Sean.md)) 11:37,
31 May 2013 (UTC)
