[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)TimBL

* * *

#  Multiuser considerations

Multiuser access is made easier with a client/server model.We obviously want
this. We also need simultaneous reading and writing of the same database. This
is done by locking parts or all of the database while they are updated. One
has to decide on the unit of data to be locked. I ([TBL](https://www.w3.org/People/Berners-
Lee/Overview.html)) imagine that it would be a node, not a database.

There is a specific problem which all distributed hypertext systems have had
to tackle, in [linking to living documents](https://www.w3.org/DesignIssues/LinkToLiving.html) .

##  Annotation

Annotation is the linking of a new commentary node to someone else's existing
node. It is the essence of a collaborative hypertext. An annotation does not
modify the text necessarily: one can separate protection against writing and
annotation.

##  Protection

Protection against unauthorized reading and writing is provided by servers. We
use the word ªdomainº to describe a set of data which has the same protection.
Life is simple if the domain is the database, or all the data administered by
a given server. One can also add author-based protection to the contents of a
node, or links, which have author information stored about them.

There is a problem illustrated by the following example. One might want to
make a private annotation to something which is visible world-wide but
unwritable. The annotation would be invisible to another reader: it would be
stored in a private domain. The node itself is visible everywhere: it is
stored in a public domain. This is a general problem of links being in a
different domain to nodes.

##  Private overlaid web

A possible solution to this is to have, in the private domain, a partial copy
of the public web, so that link information can be added to it. The copy of
the net could also be used to tag on local cached copies of the contents of
the remote nodes.

The writer would have to be aware of the domain into which he was writing. One
could use a server per domain, but could imagine the need for more than one
server per domain, or more than one domain per server.

See also: [Generic
Linking](../../Products/Microcosm/Microcosm.html#GenericLinking)

##  Locking and modifying

Modification of text in a multiuser environment requires in principle some
sort of atomic locking feature, so that two users do not update the same text
at the same time. In fact some systems do not have this and still survive
quite well: it depends a lot on the human environment.

Practically, the HTTP protocol must contain a lock/unlock command, and some
way of recovering from a lock left on by a vanished user. The actual
implementation will depend on the server or gateway. In the case of files,
then a number of possibilitie exist:

  * One can write-protect the file temporarily. This unfortunately levaes no clue as to who has locked it, when and why. It is also indistinguishable from a genuine protection to a document which should not be modified 
  * One can create a lock file containing information about who/when/why, whose name is derived from the name of the file in question. 

