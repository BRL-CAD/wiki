------------------------------------------------------------------------

# Notes on Class Diagrams

-   Once Use Cases have initially been grouped together, then Classes
    need to be identified.
-   Categorize classes into *entity*, *boundary*, or *control*.
    -   Entity classes contain long term data.
    -   Boundary classes interface with actors.
    -   Control classes encapsulate a use case's behavior.





# Class Diagram Legend

![](../img/ClassDiagramInitial.jpg)





-   Classes are drawn as boxes with 3 divisions:
    -   (top)Class name
    -   (mid)Attributes (or members, or fields)
    -   (bottom)Methods (or functions)
-   Arrows between Classes indicate an association
    -   Numbers on each end of the line indicate Multiplicity.
        -   Example: The line between Student and Enrollment has a 1 on
            the student side and a 1..\* on the Enrollment side. This
            simply means that 1 Student Object can have 1 to inifinite
            amound of Enrollment objects. Read the other way, it means
            that any of many Enrollment objects can only have 1 Student
            object each.
    -   The direction of the arrow indicates 'knowledge of.'
        -   Example: **Student** has knowledge of **Enrollment** but
            **Enrollment** objects have no knowledge of **Student**
            objects.
-   Text descriptions written on the Arrow help add understanding to the
    association.
    -   Example: A **Student** is *enrolled*, via an **Enrollment**
        object, *in* a **Seminar**.
