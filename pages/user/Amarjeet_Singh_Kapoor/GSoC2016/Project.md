# **[User Interface for Customizing Models](https://github.com/openscad/openscad/wiki/Project%3A-Form-based-script-parameterization)**

## **Personal Information**

**Name:**Amarjeet Singh Kapoor

**Email Address:** <amarjeet.kapoor1@gmail.com>

**IRC Username:** amarjeet

**Phone number:** +91 8568988521

**Blog**: <https://amarjeetkapoor1.wordpress.com>



## **Brief Background Information**

I am 3rd year B.Tech student of Computer Science and Engineering at Guru
Nanak Dev Engineering College, Ludhiana, India.


A few of the numerous projects I have worked on are briefed below:

-   I have worked on Image Processing using OpenCV.
-   I have made a project "Civil Octave" for the Analysis of Dynamics of
    Structures.
-   Currently, I am working on completely new idea i.e SIM (Structure
    Information Model). Idea behind the project is modeling the
    structure based on information and storing it in database so that
    information can be used for analysis.


For more details, my Github account can be referred:
[<https://github.com/amarjeetkapoor1>](https://github.com/amarjeetkapoor1)


I have knowledge of C++, Python, Shell scripting, HTML, CGI, SQL, LaTeX,
doxygen, etc.

## **Project Information**

### **An Overview**

This project is based on the User interface of OpenSCAD Software. The
main idea of this project is to provide users with features to change
certain variables or parameters in .scad file using form like interface
which may include slide bar, check box, text box, ranges etc. so that we
can visualize the changes in output on the basis of input side by side
instead of manually changing different parameters. It will help the user
able to create the templates for given model which can further be
changed as per user's requirements.

### ***Detailed Description***

The basic implementation of the this project is almost done in form of
prototype. There is need to modify structure of the project.We have to
divide the task in to there parts: ![](../../img/image05.png)

<dl>
<dt>

**Front end**

</dt>
<dd>

It will deal with how the parameter will look to user like in form of
range or spinbox etc. This part will include two parts:

<dl>
<dt>

*Individual Parameter*

</dt>
<dd>

This will define how individual parameters will look like

</dd>
<dt>

*Container Widget*

</dt>
<dd>

This will contain UI features common to all parameter. This widget will
contain all parameter widget.

</dd>
</dl>
</dd>
<dt>

**Back end**

</dt>
<dd>

This will include the parser part that will create AST nodes and we can
extract the parameters from the AST. we can use the single parser for
whole .scad file or separate parser for extracting the parameters with
annotations.

The Back end part will also include the parameter extractor and injector
or the injector can be included in parameter object which will serve as
interface

</dd>
<dt>

**Interface**

</dt>
<dd>

This will include the parameter object which will serve as interface
between both Back end and Front end. Parameter object will contain
information regarding each individual parameter like parameter name,
default value and information how these parameter will be displayed as
widgets to user. Parameter object could also include the method to
inject the value of individual parameter in to the AST.

</dd>
</dl>

![](../../img/main.jpg)

There is need to modify some existing features and to enhance its
functionality so that it could be more interactive and user friendly. We
can improve its UI for parameter window by adding the following new
features under the scope of this project

1.  **Option to specify input widget**
    >
    > At present, input type widget in the output form is automatically
    > identified based upon the values specified by user in annotation.
    >
    > With this feature we want to provide additional functionality to
    > users that gives them additional control about the type of input
    > widget i.e they can choose between different widgets like spinbox,
    > vertical slider, horizontal slider, drop box, text box etc for
    > getting the value of parameter through parameter window from user.
    > And we can provide some more features like specify the increment
    > value in range widget and some additional features like:
    >
    > 1.  We can use syntax like
    >     *@parameter(\["spinbox"\],\[1:10\],\[2\])* which will make a
    >     spinbox with value range between 1:10 and will increment next
    >     value by 2 as we increase values in spinbox.
    > 2.  If user specifies *@parameter(\[1:10\])* then it will take the
    >     default input widget like it's working in its present state.
    >
    > We will extend the code in *ParameterEntryWidget::setValue()*for
    > implementation purpose. Following will be GUI widgets that will be
    > supported in the scope of this project:
    >
    > <dl>
    > <dt>
    >
    > Proposed syntax
    >
    > </dt>
    > <dd>
    >
    > parameter(\[ InputType,attributes\],\[values\])
    >
    > </dd>
    > <dt>
    >
    > Input widget options
    >
    > </dt>
    > <dd>
    >
    > 1.  Spinbox
    >     -   attributes -: min value, max value, increment size
    >     -   E.g. parameter(\[“spinbox”,IS\],\[ MinValue : MaxValue \])
    > 2.  Checkbox
    >     -   E.g. parameter(\[“checkbox”\],\[true\] )
    > 3.  radio button
    >     -   options -: name of first value while be default
    >     -   E.g.
    >         parameter(\[“radiobutton”\],\[firstvalue,secondvalue,...\]
    >         )
    > 4.  Vector
    >     -   Attributes -:min value ,max value, increment size
    >     -   Question -: Max number of spinbox to be supported?
    > 5.  slider (horizontal)
    >     -   attribute -: min value, max value, increment size(IS)
    >     -   E.g. parameter(\[“Hslider”,IS\],\[ MinValue : MaxValue\] )
    > 6.  slider (vertical)
    >     -   attribute -: min value max value
    >     -   E.g. parameter(\[“Vslider”,IS\],\[ MinValue : MaxValue\] )
    > 7.  Text-:
    >     -   attribute-: size of text
    >     -   E.g. parameter(\[“Text”,size of text\] )
    > 8.  Default -: When no input parameter widget is specified like at
    >     present stage.
    >     -   E.g. Parameter(\[1 : 10\])
    >
    > </dd>
    > </dl>

2.  **Grouping of parameters**
    >
    > At present, the parameter widget are shown as individual widget.
    > We can group the related or alike parameters. This feature will
    > help in grouping the parameters which are related and we can make
    > the group of parameter collapse or expand to provide better user
    > interface and more useful for bigger models.
    >
    > One of the two syntaxes from below can be used:
    >
    > 1.  *@group("name")* before *@parameter()* to specify which group
    >     the parameter belongs else they will be displayed as
    >     individual parameters.
    > 2.  We can use *@parameter( , , group="name")* where group is
    >     optional parameter in *@parameter* annotation.

3.  **Reflecting changes made to variable's value through form**
    >
    > At present, if we make any changes to the value of parameterized
    > variable, we cannot save those changes by assigning that new value
    > to the variable automatically and for that we have to manually
    > change that variable's value.
    >
    > A save button can be provided with the help of which the values
    > given through variables can be saved i.e. changes we made to model
    > through form are temporary and don't exist after we open that
    > model file again but we can make it permanent in program.
    >
    > e.g. We can give a save button on top of parameter list which will
    > save the new values in the .scad file and we can give optional
    > save button for saving the individual parameter in parameter
    > window.

4.  **Make UI better**
    >
    > We can make UI of the parameter window better by providing
    > additional features like:
    >
    > 1.  Make individual input widgets dockable so that we can adjust
    >     the position of the individual input widgets.
    > 2.  Make description hover the input widget when we hover cursor
    >     over that input widget.
    > 3.  Make the input widgets more space efficient.
    > 4.  Option to minimize the parameter and library window instead of
    >     just hide option.
    >
    > And their can be many more based upon the user's feedback.

5.  **Resolve issues found with existing code** There are some issues
    > with existing code like if we change the value in @parmameter then
    > changes are reflected on parameter window but if we change the
    > value of parameterized variable then no corresponding change occur
    > on the parameter window for viewing new input widget based upon
    > the change in value of parameterized variable we have to reopen
    > the file. e.g. For an instance in following screenshot 1,
    > everything is correct. ![](../../img/image07.png)
    > But if the value of G=False and resolution=\[10,34,45\] are
    > changed from their initial value of G=0 and resolution=10, than
    > result is screenshot 2 but instead it should be as per screenshot
    > 3 which is obtained on re-opening the document.
    > ![](../../img/image06.png)
    > ![](../../img/image03.jpg)
    >
    > We can do this by not only storing the parameters based on name
    > only but by both name of parameter and Type of data in parameter.

6.  **Saving scad file without annotation**(optional)
    >
    > After making all the changes in model we can save those changes in
    > file without annotation code which will make scad file backward
    > compatible.

## **Milestones**

**Community Bonding Period**

-   Interaction with the community and get to know about the existing
    code.
-   Study existing parameter widget code and will try fixing some
    existing bugs.

**23rd May-9th June**

-   Make Front end ( UI part) separate from rest of code. 
-   Make different object for different input option to be supported.
-   Check each use case associated with each parameter widget. 
-   Improve UI 
-   Take community feedback for further changes 
-   Documentation 

**10th June-26th June**

-   Make interface between Frontend and Backend (parameter object) 
-   Structure it to make it independent for back-end 
-   Code to inject parametric values in AST
-   Solving issues found by other people on using this code. 
-   Documentation 

**Mid term** **27th June-24July**

-   Start with back-end  
-   Take community feedback on syntax to be supported  
-   Code to Parse the .scad file to recognize parameters 
-   Code to extract the required parameter info from (AST) 
-   Write Back-end to support the user specified input widget  
-   Work on feature of Grouping of Parameters. 

**25th July -14th August**

-   Add feature to save current value of parameter as default 
-   Write example .scad file for the new features added after mid term. 
-   Add feature of Saving scad file without annotation. 
-   Add any Additional feature required. 

**15th August- 23August**

-   Testing and cleaning. 
-   Time to make up for missed milestone (if any). 
-   Finalize everything 

**23August onwards**

-   **FINAL EVALUATION**



## **Time Availability**

I will be available 40 hours / week, if needed can spend more .

## **Why OpenSCAD?**

I liked the concept of OpenSCAD (CAD for programmers) during the
different seminars that were conducted regarding the OpenScad in our
group. When I saw your project of Form based script parameterization I
found it really interesting that we can make a template of the model and
then change the model based on the form based parameter.

## **Why me?**

I am really enthusiastic to contribute in such a project which can
improve user experience. I believe that I am a quick learner and this
opportunity would enhance my skills. I truly feel that I will be
maintaining and cherishing this bond in terms of time-to-time
contribution in future also and would be a valuable asset to the
organization.

