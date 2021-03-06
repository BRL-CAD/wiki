## Shaders

A shader is a way to assign visual material properties to geometry. They
are applied to regions.
To apply a shader to a specific region:
1.Create the model (in our case a sphere: my.sph) and save it as a
combination/region(sph.r).

[Create a Sphere Using MGED](image:_ShadersShot1.png.md)

2\. Go to the “Edit” button on your Graphics Window/Command Window then
click “Combination Editor” button.

[MGED Edit Menu](image:_ShadersShot2.png.md)

3\. A new window will open. Hit the button on the right of the Name
zone, click “Select from all” and chose the region you want to edit.

[Combination Editor](image:_ShadersShot3.png.md)

4\. Hit the “Show Shader” button.

[Show Shader](image:_ShadersShot4.png.md)

5\. The window will change and you will be able to see the appearance
properties of your region. Default shader for unspecified geometry is
“plastic”. You can edit it by choosing from the list that opens if you
click the button on the right of the shader zone.

For you to get the 3D shape you have to raytrace your model. To do that
you must write in the Command Window “B sph.r” and then “rt”, after
avery change you make to your model. A new window will open with the
raytraced model.

(sph.r is the example model. Where sph.r is written you should write
your models name.)

[Raytracing in MGED](image:_ShadersShot5.png.md)

**Default:**

[Default Raytraced Sphere](image:_ShadersShot6.png.md)
[Modifying Attributes](image:_ShadersShot7.png.md) [Object
Properties](image:_ShadersShot8.png.md)

6\. Change the Transparency, mirror reflectance, Specular reflectivity,
Difuse reflectivity, Refractive index, Extinction, Shininess and
Emission values, raytracing at the same time, so you can find the shader
you want.

**Blue mirror:**

[Blue Mirror Attributes](image:_ShadersShot9.png.md) [Blue
Mirror](image:_ShadersShot10.png.md)

7\. If you want to apply more then one material property you can choose
stack from the list. Use the “Add shader” button to add as many shaders
you want.

[Add Shader](image:_ShadersShot11.png.md)

**Example:**

[Set up Shader](image:_ShadersShot12.png.md) [New Settings
Example](image:_ShadersShot13.png.md)

You should note that the ordering of the shaders matter.

If you change their order...

[Different Order](image:_ShadersShot14.png.md)

You get...

[New Example](image:_ShadersShot15.png.md)

Here you can find an Introduction to MGED and Shaders presentation:
[Documentation](../Documentation.md)
