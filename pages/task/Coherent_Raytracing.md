Contact "brlcad" on irc.freenode.net

BRL-CAD has one of the oldest and fastest parallel ray tracing
implementations around but we don't currently leverage modern techniques
that minimize context switching and data access. With implicit geometry
and constructive solid geometry (CSG) Boolean operations, we also have a
very different approach to ray tracing that has its own set of academic
challenges.

Your project is to help us introduce a data-coherent pipeline into
BRL-CAD using ray bundling, packet tracing, and cache-coherent
processing. Currently, the ray tracer shoots one ray at a time. Your
objective is to make it shoot postage stamps at a time (e.g., 32x32)
while evaluating all of those rays simultaneously.

Difficulty: Medium to Hard

Languages: C