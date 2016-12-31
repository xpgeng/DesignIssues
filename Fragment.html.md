Tim Berners-Lee

Date: April, 1997

Status: personal view, but believed to be my best expression of the underlying
architecture for W3C development. Editing status: Good enough fo discussion.

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Axioms of Web Architecture

* * *

#  URI References: Fragment Identifiers on URIs

The URI by itself is a powerful thing, but there is a more powerful concept
which is the URI reference.

The URI reference is a thing you build by taking a URI for an information
object, adding a "#" sign and then a **Fragement identifier**. (The last term
is historical, so try not to thinl of it necessarily identifying a fragment).

The fragment identifier is a string after URI, after the hash, which
identifies something specific as a function of the document. For a user
interface Web document such as HTML poage, it typically identifies a part or
view. For example in the object

    
    
             http://foo/bar#frag
     
    

the string "frag" is the fragment identifier. It is badly named, as it can
identify anything.

(Depending on where you look, the URI is considered to include the fragment
identifier, or to have the fragment identifier appended to it.  This is
important for the BNF, but in practice you will find people using the terms
URI and URL loosely to things which do or do not include a possible fragment
identifier. Formally, the URI **does** include the fragment ID)

In practice, you can divide the processing which occurs when following a link
using HTTP into three steps:

  1. The client figures out which server to contact by parsing part of the URL, and sends the URL as a request to the server; 
  2. The server figures out which object is referred to by parsing the rest of the URL, and returns some rendition of it to the client; 
  3. The client presents all or part of the object to the user 

The last part typically involves finding some software class which can handle
the given MIME type, and passing it the data stream.  At the same time, the
fragment identifier is passed as a parameter to the created object.

For HTML, the fragment ID is an SGML ID of an element within the HTML object.
For XML, if it is just a word, then it is the XML ID of an element in the
document.

####  Axiom

The significance of the fragment identifier is a function of the MIME type of
the object

This means that the fragment id is opaque for the rest of the client code.
The HTTP engine cannot make any assumptions about it.  The server is not even
given it.

It also means that for any new data type one can be creative about using the
fragment ID in a relevant way. For example, for a 3D object the fragment ID
could give a viewport. For a music object, the Fragment ID could give a
section in time, or a set of parts, or it could include a suggested tempo.
For future versions of HTML, the fragment ID could be made more powerful to
include a range or "ladder" reference to a part or parts of the SGML element
tree by position. A very useful fragment ID for plain text would allow ranges
to be quoted by line and character number

These things are all decisions made when the MIME type is defined.  Therefore,

The fragment ID spec for a new MIME type should  be part of the MIME type
registration process.

Different MIME types then can have different fragment ID specifications. When
HTTP for example negotiates between different content types, it is clearly
useful for those types to have a consistent (hopefully identical) fragment ID
syntax and semantics.

###  Fragment identifiers for RDF identify concepts

The semantic web has information about anything. The fragment identifier on an
RDF (or N3) document identifies not a part of the document, but whatever
thing, abstract or concrete, animate or innanimate, the document describes as
having that identifier.

It is important, on the Semantic Web, to be clear about what is identified. An
`http:` URI (without fragment identifier) necessarily identifies a [generic
document](https://www.w3.org/DesignIssues/Generic.html). This is because the HTTP server response about a URI
can deleiver a rendition of (or location of, or apologies for) a document
which is identified by the URI requested. A client which understands the http:
protocol can immediately conclude that the fragementid-less URI is a generic
document. This is true even if the publisher (owner of the DNS name) has
decided not to run a server. Even if it just records the fact that the
document is not available online, still a client knows it refers to a
document. This means that identifiers for arbitrary RDF concepts should have
fragment identifiers. This, in turn, means that RDF namespaces should end with
"#".

###  Object Names as fragment identifiers

When a document language (MIME type) has some form of intra-document naming
for objects then it is intuitive is these names can be directly used as
fragment identifiers. This is true for XML, that the XML ID which is used to
identify elements can be directly used as a fragment identifier.

###  Fragment IDs and Content negotiation - known bug

If content negotiation occurs across types which do NOT share a fragment ID
specification, then rigidly there has been an error. In practice, HTML was the
only type (in 1997) which allowed fragment IDs anyway, and other types ignore
it. Also, as falling back from a pointer to a specific view to a pointer to
the whole document has been considered effective fallback procedure, so no
harm was done. Now (2001) it becomes more of a problem. there have been
proposasl to add the requested fragment idntifier to the HTTP request to fix
this.)

In the future, metadata returned or warnings returned should indicate to the
client that this could be a problem. Also, in new access protocols, the
fragment ID requested could be shipped to the server as a hint, which would
allow the server and client to negotiate and if successful arrange for the
fragment ID to be converted to a suitable equivalent value for an alternative
MIME type.

###  User awareness of the form of a reference

Clearly when a fragment ID is generated and associated with a URI which is
generic in any way (language, version, etc as well as content-type), then
there is a possible failure of the fragment-id refers to something which is
not defined in any specific instance.  It would be appropriate for a client,
when generating a link (or bookmark, etc) to provide the user with a choice of

  * A bookmark to the whole living document, or 
  * A bookmark to a specific part of a "dead" version; 
  * Intermediate combinations.  

As both these options are meaningful and useful, they will have to surface at
the user interface level.

* * *

[Back to URIs](https://www.w3.org/DesignIssues/Axioms.html) \--- [Next: Links and the law](https://www.w3.org/DesignIssues/LinkLaw.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

_$Id: Fragment.html,v 1.6 1998/03/04 17:24:58 timbl Exp $_

