Plan for Image Processing Utilities

# Introduction

Carrying forward from my proposal on the wiki page and Google-Mellange.
In this page I add, improvements for my plan and detail it further. Here
I add points from my trunk (collected since the proposal day) and would
like valuable feedback from the core-developers, so that the plan is in
sync with the organization's goal and needs.

# Key Points

-   There are arount 125 utilities in total in the /src/util folder. Not
    all of these utilities, are image processing tools.

<!-- -->

-   There are around 35 tools which deals in conversion of one format to
    other.

<!-- -->

-   Other Image Processing Functions to be implemented have been divided
    into Groups based on there similarities in implementation and such
    that each week during the

development phase 1-2 Groups could be implemented. Details of this will
be discussed in further sections.

# Image Conversions

The week from July 1 - July 15 during the development phase is dedicated
to import/export. I have been working on this front and have submitted
few patches. Although fine tuning is required. Once the complete Import
Export Functions (very few are left) are deployed Image conversions
becomes very easy. Following is a table which describes the current
image conversions tools.

|           |                                                                                                                                                     |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| alias-pix | Convert ALIAS(tm) PIX format image files to BRL PIX format files.                                                                                   |
| ap-pix    | Applicon color ink jet printer to .pix file converter.                                                                                              |
| bw-a      | Convert a bw file into an ASCII bitmap.                                                                                                             |
| bw-pix    | Merge three BW files into one RGB pix file. (i.e. combine the colors)                                                                               |
| bw-png    | Convert bw file to PNG (Portable Network Graphics) format                                                                                           |
| bw-ps     | Convert a black and white (bw) file to an 8-bit PostScript image.                                                                                   |
| bw-rle    | Encode a .bw file using the Utah Raster Toolkit RLE library                                                                                         |
| bw3-pix   | Convert an 8-bit black and white file to a 24-bit color one by replicating each value three times.                                                  |
| pix-alias | Convert BRL PIX format image files to ALIAS(tm) PIX format files.                                                                                   |
| pix-bw    | Converts a RGB pix file into an 8-bit BW file.                                                                                                      |
| pix-bw3   | Converts a RGB pix file into 3 8-bit BW files.                                                                                                      |
| pix-orle  | Encode a .pix file using the old ORLE library                                                                                                       |
| pix-png   | Convert pix file to PNG (Portable Network Graphics) format                                                                                          |
| pix-ppm   | convert BRL .pix files to ppm                                                                                                                       |
| pix-ps    | Convert an RGB (pix) file to an 24-bit color PostScript image.                                                                                      |
| pix-rle   | Encode a .pix file using the Utah Raster Toolkit RLE library                                                                                        |
| pix-spm   | Turn a pix file into sphere map data.                                                                                                               |
| pix-sun   | Program to take a BRL-CAD PIX format image file and convert the image to a Sun Microsystems 8-bit deep color "rasterfile" format image.             |
| pix-yuv   | Convert a .pix file to a .YUV file, i.e. in CCIR-601 format.                                                                                        |
| pl-asc    | Plot3(5) to ASCII converter.                                                                                                                        |
| pl-dm     | Example application that shows how to hook into the display manager.                                                                                |
| pl-hpgl   | Convert a unix-plot file to hpgl codes.                                                                                                             |
| pl-pl     | Gets rid of (floating point, flush, 3D, color, text).                                                                                               |
| pl-ps     | Display plot3(5) as PostScript. Based on pl-X and bw-ps                                                                                             |
| pl-tek    | Convert 3-D color extended UNIX-plot file to Tektronix 4014 plot. Gets rid of (floating point, flush, 3D, color, text).                             |
| pl-X      | Display plot3(5) on an X Window System display (X11R2) lcolor                                                                                       |
| png-bw    | Display info about a PNG (Portable Network Graphics) format file                                                                                    |
| png-pix   | Convert PNG (Portable Network Graphics) format to pix                                                                                               |
| mac-pix   | Read MacPaint document and output pix(5) or bw(5) raster image                                                                                      |
| orle-pix  |                                                                                                                                                     |
| sun-pix   | Program to take Sun bitmap files created with Sun's \`\`screendump'' command, and convert them to pix(5) format files.                              |
| xyz-pl    | Program to take input with up to 3 white-space separated columns, expressed as x y z and produce a 3-D UNIX-plot file of the resulting space curve. |
| yuv-pix   | Convert a .yuv file to a .pix file, i.e. in CCIR-601 format.                                                                                        |

This tools will be converted to IP functions. The structure of the
function (not finalized) might look like the following.

`   int icv_convert(char* input_filename, struct icv_size* input_size, char* output_filename, int cvt2status)`

# Other Image Processing Functions

I have chosen a set of image processing functionalities and divided them
into groups with similar implementation details. This division will also
help during development phase. During each week 1-2 Groups will be
chose. Details of the combinations for each week are being studied at
present so that load is balanced in each week. This will also ensure and
bring more structure in the current plan, thus minimizing the
implementation risk. Details of each group is given in the following
sections. Although in days to come more group specific comments will be
added.

## Crop or Rect (GROUP\#1)

-   **bwrect** Remove a portion of a potentially huge .bw file.
-   **pixrect** Remove a portion of a potentially huge pix file.
-   **bwcrop** Crop Black and White files.
-   **pixcut** Extract a piece of a pix file. If the parameters of the
    file to be extracted do not fit within the original pix file then
    the extra area is filled with a background solid color.

### Comments

## Differences and other arithmetic operations (GROUP\#2)

-   **bwdiff** Take the difference between two BW files. Output is:
    (file1-file2)/2 + 127
-   **pixdiff** Compute the difference between two .pix files. To
    establish context, a half-intensity monochrome image is produced
    when there
-   **pixsaturate** A saturation value of 0 gives monochrome, 1.0 gives
    the original image, and values larger than 1.0 give a more saturated
    image.
-   **bwmod** Modify intensities in Black and White files. Allows any
    number of add, subtract, multiply, divide, or

### Comments

## Filters, (GROUP\#3)

-   **bwfilter** Filters a black and white file with an arbitrary 3x3
    kernel. Leaves the outer rows untouched.
-   **pixfilter** Filters a color pix file with an arbitrary 3x3 kernel.
    Leaves the outer rows untouched. Allows an alternate divisor and
    offset to be given.
-   **pix3filter** Filters a color pix file set with an arbitrary 3x3x3
    kernel. Leaves the outer rows untouched.
-   **pixfade** Fade a picture

### Comments

## Histograms and Equalizations (GROUP\#4)

-   **bwhisteq** Build up the histogram of a picture and output the
    "equalized" version of it on stdout.
-   **bwhist** Display, and optionally dump to tty, a histogram of a
    black and white file. Black is top of screen, white bottom.
-   **pixhist** Display a color histogram of a pix file. 0 is top of
    screen, 255 bottom.

### Comments

## Scale or Shrink (GROUP\#5)

-   **bwscale** Scale a black and white picture.
-   **pixscale** Scale an RGB pix file.
-   **bwshrink** scale down a picture by a uniform factor.
-   **pixshrink** scale down a picture by a uniform factor.

### Comments

## Stats (GROUP\#6)

-   **bwstat** Compute statistics of pixels in a black and white (BW)
    file. Gives min, max, mode, median, mean, s.d., var, and skew.
-   **pixstat** Compute statistics of pixels in a PIX file.
-   **pixcolors** Count the number of different pixel values in a PIX
    format image.
-   **pixcount** Sort the pixels of an input stream by color value.
-   **imgdims** Guess the dimensions of an image

### Comments

## Thresh (GROUP\#7)

-   **bwthresh** Threshold data in BW(5) format. thresholds stream of
    data.
-   **pixclump** Quantize the color values in a PIX(5) stream to a set
    of specified values

### Comments

## Interpolate/Decimate (GROUP\#8)

-   **pixhalve** Reduce the resolution of a .pix file by one half in
    each direction, using a 5x5 pyramid filter.
-   **pixinterp2x** Read a .pix file of a given resolution, and produce
    one with twice as many pixels by interpolating between the pixels.

### Comments

## Background and Border (GROUP\#9)

-   **pixbackgnd** Background Maker
-   **pixbgstrip** Background Un-Maker
-   **pixborder** Add a 1-pixel-wide border to regions of a specified
    color

### Comments

## Merge or Split (GROUP\#10)

-   **pixmerge** Given two streams of data, typically pix(5) or bw(5)
    images, generate an output stream of the same size, where the value
    of the output is determined by a formula involving the first
    (foreground) stream and a constant, or the value of the second
    (background) stream.
-   **pixdsplit** Disentangle the chars from the doubles in a pixd(5)
    stream
-   **pixfields** (not exactly Merge Split but similar) \* pixfields
    takes two input pictures and extracts field 1 from the first pix
    file and field 2 comes from the second pix file. This is useful for
    creating field-by-field animation for NTSC video display.
-   **pixfieldsep** (not exactly Merge Split but similar) \* Separate an
    interlaced video image into two separate .pix files.

### Comments

## Morphing and other Misc (GROUP\#11)

-   **pixmorph** Utility for morphing two BRL-CAD pix files.
-   **pixtile** Given multiple .pix files with ordinary lines of pixels,
    produce a single image with each image side-by-side, right to left,
    bottom to top on STDOUT.
-   **pixuntile** Given a single .pix file with multiple images, each
    side-by-side, right to left, bottom to top, break them up into
    separate .pix files.
-   **pixembed** Embed a smaller pix file in a larger space, replicating
    the boundary pixels to fill out the borders, and output as a pix
    file.
-   **pixpaste** pixpaste will insert an arbitrary pix file into another
    pixfile. If the image being pasted does not fit within the
    destination file then the excess is discarded.
-   **pixmatte** Given four streams of data elements, where element is
    of arbitrary width, typically pix(5) or bw(5) images, output a
    stream of the same number of data elements.
-   **pixelswap** interchange pixel values in an image

### Comments

# Feasibility

The above functionalities were grouped with associated commonalities.
These functionalties will be added as part of the ICV library. These
list of functionalities have been drawn from the Image Processing Tools
available with brlcad which indeed is the aim of this project.

Thus the implemnetation task will envolve syncing the tools with
structures of LIBICV and the said functionalities to the library. This
will help in inter-function communication with the whole BRLCAD source.

Also once all the structures are identified (work is cuurently
underway), syncing and implemneting a function will require very few
functional points. And thus is also feasible.