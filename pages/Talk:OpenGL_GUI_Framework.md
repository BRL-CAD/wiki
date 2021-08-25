## Excerpts from comments

Useful bits extracted from comments made before submission deadline.
**Quotations slightly summarized and thus not exact/complete**, for
brevity; and also edited to fit them into different sub-topics.

### About project plan

Sean

> Since this project involves integrating with a back-end, one that is
> also being developed in parallel and does not yet exist, you'll either
> need to be able to stub back-end functionality as needed, or actually
> plan to contribute to the back-end and associated protocol as part of
> your development. Either approach would understandably affect your
> progress, but it's something to keep in mind with regards to the
> timeline and expectations.

### About GUI

Sean

> I'd like to hear your thoughts on how you'd go about providing a
> console and other GUI widget elements. Did you have a toolkit in mind?
> The options are notably limited for opengl applications (particularly
> for providing complex interfaces) and can be decided upon later, but
> I'd like to hear your thoughts. The design can of course be abstracted
> so that the actual widget layer doesn't matter so much (similar to how
> the graphics engine could be abstracted so OGRE could be replaced if
> desired), but there are other bigger considerations like whether the
> interface is zoomable/scalable or fixed.

Manuel

> I already used CEGUI with CrystalSpace \[and OpenSceneGraph\] and it's
> originally from OGRE, so I guess that it's the most straightforward
> option.
>
>
>  
> In CEGUI you can define the interface with XML files so it's often
> easier to test than having to recompile for every change. The units in
> principle are scalable, so you define the height and width of the
> widgets relative to the screen size (maybe in newer versions some of
> this changed, but there's only one stable release since I was using
> it). Is there a priori any preference about this, or goals that the
> widget system should absolutely meet? I think that most of the widget
> libraries for OpenGL are quite limited, as you say.
>
>
>  
> And for OGRE there's the following quote about GUIs: "MyGui joins the
> ranks of GUI systems available for OGRE, in addition to CEGui,
> BetaGUI, QuickGUI, RBGui and OpenGUI" from
> <http://www.ogre3d.org/index.php?option=com_content&task=view&id=449&Itemid=2>
> (I couldn't find a more comprehensive list with explanations).

Sean

> We'd of course probably want something considerably more
> polished/clean than the rather gamey default interface seen in the
> CEGUI screenshots. If I recall correctly, the last time I spoke with
> the CEGUI developers they indicated that while you can "scale" the
> interface, the effect is the same as scaling a raster image. So the
> application has to manage "native" sizes to minimize scaling
> artifacts. It didn't support scalable vector graphics instead of
> rather imagery. Something we can probably live with, but it "would
> really be nice".
>
>
>  
> Would also be useful if you could verify which of the available
> toolkit options you mention are suitable and describing the various
> tradeoffs. That is, presuming CEGUI isn't already known to be the best
> option available. If it is, then it sounds like a workable plan I
> could go with myself (other mentors feel free to chime in if
> otherwise).
>
>
>  
> Another thing to keep in mind for the context itself, multiple display
> support should be inherent with respect to the apps ability to go
> fullscreen (across multiple displays or single display) or windowed.
> CAD apps are usually heavily limited by screen real-estate.

Manuel

> I was checking CEGUI and it seems that they don't have new
> functionalities in 0.6.0 (released a couple of weeks ago) that could
> overcome the problems that you say (supporting vectorized formats or
> so), and I read some threads in the forums about that being unlikely.
>
>
>  
> About the rest, first impressions:
>
>
>  
> - MyGUI: Lack of pages describing features, only Doxygen
> documentation... Some screenshots:
> <http://sourceforge.net/project/screenshots.php?group_id=193706>
>
>
>  
> - BetaGUI: Too basic, only intended for quick demos and only for OGRE.
>
>
>  
> - QuickGUI: It's a mix between BetaGUI and CEGUI and with the same
> limitations, also only for OGRE. From the author: "Under the hood
> everything is implemented in pixels, but the user works in Relative
> coordinates. \[...\]. "As far as sizing, I don't know how I would
> implement that functionality. Looking at windows on XP for example,
> you can resize the MyComputer window, and the icons will move around,
> and add scroll bars, etc. I think at the moment that is too advanced
> for what I want to accomplish. I do plan to support scaling of
> windows, similar to WoW, where everything in the window gets bigger,
> so you can shrink/blow it up easily to match your preference".
>
>
>  
> - RBGui: I didn't find much info (features list and the like) except
> for a longish thread of about 30 pages in OGRE forums. The video of
> the GUI editor is nice, though: <http://rightbraingames.com/Gui.wmv>
>
>
>  
> - OpenGUI: Same lack of pages describing features, and it seems very
> old and simple:
> <http://opengui.rightbracket.com/component/option,com_gallery2/Itemid,49/>
>
>
>  
> - GUIchan: While looking at this I also found this one. List of
> features: <http://guichan.sourceforge.net/wiki/index.php/Features>
> which doesn't give much information about that (but you can also see
> some screenshots in that website, and it doesn't seem especially
> advanced).
>
>
>  
> - Another one that I found, Navi, the capabilities look amazing and it
> seems the more powerful of all, with all the capabilities of Mozilla
> browsers:
> <http://navi.agelessanime.com/wiki/index.php/NaviLibrary_Overview>
>
>
>  
> So having a look at this, I can only see Navi and RBGui as potentially
> better than CEGUI.

Sean

> Thanks for the summary impressions of the various toolkits. I didn't
> think that there really was any "better" option than CEGUI, I'm
> probably most just complaining that there's not a great option.. :-)
>
>
>  
> Navi is very impressive indeed, but the LLMozLib that it depends on
> (UBrowser) is Windows-only right now. As that is a fundamentally
> different way to provide the GUI (i.e. via HTML), you'd have to talk
> to research or talk to the devs to see how much effort porting to
> other platforms would take (is it just a simple matter of wrapping
> other native gl interfaces?) since portability to at least Linux, BSD,
> and MacOSX would be required down the road. Also, it would be good to
> know what the external dependencies are. The best aspect of the
> approach, though, is that you can end up with fixed resolution or
> resolution-independent displays.
>
>
>  
> The same mostly goes for RBGUI too .. it's a \*very\* impressive demo
> video and looks like it might even be reasonably extensible, but it's
> also presently only available for Windows. If selected, this one
> definitely deserves investigating how much effort porting would
> actually take and how well it could support a scalable interface.

Manuel

> About porting those, Navi maybe it's complicate, but it doesn't seem
> that getting RBGui to work in Unices is much of a problem:
> <http://shiware.com/media/> (look at the
> <http://shiware.com/media/rbgui-linux.png> and
> <http://shiware.com/media/RBGui010linux.diff> especially), unless they
> are requiring much more system-dependent functions now than in middle
> of July 2007 (the date of the files in the server). There's even
> <http://rpm.pbone.net/index.php3/stat/4/idpl/6224695/com/rbggui-devel-0.1.3-14.15.i586.rpm.html>
> from March 2008... :)
>
>
>  
> If it's not difficult to get it working, I would initially try to use
> it instead of CEGUI, starting to test before the official coding
> starts -- resorting to CEGUI is always possible, but since we already
> know what it can offer (and it's not that much) it would be preferable
> to exhaust other options first.