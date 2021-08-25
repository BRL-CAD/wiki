### Development Log

## 2/17

-   Found exactly how to create a test

## 2/19

-   Found best files to begin trying to fuzz

## 2/24

-   Made basic programs using zzuf and afl to begin fuzzing

## 2/27

-   Tried to integrate AFL with BRL-CAD tests

## 3/2

-   Began learning and practicing new fuzzer -- LibFuzzer
-   Went through tutorials on LibFuzzer and wrote sort programs to run
    it on
-   Followed this tutorial:
    <https://github.com/google/fuzzing/blob/master/tutorial/libFuzzerTutorial.md>

## 3/4

-   Tried to link LibFuzzer target to BRL-CAD library
-   Struggled with the compilation of BRL-CAD (required installing
    libraries not needed before)
-   Struggled with compiling target so it had BRL-CAD libraries

## 3/9

-   Experimented with compiling target and consulted Shikhar, a PHd
    student at UT
-   Found the BRL-CAD header file and the exact syntax needed to fully
    compile my target
-   Built the target, ran it in various ways tinkering with how the data
    was input into bu_sort, checking if the output was correct, adding
    seeds to the input
-   Used this compilation statement

clang++ -g -O1 -fsanitize=fuzzer -Iinclude -Ibuild/include
-Ibuild/include/openNURBS/ target.cc -Lbuild/lib -Wl,-rpath
-Wl,build/lib -lrt -lbu

## 3/23

-   Learned Jenkins CI and successfully built BRL-CAD
-   Started creating a build to test BRL-CAD immediately

## 3/25

-   Fixed testing BRL-CAD in Jenkins
-   Began creating infrastructure for a "make fuzz"

## 3/30

-   Looked at other regression tests cmake files to find what exactly is
    required to compile
-   Tried to mimic these to compile fuzzing tests

## 4/1

-   Switched strategies for compiling using cmake, spent most of my time
    reading documentation to better understand how exactly cmake works
    and how that can be applied to fuzzing

## 4/13

-   Figured out how to create a fuzz directory in the build
-   Began writing run.sh to find libraries and compile the test
-   Used the benchmark file to base the run.sh off of but cannot figure
    out how to find the target

## 4/17

-   Much closer to compiling target -- using add_executable and linking
    targets with target_link_libraries
-   Found how to link libfuzzer with the target in cmake
-   Added dependency bu
-   Still having trouble figuring out how to add the dependency rt
-   Getting error that it is an executable that cannot be shared

## 4/27

-   Changed compiler to Clang for building BRL-CAD
-   Successfully compiled fuzz test
-   Able to run fuzz test with "make fuzz"

## 4/28

-   Compiled Sean's random command generator using "make fuzz"

## 4/29

-   Created a patch for local SVN changes

## 4/30

-   Compiled new make fuzz target which runs random commands -- already
    finds bugs
-   Need to find how to record code coverage and improve it