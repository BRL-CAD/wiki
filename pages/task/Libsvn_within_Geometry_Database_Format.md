BRL-CAD's new Geometry Service is intended to provide modeling software
with the ability to act as a "client" that can request models and
versions of models from a repository, much like BRL-CAD's source code is
stored in a repository and developers can request specific subsets and
revisions. This Geometry Service will be utilizing the subversion
libraries for version control "under the hood".

While geometry databases are currently stored as files, the goal for
geometry service is to allow individual regions to be revision
controlled instead of just .g files. This raises the question of how to
handle the geometry data for a server on the backend - lots of tiny .g
files, one per region?

An interesting possibility is to make use of the ability of the
subversion libraries to communicate to different backend systems to
store revision information. The current default backend (FSFS) is
filesystem based, but there is an older backend based on BerkeleyDB.
This project would investigate the possibility of porting the FSFS
filesystem based subversion backend logic to communicate directly with
the .g database format, storing geometry revisions and geometry
information without needing to interact with regular files. Because the
Geometry Service is a special case (it does not need to revision control
arbitrary file types) a geometry specific backend may be able to improve
on performance characteristics of a basic subversion approach.

The other piece of the puzzle required for subversion-in-.g-files is the
ability to check out a revision of a repository to a .g file, instead of
individual files on a filesystem. This may be more challenging - it is
not currently known how deep the assumptions of "checkout writes to
filesystem" are embedded in the subversion libraries.

The task is to both commit into and checkout into .g file based
subversion repositories.

# References

-   geomcore module
    -   separate from the 'brlcad' checkout, containing the geometry
        service

<!-- -->

-   <http://svnbook.red-bean.com/en/1.5/svn.developer.layerlib.html>

Requires:

-   Familiarity with C
-   (optional) Knowledge of Apache Portable Runtime and Subversion
    libraries