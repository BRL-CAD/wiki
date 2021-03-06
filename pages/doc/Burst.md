**burst** is one of multiple [BRL-CAD
Commands](BRL-CAD_Commands.md).

## Running BURST

For a detailed overview of burst, see the burst man page (TODO - add
link to this when we get it online...)

To do a basic burst run, the first step is to define a burst command
file. The following is a simple example based on the ktank.g model
distributed with BRL-CAD (we'll refer to this file as ktank.b):

    units                   inches
    shotline-file           ktank_burst.shotlines
    error-file              ktank_burst.log
    plot-file               ktank_burst.plot
    image-file              ktank_burst.pix
    burst-file              ktank.burst
    burst-air-file          ktank_air.ids
    burst-armor-file        ktank_armor.ids
    critical-comp-file      ktank_crit.ids
    color-file              ktank_burst_colors
    burst-distance          0
    cell-size               16
    attack-direction        0 0
    max-spall-rays          50
    cone-half-angle         45
    target-file             ktank.g
    target-objects          tank
    report-overlaps         no
    shotline-burst          yes
    #ground-plane           yes 66 200 200 200 200
    execute

We also need to create a number of support files to specify idents:

ktank_air.ids:

    2-3
    5

ktank_armor.ids:

    100-121

ktank_crit.ids:

    618-839
    940-949

We deliberately don't create a file named ktank_burst_colors, to
provide an error to log.

We also need to copy the ktank.g database from share/db/ktank.g into the
current directory. With this setup, burst can be run with the command
line command:

     burst -b < ktank.b

## BURST Results

The results should be as follows:

ktank.burst:

    1    0.0000   0.0000  0.00     256.00 inches  0.028755
    2  -48.000  -48.000
    3    87.87    29.73   512  1  -0.133  180.00   0.991 0
    3    51.87    29.73   513  1  -0.133  180.00   0.991 0
    3    15.87    29.73   514  1  -0.133  180.00   0.991 0
    3   -20.13    29.73   515  1  -0.133  180.00   0.991 0
    3   -56.13    29.73   516  9  -0.133  180.00   0.991 0
    2   48.000  -48.000
    3    87.87    29.73   505  1  -0.133  180.00   0.991 0
    3    51.87    29.73   506  1  -0.133  180.00   0.991 0
    3    15.87    29.73   507  1  -0.133  180.00   0.991 0
    3   -20.13    29.73   508  1  -0.133  180.00   0.991 0
    3   -56.13    29.73   509  9  -0.133  180.00   0.991 0
    2  -48.000  -32.000
    3   125.55    15.10   517  1  -0.727  180.00   0.686 0
    ...

ktank_burst.shotlines:

    1    0.0000   0.0000   16.00   55.04  -55.04   60.16  -61.02 inches
    2  -48.000  -48.000
    3    87.87  -0.133  180.00   512    29.73    29.73  1    0.00    0.00
    3    51.87  -0.133  180.00   513    29.73    29.73  1    0.00    0.00
    3    15.87  -0.133  180.00   514    29.73    29.73  1    0.00    0.00
    3   -20.13  -0.133  180.00   515    29.73    29.73  1    0.00    0.00
    3   -56.13  -0.133  180.00   516    29.73    29.73  9    0.00    0.00
    2   48.000  -48.000
    3    87.87  -0.133  180.00   505    29.73    29.73  1    0.00    0.00
    3    51.87  -0.133  180.00   506    29.73    29.73  1    0.00    0.00
    3    15.87  -0.133  180.00   507    29.73    29.73  1    0.00    0.00
    3   -20.13  -0.133  180.00   508    29.73    29.73  1    0.00    0.00
    3   -56.13  -0.133  180.00   509    29.73    29.73  9    0.00    0.00
    2  -48.000  -32.000
    3   125.55  -0.727  180.00   517    22.00    15.10  1   46.66   46.66
    3    78.39   0.933  180.00   512    30.00    10.77  1   68.96   68.96
    ...

as well as plot and pix files. (TODO - show example images...)
