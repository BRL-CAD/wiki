# Notes on implementing material object

BRL-CAD uses simple material properties, presently limited to density,
for calculating weights, moments of inertia and other geometric analyses
by tools such as rtweight and gqa which rely on text files to gather
material information. When computing weight,volume, regions are
interrogated and associated with a material depending on it's GIFTmater
id.

It would be more flexible to have (non-geometric) material objects that
store properties and can be associated with geometric objects from a .g
database and that can be used with the current set of BRL-CAD
commands/tools.

The on-disk version of each object consists of three distinct parts:
Object Header, Object Interior and Object Footer. Object specific data
is stored in the Object Interior, either or in both Object Body or
Object Attributes. Writing on disk is done by rt_db_put_internal()
which inspects the handle on the internal format of a database object
for the major/minor type.

BRL-CAD already has a class for non-geometric objects:
DB5_MAJORTYPE_ATTRIBUTE_ONLY (major type 3), has no object body and
only uses Object Attributes to store object information. At the moment
all DB5_MAJORTYPE_ATTRIBUTE_ONLY objects are minor type 0. There
should be minor types for material and shader objects.

Internal object specific methods are stored in the OBJ (struct
rt_functab array). When building internal objects, the minor type is
used as an index to point the right methods for that type of object. For
now, material and shader objects are at the end of the OBJ array.
<img src="Rt_material_internal2.png" title="fig:Rt_material_internal2.png" width="364" alt="Rt_material_internal2.png" />

There should probably be a new array that stores just
DB5_MAJORTYPE_ATTRIBUTE_ONLY object methods for the material and
shader minor types.

Since low-level routines that handle object exporting, store internal
attributes to the on-disk objects Attributes section it 'd be natural to
store material properties in idb_avs. I was thinking it would be better
if rt_material_internal would actually contain just a pointer to
idb_avs and make operations on it. Right now, on my patch,
rt_material_internal contains an bu_avs structure that's being copied
to idb_avs when exporting.

<figure>
<img src="Rt_material_internal.png" title="Rt_material_internal.png" width="800" alt="Rt_material_internal.png" /><figcaption aria-hidden="true">Rt_material_internal.png</figcaption>
</figure>

To associate regions with materials the most sane way I could think of
was to store the material object's name in one of the region's internal
representation fields. When a tool (l/...) would want to inspect a
region's material properties it would check the string (bu_vls) stored
in the region's internal representation (rt_comb_internal) and perform
a database lookup for the object with that name. rt_comb_internal
already has a bu_vls field "material" which is not used anyways. If the
lookup fails it means that the material doesn't exist (anymore). This is
convenient because many regions can reference the same material object
and this way changes to the material properties are "propagated" to all
the objects that reference that material.

When raytracing is performed and tree state is built from combs
(db_apply_state_from_comb), material object name is stored in the
ts_mater field (struct mater_info). This way rtweight and gqa can
perform db lookups for local material objects.

The rough submitted
[patch](https://sourceforge.net/p/brlcad/patches/302/) covers most of
these details. If the feedback is positive on the implementation details
the next step is to provide an API to modify material properties and
make sure all tools work the new type of objects (e.g.:
adding/modifying/removing properties attr or making it easy for a region
to reference a material object using mater).

Another issue I want to tackle is binary attributes. Material properties
are either float or double types and they're stored in bu_avs which can
currently only map string to string. I've been following Tom Browder's
work on this. He wanted each pair in an avs to be flexible enough to
hold a different mapping. What I don't understand is the format that he
wants/wanted to use to store the data:

***/\* format is: <ascii name> NULL &lt;binary length \[network order,
must be decoded\]&gt; &lt;bytes...&gt; \*/***

Given we have a pair (string - int/float/double... type), binary length
(would have to be decoded) stores the length of the pair's value. What I
don't understand is how we are to determine how long is the binary
length field. We would probably need another separator (NULL) but that
might be interpreted as part of the binary length field. An easy way out
is to just store the binary length as ascii, separated by NULL.