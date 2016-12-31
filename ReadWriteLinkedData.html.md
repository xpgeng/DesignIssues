Tim Berners-Lee  
Date: 2009-16-08, last change: $Date: 2013-08-16 18:45:00 $  
Status: personal view only. Editing status: Not finished at all @@

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

# Read-Write Linked Data

There is an architecture in which a few existing or Web protocols are gathered
together with some glue to make a world wide system in which applications
(desktop or Web Application) can work on top of a layer of commodity read-
write storage. The result is that storage becomes a commodity, independent of
the application running on it.

Introduction

The [Linked Data article](https://www.w3.org/DesignIssues/LinkedData.html) gave simple rules for putting data
on the web so that it is linked. This article follows on from that to discuss
allowing applications to write as well as read data.

It is part of a series: future notes discuss socially-aware decentralized
access control of reading and of writing to linked data, and of notification
of changes. The overall goal is one in which storage with the necessarily
functionality is a ubiquitous commodity, and application growth becomes
dramatic as the provision of storage is decoupled from the design and
deployment of applications. The storage is aware of different people and
groups which may want access; it is aware of metadata such as licensing and
appropriate uses of the data, so to help agents behave responsibly; and it can
alert those who are interested when data changes. Without looking ahead too
much, though, here let us look at protocol options for writing to the web of
data.

### Motivating Writing

I hope I do not have to motive here the fact that the Web in general should be
read-write. That has been done in many places, from 'Weaving the Web', to the
Read-Write Web blog. (I actually realize that in 20 year of writing these
articles, I haven't written a separate page on that topic! ) Let me summarize
here by saying the WWW was originally developed with the goal to be a
collaborative space in which people could collectively design, discuss, share
and manage things. Being able to impart one's knowledge, or put down a new
design or correct or annotate existing work, is I think a key functionality of
the Web. Even better, can it be a place we we are creative jointly
("intercreative™") .

This applies to data as much as to documents. To take just one example, shared
calendar systems are one example of shared data systems which, while they are
silos within the domain of calendaring, they have a classic burning need for
multi-person collaboration and the need to be able to create and modify as
well as read. In fact, collaboratively figuring out people's intersecting
calendars is a classic challenge task. The goal is to make an infrastructure
which will make it easy to write powerful collaborative applications. Also, I
like the maxim that wherever you have access to information which you have the
authority to correct or extend, there should be an easy way for you to do at
that place. This clearly applies as much to data as to documents.

## Outstanding issues

This article does not deal with the database-like storage APIs and
specifically with atomic transactions, or fine-grained access control.

## Architectures

The linked data world has a simple model. A set of documents in the Web each
have a URI and a graph of linked RDF triples. Modification to this space
consists of modification the triples in one more documents. We will consider
here the question of small incremental changes, and not consider the question
of large atomic changes which must be performed as an atomic transaction. @@

### File write-back

The model is that all data is stored in a document (virtual or actual file)
named with a URI. One way of changing the data is to overwrite the whole file
with an HTTP PUT operation. Whereas typical Apache servers are not configured
out of the box to accept PUT, when they are configured for WebDAV (The Web
Distributed Authoring and Versioning specs) then they do. For historical
reasons*, they advertise that they support with PUT with an HTTP header line

    
    
    MS-Author-Via: DAV
    

### SPARQL Update

An alternative protocol for doing a change is to send just a small change as a
patch back to the server. The patch fill is a small file which describes the
change necessary to the graph. The patch may be generated directly by a user
interface action, or an inference result, or alternatively the change may have
been made in copy local to the client, and the patch file of the differences
generated automatically. For compatibility with the above, An HTTP server
advertises that it supports with SPARQL/Update with an HTTP header line

    
    
    MS-Author-Via: SPARQL
    

The change in the resource is described in SPARQL UPDATE message, which is
posted to the URI of the data file itself.

The SPARQL update message only uses the **default graph, which is the graph of
the document in question**. The SPARQL GRAPH directive is not used.

The query is sent using SPARQL in the body of the HTTP POST. A content-type
header must be sent. The content type is ** application/sparql-update** **.
(The following single line curl command is an example).

    
    
    curl -d 'INSERT DATA \
    { <http://dig.csail.xvm.mit.edu/2007/wiki/people/JoeLambda#JL> \
                 <http://xmlns.com/foaf/0.1/age> 66 }' \
     -H Content-type:application/sparql-query \
      http://dig.csail.mit.mit.edu/2007/wiki/people/JoeLambda
    

Note that a WHERE clause may well be used, as when modifications to the
document are made which involve blank nodes, it may be necessary to give
enough context to unambiguously identify the blank nodes.

(A server may also support SPARQL queries as well as SPARQL updates. if this
is so, note the content-type header is the same, and the request body must be
parsed to know whether it matches the query or the update grammar.)

#### Note: 409 Conflict

A SPARQL update message often contains both a DELETE and then an INSERT. This
may be used to update a field from one value to another. When more than one
application or user is using the same data, there may arise times when the
DELETE fails because another user has already deleted the same data. In this
case it **very important** that the delete does not fail silently. The HTTP
server MUST return error status 409. ("409 Conflict" indicates that the
request could not be processed because of conflict in the request, such as an
edit conflict). The client can then for example inform the user by backing out
the change the user was trying to make, or it can retry a reservation later.
The atomicity of the DELETE,INSERT function can be used to provide various
mutual exclusion systems, such as reserving a resource or generating unique
sequential numbers, and so on.

### A Data Wiki

The protocols above can be used to implement a data wiki. This is a piece of
URI space in which any data can be edited by anyone, just as a text wiki can
be. To make a data wiki, also one needs this extra rule:

Whenever a client requests a page which doesn't previously exist, instead of
returning a "400 Not found" error, the server returns 200 OK, and a valid data
document (in RDF/XML or N3) which contains zero triples. (This does not mean a
zero length document in RDF/XML, but it can be in N3)

## Conclusion

The world of linked data can be extended to a world of read-write linked data
easily. The existing protocols and formats HTTP, WebDav, RDF and SPARQL can be
connected together as defined above, with a little glue from the reuse of
existing HTTP headers. This creates a space in which new applications can
easily be written to operate using shared linked data.

Of course for many real-world applications, one does not want a data wiki in
which anyone can write. We therefore need to extend the system to include
access control. This is discussed in the [article on Socially-aware Cloud
Storage](https://www.w3.org/DesignIssues/CloudStorage.html).

* * *

## Followup

The [Editing Data wiki page](http://esw.w3.org/EditingData) is a place to list
clinet and server implementations, and pointer to more inoformation

  * The video mix by dataprtability.org, first minutes
  * The video by the diaspora team in leading up to summer 2010
  * 2010-06-01, Chimezie Ogbuji, editor, [SPARQL 1.1 Uniform HTTP Protocol for Managing RDF Graphs](http://www.w3.org/TR/sparql11-http-rdf-update/) is a working draft which currently (2010) may hopefully specifiy this functionality.

## Footnotes

* Microsoft introduced a completely proprietary protocol for write-back called the "Microsoft Frontpage Extensions". Later, this MS-Author-Via header was [ introduced by Microsoft](http://msdn.microsoft.com/en-us/library/cc250217%28v=PROT.10%29.aspx) to allow Microsoft clients to turn _off_ the front page extensions and use WebDAV. As a result, most WebDAV servers in 200X provided that header. It was natural therefore natural to use the same header to adverize the availablity of SPARQL. Perhaps the MS stands for "modification service". 

** This was application/sparql-query until 2013. This was changed as the code out there changed to track the LDP work. A liberal server accepts both application/sparql-query and application/sparql-update. It is possible that a patch language and patch MIME type are developed for this. 

## References

See [references in next article.](https://www.w3.org/DesignIssues/CloudStorage#references)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

