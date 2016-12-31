Tim Berners-Lee  
Date: 1998, last change: $Date: 2013-03-04 22:56:21 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Principles of Design

Again and again we fall back on the folklore of the principles of good design.
Sometimes I need a URI for them so this is started as collection of them. I
have written about some in many places. Principles such as **simplicity** and
**modularity** are the stuff of software engineering; **decentralization** and
**tolerance** are the life and breath of Internet. Brian Carpenter has
enumerated some principles of design of the Net
[[carpenter](https://www.w3.org/DesignIssues/Architecture.html#carpenter)]. The third pair of ideas I have
found commonly useful for the Web. I mentioned them in a keynote at WWW7 and
the note on [Evolvability](https://www.w3.org/DesignIssues/Evolution.html).

This is largely "motherhood and apple pie" but it still needs a home.

##  Simplicity

> "Keep it simple, stupid!"

Simplicity is easily to quote but often ignored in strange ways. Perhaps this
is because it is the eye of the beholder.

A language which uses fewer basic elements to achieve the same power is
simpler.

Sometimes simplicity is confused with 'easy to understand". For example, a
two-line solution which uses recursion is a pretty simple, even though some
people might find it easier to work though a 10-line solution which avoids
recursion.

In XML, "Processing Instructions", those things which start with "&lt;?" are
**not** simple. They look simple, just an extra sort of thing in the language,
but the complicate what was a very clean design of elements and attributes,
and a complication in the underlying syntax is has great effect. All
specifications which refer to XML processing will have to figure out what to
do about processing instructions as well as elements.

##  Modular Design

When you design a system, or a language, then if the features can be broken
into relatively loosely bound groups of relatively closely bound features,
then that division is a good thing to be made a part of the design. This is
just good engineering. It means that when you want to change the system, you
can with luck in the future change only one part, which will only require you
to understand (and test) that part. This will allow other people to
independently change other parts at the same time. This is just classic good
software design and books have been written about it. The corollary, the TOII
is less frequently met.

Modular design hinges on the simplicity and abstract nature of the interface
definition between the modules. A design in which the insides of each module
need to know all about each other is not a modular design but an arbitrary
partitioning of the bits. [(More ...)](https://www.w3.org/DesignIssues/Modularity.html)

##  Being part of a Modular Design

Its is not only necessary to make sure your own system is designed to be made
of modular parts. It is also necessary to realize that your own system, no
matter how big and wonderful it seems now, should always be designed to be a
_part_ of another larger system.

This is often much more difficult than modularity.

##  Tolerance

> "Be liberal in what you require but conservative in what you do"

This is the expression of a principle which applies pretty well in life, (it
is a typical UU tenet), and is commonly employed in design across the
Internet.

Write HTML 4.0-strict. Accept HTML-4.0-Transitional (a superset of strict).

This principle can be contentious. When browsers are lax about what they
expect, the system works better but also it encourages laxness on the part of
web page writers. The principle of tolerance does not blunt the need for a
perfectly clear protocol specification which draws a precise distinction
between a conformance and non-conformance. The principle of tolerance is no
excuse for a product which contravenes a standard.

##  Decentralization

This is a principle of the design of distributed systems, including societies.
It points out that any single common point which is involved in any operation
trends to limit the way the system scales, and produce a single point of
complete failure.

Centralization in social systems can apply to concepts, too. For example, if
we make a knowledge representation system which requires anyone who uses the
concept of "automobile" to use the term
"http://www.kr.org/stds/industry/automobile" then we restrict the set of uses
of the system to those for whom this particular formulation of what an
automobile is works. The Semantic Web must avoid such conceptual bottlenecks
just as the Internet avoids such network bottlenecks.

##  Test of Independent Invention

> If someone else had already invented your system, would theirs work with
yours?

Does this system have to be the only one of its kind? This simple thought test
is described in more detail in "[Evolution](https://www.w3.org/DesignIssues/Evolution.html#TOII)" in these
Design Issues. It is connectted to modularity inside-out: designing a system
not to be modular in itself, but to be a part of an as-yet unspecified larger
system. A critical property here is that the system tries to do one thing
well, and leaves other things to other modules. It also has to avoid
conceptual or other centralization, as no two modules can claim the need to be
the unique center of a larger system.

##  Principle of Least Power

In choosing computer languages, there are classes of program which range from
the plainly descriptive (such as Dublin Core metadata, or the content of most
databases, or HTML) though logical languages of limited power (such as access
control lists, or _conneg_ content negotiation) which include limited
propositional logic, though declarative languages which verge on the Turing
Complete (Postscript is, but PDF isn't, I am told) through those which are in
fact Turing Complete though one is led not to use them that way (XSLT, SQL) to
those which are unashamedly procedural (Java, C).

The choice of language is a common design choice. The low power end of the
scale is typically simpler to design, implement and use, but the high power
end of the scale has all the attraction of being an open-ended hook into which
anything can be placed: a door to uses bounded only by the imagination of the
programmer.

Computer Science in the 1960s to 80s spent a lot of effort making languages
which were as powerful as possible. Nowadays we have to appreciate the reasons
for picking not the most powerful solution but the least powerful. The reason
for this is that the less powerful the language, the more you can do with the
data stored in that language. If you write it in a simple declarative from,
anyone can write a program to analyze it in many ways. The Semantic Web is an
attempt, largely, to map large quantities of existing data onto a common
language so that the data can be analyzed in ways never dreamed of by its
creators. If, for example, a web page with weather data has RDF describing
that data, a user can retrieve it as a table, perhaps average it, plot it,
deduce things from it in combination with other information. At the other end
of the scale is the weather information portrayed by the cunning Java applet.
While this might allow a very cool user interface, it cannot be analyzed at
all. The search engine finding the page will have no idea of what the data is
or what it is about. This the only way to find out what a Java applet means is
to set it running in front of a person.

I hope that is a good enough explanation of this principle. There are millions
of examples of the choice. I chose HTML not to be a programming language
because I wanted different programs to do different things with it: present it
differently, extract tables of contents, index it, and so on.

* * *

##  References

[B. Carpenter, Editor: "Architectural Principles of the
Internet"](https://www.w3.org/DesignIssues/ftp://ftp.isi.edu/in-notes/rfc1958.txt) Internet Architecture
Board, June 1996, RFC1958

* * *

## Follow up

In her talk [ The Science of
Insecurity](http://www.youtube.com/watch?v=3kEfedtQVOY), Meredith Patterson
makes the point that the principle of least power is important for security of
interfaces which may be exposed to attack.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

