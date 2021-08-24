## Types of Implicit Parameters

At the level of constraint networks, calculations are done in terms of
Variables or indpendent real values / floating point numbers. But in the
construction of geometry these are clustered together in terms of
implicit parameters. Typical implicit parameters are

1.  **Vectors** - A 3 dimensional vector is a 3-tuple which is used to
    hold direction as well as magnitude. In BRL-CAD primitives, they may
    represent
    1.  Radius vectors ( Center of a sphere)
    2.  Direction vectors (Direction of a plane)

## Types of Implicit Constraints

An enumeration of the set of contraints observed in the primitives below

1.  **Modulus Comparison** : Comparison of the modulus of a vector to a
    real number ( 0 for non-negativity ) or the modulus of another
    vector
2.  **Perpendicularity of Vectors**

## Implict Constraints by Primitive

### ell (Ellipse)

Ellipse is built using the Center (radius vector V) and 3 Vectors (A, B,
C st. \|A\| = radius) 2 types: Non-negativity/Modulus comparison,
Perpendicularity Constraints:

1.  \|A\| &gt; 0
2.  \|B\| &gt; 0
3.  \|C\| &gt; 0
4.  A.B = 0
5.  B.C = 0
6.  C.A = 0

### rec (Right elliptical cylinder)

3 types: Non-negativity/Modulus comparison, Perpendicularity, Vector
equality

Constraints:

1.  \|H\| &gt; 0
2.  \|A\| &gt; 0
3.  \|B\| &gt; 0
4.  A = C
5.  B = D
6.  A.B = 0
7.  H.A = 0
8.  H.B = 0

### rhc (Right hyperbolic cylinder)

3 types: Non-negativity/Modulus comparison, Perpendicularity

Constraints:

1.  \|H\| &gt; 0
2.  \|B\| &gt; 0
3.  \|R\| &gt; 0
4.  H • B = 0
5.  c &gt; 0
6.  \|B\| ≥ c

### rpc (Right parabolic cylinder)

2 types: Non-negativity/Modulus comparison, Perpendicularity

Constraints:

1.  \|H\| &gt; 0
2.  \|B\| &gt; 0
3.  \|R\| &gt; 0
4.  H.B = 0

### sph (Sphere)

Sphere is a particular case of the ellipse

Constraints: 2 types: Modulus comparison, Perpendicularity

1.  \|A\| &gt; 0
2.  \|B\| &gt; 0
3.  \|C\| &gt; 0
4.  \|A\| = \|B\|
5.  \|A\| = \|C\|
6.  \|B\| = \|C\|
7.  A.B = 0
8.  B.C = 0
9.  C.A = 0

### tgc (Truncated General Cone)

Constraints: 5 types: Modulus comparison, Logical Combination,
Perpendicularity, Non-planarity, Parallelism

1.  \|H\| &gt; 0
2.  \|A\| & \|B\| not zero together
3.  \|B\| & \|D\| not zero togehter
4.  \|A\|\*\|B\| and \|C\|\*\|D\| not zero together
5.  H is nonplanar to AB plane
6.  A.B = 0
7.  C.D = 0
8.  A \|\| C ( A is parallel to C )

### tor (Torus)

Tor is built using the following input fields

`V    V from origin to center`
`H    Radius Vector, Normal to plane of torus.  |H| = R2`
`A, B     perpindicular, to CENTER of torus.  |A|==|B|==R1`
`F5, F6   perpindicular, for inner edge (unused)`
`F7, F8   perpindicular, for outer edge (unused)`

Constraints: 2 types: Modulus comparison, Perpendicularity

1.  \|A\| = \|B\|
2.  A.B = 0
3.  B.H = 0
4.  H.A = 0
5.  \|H\| &gt; 0
6.  \|H\| &lt; \|A\|