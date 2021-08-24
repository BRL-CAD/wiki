__NOTOC__

------------------------------------------------------------------------

# Notes on Use Cases

-   A use case is a sequence of interactions that describes one clear
    goal for the user.
-   One or many Use Cases may make up the functionality described in a
    single [Requirement](GS_Requirements_Standard.md).





# Sample Use Cases

-   Identified Actors for the GS Network Library:
    -   Network
    -   GS Application that uses GSNetLib



==1. List all Use Cases for an Actor== The Actor 'Network' has the
following use-cases:

-   Transport message to GSNetLib
-   Transport message from GSNetLib


The Actor 'GS Application' has the following use-cases:

-   Open new connection
-   Close connection
-   Listen for new connections
-   Place Message into SendQueue
-   Retrieve Message from ReceiveQueue


==2.Detail Each Use-Case (Pseudo-Formally)==

-   Usually written somewhat vaguely, so as to describe a process, but
    not detail how to implement code.
-   This can be difficult for describing complex Use Cases. In this
    event, use of a form of pseudo code is acceptable.




### Ex 1: OpenNewOutBoundConnection


**Use Case**: OpenNewOutBoundConnection

**Initiating Actor**: GS Application

**Participating Actors**: (none)

**Preconditions**: (none)

**Primary Flow**:


1 Initiating Actior (IA) requests a new *connection object*, providing
hostname and port.

2 The *connection object* attempts to connect to *hostname* on *port.*

3 If connection is successful, GSNetLib returns a connected *connection
object*

<!-- -->


**Alternative Flows**


**Extention Point**: During step \#3.

**Precondition**: The connection is not successful.


3.1 GSNetLib returns a null object.

**Remerge Point**: None. Alternative end to use case.




### Ex 2: OpenNewInBoundConnection


**Use Case**: OpenNewInBoundConnection

**Initiating Actor**: GSNetLib Listener

**Participating Actors**: (none)

**Preconditions**: (none)

**Primary Flow**:


1 Initiating Actior (IA) requests a new *connection object*.

2 If connection is successful, GSNetLib returns a connected *connection
object*

<!-- -->


**Alternative Flows**


**Extention Point**: During step \#2.

**Precondition**: The connection is not successful.


2.1 GSNetLib refuses the incoming connection.

**Remerge Point**: None. Alternative end to use case.
