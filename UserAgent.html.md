Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:10 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Axioms of Web Architecture: n

* * *

#  User Agent watch points

Interpreting HTTP

Browsers and Email programs are user agents. This isn't just a formal long
term for them, it is an important issue. They are programs which act on behalf
of, and represent, the user.

The computer protocols such as HTTP are defined to carry a particular meaning,
and it behooves a user agent to representthat meaning to the user, or the whol
system of peeople and machines breaks.

Here are a few ways in which browser designs should and often have not lived
up to this.

###  Distinguish between HTTP "301 Moved permanently" and "302 Found"

There are two forms of redirection in HTTP. Each gives a new place to look for
a resource, but for completely different reasons.

"[301
Moved](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.2)" is a
response which indicates that the server has committed the unthinkable and for
some reason not in a position to serve the document at that URI. It indicates
that all references to the original should be change to the new one, including
bookmarks and document links. This is an expensive solutin to a serious
problem. It does not, of course, work completely, but it is the HTTP way for a
server to alert a client of this situation.

"[302
Found](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.3)" is a
response which indicates that the server is working as a name server. It is a
success result indicating that you asked for a good document, and that the
actual contents can curently be found at the given URI.

The imporant use of name server functionality is when for some reason it is
impractical to server the document directly from a server which can hold the
persistent URI.. For example, a university might issue definitive URIs for its
successful theses, and might have a very reliable, stable, low bandwidth
machine which handles that URI space. However the content of the theses might
in practice be delivered by fast machines located in the departments. The
university may make a persistence commitment for the original URI but not for
the department's server. Similarly, a user may for load reasons or speed
reasons be directed to a mirror.

It is important that when a user agent follows a "Found" link that the user
does not refer to the second (less persistenet) URI. Whether copying down the
URI from a window at the top of a doucment, or making a link to the document,
or bookmarking it, the reference should (except in very special cases) be to
the original URI.

Very few browsers (Mozilla? Amaya&gt;) implement this properly as of 1999.

There is also [ 307 temporary
redirect](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.8),
which is similar to a 302 Found.

See also:

  * [Cool URIs don't change](http://www.w3.org/Provider/Style/URI.html) (In the Style Guide for Online Hypertext) 

###  Distinguish between an HTTP _POST_ and a _GET_

GET operations (as happen when you follow a regular hypertext link) are
fundamentally different from POST operations (as happen when you submit a form
to order a book), The first is reversible, has no long term effect, cannot
comit a user to anything. The latter does committhe user.

A graphic client, for example, should use a very different **cursor** while
the user is hovering over a POST button to when the user is hovering over a
GET link.

Doing a POST is like sending an email. (Currently 1999 it may be more secure
because it will often happen over an https secure connection while many email
clients do not encrypt messages.) It is really important to be able to find a
list of the emails you have sent: these are the things you are committed to.
The same applies to HTTP POST forms. The web client should **keep a record**
of POSTs which have been submitted.

This would of course waste a lot of space for those web sites which get GET
and POST muddled, but they are fundmentally broken anyway and the sooner we
just fix this misuse on all sides the better. In the future, digital signature
will be an action just like POST, but with weight added and the user awareness
of the choice of key. Understanding when a commitment is made is a really
important part of the user interface. Get it right.

See also:

  * [Axioms: HTTP GET if and only if no side effects](https://www.w3.org/DesignIssues/Axioms.html#get)
  * [HTTP specification](https://www.w3.org/DesignIssues//Protocols/rfc2616/rfc2616.html)

##  Hide URIs

Objective: A web user should never be aware of a URI while using the Web,
either creatively or browsing.

####  Techniques:

  * Hide all access to URIs inside special "under the hood" windows or status bars; 
  * Use titles to identify resources; 
  * Introduce RDF properties to indicate short titles and icons to make this easier; 
  * Remove all URI-aware functions to a special (optional) menu; 
  * Allow files for upload, or other documents to be referenced by drag-and-drop, or copy referemce/link to clipped 

Web **servers** have to help by generating URIs for new documents. A new
document creation form should redirect the user to a document whose UIRI has
bene generatde, and which the user can then edit.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

