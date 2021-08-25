This page is a draft to present the new options to be added RT
application. Waiting for review before implementing.

## Usage

-L \# \#

The first number will define the firing pattern and the second one the
frequency on which the framebuffer will be updated.

\- Firing Pattern options:

1.  Normal (default)
2.  Increasing
3.  Multiple Samples
4.  Random

\- Frequency of updates

1.  Unbuffered - updates after every pixel
2.  Scanline - updates after each line (default, except for Random)
3.  Image - updates only after the image is finished
4.  Frame - updates after each frame is finished (only makes sense for
    multi-frames mode)

Table of valid combinations

|            |     |     |     |     |
|------------|-----|-----|-----|-----|
| Fire\\Freq | 1   | 2   | 3   | 4   |
| 1          | X   | X   | X   |     |
| 2          | X   | X   |     | X   |
| 3          | X   | X   |     | X   |
| 4          | X   |     |     |     |

## Examples

./rt -L"1 2" -- the same as default

./rt -L"4" -- unbuffered random mode

./rt -L"3" -- scanline multi-sample mode

./rt -L"3 1" -- unbuffered multi-sample mode