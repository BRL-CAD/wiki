A **VOL** primitive represents a three-dimensional grid of cells, also
referred to as voxels, which are each either solid or empty. It is
defined by a three-dimensional array of unsigned char values (read in
from a binary file), where each value represents a cell that is solid if
the value lies between the primitive's given upper and lower thresholds,
inclusively.

Information about the creation of a VOL primitive using **in** is
available in the [list of
primitives](BRL-CAD_Primitives#vol.md).

## Inserting volumetric data of a CT scan in MGED

Stanford hosts an [archive of volumetric
data](http://graphics.stanford.edu/data/voldata/) for testing purposes.

For this example, let's use the first set of data: "CT study of a
cadaver head". It contains 113 files of two-dimensional data with a
resolution of 256x256. Each file represents one slice, so we'll need to
concatenate them into one file to be able to import it into MGED. In
addition, the data is in the form of 16-bit unsigned integers, so we'll
need to use **cv** to convert it into unsigned chars.

First, download the archive and extract its contents into a directory,
which we'll call *scanslices*:

`$ wget `[`http://graphics.stanford.edu/data/voldata/CThead.tar.gz`](http://graphics.stanford.edu/data/voldata/CThead.tar.gz)
`$ mkdir scanslices`
`$ tar -zxvf CThead.tar.gz -C scanslices`

### Formatting the data

Next, concatenate them into one file, *scandata16*:

`$ cat $(ls -v scanslices/*) > scandata16`

Or, if **ls** doesn't support the **-v** flag:

`$ cat $(for file in scanslices(CThead.{1..113}; do echo $file; done) > scandata16`

Convert *scandata16* from 16-bit little-endian unsigned integers to
big-endian unsigned chars using **cv** and write the data to
*scandata8*:

`$ cv hu16 nuc scandata16 scandata8`

### Importing into MGED

The data in *scandata8* should now be ready to be imported into MGED:

`mged> in`
`Enter name of solid: scan`
`Enter solid type: vol`
`Enter name of file containing voxel data: scandata8`
`Enter X, Y, Z dimensions of file (number of cells): 256 256 113`
`Enter lower threshold value: 8 255`
`Enter X, Y, Z dimensions of a cell: 1 1 1`
