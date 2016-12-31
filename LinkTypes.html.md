[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)TimBL

* * *

#  Link Types

See [discussion of whether links should be typed](https://www.w3.org/DesignIssues/Topology.html#4) .

Descriptive (normal) link types are mainly for the benefit of users and
tracing, and graphics representation algorithms. Some link types for example
express relationships between the things described by two nodes.

A Is part of B / B includes A

A Made B / B is made by A

A Uses B / B is used by A

A refers to B / B is referred to by A

##  Magic link types

These have a significance known to the system, and may be treated in special
ways. Many of these relate whole nodes, rather than particular anchors within
them. (See also [multiended links](https://www.w3.org/DesignIssues/Topology.html#12) and predicate logic)
Suggestions:

###  UseIndex

The destination is the related index for a search by a user reading this
document who asks for an index search function.

A document may have any number of index links, causing several indexes top be
searched in a client-defined manner.

###  UseGlossary

The destination of the link is an index which should be used to resiolve
glossary queries in the document. (Typically, a double-clik on a word which is
not within an anchor).

A document may have any number of glossary links.

###  Annotation

The information in the destination node is additional to that in the source
node, and may be viewed at the same time. It may be filtered out (as a
function of author?).

Annotation is used by one person to write the equivalent of "margin notes" or
other criticism on another's document, for example.

[Tracing](https://www.w3.org/DesignIssues/TracingLinks.html) may ignore annotations when generating trees or
sequences.

###  Next, Previous, Up

These terms may be applied to the tree the user creates in her browsing, but
if the author puts links in, then a tree structure may be proposed by the
author. This is very natural with hypertext versiins of books, etc.

###  Embedded information

If this link is followed, the node at the end of it is embedded into the
display of the source node. This is supported by Guide, but not many other
systems. It is used, in effect, by those systems (VAX/notes under Decwindows,
Microsoft Word) which allow "Outlining" -- expanding a tree bit by bit.

The browser has a more difficult job to do if this is supported.

###  person described by node A is author of node B

This information can be used for protection, and informing authors of
interest, for sending mail to authors, etc.

###  person described by node A is interested in node B

This information can be used for informing readers of changes.

###  Node A is in fact a previous version of node B

###  Node A is in fact a set of differences between B and its previous

version. This information will probably not be stored as nodes, but be
generated from regular diff files. or some other delta method.

