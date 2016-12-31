[![](https://www.w3.org/Icons/WWW/arch1990.gif)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

#  Building back-links

##  Why back links?

This [discussion on link topology](https://www.w3.org/DesignIssues/Topology.html#14) differetiates between
systems with mon-directional and those with bidirection links. In practice, a
system

in which different parts of the web have different capabilities cannot insist
on bidirectional links.

Imagine, for example the publisher of a large and famous book to which many
people refer but who has no interest in maintaining his end of their links or
indeed in knowing who has refered to the book. In this case the link may be
only of use to the person who made it.

However, there are cases in which the back-links are of great interest, and so
they may be generated off line.

##  How?

One way is for a [daemon](https://www.w3.org/Terms.html#daemon) to read all of the documenst
on a particular domain, and make a database of the links, then redistribute to
the servers the back links.

Another way is suggested by Phillip Hallam-Baker who "wondered about a tag
being added to the get protocol to indicate where the text was being accessed
from. This could then be used by intelligent servers to create back links - if
this was desired. This would allow the wed to grow dynamicaly since I would
know that logging onto any "key" W3 server I would be able to travel to all
those parts of the web I was meant to..."

This method would also provide intersting statistics on the use of particular
links, which would enhance the usage logging.

_________________________________________________________________

[Tim BL](http://www.w3.org./hypertext/TBL_Disclaimer.html)

