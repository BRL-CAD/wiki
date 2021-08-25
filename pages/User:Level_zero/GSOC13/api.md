# API CALLS

## Cropping(Group1)

**for bwrect, pixrect** **Comments**

-   Removes a rectangular portion of a potentially huge image.
-   *orig*, is the point that corresponds to Bottom left corner to
    extract the image from
-   *area* corresponds to the total number of pixels in the new map.
-   *img_out* is the output image.

`   int`
`   icv_rect(const icv_image_t *img,`
`            const icv_point_t *area,`
`            const icv_point_t *orig`
`            icv_image_t *img_out);   `

**for bwcrop**

**Comments**

-   Crops file with arbitrary points
-   *p1*, *p2*, *p3*, *p4* are left lower, right lower, left upper and
    right upper points respectively.
-   *img_out* is the output image.

`   int`
`   icv_crop(const icv_image_t *img,`
`            const icv_point_t *p1,`
`            const icv_point_t *p2,`
`            const icv_point_t *p3,`
`            const icv_point_t *p4,`
`            const icv_size_t *outsize,`
`            icv_image_t *img_out);`
`            `

## Operations (Group2)

**for bwdiff, pixdiff**

**Comments**

-   Performs arithmetic operations between the pixels of two images.
-   *img_1* and *img_2* are two input images.
-   *opr* corresponds to the operation information.
-   *img_out* is the output image.

`   int`
`   icv_airth2(const icv_image_t* img1,`
`              const icv_image_t* img2,`
`              const icv_operation_t *opr,`
`              icv_image_t *img_out) `

**for bwmod**

**Comments**

-   Performs arithmetic operations with a value of the pixels of the
    input image, the resultant value is replaced in the same input
    image.
-   *oper* is the array corresponding to the operations.
-   *numop* is the number of operations.
-   *img_out* is the output image.

`   int`
`   icv_airth1(icv_image_t* img,`
`             const icv_operation_t *oper[],  `
`             const int numop); `

**for Pixsaturate**

**Comments**

-   *saturation* is the saturation value
-   *img_out* is the output image.

`   int`
`   icv_saturate(const icv_image_t *img,`
`                const double saturation,`
`                icv_image_t *img_out);`

## Filters (Group3)

'''for bwfilter, pixfilter, pix3filter, pixfade

**Comments**

-   Performs filtering of image using convolution with the kernel.
-   *kernel* corresponds to kernel used for image filter
-   *img_out* is the output image.

`   int`
`   icv_filter(const icv_image_t *img,`
`              const icv_kernel_type_t kernel;`
`              icv_image_ *img_out);`

## Histogram (Group4)

**for bwhist, pixhist**

**Comments**

-   Finds histogram of the image
-   *bin* is the number of bins for calculating histogram
-   *bin_out1*, *bin_out2* and *bin_out3* are the pointers for output
    histograms
-   For three channel image this is called with all the three output
    pointers, for bw image this is called with pointers only for first
    and others are left as NULL

`   int`
`   icv_hist(const icv_image_t *img,`
`            const int bin,`
`            long *bin_out1,`
`            long *bin_out2,`
`            long *bin_out3);`

**for bwhisteq**

**Comments**

-   Calculates histogram equalization of the image

`   int `
`   icv_histeq(const icv_image_t *img,`
`                   icv_imgage_file_t *img_out);`

## Scale (Group5)

**for bwscale, pixscale**

**Comments**

-   *outsize* is the required output size
-   *method* is the prescribed method

`   int    `
`   icv_scale(const icv_image_t *img,`
`                  const icv_size_t *outsize,`
`                  const icv_scale_method_t method,`
`                  icv_image_t *img_out);`

**for bwshrink, pixshrink**

**Comments**

-   *factor* is shrinking factor.
-   *method* is the prescribed method.

`   int`
`   icv_shrink(const icv_image_t *img,`
`                   icv_image_t *img_out,`
`                   const int factor,`
`                   const icv_shrink_mehtod_t method);`

## Stats (Group6)

**for imgdims, pixcount** Not useful

**for pixstat, bwstat**

**Comments**

-   finds the image statistics

`   int`
`   icv_stat(const icv_image_t *img,`
`                 icv_stat_t *stat1, `
`                 icv_stat_t *stat2,   `
`                 icv_stat_t *stat3);`

**for pixcolors**

`   int`
`   icv_colors(icv_image_t *img) `
`   /* Prints all the colors */    `
`   `

## Threshold (Group7)

**for bwthresh**

**Comments**

-   *val* is a pointer to an array of threshold values
-   *num_thresh* is the number of the threshold values
-   *img_out* is the output image

`   int`
`   icv_threshold(const icv_image_t *img,`
`                      icv_image_t *img_out,`
`                      const unsigned char *val,`
`                      const int num_thresh);`

**for pixclump**

`   int`
`   icv_clump() `
`   /* Need Suggestions */`
`   `

## Interpolate (Group8)

**for pixinterep2x**

**Comments**

-   Interpolates the image two twice its resolution

`   int`
`   icv_interep2x(const icv_image_t *img,`
`                      icv_image_t *img_out);    `

**for pixhalve**

**Comments**

-   Decimates the image

`   int`
`   icv_halve(const icv_image_t *img,`
`                  icv_image_t *img_out);`

# Structure

-   ICV_IMAGE_FILE

` struct icv_image_file {`
`   uint_32 magic;`
`   char* filename;`
`   int fd;`
`   int format;`
`   int width, height, depth;`
`   unsigned char *data;`
`   unisgned long flags;        `
` };`

-   ICV_SIZE

` struct icv_size {`
`   int height, width;`
` };`

-   ICV_POINT

` struct icv_point {`
`   int x,y;`
` };`

-   ICV_OPERATION

` struct icv_operation {    `
`   char oper;`
`   double val; `
` };`
`   `

-   ICV_KERNEL

` struct icv_kernel {`
`   char *name;`
`   char *uname;        /* What is needed to recognize it */`
`   int *kern;`
`   int kerndiv;    /* Divisor for kernel */`
`   int kernoffset; /* To be added to result */`
` };`

-   ICV_STAT

`   struct icv_stat {`
`     int max, min, mode, median;`
`     double mean, var, skew;`
`     long sum, partial_sum;`
`   };`