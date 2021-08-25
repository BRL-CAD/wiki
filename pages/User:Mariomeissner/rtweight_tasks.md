This page is a list of the tasks remaining to make rtweight a usable
tool with the new Voronoi implementation that Mario Meissner coded
during his SOCIS 2017 program.

For any questions about the current algorithm, please send an email to
jmariomeissner@gmail.com

**Minor required code changes**

\- Get rid of all static arrays, and make use of dynamic memory instead.

\- Get rid of the MARGIN variable and use already existing BU tools to
handle float comparisons.

\- Find a better way to grant all hit calls access to the user_plist.
Currently this is a global variable.

**Major tasks**

\- Handle different materials properly. For now we assume all our data
points are for one material, and we don't check which material we are
crossing.

\- Add an option to create and store a new datapoint-set to a file.

\- Add an option to use a file to load the datapoints.

\- Change the usage function to reflect all the changes.

\- Change the return text to reflect all the changes.