[category:Geometry Service](category:Geometry_Service.md)

The formal way to specify the URL of a directory or concrete resource in
a Geometry Service repository is as follows:

`gs://host.of.geometry.service[:port]/name[:revision]/name[:revision]/...etc[:revision}[/]`

**\[port\]** Port is an optional paramater, default is 5309.

**\[revision\]** Revision is an optional per path step parameter,
default is HEAD.

**\[/\]** A trailing backslash indicates a directory, whereas the
absense of a backslash indicates a concrete resource.

----

### Examples

Requesting

`gs://geoserv.brlcad.org/wheeled/civilian/cars/sports/lotus/ `

would return a directory listing.


Where as requesting

`gs://geoserv.brlcad.org/wheeled/civilian/cars/sports/lotus/elise.g`

would return valid geometry.


and requesting

`gs://geoserv.brlcad.org/wheeled/civilian/cars/sports/lotus/elise.png`

would return a PNG image of the associated geometry.
