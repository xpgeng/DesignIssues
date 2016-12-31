Tim Berners-Lee

Date started: January 6, 1997

. Status: personal view, but corresponds  generally to the W3C architecture
for metadata.

.

Additions are at the end about consistency in label/metaset/collection syntax
and semantics.

The syntaxes used in this document are meant to illustrate the architecture
and be clear but are otherwise random. This note was written before the more
general [Semantic Web](https://www.w3.org/DesignIssues/Semantic.html) note.

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Axioms of Web Architecture: Metadata

* * *

#  Metadata Architecture

####  Preface

_This document was written before the Semantic Web Roadmap, but is an
introduction to the same ideas. Both introduce the world of machine-readable
data on the web. This document introduces the concepts in the historical
sequence at W3C, where the first driving applications of semantic web were
metadat, and the first driving metadata applications were endorsement labels
(PICS)_.

##  Documents, Metadata, and Links  

The thing which you get when you follow a link, when you de-reference a URI,
has a lot of names. Formally we call it a **resource**. Sometimes it is
referred to as a document because many of the things currently on the Web are
human readable documents. Sometimes it is referred to as an object when the
object is something which is more machine readable in nature or has hidden
state. I will use the words document and resource interchangeably in what
follows and sometimes may slip into using "object".

One of the characteristics of the World Wide Web is that resources, when you
retrieve them, do not stand simply by themselves without explanation, but
there is information about the resource. Information about information is
generally known as **Metadata**. Specifically, in the web design,

####  Definition

Metadata is machine understandable information about web resources or other
things  
---  
  
The phrase "machine understandable" is key.  We are talking here about
information which software agents can use in order to make life easier for us,
ensure we obey our principles, the law, check that we can trust what we are
doing, and make everything work more smoothly and rapidly. Metadata has well
defined semantics and structure.

Metadata was called "Metadata" because it started life, and is currently still
chiefly, information about web resources, so data about data.  In the future,
when the metadata languages and engines are more developed, it should also
form a strong basis for a web of machine understandable information about
anything: about the people, things, concepts and ideas.  We keep this fact in
our minds in the design, even though the first step is to make a system for
information about information.

For an example of metadata, when an object is retrieved using the HTTP
protocol, the protocol allows information about its date, its expiry date, its
owner, and other arbitrary information to be sent by the server. The world of
the World Wide Web is therefore a world of information and some of that
information is information about information. In order to have a coherent
picture of this, we need a few axioms about metadata. The first axiom is that
:

####  Axiom

metadata is data.  
---  
  
That is to say, information about information is to be counted in all respects
as information. There are various parts of this.

One is that metadata can be stored regarded as data, it can be stored in a
resource. So, one resource may contain information about itself or about
another resource. In current practice on the World Wide Web there are three
ways in which one gets metadata. The first is the data about a document
contained within the document itself, for example in the HEAD part of an HTML
documents or within word processor documents. The second is that during the
HTTP transfer the server transfers some metadata to the client about the
object which is being transferred. This, during an http GET, is transferred
from the server to the client and, during a PUT or a POST, is transferred from
the client to the server. One of the things which we have to rationalize in
our architecture of the World Wide Web is who exactly is making the statement.
Whose statement, whose property is that metadata. The third way in which
metadata is found is when it is looked up in another document. This practice
has not been very common until the PICS initiative was to define label formats
specifically for representing information about World Wide Web resources. The
PICS architecture specifically allows for PICS labels which are resources
about other resources to be buried within the resource itself, to be retrieved
as separate resources, or to be passed over during the http transaction. To
conclude,

Metadata about one document can occur within the document, or within a
separate document, or it may be transferred accompanying the document.  
  
---  
  
Put another way, metadata can be a first class object.

The second part of the above axiom is:

Metadata can describe metadata  
---  
  
That is, metadata itself may have attributes such as ownership and an expiry
date, and so there is meta-metadata but we don't distinguish many levels, we
just say that metadata is data and that from that it follows that it can have
other data about itself. This gives the Web a certain consistency.

##  The Form of Metadata  

Metadata consists of assertions about data, and such assertions typically,
when represented in computer systems, take the form of a name or type of
assertion and a set of parameters, just as in the natural language a sentence
takes the form of a verb and a subject, an object and various clauses.

####  Axiom

The architecture is of metadata represented as a set of independent
assertions.  
---  
  
This model implies that in general, two assertions about the same resource can
stand alone and independently. When they are grouped together in one place,
the combined assertion is simply the sum (actually the logical AND) of the
independent ones. Therefore (because AND is commutative) collections of
assertions are essentially unordered sets. This design decision rules out for
example, in simple sets of data, assertions which are somehow cumulative or
later ones override earlier ones. Each assertion stands independently of
others.

We will see below how logical expressions are formed to combine assertions in
more varied ways, and syntactic rules which allow the subject at least of the
assertion to be made implicit. But neither of these change the basic operation
of combining assertions in unordered AND lists.

###  Attributes

Assertions about resources are often referred to as attributes of the
resource. That is, the type of assertion is an assertion that the object, the
resource in question, has a particular named property such as it's author, and
in that case the parameter is the name or identity of the author. Similarly,
if the attribute is the document's date of expiry then the parameter is that
date.

Often, a group of assertions about the same resource occur together, in which
case the syntax generally omits the URI of that resource as it is implicit. In
these cases, when it is clear from the context about which resource the
assertion is being made, the assertion often takes the form of a list of
attributes and values. In RFC822 format messages, such as mail messages and
HTTP messages, metadata is transferred where the attribute name is an RFC822
header name and the rest of the RFC822 line is the value of the attribute,
such as Date: and From: and To: information. The attribute value pair model is
that used by most activities defining the semantics of metadata today.  

I use the word "assertion" to emphasize the fact that the attribute value pair
when it is transferred is a statement made by some party. It does not simply
and directly imply that the resource at any given time has that value for the
given attribute. It must be seen as a statement by a particular party with or
without implicit or explicit guarantees as to validity. Throughout the World
Wide Web, as trust becomes an important issue, it will be important for
software -- and people -- to keep track of and take into account who said what
in terms of data and metadata. So, our model of data of a resource is
something about which typically we know the creator or the person responsible,
and typically the date of which the information was created, which implies, in
the case of a piece of information which makes an assertion, the date at which
the assertion was made.

An assertion

> (A u1, p, q...)

typically has as explicit parameters,

  * the URI of the resource about which the assertion is made (u1). 
  * some identifier (A) for the type of assertion being made, such as author or date or expiry date. 
  * other parameters (p, q,...) according to the type of assertion. 

As implicit or explicit or implicit parameters,

  * The party making the assertion 
  * The date/time of the assertion 
  * etc... 

We can often make an analogy with programming languages. An assertion in
metadata can be compared with a function call in a programing language. In
object oriented languages, the object of the function has a special place
among the parameters just as the subject of an assertion does in metadata. In
object oriented languages, though, the set of possible functions depends on
the object, whereas in metadata the set of assertion types is more or less
unlimited, defined by independent choice of vocabulary. _Anyone can say
anything about anything_.

###  A space for attribute names

It is appropriate for the Web architecture to define like this the topology
and the general concepts of links and metadata. What about the significance of
individual relationships? Sometimes, as above, these are special, defined in
the architecture, and having an architectural significance or a significance
to the protocols. In other cases, the significance of relationships or indeed
of attributes is part of other specifications, other design, or other
applications, and must be defined easily by third parties. Therefore, the set
of such relationship and attributes names must be extremely easily extensible
and therefore extensible in a decentralized manner. This is why

the URL space is an appropriate space for the definition of attribute names.  
---  
  
We have already (1997) several vocabularies of attribute names: for example,
the HTML elements which can occur within the HEAD element, or as another
example, the headers in an HTTP request which specify attributes of the
object. These are defined within the scope of particular specifications. There
is always pressure to extend these specifications in a flexible way. HTTP
header names are generally extended arbitrarily by those doing experiments.
The same can also be true of HTML elements and extension mechanisms have been
proposed for both. If we look generically at the very wide space of all such
metadata attribute names, we find something in which the dictionary would be
so large that ad hoc arbitrary extension would be just as chaotic as central
registration would be stifling.

> **Aside: Comparison with Entity-Relationship models**.

>

> This architecture, in which the assertion identifier is taken from
(basically) URL space differs from the "Entity-relationship" (ER) model and
many similar models like it, including most object-oriented programming
systems. In an ER model, typically every object is typed and the type of an
object defines the attributes can have, and therefore the assertions which are
being made about it. Once a person is defined as having a name, address and
phone number, then the schema has to be altered or a new derived type of
person must be introduced before one can make assertions about the race, color
or credit card number of a person. The scope of the attribute name is the
entity type, just as in OOP the scope of a method name is an object type (or
interface)By contrast, in the web, the hypertext link allows statements of new
forms to be made about any object, even though (before anything other than
syntax checking) this may lead to nonsense or paradox. One can define a
property "coolness" within one's own part of the web, and then make statements
about the "coolness" of any object on the web.

>

> This design difference is in essence a resurfacing of the decision to make
links mondirectional, sacrificing consistency for scalability.

>

> An advantage of ER systems is that they allow one to work, in the user
interface for example, with a set of properties which "should" be defined for
each entity. You can define these in the Metadata's predicate calculus by
defining an expression for a "well specified" object. ("For all _X_ such that
_X_ is a customer _X_ is well-specified if there exists _n_ such that _n_ is
the name of _X_ and there exists _t_ such that _t_ is the telephone number of
_X_ and...)

>

> end of aside.

###  Metadata ("Entity") headers in HTTP

In the above it is important to realize that the HTTP headers which contain
what can be considered as metadata ("entity headers") should be separated
quite distinctly from HTTP headers which do not. HTTP headers which contain
metadata contain information which can follow the document around. For
example, it is reasonable for a cache to pass such information on without
treatment, it is reasonable for clients or other programs which process data
to store those headers as metadata with the document for later processing. The
content of those headers do not have to be associated with that particular
HTTP transaction. By contrast, the RFC822 headers in HTTP which deal
specifically with the transaction or deal specifically with the TCP link
between the two application programs have a shorter scope and can only be
regarded as parameters of the HTTP method. To make this separation clear will
be to make it easier not only to understand HTTP and how it should be
processed, it will also make it clear which pieces of HTTP can be used easily
and transparently by other protocols which may use different methods with
different parameters. The clarification of the architecture of HTTP such that
both the metadata and the methods can be extended into other domains is an
important part of the work of the World Wide Web Consortium. The Internet
protocols SMTP and NNTP and HTTP as well as many new and proposed protocols
share much of the semantics of the RFC822 headers. Formalizing the shared
space and making it clear that there is a single design for a particular
header, rather than four designs which are independent and happen to look very
similar, requires a general architecture, some careful thought, and is
essential for the future design of protocols. It will allow protocol design to
happen in small groups which can take for granted the bulk of previous work
and concentrate on independent new design.

####  Authorship of HTTP entity headers

It may be possible to remove or at least encompass the apparent anomaly of
metadata transferred from an HTTP server by creating a special link type which
links the document itself to the set of attributes which the server would give
in the HTTP headers. In other words, the server would be able to say, "here is
a document, here is some metadata about it, and the metadata about it has the
following URL". This would allow one, for example, request a signed copy of
the HTTP headers. It would allow one to ask about the intellectual property
rights of those headers, and the authorship of those headers.

It is important to be completely clear about the authorship of the HTTP
headers. The server should be seen as a software agent acting on behalf of a
party which is the publisher or document author: the definer of the URI to
resource identity mapping. The webmaster is only an administrator who is
responsible for ensuing that (through an appropriately configured server) the
transactions on the wire faithfully represent the statements and wishes of
that party.

##  Links  

An assertion of relationship between two resources is known as a **link**.

In this case, it is a triple

> (_A u1 u2_)

of:

  * the type of assertion being made, that is, the relationship which is being asserted, 
  * the first URI, 
  * and the second URI. 

These sorts of assertions, links, are the basis of navigation in the World
Wide Web; they can be used for building structure within the World Wide Web
and also for creating a semantic Web which can express knowledge about the
world itself. That is to say, links may be used both for the structure of
data, in which case they are metadata, but also they may be used as a form of
data.

Links, like all metadata can be transferred in three ways. They can be
embedded in a document, which is one end of the link, they can be transferred
in an HTTP message, for example what is called the header of the document, and
they can be stored in a third document. This latter method has not been used
widely on the World Wide Web to date.

##  Goal: Self-describing information  

A critical part of the design of the whole system is the way that the
semantics of metadata or indeed of data are defined. The semantics of metadata
in our RFC822 headers in mail messages and in http messages are defined by
hand in english in the specifications of those protocols. The PICS system
takes this to one stage further in terms of flexibility by allowing a message
to contain a pointer to the document which defines, in human readable terms,
the semantics of each assertion made within a PICS label. In the future we
would like to move toward a state in which any metadata or eventually any form
of machine readable data carries a reference to the specification of the
semantics of all the assertions made within it.

For example, suppose that when a link is defined between two documents, the
relationship which is being asserted is defined in a such way that it can be
looked up on the World Wide Web (i.e. using some form of URI), and someone or
some program, which has not come across that relationship before can follow
the link and extend its understanding or functionality to take advantage of
this new form of assertion.

In the case of PICS, one can dynamically pick up a human readable definition
of what that assertion really means. In PICS (and in theory in SGML using
DTDs), one can also pick up a machine readable definition of what form that
assertion can take, what syntax, what types of parameters it can take. This
allows a human interface to a new PICS scheme to built on the fly. To go one
step further, one could, given a suitable logic or knowledge representation
language, pick up a machine readable definition of the semantics of that
assertion in terms of other relationships.

The advantages of such self describing information is that it allows
development of new applications and new functionality independently by many
groups across the web. Without self-describing information, development must
wait for large companies or standards committees to meet and agree on the
commonly agreed semantics.

Of course a pragmatic way of extending software to handle new forms of
information is to dynamically download the code to support a software object
which can handle such data for one. Whereas this is a powerful technique, and
one which will be used increasingly, it is not sufficient. It is not
sufficient because one has to trust the implementation of the object, and the
state.

####  Goal

As much as possible of the syntax and semantics should be able to be acquired
by reference from a metadata document.  
---  
  
###  Building Applications using Link Relationships

It turns out that a very large number of applications both built on top of the
web and also built within the infrastructure of the Web can largely be built
by defining new relationship types. Examples of these are the document
versioning problem which can be largely solved by defining link values
relating documents to previous and future versions and to lists of versions;
intellectual property rights, distribution terms, and other labeling which can
be solved by making a link from one document to the document containing the
metadata.

* * *

###  Summary so far

  1. Metadata is data 
  2. Metadata may refer to any resource which has a URI 
  3. Metadata may be stored in any resource no matter to which resource it refers 
  4. Metadata can be regarded as a set of assertions, each assertion being about a resource  (A  _u1_  ...). 
  5. Assertions which state a named relationship between two resources are known links  (A _u1 u2_) 
  6. Assertion types (including link relationships) should be first class objects in the sense that they should be able to be defined in addressable resources and referred to by the address of that resource  A in { u } 
  7. The development of new assertion types and link relationships should be done in a consistent manner so that these sort of assertions can be treated generically by people and by software. 

* * *

_Rough from here on down_

###  Label syntax: Assertions about a common subject

When labeling information, it is often useful to make a lot of statements
about the same object. It is also useful to be able to make the same set of
statements about a set of resources. For example, the assertions

    
    
    (A1 u1  a b ... )
     (A2 u1  c d )
     (A2 u1  a f g h )
     
    

might be written

    
    
    (for u1
             (A1 a b ... )
             (A2 c d )
             (A3 a f g h )
     )
     
    

Therefore in the syntax of an actual assertion the subject is implicit. This
is just the case with RFC822 headers which implicitly refer to the following
body, and with HTML "HEAD" element contents which implicitly refer to the
containing document.  (Though notice there is a fundamental difference,
discussed [below](https://www.w3.org/DesignIssues/w:/DesignIssues/temp.html#mesages), between a general label
and a message header because the message header is definitive.)

So it is wise to recognise the label as case which it is wise to specifically
optimize in the syntax. _[In RDF this indeed the case, that the subject is
established as a context, and then many properties are given within that
context. -2000/9]_

Assertions, when the subject is implicit, are known as attribute-value pairs
as discussed above. Let's use the term "label" for a set of assertions with
the subject extracted.  Like the label on a jam jar, it contains information
but there must be something else (in this case if its placement on the jar)
which tells you to what it applies.  (The PICS label in fact contained other
information too, including the subject and meta-meta-data about the authorship
of the label.)

Local definition:

A label is a set of assertions with a common implicit subject.  In this
architecture it is a set of attribute-value pairs  
---  
  
_(There is a convention that you can write "Jam" on a jam jar label.  You
don't write "Jam jar" or "Jam Jar label".   Even though I once saw a label on
a cardboard box with the words "Equipment shipping box label" on it!)_

###  Authorship of Metadata

It follows from the fact that metadata is data that here can be metadata about
it.  Some of this metadata becomes crucial when we consider a trust model.
The logic we need includes the author of metadata

p1: (A u1 . . .)

where p1 is ,in a system with low trust, the author as stated, but in a
cryptographically secure system is a principle represented by a key.

On the web, the granularity of information is the resource. Authorship and
access control genrally use this granularity. Therefore, typically, the trust
one places in an assertion is function the document which asserted it, and the
metadata about that document. However, when information is then combined from
many resources, one needs a language which allows the source of the original
to be recorded. Like blockquote in HTML, this separates the data itself from
the resource, so the resource does assert the data directly but asserts that
it was asserted.

##  Analysing labels

See [Analysing PICS labels as generic Metadata](https://www.w3.org/DesignIssues/Labels.html)

where we look at PICS labels and try to sift out the actual semantics of them.
This is a thought experiment generating requiremnts. The conclusions are that
information such as authorship and date information in fact form a tree of
assertions about assertions, and it is important to be clear about the
structure of that tree. The notion of a message is brought up there too, but
not followed up as it is not germaine to the discussion at this point.

##  Algebraic Manipulations

If you can make assumptions about the properties of labels then you can
manipulate them, possibly without knowing everything about their meaning.
Properties such as commutativity, transitivity and associativity would be very
useful to have easily available: perhaps in the syntax, or failing that in the
schema.

[See [Semantic Web roadmap](https://www.w3.org/DesignIssues/Semantic.html) for higher levels of logic]

For example, given a label saying a pair of jeans has a 32 inch waist and a
price of $28, I can deduce a label which just has the price of $28.  But given
a label which says that the punishment for the crime is a 2 month in jail and
a fine of $3000,  I can't deduce one that says that that the punishment  is 2
months in jail.

A typical use of metadata will be to provide a statement along with its proof
to be verified by another party.  Being able to process these things
efficiently and with limited knowledge will be crucial.

The most practical way to do this is to create a basic commonvocabulary for
the logical functions. Sometimes known as the "RDF upper layers", these are
mentioned in the [note on the Semantic Web.](https://www.w3.org/DesignIssues/Semantic.html)

####  Ordered/Unordered

The axiom of independence of assertions above gives us that in any set of
assertions, as assertions are independently true, specific assertions may be
removed or reordered, leaving the document just as valid (though possibly less
informative).

Examples of unordered things currently are: RFC822 message header lines, SGML
attributes. Examples of ordered things are: HTTP header lines and SGML
elements.

Do we need a form in which we can make an assertion which has many parameters
which are in fact not mutable in any way?

##  Summary of Requirements

There are ways of representing  the above things:  messages, labels,
specifying labels, and statements and distinguish between them.

As much as possible of the syntax and semantics should be able to be acquired
by reference from a metadata document.

It must be possible to mix multiple vocabularies within the same scope.

The syntax and structure should be such that as many manipulations as possible
can be done without having to know the semantics of the vocabulary in use.

A common voabulary for basic logic and knowledge representation functionality
will be required.

* * *

##  References

PICS \- The PICS project was a project to define standards for interchange of
endorsement information, aimed at the content filterting problem. See the PICS
home page.

* * *

Tim BL,  January 1997

Last edit $Date: 2009/08/27 21:38:08 $

