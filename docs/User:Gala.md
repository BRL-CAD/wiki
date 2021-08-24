### Gala's Sandbox Page

#### Handy Links

[Community_Publication_Portal](Community_Publication_Portal "wikilink")

#### Introduction to new .deb and .rpm builds

Brief article overviewing the efforts by jordisayol for Debian, Ubuntu,
Fedora, and openSUSE. Included are new icons, menu items, mime type
associations, and more.

#### Gala: New BRL-CAD Linux Release Packaging Process Automation

By: Gala Taylor

BRL-CAD supports Debian, Ubuntu, Fedora, and openSUSE, and other Linux
distributions. Jordi Sayol recently finished automating the BRL-CAD
Linux release packaging process, and he took some time out to chat with
Gala Taylor about it - and also answer some question about what it's
like to work on the BRL-CAD project.

**Gala Taylor (GT)**: How long have you been working on the BRL-CAD
project?

**Jordi Sayol (JS)**: I've been involved with the BRL-CAD project since
January 2011.

**GT**: How much education and experience were required to prepare you
to contribute to the BRL-CAD project?

**JS**: My experience is just as an advanced Linux user.

**GT**: Do you need to physically meet with the other team members in
order to contribute to the BRL-CAD project, or is it sufficient to work
on-line?

**JS**: All of my collaboration is done on-line.

**GT**: The BRL-CAD project is a collection of over four hundred tools,
utilities and applications, with over a million lines of source code.
With such a massive and complex system, how do you decide what to work
on? Is it necessary to understand all that code in order to contribute
to the project?

**JS**: My responsibility is focused on building binary packages of
BRL-CAD for Linux systems.

**GT**: Besides the release processing work which is described in the
HACKING file, can you walk me through the process of actually
transforming a developer’s checked-in source code into an .rpm or .deb
that is ready to be downloaded and installed?

**JS**: It's quite simple. I have created two bash scripts that automate
this process. The "sh/make_deb.sh" script creates a deb package
installable on Debian-like systems. This currently includes Debian,
Ubuntu, Linux Mint, and other distributions. The "sh/make_rpm.sh"
script creates an rpm package for Fedora-like systems. This includes
Fedora, Centos, Redhat, and some other distributions, or OpenSUSE,
depending on the system where it is built. There are separate rpm
packages for Fedora and OpenSUSE because they do not share the same
nomenclature on their packages. Note also that both scripts create
deb/rpm packages for the host architecture where they are executed, and
that the results are currently only tested on x86_32 and x86_64 hosts.

With these scripts, anyone can easily create their own deb/rpm packages
as needed. This is especially useful if the user wants to install
BRL-CAD on a very old system, maybe requiring special compilation for
specific graphic cards drivers, etc.

**GT**: Thank your for your time today and your contributions to
BRL-CAD, Mr. Sayol!

**JS**: It was a pleasure.

Please visit the BRL-CAD project website for more information:
<http://brlcad.org>

**Jordi Sayol** is the maintainer of the BRL-CAD Linux release packaging
process.

**Gala Taylor** is a 2012 Google Code-In participant. Although she has
used various Free and Open Source Software (FOSS) products over the
years, and has contributed example files and tutorials to several
projects, this is the first time she has actively participated in the
development of FOSS code. Gala is currently in 9th grade, and her
favorite computer language is Java.