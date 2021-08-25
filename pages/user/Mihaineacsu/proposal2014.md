## Student Information

`Name: Mihai Neacșu`
`Email: mihai.mneacsu@gmail.com`
`Telephone: +40 755 283 297`
`Time zone: UTC+02:00`
`IRC:  mihaineacsu`
`Source control username on github: mihaineacsu`
`Source control username on sourceforge: mihaineacsu`

## University Information

University: Politehnica University of Bucharest
Major: Computer Science
Current Year and Expected Graduation date: 4th year, 2014
Degree: BSc

## Abstract

BRL-CADs material database will help users list, share, download and
load material information and have that information be seamlessly
integrated with BRL-CADs modelling (Archer) and analysis (gqa) tools.
Part of this project will consist of creating a centralised repository
where users can perform the above mentioned actions. It will provide
users the means for searching, sorting/filtering, specifying, storing,
importing, exporting, and reusing material properties. The second part
of the project will consist of creating a command-line tool that uses
the online material database/repository in order to get/put material
data, create .density files (and other formats), or add material data to
a .g geometry file. Further on, emphasis will be put on integrating it
with BRL-CAD such as making it a part of the Geometry Editing Library
(libged).

## Detailed description

Server-side

Will provide a REST(Representational state transfer) API. Why REST?
Because REST is a simple way to organize interactions between
independent systems. It allows us to interact with minimal overhead with
clients.

How does it work? We operate on URLs and each URL identifies a resource.
These are exactly the URLs which are assigned to web pages.

So for e.g.. performing a GET request on mater.brl-cad.org/list will
provide us a with a JSON that the client will interpret and show to the
user in an organised way. The client can either be a running BRL-CAD
instance or the browser.

{

` "type": “BRL-CAD Materials List",`
` "format-version": "1.0.0",`
` "materials": [`
`   { `<material-details>` },`
`   { `<material-details>` }`
` ]`

}

where material-details JSON is: {

` "name": “Iron",`
` “id”: 3432,`
` “traits”: [`
`   “Density”: “7.87 g/cm^3”,`
`   “Specific Heat”: {“value”: “0.12 cal/g C”, “temperature”: 100 C”}`
` ]`
` "short": “Short description",`
` "screenshot-url": "`[`http://foo.com/screenshot.jpg`](http://foo.com/screenshot.jpg)`",`
` "version": "1.0",`
` "authors": [`
`   {`<author-details>`},`
`   {`<author-details>`}`
` ]`

}

where author-details JSON is: {

` "author-name": "Weiss Richard",`
` "author-contact": "some free text, probably email",`
` "author-url": "`[`http://a.nice.site/with/a/homepage.html`](http://a.nice.site/with/a/homepage.html)`"`

}

This is quite bloated but a simple version listing just the materials
and their properties might be more suitable when accessing the REST API
from BRL-CAD.

Proposed REST API:

GET mater.brlcad.org/list - list all available materials
GET mater.brlcad.org/list?id=MATERIAL_ID&name=MATERIAL_NAME - search
and list by MATERIAL_ID or MATERIAL_NAME
POST mater.brlcad.org/remove?id=MATERIAL_ID - remove MATERIAL_ID, only
available to some privileged authenticated users
POST mater.brlcad.org/update?id=MATERIAL_ID - add or update
MATERIAL_ID, only available to some privileged authenticated users
The last 2 resources require POST actions because they need credential
checks in the process. The ability to update/remove a certain material
would only be available to some groups of users such as admins or the
author.

We’ll need to setup an an admin interface in order for some privileged
users to easily review, add, update, remove materials.

I’ve noticed existing work on material database is using XML format to
display available materials, I would suggest using JSON as it is a bit
lighter, human-readable, but that’s more of a personal preference and
just an implementation detail. Exporting the data can be done in either
format, but we might want to consider the lightest option for BRL-CAD
parsing (there are number of XML/CSV/JSON parser for C++ out there but I
haven’t tested any of them performance wise yes - I don’t really know if
it could a be strain of performance if there is a large number of
materials and we reach a point where the user can browse available
options in BRL-CAD).

Client-side

Clients will initially request a list of materials from the Server. They
will interpret the JSON and display to include informations such as
Author, Description, and most importantly their traits.

The materials list will be accessible from browser - a dinamically
generated page will list all the materials and offer options for
authenticate in order to add new materials. BRL-CAD - initially just a
command line tool that talks to the website to get/put material data,
create .density files (and other formats), or add material data to a .g
geometry file

HTTP requests on BRL-CAD can be made using either libcurl to retrive
data and jsoncpp to parse the JSONs if we to decide to opt for a JSON
format. I would look into what’s fastest/most stable out there.

## Timeline

June
Week 1: Decide details on server implementation and start working on
providing a REST API
Week 2: Have a fully working API implemented and create a test suite for
it
Week 3: Create an admin area for managing the available resources
Week 4: Set up website that lists and enable users to perform actions
such as searching, viewing, adding materials
  July Week 1: Start working on BRL-CAD command-line command
Week 2: create .density files (and other formats),
Week 3: add material data to a .g geometry file
Week 4: other API routines and integrate in libged
August
Week 1: Continue working on previous point
Week 2: Have a fully working interface with a passing test suite
Week 3: Refactoring & documentation
Week 4: Refactoring

This provides a rough guideline of how the project will be done. As you
will see, I plan to start working right after the accepted proposals
list is published. Because of that, according to my timeline, I will
have ﬁnished the project earlier. I don't know if this will be the case,
but in all events, I will have time to cover any unexpected issue that
may come up.

## Bio

I’m Mihai, a CS undergraduate at Politehnica Univ. of Bucharest,
currently in the 4th and final year of study.

I believe each of us needs to leave his mark in some way, for me it has
been about making software that is used by as much as many other people.
I didn't have any real opportunity to do so, until I found out about the
Open-Source Development Course, taking place in our university. I
applied and after a series of interviews I was accepted. It's a course
that helps students make their first contributions within an open-source
project and get a feeling of what real world software development means.
I got to learn about working in an open-source community, using
version-control systems like git, unit-testing, asking for help on
mailing lists and other things like that.

One of the open source projects I got to contribute to was Jeopy, a
local-network multiplayer quiz game written in Python with PyQt (Python
binding for Qt) that features trivia in computer science and was used in
some of the first year's classes for the undergraduate students at my
university in order to help them recap course material. Four years
later, I'm still participating in the Open-Source Development Course but
as a mentor.

I’m actively involved in university life, I am an undergraduate teaching
assistant for a few classes and I try to participates in technical paper
presentations as often as I can.

I am the first one to sign up for hackathons as I strongly believe them
to be a unique chance to get together with people who also share my
passion in building something new and want to learn from each other in
the process.

Last summer I was an an intern at the romanian start-up uberVU. I
continued to work there for another 7 months after the internship was
completed. uberVU is a social media analytics applications and my work
was mainly focused on backend services (mostly Python), where I had to
implement a few systems and ensure they’re scalable and robust.

I volunteer a few hours week at Hospice of Hope, a palliative care
center. I also volunteer for activities organised by the Romanian Open
Source Education group which I’m also a part of.

I’m a disciplined individual and I try to organise myself as best as I
can though that doesn’t always happen as I always get involved in a big
number of projects. That would not be the case this summer as I’m
finishing university and considering tackling just a couple of
open-source project, BRL-CAD being one of them.

## Why did I choose to apply for BRL-CAD?

To be honest, I’m not an avid user of CAD software. I haven’t used one
since high-school, at some time back then I did get into 3D modelling
and photo editing and many many other activities because I was pretty
much clueless of what I wanted to do so I experimented with every kind
of piece of software I could get my hands on. I got to work with AutoCAD
and Cinema 4D and it was quite insightful stuff on how 3D modelling is
done. I’m particularly fond of this project because it involves working
on the web platform and on BRL-CAD and I’d love to work on tying them
together. I feel that getting involved in a project of this magnitude
will help me bring my skills to a higher standard. The community was
open, friendly and helpful and that’s also a big plus. In a nutshell,
this project is, to me, the perfect opportunity to learn new things, to
continue my development as a programmer and to do what I've always
wanted: contribute with a piece of software that would actually help the
community.