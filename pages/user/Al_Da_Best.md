## Personal Information

Name: Alex Taylor
Email: alex.taylor42@live.co.uk
IRC Name: Al_Da_Best
Brief Background: I am 18 years old, in my first year studying
Aeronautical Engineering at [Loughborough
University](http://lboro.ac.uk/) (UK). I left College with high grades
in maths, physics and computing, with maths being my strongest point
academically.

## Google Summer of Code 2012

The current simulation available in BRL-CAD has not been developed in
depth, and is quite limited in its implementation. It can currently only
simulate very basic situations in vacuums. For this project I aim to
vastly improve this area by adding additional features such as variable
fluid for the object to fall through, a variable ground surface which
would allow simulating reactions from it through use of the coefficient
of restitution and other such formulae. Another feature would be to
allow for variable gravity, since gravity is weaker at greater distances
from the Earth, and indeed other large masses. After some thought and
looking at the available physics engines I have opted to go with the
Bullet engine. The reasons for this include its superior capability to
constantly check for collisions, combined with its relatively fast
simulations compared to, say, ODE and it is already integrated to some
extent into BRL-CAD.

[Project Details](Al_Da_Best/gsoc2012project.md)

[Development Log](Al_Da_Best/devlog.md)
