One of BRL-CAD's more powerful tools is search - essentially the Unix
find command adapted for geometry. A missing but desirable feature for
search is to be able to execute geometry editing commands the way find
can run programs on its results. Say, for example, we want to draw in
the MGED window all objects whose name starts with the letter s. We can
currently find those objects:

search . -name s\*

but we would have to capture the output and run a Tcl script in mged to
display the results. The exec feature would allow us to simply:

search . -name s\* -exec draw {} ;

(Note: quoting of options in the above examples is not what is required
for the MGED tcl prompt, but has been simplified for clarity - an
enhancement to MGED that would make using search easier would be a
setting that checks which command is being run before applying Tcl
globbing logic. This would allow search to recive the above commands "as
is" while still allowing 'ls \*' to work as expected, although that
should be user configurable because some users would type a search
command expecting Tcl globbing to work.)

Adding the exec option to the search command will require changes not
only to search but to how command tables are structured in BRL-CAD -
currently tables mapping commands to function calls are present in MGED,
and they would need to live at a lower level in order to allow exec to
find and run them (search is a library function and as such cannot know
anything about MGED). A student proposal would identify the needed
changes to both search and BRL-CAD's tools and libraries (they could be
more extensive than one might expect - remember the goal is to do it
"the right way", not just a way that works.) Students interested in this
topic are encouraged to discuss it with developers on IRC or email (IRC
is preferred.)

# References

-   src/librt/search.c
-   src/libged/search.c
-   src/mged/setup.c

# Requirements

-   Familiarity with C