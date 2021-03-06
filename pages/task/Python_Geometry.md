python-brlcad is an on-going effort to wrap BRL-CAD functionality with
python code (see References).

The project is in its early development stage, the source code allows
for now the scripting (read/modify/write) of only a selected set of
primitives using libwdb.

To complete the goal of this GSOC task, the rest of the primitives which
are not yet implemented would need to be done:

ARS, BINUNIF, BOT, BREP, CLINE, DSP, EBM, GRIP, HALF, HF, METABALL,
NURB, PG, SUBMODEL, SUPERELL, VOL, PNTS, ANNOTATION, HRT, CONSTRAINT

The following primitives are already wrapped, and can serve as example
for the rest:

ARBN, ARB, EHY, ELL, ELL, EPA, ETO, EXTRUDE, HYP, PIPE, PARTICLE,
REVOLVE, RHC, RPC, SKETCH, TGC, REC, TOR, COMBINATION

# References

-   <https://github.com/kanzure/python-brlcad>
-   <https://github.com/nmz787/python-brlcad-tcl>

# Requirements

-   Familiarity with C;
-   Strong familiarity with python