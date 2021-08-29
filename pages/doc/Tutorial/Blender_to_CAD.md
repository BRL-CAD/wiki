1\. Open Blender
![](../img/Blender_Step_1.jpg)

2.Use the scale manipulator to flatten and expand the cube so it looks
like a tabletop.
![](../img/Blender_Step_2.jpg)

3.Go to the Add menu or use the shortcut Shift+A. Add a cube.
![](../img/Blender_Step_3.jpg)

4.Use the scale manipulator to expand and flatten this cube so it looks
like a table leg. Then duplicate this table leg 3 times.
![](../img/Blender_Step_4.jpg)

5.Move the legs of the table so it represents a table.
![](../img/Blender_Step_5.jpg)

6.Select all the legs and the tabletop, and then click joins on the left
side of the window under Object.
![](../img/Blender_Step_6.jpg)

7.Go to File on the top left corner and select export. Under the export
select obj.
![](../img/Blender_Step_7.jpg)

8.You will get an export window. Name your file test (optional).

9.Once you have named your file click on the Export OBJ button, which
can be found in the top right corner, to export your blender file.
![](../img/Blender_Step_9.jpg)

10.Go to the BRL-CAD bin directory and give the command to turn you obj
file into a .g file. This command exports the obj-formatted file to a .g
file. The syntax of the obj-g command is

`>obj-g input.obj output.g  `

Don’t forget to enter a path for your files. To see all the uses of the
obj-g command just enter “obj-g.”

11.Open mged. You will see two windows, a command window that is white
and a graphics window that is black.

|                                                    |                                                                      |
|----------------------------------------------------|----------------------------------------------------------------------|
| ![](../img/MGED_7.22_Step_11.jpg) | ![](../img/MGED_7.22_Graphics_Step_11.jpg) |

12.Select File and click open. Open you .g file that you just made.
![](../img/MGED_7.22.0_Command_Window_Step_12.jpg)

13.Then click on Tools. Open Geometry Browser under tools. Double click
on the top object to display it.
![](../img/MGED_7.22.0_Command_Window_Step_13.jpg)

![](../img/Geometry_Browser_Step_13.jpg)

14.Click on View. Select “az35,el25”
![](../img/MGED_7.22.0_Command_Window_Step_14.jpg)

15.Click on Tools once again. Select the Raytrace Control Panel. Hit the
raytrace button.
![](../img/MGED_7.22.0_Command_Window_Step_15_-1.jpg)

![](../img/Raytrace_Control_Panel_Step_15_and_16_-4.jpg)

![](../img/MGED_7.22_Step_15_-2.jpg) Once you
have Raytraced, you should have an image the looks like this:
![](../img/MGED_7.22_Step_15.jpg)

16.Do you remember what the table looked like when we were done with it
in Blender? It was upside down and now it’s on its side. Rotating the
table reorients it correct way. To reorient your table the right way,
enter these commands in the command window:

` sed default.1.1.b.c.s `

|                                                          |                                                                            |
|----------------------------------------------------------|----------------------------------------------------------------------------|
| ![](../img/MGED_7.22_Step_16_-1.jpg) | ![](../img/Fullscreen_capture_Step_16_-1.jpg) |

` rot –90 0 0 `
`{| border="0"`

\|-
\|![](../img/Fullscreen_capture_Step_16_-2.jpg)\|\|![](../img/Fullscreen_capture_Step_16_-2_-2.jpg)
\|}

` accept `
`{| border="0"`

\|-
\|![](../img/Fullscreen_capture_Step_16_-3.jpg)\|\|![](../img/MGED_7.22_Step_16_-3.jpg))

With that final rendering your import is complete!
![](../img/MGED_7.22.0_Graphics_Window_Step_16_-5.jpg)
)
