I am Mohit, a GSoC student participant with BRL-CAD for the year 2013.
My GSoC-13 project was aimed to consolidate and develop an image
processing and conversion library.

To start my work, I adopted BRL-CAD's standard coding style, grasped
functions related to its utility library (libbu) and focused on the
status of image processing library previously in place (LIBICV). After
which I worked on the various tools of Image Processing in BRL-CAD and
listed and grouped them as per the processing they are involved in.
Prior to my application period and during very initial phase of coding
period, I created few patches to earn my commit rights. And was
successfully granted one on 26th July.

My first challenge was to decide on the image containers. After
discussions on mails and IRC. And writing some testing codes I along
with my mentors decided on the current image processing container. This
included changing the data type of the image data. Included new entries
for number of channels and other image rules. And the most important
scrapping the file descriptor used in the image containers. Thus the
name also changed from icv_image_file to icv_image. The data was no
longer associated to a file but rather an image.

Even bigger challenge was to incorporate these changes in the existing
use of the image processing library in the BRL-CAD utilities like rt and
libraries like ged and all. Also, I was strictly guided to adopt
sequential and minimal change during commits. This required exploring
code base of rt and other places where LIBICV was used. Later I
completed the task with few modifications and reiterations. This was
challenging because rt follows RTUIF (Ray-Tracing User Interface
Framework ) involving many files different functions and different
privileges to use image reading/writing. With few complications I was
later successful in implementing the changes.

After coming to a standard implementation and setting the game rules
right other tasks were both easy and smooth. I wrote APIs for image
processing of functions including but not limited to convolution (also
special convolution including three images \[icv_filter3\] ), cropping
(a special cropping with any four points of a quadrilateral
\[icv_crop\]), resizing (with two ways to interpolate and two to
decimate).

I also used these APIs in BRL-CAD's image processing tools and modified
there documentation pages when required.

Later I wrote the reading and writting plugin for different image
formats. Currently ICV has capibility to read/write images from/to both
pipes and files. Also In the case of BRL-CAD raw data of BW, PIX and
DPIX the library has an added capability to read without the size being
specified. Other implemented format is ppm.

Sean and Erik were great mentors. They would always guide and insist me
on adopting standard practices whose importance I realize now. Really
maintaining large and old code-bases is both fun and learning.

It was my first time in Open-Source Coding. I enjoyed and believe this
summer will be cherishable.

# Future Work

In future I will be working on other formats. The whole point on
adopting the new image container was to use rt's capacities to render
high quality images and get an ability to store images of high
definition format like OpenEXR in BRL-CAD. Therefore I will be working
on it.

'''''P.S. This summary is the copy of the mail posted on brlcad-devel
list.