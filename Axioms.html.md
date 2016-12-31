Tim Berners-Lee

Date: December 19, 1996

Status: personal view. Editing status: Italic text is rough. Reques complete
edit and possibly massaging, but content is basically there. Words such as
"axiom" and "theorem" are used with gay abandon and the reverse of rigour
here..

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Universal Resource Identifiers -- Axioms of Web Architecture

  * Universal Resource Identifiers
    * Universality
    * Global uniqueness
    * Sameness
    * Identity
    * Canonicalization - when is a URI the saem URI?
    * Identity abuse
    * Not a unique space, just universal
  * Identity, State and GET
    * Opacity
    * Query strings
  * Relative URIs
    * Matrix spaces
  * [The properties of different URI schemes](https://www.w3.org/DesignIssues/Axioms.html#Properties)

* * *

#  Universal Resource Identifiers

The operation of the World Wide Web, and its interoperability between
platforms of differing hardware and software manufacturers, depend on the
specifications of protocols such as HTTP, data formats such as HTML, and other
syntaxes such as the URL or, more generally, URI specifications. Behind these
specifications lie some important rules of behavior which determine the
foundation of the properties of the Web. These are rules and principles upon
which new designs of programs and the behavior of people must rely. And it is
that reliance which makes the Web both an information space which works now,
and the foundation for future applications, protocols, and extensions. The
more essential of these I refer to loosely as axioms, and the most basic of
these have to do with URI.  

The aim of thes article is to summarize in one place the axioms of Web
architecture: those invariant aspects of Web design which are implied or
stated in various specifications or in some cases simply part of the folk law
of how the Web ought to be used. Especially for these latter cases, this
article is designed to tie together the Web community in a common
understanding of how we can progress, extend, and evolve the Web protocols.
_Terms such as "axiom", and "theorem" are used with gay abandon rather than
precision as this not a mathematical treatise._  

##  Universal Resource Identifiers  

The Web is a universal information space. It is a space in the sense that
things in it have an address. The "addresses", "names", or as we call them
here identifiers, are the subject of this article.  They are called
**Universal Resource Identifiers** (URIs).

An information object is "on the web" if it has a URI.  Objects which have
URIs are sometimes known as "First Class Objects" (FCOs).  The Web works best
when any information object of value and identity is a first class object.  If
something does not have a URI, you can't refer to it, and the power of the Web
is the less for that.

By _Universal_ I mean that the web is declared to be able to contain in
principle every bit of information accessible by networks. It was designed to
be able to include existing information systems such as FTP, and to be able
simply in the future to be extendable to include any new information system.

The URI schemes identify things various different types of information object,
wich play different roles in the protocols. Some identify services, connection
end points, and so on, but a fundamental underlying architectural notion is of
information objects - otherwise known as generic **documents**. These can be
**represented** by strings of bits. An information object conveys something -
it may be art, poetry, sensor values or mathematical equations.

The Semantic Web allows an information objects to give information about
anything - real objects, abstract concepts. In this case, by combining the
identifier of a document with the identifier, within that document, of
something it describes, one forms an idenifier for anything. This is done with
"#" and fragment identifiers, discussed later.

####  Axiom 0: Universality 1

Any resource anywhere can be given a URI

####  Axiom 0a: Universality 2

Any resource of significance should be given a URI.

(What sorts of things can be resources? A very wide variety. The URI concept
istelf puts no limits on this. However, URIs are divided into schemes, such as
http: and telenet:, and the specification of each scheme determines what sort
of things can be resources in that scheme. Schemes are discussed later.)

This means that no information which has any significance and persistence
should be made available in a way that one cannot refer to it with a URI.

In fact, we take care before extending the URIs to include any old system,
because URIs of any form must also be understood anywhere in the world.

When you specify a URI, a Universal Resource Identifier, (often people use the
more restricted term "URL", Uniform Resource Locator), first axiom is:

####  Axiom 1: Global scope

It doesn't matter to whom or where you specify that URI, it will have the same
meaning.

So, this means that there is no scope within which a URI must be placed for it
to hold. All you need say is that something is "on the Web" and that is
enough. Anyone can follow that hypertext link, anyone can look up that URI.
Now, the sorts of URI that we find typically start "`http:`" indicating that
this URI points into a space of objects accessed using the hypertext transfer
protocol. But there are many other sorts of URI, and a key to the Universality
is that this universal space of identifiers whether you call them names
addresses or locators, is universal through the range of pre-existing
protocols such as SMTP, and NNTP, through protocols designed for the Web
specifically (HTTP) through, in principal, to new protocols yet to be
invented. So, there is a theorem, if you like, of URIs that:

Any new space of identifiers or address space can be represented as a subset
of URI space.

You can prove this easily because there is no limit to the length of a URI and
any new name system or address system can be incorporated simply by encoding
the value of names or addresses into an acceptable, printable string and
prefacing that string with a standard prefix for that new scheme. So, you
could replace http:, for example with ISBN: or X500: depending on the new
scheme.  

There is a second axiom of URIs which is difficult to characterize exactly but
accepted in some form by everyone who uses the Web in some form and that is
that:

####  Axiom 2a: sameness

a URI will repeatably refer to "the same" thing

The same identifier string is expected from one day to the next to point to,
in some sense, the same object. That is a very important axiom, and it leaves
open the "in some sense" behind which is a very complicated discussion of the
concept of identity. When are two things "in some sense" the same.  

####  [Axiom 2b: identity](https://www.w3.org/DesignIssues/Axioms.html#Universality)

of URIs clears up the vagueness of 2a and is that

the significance of identity for a given URI is determined by the person who
owns the URI, who first determined what it points to.

We do not discuss in detail here the definition of owner because the mechanism
by which a person or agent comes to get or create or be allocated a new URI
varies from scheme to scheme. But in every scheme in practice there is a way
of making a new URI. In many schemes, the scheme itself implies or requires
some properties of identity. The scheme, if you like, imposes constraints
within which the owner of a URI is free to define identity.

The implication here is that we will need protocols for exchanging any
guarantees of the properties of given URIs: they are not simply laid down in
the specification of the web. This is in tune with a general philosophical
principle of design (after Bob Scheifler and others):

> The technology should define _mechanisms_ wherever possible without defining
_policy_.

because we recognize here that many properties of URIs are social rather than
technical in origin.

Therefore, you will find pointers in hypertext which point to documents which
never change but you will also find pointers to documents which change with
time. You will find pointers to documents which are available in more than one
format. You will find pointers to documents which look different depending on
who is asking for them. There are ways to describe in a machine or human
readable way exactly what sort of repeatability you would expect from a URI,
but the architecture of the Web is that that is for something for the owner of
the URI to determine.

####  Identity abuse

_All the same, a word of caution is appropriate about the indiscriminate or
deliberately misleading abuse of the identity of the object refered to by a
URI. A web server is often in a position to know a lot of context about a
request. This can include for example, the person who is asking, the document
they were reading last from which they followed the link.  It is possible to
use this information to dramatically change the content of the document
refered to.  This undermines the concept of identity and of reference in
general.  To do that without making it clear is misleading both to anyone who
quotes the URI of a page or who follows the link._

_Unless it is clearly indicated on the page (or using a future protocol) , to
return differing information for the same URI must be considered a form of
deception.  It also of course messes up caches. Note the HTTP 1.1 "Vary"
header allows this indication to be passed._

####  When is a URI "the same URI"?

Two URIs are the same if (and only if) they are the same character for
character.

Two URIs which are different may in fact be equivalent, in that they may refer
to the same thing, and give the same result in all operations. In some cases
any agent looking at two URIs can deduce, from knowledge of the various web
standards, that they must be equivalent, in that they must refer to the same
thing. For example, HTTP URIs contain domain names, and the Domain Name System
is case-insensitive. Therefore, while it is normal practice to use lower case
for domain names, any agent which comes across two URIs which differ only in
the case of the domain name can conclude that they must refer to the same
thing. In another case, a client agent may use out-of-band information about a
web site to know that its URI paths are case-invariant, or that URIs ending in
"/" and "/index.html" are equivalent. It is bad engineering practice to make
new protocols require such processing.

There are a long series of such algorithms. Which ones an agent can apply
depends on what information it has to hand, and depend on what knowledge of
which protocols has been programmed into it. New schemes may be defined in the
future, for which different forms of canonicalization can be done. There is,
therefore, **no definitive canonicalization** algorithm for URIs. Generic URI
handling code should handle URIs as case-sensitive character strings. It is
**not** recommended that, for example, encryption and signature algorithms
attempt to canonicalize URIs before signature, because of the arbitrariness of
any attempt to define a canonicalization algorithm.

The only canonicalization one could insist upon would be that defined by the
algorithms in the URI specifications. This incldues the generation of an
absolute URI from and the hex-encoding or decoding of all non-reserved
characters.

###  URIs and the Test of Independent Invention

The concept of a web as a "space" is based on these axioms of design. As a
result, the web behaves to a certain extent as a system with state, and an
important part of the work of the system is the distribution of visible state
rather than the execution of invisible remote operations.

####  Axiom 3: non unique

URI space does not have to be the only universal space

The assertion that the space of URIs is a universal space sometimes encounters
opposition from those who feel there should not be one universal space. These
people need not oppose the concept because it is not of a single universal
space: Indeed, the fact that URIs form universal space does not prevent anyone
else from forming their own universal space, which of course by definition
would be able to envelop within it as a subset the universal URI space.
Therefore the web meets the "independent design" test, that if a similar
system had been concurrently and independently invented elsewhere, in such a
way that the arbitrary design decisions were made differently, when they met
later, the two systems could be made to interoperate.

There may be in the world many universal spaces, and there need not be any
particular quarrel about one particular one having a special status. (Of
course, having very many may not be very useful, and in the World Wide Web,
the URI space plays a special role by being the universal space chosen in that
design.)

For example, it would be possible to map all international telephone numbers
into URI space very easily, by inventing a new URI "phone:" after which was
the phone number. It would in fact also conversely be possible to map URIs
into international phone numbers by allocating a special phone number not used
by anyone else, perhaps a special country code for URI space, and then
converting all URIs into a decimal representation. In that case, both URIs and
phone numbers would be universal spaces. Identifiers in one space would be
consisting only of numbers, and in the other of alphanumeric characters. One
would be shorter than the other, but there is no reason why, in principle, the
two could not co-exist, allowing you to dial any Web object from a telephone
as a telephone number, and point to any phone from a hypertext document.  

So, on this last axiom rests not specifically the operation of the web, but
its acceptance as a non-domineering technology, and therefore our trust in its
future evolvability.

###  Identity, State and GET

From the fact that the thing referenced by the URI is in some sense repeatably
the same suggests that in a large number of cases the result of de-referencing
the URI will be exactly the same, especially during a short period of time.
This leads to the possibility of caching information. It leads to the whole
concept of the Web as an information space rather than a computing program. It
is a very fundamental concept. Not only do the concepts of navigation around
the space remembering "places" in the Web and other humanly visible aspects of
the nature of the Web depend on it, but also many technical architectural
properties depend on it. For example, the implication is that the GET
operation in HTTP is an operation which is expected to repeatably return the
same result. As a result of that, anyone may know that under certain
circumstances that they may instead of repeating an HTTP operation, use the
result of a previous operation. The operation is "idempotent". This, in turn,
allows software to use previously fetched copies of documents and it requires
that the HTTP GET operation should have no _side effects_. For example, GET
should never be used to initiate another operation which will change state. In
general (see the HTTP 1.1 spec) the notion of side-effects is that of any
significant communication between the parties. A user can never be held
accountable to anything as a result of doing a GET. The server may for example
log the number of requests, but the client user cannot be held responsible for
that: it does not constitute communication between the two parties.

It is wrong to represent the user doing a GET as committing to something or
putting themselves on a mailing list, doing any operation which effects the
state of the Web or the state of the users relationship with the information
provider or the server. To ignore this rule can be to introduce a serious
security problem in a website.

So, from this principal, we have a principal of the http protocol that :

####  Axiom

In HTTP, GET must not have side effects.

The introduction of any other method apart from GET which has no side effects
is also incorrect, because the results of such an operation effectively form a
separate address space, which violates the universality. A pragmatic symptom
would be that hypertext links would have to contain the method as well as the
URI in order to able to address the new space, which people would soon want to
do.

####  Axiom

In HTTP, anything which does not have side-effects should use GET

This means that for people implementing systems in which users request
information and execute operations using forms, when the form simply requests
information it must result in a GET operation. Indeed this is very much to be
favored over a post operation because the result of a GET operation has a URI
and may be leaked to, for example, may be put into a bookmark. This violates
the [axiom of universality](https://www.w3.org/DesignIssues/Axioms.html#Universality2) above.

However, when the result of a form is to execute an operation, which changes
the Web or a relationship of a user to anyone else, then the GET operation may
not be used and POST or other method either through HTTP or mail must be used.
Only by sticking to this rule can such systems interoperate with caches and
other agents which exploit the repeatability of HTTP GET of URI dereferencing
in the future.  

The axiom above about URIs pointing in principle to conceptually the same
thing has a corollary which says that URIs do not always have to point to
_exactly_ the same set of bits. This means that URIs can be "generic". See the
[discussion of generic URIs](https://www.w3.org/DesignIssues/Generic.html).  

###  The Opacity Axiom  

The concept of an identifier referring to a resource is very fundamental in
the World Wide Web. Identifiers will refer to resources all different sorts.
Any addressable thing will have an identifier. There are mechanisms we have
just discussed for extending the spaces of identifiers into name spaces which
have different properties. Different spaces may address different sorts of
objects, and the relationship between the identifier and the object, such as
the uniqueness of the object and the concept of identity, may vary. A very
important axiom of the Web is that in general:

####  Axiom: Opacity of URIs

The only thing you can use an identifier for is to refer to an object. When
you are not dereferencing, you should not look at the contents of the URI
string to gain other information.

For the bulk of Web use URIs are passed around without anyone looking at their
internal contents, the content of the string itself. This is known as the
**opacity**. Software should be made to treat URIs as generally as possible,
to allow the most reuse of existing or future schemes.

For example, within an HTTP identifier, even when access is made to the
object, the client machine looks at the first part of the identifier to
determine which server machine to talk to and from then on the rest of the
string is defined to be opaque to the client. That is the client does not look
inside it, it can not deduce an information from the characters in that
identifier. It has been very tempting from time to time for people to write
software in which a client will look at a string such as ".html" on the end of
an identifier, and come to a conclusion that it might be hypertext markup file
when dereferenced. But these thoughts of breaking of the rule could lead to a
broken architecture in which the generality of URIs is something one can no
longer depend on.

Opacity of the URIs opens the door to new URI schemes, it opens the door to
excitingly different interpretations of HTTP URI spaces. For example, servers
can use the opaque string to carry all kinds of parameters to spaces with new
topologies.

As a result of this axiom the many parts of metadata, that information about
the object that a client might be tempted to infer from the actual sting value
of the URI but can't, have to be made available through the HTTP protocol.
That is the purpose of some of the headers of the HTTP protocol and is
discussed in the next section.

Another example of a reason for keeping the URI opaque is that other address
spaces for example within an HTTP servers address space the rest of the URI
can be used as a coded representation of a name in some local space.
Typically, when that is done, when the server serves as a gateway into an
existing space, then it is extremely useful to be able to use the string in
any way consistent with the URI syntax rules to represent coded names from the
other space. The server can encode, within the URI, complex locations in some
legacy system which is being mapped into an information space for the first
time. So, for example, names which come from names in some sort of a database
might by coincidence end up with .html with no implication that there is a
hypertext markup language document involved, just that the particular encoding
used happened to produce that string of bits.

####  Query strings

An important case is the treatment of the question mark in HTML forms. There
is a convention that infformation returned from HTML forms is returned by
encoding it and appending it to the URI. The question mark within the URI is
used to separate the basic URI from parameters which are appended to it to
perform an operation. A typical use is for a search, and the string following
the question mark is often known as a query string.

When a query string and fragment identifier are used, the function evaluated
on dereferencing a URL

    
    
             http://foo/bar?baz#frag
     Is
             select(get( "foo", "query("bar","baz")), "frag") 
     
    

where

  * query (resource, querystring) is evaluated by the resource "bar" 
  * "bar" is opaque to all except the server "foo" ; 
  * "baz" is a format understood by client and by the resource "foo/bar"; 
  * get(server, restofuri) is executed by the client engine which understands "foo" but not "bar" 
  * select(fragmentid, resource) is evaluated on the client by the resource's handling code 

Query strings are clearly not opaque to the client. However, they should be
opaque to (for example) proxies.

Apart from searches, other operations are performed, for example by those
filling out HTML forms which are set up to have an HTTP "GET" action. This is
done in situations in which the results of that operation of the URI are
quasi-static. In other words, the resource referred to by the complete URI
(including the query mark and the query string after it) follows the axiom of
slow change above: the result of performing the operation is repeatable in
some fashion.

It is tempting and often done to assume that the result of such an operation
will be more transient than that of a URI with less or without a query string.
To make this assumption breaks the Opacity rule in general. Not only that, but
this is in many cases a completely wrong assumption. For example, the query
string is sometimes used to indicate parameters such as a personalized sub-
space which is being browsed. Unfortunately, because the Opacity rule has been
broken by clients and caches which don't cache documents whose URIs contain
question marks, the question mark is sometimes been deliberately inserted in
order to defeat caches. This creeping use of non-standard and axiom breaking
conventions could clearly be damaging to other systems which use the question
mark for other reasons for perfectly cacheable documents.

##  Hierarchies and Relative URIs

While discussing the universality of Universal Resource Identifiers, it is as
well to discuss the place of the Universal Syntax as this has been the source
of some misunderstanding as to the intent and advantages behind this. The URI
Syntax, now famous through its HTTP form uses slashes to indicate a
hierarchical structured name or address. Apart from that, the strings between
the slashes are opaque. There is nothing to say that the string between a
double slash and a slash must be in all URI schemes a fully qualified domain
name; there is nothing to relate strings between single slashes to parts of a
unix file name. The reason that the slashes have been instituted as common
universal syntax for a hierarchical boundary is that hierarchical schemes are
common and that relative naming within a hierarchical space has many
advantages.

Relative naming allows small groups of documents which are located close
within a tree to refer to each other without being aware of their absolute
position within any absolute tree. It turns out that for scalability of the
creation of material on the Web, this is essential. This has been found both
for file names in most modern operating systems and for HTTP URLs, and one can
also reasonably assume that it will be true for any other hierarchical scheme.
Therefore, it is important that the generic concept of a hierarchical scheme
is kept separate for future use from specific schemes which involve possibly
to be outdated forms such as fully qualified domain names.  

####  An example in using relative URIs

Let us take, for example, the exercise of mapping an international telephone
number onto the URL. International telephone numbers are hierarchical. For
example, the meaning of and the format of a telephone number depends on the
country, but there is a universal format for a telephone number in the world
which can be understood everywhere. This format is, in fact, a plus sign
indicating that one starts at the top of the hierarchy: that this is an
absolute international telephone number. It is followed by the country code,
the area code (if any) and the telephone number. Mapping this onto the URL
syntax, the double slash would be used to indicate that one is starting from
the top of the tree, so the number

+1 (617) 253-5708

would be written with a double slash instead of the plus and then slashes at
the other hierarchical boundaries.:

    
    
            phone://1/617/253-5708
     
    

(The dash here is used for decoration. In practice people like to break
telephone numbers up in various ways for readability, even though the
punctuation has no hierarchical significance.) Of course, there could be other
mappings used, but let us look at how this particular mapping using the
slashes would be used in relative URIs. Suppose we are in a context in which
that telephone number is the default. Suppose, for example we have declared
that that number is the absolute base telephone number ("base URL") within a
conversation: typically, we are talking to somebody who lives in the same area
code.

Using the relative URL pausing rules, we can refer to another local telephone
number simple as, for example, 861-5000 with no punctuation. This is just what
we do in practice. We can refer to a telephone number within the same country
as /800/123-4567. Although these are not quite the conventions currently used
for telephone numbers, they are just as compact as the various conventions of
putting brackets around the area code, and would probably be parsed correctly
by a human.

To indicate an international number we simply start with a double slash. For
example,

    
    
            phone://41/22/767-6111. 
     
    

Now, suppose instead we had used another system. We had just decided that for
consistency, we would simply use the plus sign and for example, parenthesis
around an area code. This would mean that whereas you can use the conventions
of simply omitting the area code for the local telephone number, and you could
use a plus sign to indicate an international telephone number. If you put
`phone:` in front of it, to have it correctly parsed by a URL parser, you
would always have to use the full international form. Now, there may be some
who would prefer to always see the full international form in telephone
numbers because telephone numbers are of fairly limited length. However, the
principle of relative names or local telephone numbers being useful is
established beyond question. There is also perhaps as much public use of the
double slash in URIs as there is of the plus sign in international telephone
numbers. (Within the United States of America there seem to be relatively few
people who understand the significance of the plus sign or for that matter
know what their country code is!).

So, in general when looking at new naming schemes which may have a
hierarchical nature we should regard the slash and the double slash as common
syntax. It may be that we can transition to a shorter form in which, for
example, a double slash is assumed after the colon in a fully qualified URL in
order to address the worry that the URL syntax is clumsy when you include the
scheme name prefix. _  
_

####  Myth:

Myth: "The // must only be used to introduce a fully qualified domain name."

####  Grandfathering hierarchies: generalizing the scheme

It is worth noting that the syntax with the double slash can in fact be
extended for use with a triple slash if one wanted to be able to start at any
level in a much more complicated hierarchical structure. For example, suppose
international telephone numbers were to be extended to cover a planetary code
in the future. Then the planetary code could be attached to the front of the
international code. The triple slash could introduce the interplanetary code,
and the double slash would introduce the international code. Indeed, this is
how the double slash came to be: when hierarchical naming schemes such as
those in unix file systems was extended to a networks file system on the
Apollo domain the extra slash was introduced. Similarly, Microsoft NT
networking now uses double backslash in exactly the same way.

RFC1630 is an information RFC I wrote about URIs in WWW because getting
consensus on the philosophy of all this in open forum ws going to take a long
time at best. It contains an algorithm for parsing relative URIs which in fact
would pause a relative URI in an environment with any arbitrary number of
consecutive slashes. (The only problem with this scheme is, like others which
use the same delimiter for beginning and ending strings or that one cannot
represent an empty string. This is already a problem with the file syntax when
an empty string is used for the host name resulting in three consecutive
slashes.)_  
_

To quote RFC1630:

> If the scheme parts are different, the whole absolute URI must be given.
Otherwise, the scheme is omitted, and:

>

> If the partial URI starts with a non-zero number of consecutive slashes,
then everything from the context URI up to (but not including) the first
occurrence of exactly the same number of consecutive slashes which has no
greater number of consecutive slashes anywhere to the right of it is taken to
be the same and so prepended to the partial URL to form the full URL.
Otherwise:

>

> The last part of the path of the context URI (anything following the
rightmost slash) is removed, and the given partial URI appended in its place,
and then:

>

> Within the result, all occurrences of "xxx/../" or "/." are recursively
removed, where xxx, ".." and "." are complete path elements.

The algorithm may not be perfect in its handling of "." and "..", but it
applies to any numbler of slashes.

###  Matrix spaces and Semicolons

There are a lot of web sites in which documents -- often virtual document --
vary along several dimensions. They are naturally arranged not on a tree but
on a matrix. The URI for a map, for example, might be:_  
_

    
    
    _         //moremaps.com/map/color;lat=50;long=20;scale=32000  
    
    _
    

(I had an idea to make special form of relative URIs for these. See [Matrix
URIs](https://www.w3.org/DesignIssues/MatrixURIs.html) for the idea, not a feature of the web as of 2001.)

##  The properties of different URI schemes

As noted above, the concept of a URI itself does not define the particular
identity properties which exist between a URI and the resource associated with
it. The [axiom above](https://www.w3.org/DesignIssues/Axioms.html#Universality) leaves the owner of the URI to
define it. However, different URI schemes are defined and implemented in
different ways, and this itself can impose restrictions on the mapping.

Some of the properties of URI to resource mappings which vary from space to
space were discussed in RFC1630. Some schemes (such as HTTP) leave answers up
to the information publisher (URI owner).

There is a lot of flexibility and growth to be gained by allowing any sort of
URI, not one from a particular scheme, in most circumstances. Similarly, one
should not make assumptions about the schemes involved. This is a facet of the
particular parameters about how the technology is used. The choice of type URI
in a pracical use of a language is an important flexibility point.

Comparison of some URI schemes  Scheme prefix  |  Identity relationship: what
does the URI correspond to?  |  Reuse  |  Persistence  
---|---|---|---  
http  |  Geneneric document as :defined by publisher. Generic URIs possible
with content negotiation  |  defined by publisher  |  defined by publisher  
ftp:  |  sequence of bits  |  defined by publisher  |  defined by publisher  
uuid:  |  expectation of uniqueness has to be upheld by publisher  |  defined
by publisher  |  (no dereference)  
sha1:  |  sequence of bits.  |  mathematically extremely unlikely  |  (no
dereference)  
mid:  |  Email message. Should be 1:1 modulo recoding, and header
addition/deletion  |  Can happen after 2 years according to the spec, but
absolutely not recommended  |  (no derefernce)  
mailto:  |  mailbox as used in email protocols  |  Socially unacceptable  |
(no dereference)  
telnet:  |  connection endpoint for interactive login service  |  defined by
publisher  |  (no dereference)  
  
###  How not to do it

Typical URI abuse by breaking this rule is occurs when a document format
provides one URI space for a "name"and one for a "location".

&lt;a href="uri1" urn="foo"&gt;

or for example the SGML reference to a "public identifier" and a "system
identifier".

The Web way is to have a reference to one URI. If in the same document you
want to incldue information such as other in some ways equivalent identifiers,
then you embed that in your document as [metadata](https://www.w3.org/DesignIssues/Metadata.html), to be
discussed later.

That allows the exatct relationship to be expressed without ambiguity, with
much more pwer and generality, and with consistency across applications.

###  See also

  * [Cool URIs don't change](https://www.w3.org/DesignIssues//Provider/Style/URI.html) \- persistence in the HTTP space 
  * [Hall of Flame](https://www.w3.org/DesignIssues/AxiomsHAF) \-- how not to do it 

* * *

$Id: Axioms.html,v 1.36 2009/03/17 17:25:35 timbl Exp $

[Next: Fragmement Identifiers](https://www.w3.org/DesignIssues/Fragment.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

