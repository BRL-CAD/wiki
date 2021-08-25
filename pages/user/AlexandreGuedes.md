## SoC Applications: "Geometry file importers to BRL-CAD"

#### Patche

I did a simple patche, it's just to show that I had build brl-cad
correctly and I know how compile and use the development environment.

<https://sourceforge.net/tracker/?func=detail&aid=2765100&group_id=105292&atid=640804>

#### Abstract

Nowadays there are many geometry formats files, each one is more
appropriate to a different application field. Consequently it is
necessary to CAD softwares to support as many file formats as possible,
aiming to reduce users' efforts.

#### Content

**Name**: Alexandre Strapação Guedes Vianna

**Email / IRC** Email: strapacao@gmail.com

IRC nick: AlexandreGuedes

##### **Context**

Nowadays there are many CAD format files, each one is more appropriate
to a different application field. Consequently it is necessary to CAD
softwares to support as many file formats as possible, aiming to reduce
users' efforts. Currently BRL-CAD is not totally compatible with some of
most popular CAD file formats, such as VRML, X3D and OBJ. Actually
according to table 1 BRL-CAD can only export to previously cited
formats. To BRL-CAD would be very interesting if models could be
imported from these formats.

![](/wiki/user/img/ConverterTable.jpg)

##### **Synopsis**

I intend to develop CAD importers to BRL-CAD. The project's main idea is
to write model importers - OBJ, VRML and X3D formats - to BRL-CAD, which
would be respectively called obj-g, vrml-g and x3d-g. Figure 1 show the
work scope.

![](/wiki/user/img/WorkScope.jpg)

##### **Benefits to BRL-CAD**

Add importers would increase BRL-CAD level compatibility with CAD file
formats. Users will have a direct way to import their models to BRL-CAD,
in other words they should avoid taking alternatives ways that can
increase errors. As example of compatibility same of popular 3D graphics
application like Blender can export to OBJ, VRML and X3D.

##### **Deliverables**

The main deliverables is implementing the obj-g converter, it requires a
hard study about BRL-CAD model representation.

The secondary deliverables is implementing another importers such as
vrml-g and x3d-g.

##### **Project Schedule**

The work can begin immediately. Currently, I’m in between university
terms, so currently I’m not attending any classes. Classes will begin
near mid April, and if time becomes a problem, one or two disciplines
may be dismissed and done later. I also work at the university; I am a
trainee in a computer graphics and virtual reality laboratory which
demands \~20 weekly hours. But I do intend focusing on GSoC, and will do
my best to give BRL-CAD 30+ weekly hours. That being said, the summer
plans are detailed below:

1\. April 20th \~ May 11th

This is referred by Google as the Community Bounding Period. It will be
used to study the problem and the source code, analyzing other
converters like g-obj. Finishing this period I should be familiarized
with BRL-CAD code and understanding structures to represent models in
BRL-CAD. Also I will implement some samples about reading BRL-CAD
models.

2\. May 11th \~ June 15th

Beginning of the program. In this period, I'll research and implement
the OBJ importer; write code documentation; test the importer.

3\. June 15th \~ July 13st

In these weeks, Just like step 1 I plan to implement another importer
probably the VRML importer.

4\. July 13st \~ July 27th

If I had already done step 1 and step 2 I can develop the X3D importer,
else I will be concentrating my efforts in finish dependences.

5\. July 27th \~ August 10th

Although I'll test each importer in their respective periods, I think it
is useful to allocate time to handle unexpected issues and testing.

6\. August 10th \~ August 17th

I’ll use this last week to refine code and documentation.

##### **About me**

I am Alexandre Strapação Guedes Vianna and I am 22. I study Computer
Science at the Federal University of Paraiba, in João Pessoa, Brazil.
Currently I am a trainee at LabTEVE\[1\] a computer graphics and virtual
reality laboratory. Since youth I always had interest for computers and
programming and too much curiosity about how programs were done. I used
to develop some scripts to games like Ultima Online, unavoidably I
started Computer Science course. My experience with big open source
projects is not that great but I'm here to learn and to contribute with
BRL-CAD project. During the graduation course I had many academic
experiences and few practices. The possibility of get a good practice
with BRL-CAD project is a great motivation. Also, I intend to continue
contributing on BRL-CAD after the summer. The participation in GSoC
might also be of great help in my intentions on spending some time
studying/working abroad after graduation.

##### **Other information and links**

Résumé :

Portuguese
<http://buscatextual.cnpq.br/buscatextual/visualizacv.jsp?id=K4218973E8&tipo=completo&idiomaExibicao=1>

English version (Incomplete)

<http://buscatextual.cnpq.br/buscatextual/visualizacv.jsp?id=K4218973E8&idiomaExibicao=2>

Sample code

In this project I develop an obj-&gt;opengl importer.

<http://sites.google.com/site/alexandrestrapacaoproject/Home/sample.rar?attredirects=0>

Paper

<http://sites.google.com/site/alexandrestrapacaoproject/Home/SBAC.doc?attredirects=0>

\[1\] <http://www.de.ufpb.br/~labteve/english/index.html>

\[2\] <http://www.uoherald.com/news/>
