------------------------------------------------------------------------

# Notes on Packages

-   Packages are simply a graphical grouping of functionality.
-   They combine multiple [Actors](GS_Actors_Standard.md) and
    [Use Cases](GS_Use-Cases_Standard.md) that have some
    comonalities.
-   Packages can also be called Systems or Subsystems.
-   Packages do not have to define internal associations between
    different Use Cases.


Example:
![](Restaurant-UML-UC.png)


!!Replace graphic with GS example!!
\*The actors in this diagram are:

-   -   WaitStaff
    -   Patron
    -   Cashier
    -   Chef

-   The combined Use Cases for all the actors are:
    -   Order Food
    -   Serve Food
    -   Eat Food
    -   Drink Wine
    -   Pay For Food


Now, depending on how the developer was intending on implementing this
in code, one could easily say that sense all the actors 'is a' Person,
then they all need to 'Eat Food.' If this food is only the food served
at this resteraunt, then perhaps all the actors do not have to 'Eat
Food.' A simple Diagram like this has already helped to identify
ambiguity in a design!
