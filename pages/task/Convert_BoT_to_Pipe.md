In the design phase of an aircraft, component positions and locations
are continually in flux leading to a lag in models of line routing.
Typically when lines are received from an aircraft manufacturer to the
vulnerability analyst, they may not terminate at the component(s) they
were meant to connect to. Therefore, when importing these lines from
high-end CAD packages such as Catia or Pro-E into BRL-CAD, they need to
be re-routed so that they reflect the aircraft systems accurately and
eliminate any overlapping issues. Currently these lines are imported
using an intermediate format such as STL, which is a facetted geometry.
In BRL-CAD this becomes a "Bag-of-triangles" (BoT) solid which cannot be
edited with any efficiency. It is very desirable to be able to import
these lines using BRL-CAD native geometry via the pipe solid. Any code
developed to accomplish this must perform the following:

\- Automatically determine pipe start and end points

\- Automatically determine BoT inner and outer diameters

\- Successfully traverse the BoT line placing pipe vertices where
necessary

\- Successfully negotiate line models that have T or Y shaped
intersections creating pipe solids for each leg

\- Accurately utilize the pipe solid bend radius attribute to limit the
number of vertices necessary to create a bend

\- Apply a vertex reduction algorithm based on user defined tolerances
(angular tolerance to define a straight segment)

\- Implement options allowing the automatic generation of a fluid
component (fuel or hydraulic fluid within the line)

\- Implement options that allow for automatic Boolean operations into
both line and fluid Regions