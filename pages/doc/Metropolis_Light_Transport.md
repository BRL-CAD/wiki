The Metropolis Light Transport algorithm consists of a bidirectional
path tracer and uses Monte Carlo method for randomly mutating the paths.
Each mutation is accepted or rejected based on carefully chosen
probability, which prevent a path that passes through an object to be
accepted. Then an estimation is made by sampling many paths, and
recording their locations on the image plane.

------------------------------------------------------------------------

## About MLT

The MLT algorithm is an unbiased solution to the rendering equation - it
computes the correct lighting in the average. For this algorithm, any
error in the final result is due to random variations among the samples
(image noise) and it can me estimated by simply adjusting the sample
variance.

The algorithm consists of tracing paths from the light source to the
camera lens and then mutating those paths, by randomly adding, excluding
or replacing a vertex. Not all mutations are automatically accepted -
each one has a chance to be rejected, depending on the relative
contribution of the new and the old paths. This assures that invalid
paths are not accepted.

After each successful mutation, the final image (two dimensional array
of pixels) is updated by finding the pixel (u, v) associated to each
visible path node (x, y, z). Each sample is weighted equally - the light
and dark areas of the final image are a result of the amount of sample
recording in each area.

------------------------------------------------------------------------

## Implementation

The algorithm will be written in C, so there would be no need for
additional classes defining points and vectors and no compatibility
issues. The structures already present, that define the basic types,
such as points, vectors and data structures, will be used. Code will be
written in src/rt.

### Bidirectional Path Tracer

The path tracer will use rt_shootray() function to create paths. The
paths will reflect and mutate based on a reflection model and the
already implemented Phong Model and shaders can be used to handle that.

The BPT is a two pass algorithm, with two rays being shot - one from the
camera and the other from the light source). Since creating and
reflecting the paths will work basically the same way, there shouldn't
be any problems to use the same functions to do both.

### Path Mutation

This is the heart of the MLT algorithm - the random mutations on the
paths. The mutations can be accepted or rejected based on probability
and/or reflection models.

### Useful Libraries

There are libraries already existent that will help immensely in the
project. These libraries are librt, libbn, libbu and liboptical.

#### librt

This library will be extremely important to the development as it
contains the raytracer that will be used to shoot and treat paths. The
path concept is similar to the rays, so probably there will be no need
for further enhancement or extension.

The paths will be started by rt_shootray() and a new function will be
written to treat hits and misses, similar to ray_hit() and ray_miss().

#### liboptical

Liboptical contains shaders and the phong model, that can be used to
handle reflection and to verify valid paths.

The interaction with the upper layers of the code would happen through
the get_args() function, in src/liboptical/opt.c. The lighting model
option would have to be selected and then a unique number, to represent
the MLT algorithm, would have to be given too. Then, some arguments,
specific to MLT, could be provided by the user, like amount of rays to
be shot, a random seed for the mutation algorithm, and others.

#### libbn

Libbn contains mathematical definitions that will be relevant to the
algorithm.

#### libbu

Libbu will be useful because of the utility functions and macros, such
as bu_list() and bu_malloc().

------------------------------------------------------------------------

## Milestones

1.  Implementation of a bidirectional path tracer - including correct
    determination of obstacles in the path (by using librt functions).
    1.  Initial design, rt_shootray() function will be used to shoot
        rays and detect collision.
    2.  Implement, using step 1.1, the path tracing function, that will
        record the points where the rays hit (structure hit).
    3.  Use the reflection model and implement it in the path tracing
        function.
    4.  Implement a way for the algorithm to detect how to connect the
        paths.
2.  Implement the path mutation algorithm.
    1.  Implement existing nodes mutation.
    2.  Implement new nodes mutation.
3.  Implement an algorithm to sample each pixel - including correctly
    detecting the coordinates in the 2D image of the path vertexes.
4.  Assemble those milestones together in the implementation of the
    final algorithm.

------------------------------------------------------------------------

## Timeline

(log available at <http://andrecastelo.wordpress.com/>)

-   Until May 26th: studying the source code, getting familiar with the
    mentors and studying the MLT and the Bidirectional Path Tracer
    algorithm.

<!-- -->

-   From May 26th to June 20th: implementation of an efficient
    bidirectional path tracer:

<!-- -->

-   From June 20th to July 1st: implementation of the path mutation
    algorithm. It will use pseudo random numbers in order to mutate the
    nodes.

<!-- -->

-   From July 1st to July 15th: implementation of the algorithm to
    sample each pixel. The paths will start from the screen and from the
    light source. If path nodes could hold information about the
    starting pixel, this would be easier.

<!-- -->

-   From July 15th to August 1st: assembly of the parts and
    implementation of the final MLT algorithm.

<!-- -->

-   From August 1st to August 18th: this period will be used to fix the
    remaining bugs, write documentation and/or implement any missing
    features.