BRL-CAD does not currently have the ability to directly import .blend
files. Blender's file format had not been regarded as a good candidate
for writing a converter, but recently the gamekit project
<http://code.google.com/p/gamekit/> implemented an ability to read data
from .blend files.

This project would investigate the gamekit .blend file parsing ability
and map it to BRL-CAD's geometry and converter system. Bonus points for
proposals that add the ability as part of the new libgcv geometry
conversion library. A student wanting to propose this topic should look
into whether gamekit's parsing is robust enough to give us what we need
for BRL-CAD geometry files.

Requirements:

-   Familiarity with C/C++

Difficulty: low