[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)TimBL

* * *

#  Navigational Techniques and Tools

[TBL](https://www.w3.org/People.html#BernersLee) There are a number of ways of accessing the
data one is looking for. Navigational access (i.e., following links) is the
essence of hypertext, but this can be enhanced with a number of facilities to
make life more efficient and less confusing.

##  Defined structure

It is sometimes nice for a reader to be able to reference a document structure
built specifically to enhance his understanding, by the document author. This
is especially important when the structure is part of the information the
author wishes to convery.

See a [separate discussion of this
point](../../Conferences/ECHT90/Structured.html) .

##  Graphic Overview

A Graphic overview is useful and could be built automatically. Should it be
made by the author, server, browser or an independent daemon?

Can one provide an overview with less granularity than the basic web by
grouping nodes in some way? The user could select from [link
types](https://www.w3.org/DesignIssues/Topology.html#4) used to imply the tree
structure.[(JFG)](https://www.w3.org/People.html#groff)

I think this depends on how long it will take. It might be interesting to
experiment with daemons which will independently make and update maps of the
web. This is not essential for a first pilot model.

##  History mechanism

This allows users to retrace their steps. Typical functions provided can be
interpreted in a hypertext web as follows:

Home

     Go to initial node 
Back

     Go to the node visited before this one in chronological order. Modify the history to remove the current node. 
Next

     When the current node is one of several nodes linked to the ªbackº node, go to the next of those nodes. Leave the ªBackº node unchanged. Modify the history to remove the current node and replace it with the "next" (new current) node. 
Previous

     When the current node is one of several nodes linked to the ªbackº node, go to the preceding one of those nodes. 
In many hypertext systems, a tree structure is forcibly imposed on the data,
and these functions are interpreted only with respect to the links in the
tree. However, the reader as he browses defines a tree, and it may be more
relevant to him to use that tree as a basis for these functions. I would
therefore suggest that an explicit tree structure not be enforced.

(If a default tree is needed by the system for some reason, then we can always
use the creation order: when a node is created it is always created with a
link to an existing node. Such links, whatever their type, may be used to
define a tree. If they are deleted, an alternative link must be chosen to
become a tree link.)

If authors want to write a tree structure into their documents, then the words
"after", "before" and "above" could be used to mean a static structure.

##  Intelligent navigation

See A. Secret's [discussion of intelligently navigation
techniques](https://www.w3.org/DesignIssues/Intelligent_Navigation.html) .

##  Index

An Index helps new readers of a large database quickly find an obscure node.
Keyword schemes I include in the general topic of indexes. The index must,
like a graphic overview, be built either by the author, or automatically by
one of the server, browser, or a daemon . The index entries may be taken from
the titles, a keyword list, or the node content or a combination of these.
Note that keywords, if they are specifically created rather than random words,
map onto hypertext ªconceptº nodes, or nodes of special type ªkeywordº. It is
interesting to establish an identity relationship between keywords in two
different databases -- this may lead a searcher from one database into
another.

Index schemes are important but indexes or keywords should look like normal
hypertext nodes. The particular special operation one can do with a good
keyword index system which one can't do with a normal hypertext system is to
do a fast search on multiple keywords. This must to be provided as an
extension to the hypertext navigation scheme. However, it is in fact analogous
to a trace starting with more than one node, which is a valid hypertext
tracing operation. The difference is that the tracing would normally be done
by a browser, but the indexed search done by the server.

When many nodes in a web represent different indexes, then a query search can
chain between them (See " [Web of indexes](https://www.w3.org/DesignIssues/ManyIndexes.html) "). [Nat
Torington's
musings](http://www.vuw.ac.nz:80/who/Nathan.Torkington/ideas/reggie.html) .

See also: [HyperText and Information
Retrieval](../../Conferences/ECHT90/HTandIR.html)

##  Node Names

These allow faster access if one knows the name. They allow people to give
references to hypertext nodes in other documents, over the telephone, etc.
This is very useful. However, in Notecards, where the naming of nodes was
enforced, it was found that thinking up names for nodes was a bore for users.
KMS thought that being able to jump to a named node was important. The node
name allows a command line interface to be used to add new nodes.

I think that naming a node should be optional: perhaps by default the system
could provide a number which can be used instead of a name.The system should
certainly support the naming of nodes, and access by name.

##  Menu of links

Regular linkwise navigation may be done with ªhotspotsº (highlighted anchors)
or may be done with a menu. It may be useful to have a menu of all the links
from a given node as an alternative way of navigating. Enquire, for example,
offers a menu of references as the only way of navigating.

