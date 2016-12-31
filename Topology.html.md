[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)TimBL

* * *

#  Topology

Here are a few questions about the underlying connectivity of a hypertext web.

##  Are links two- or multi-ended?

The term "link" normally indeicates with two ends. Variations of this are liks
with multiple sources and/or multiple destinations, and constructs which
relate more than two anchors. The latter map onto logic description systems,
predicate calculus, etc. See the "Aquanet" system from Xerox PARC - paper at
HT91). This is a natural step from hypertext whose the links are typed with
semantic content. For example, the relation "Document A is a basis for
document B given argument C". From now on however, let us restrict ourselves
to links in the conventional sense, that is, with two ends.

##  Should the links be monodirectional or bidirectional?

If they are bidirectional, a link always exists in the reverse direction. A
disadvantage of this being enforced is that it might constrain the author of a
hypertext - he might want to constrain the reader. However, an advantage is
that often, when a link is made between two nodes, it is made in one direction
in the mind of its author, but another reader may be more interested in the
reverse link. Put another way, bidirectional linking allows the system to
deduce the inverse relationship, that if A includes B, for example, that B is
part of A. This effectively adds information for free. This is important when
a critical parameter of the system is how long it takes someone to create a
link.

KMS and hypercard have one-way links; Enquire has two-way links.

There is a question of how one can make a two-way link to a protected
database. The automatic addition of the reverse link is very useful for
enhancing the information content of the database. See also:[Private overlaid
web](https://www.w3.org/DesignIssues/Multiuser.html#3) , [ Generic
Links](../../History/19921103-hypertext/hypertext/Products/Microcosm/Microcosm.html#GenericLinking)
.

It may be useful to have bidirectional links from the point of view of
managing data. For example: if a document is destroyed or moved, one is aware
of what dangling links will be created, and can possibly fix them.

A compromise that links be one-way in the data model, but that a reverse link
is created when any link is made, so long as this can be done without
infringing protection. An alternative is for the reverse links to be gathered
by a background process operating on a basically monodirectionally linked web.
See [Building Back-links](https://www.w3.org/DesignIssues/BuildingBackLinks.html).

##  Should anchors have more than one link?

There is a design issue in whether one anchor may lead to many links, and/or
on link have many anchors. It seems reasonable for many anchors to lead to the
same reference. If one source anchor leads to more than one destination
anchor, then there will be ambiguity if the anchor is clicked on with a mouse.
This could be resolved by providing a menu to the user, but I feel this would
complicate it too much. I therefore suggest a many-to-one mapping.
[JFG](https://www.w3.org/People.html#groff) disagrees and would like to see a small menu
presented to the user if the link was
ambiguous.[Microcosm](../../History/19921103-hypertext/hypertext/Products/Microcosm/Microcosm.html)
does this.

##  Should links be typed?

A typed link carries some semantic information, which allows the system to
manage data more efficiently on behalf of the user. A default type ("untyped")
normally exists in some form when types are implemented. See also a [list of
some types](https://www.w3.org/DesignIssues/LinkTypes.html) . (Should a link be allowed to have many types? (-
[JFG](https://www.w3.org/People.html#groff) ) I don't think so: that should be represented by
more than one link.(- [TBL](https://www.w3.org/People.html#BernersLee) ))

Link typing helps with the generation of [graphical
overviews](https://www.w3.org/DesignIssues/Navigation.html#6) , and with [automatic
tracing](https://www.w3.org/DesignIssues/TracingLinks.html) .

##  Should links contain ancillary information?

Does the system allow dating, versioning, authorship, comment text on a link?
If so, how is it displayed and accessed? This sort of information complicates
the issue, in that readable information is no longer carried within node
contents only. Pretty soon, following this path leads to a link becoming a
node in itself, annotatable and all. This perverts the data model
significantly, and I cannot see that that is a good idea. Information about
the link can always be put in the source node, or in an intermediate node, for
example an annotation. However, this makes tracing more difficult. It is
certainly nice to be able to put a comment on a link. Perhaps one should make
a link annotatable. I think not.

##  Should a link contain Preview information?

This is information stored at the source to allow the reader to check whether
he wants to follow a link before he goes. I feel that the system may cache
some data (such as the target node title), or the writer of the node may
include some descriptive material in the highlighted spot, but it is not
necessary to include preview information just because access may be slow.
Caching should be done instead of corrupting the user interface. If you have a
fast [graphic overview](https://www.w3.org/DesignIssues/Navigation.html#6) , this could remove the necessity
for a preview function.

