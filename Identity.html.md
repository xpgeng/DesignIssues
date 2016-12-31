Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Web Design Issues

_This page assumes an imaginary nsmespace referred to as play: which is used
only for the sake of example. The readers is assumed to be able to guess its
specifictaion.Much of this page was originally a note to the [Strawman
Syntax](https://www.w3.org/DesignIssues/Syntax.html)._

* * *

###  Identifiers - what is identified?

When XML is used to represent a directed laballed graph which is used to
represent information about things, then one must be able to make statements
about parts of an XML document, parts of the DLG (such as RDF nodes) and of
course the objects described.

In most cases it seems obvious to the human reader. The jam jar label text
does not (normally) read "jam jar label text" or "jam jar label" or "jam jar"
but "jam".

Take the case of a statement about a person in amaginary syntax

    
    
    <z:person id="foo">
       <head>
          <play:author>Zoe</play:author>
       </head>
       <play:name>Albert</play:name>
       <play:mailbox resource="mailto:adoe@bar.com"/>
       <play:son-name>Bill</play:son-name>
       <play:daughter-name>Claire</play:daughter-name>
       <play:father>
          <z:name value="Joe"/>
          <z:wrote href="#foo">
          <z:friend resource="#foo"/>
       </play:father>
    </z:person>
    

The XML element has one attribute and four child elements. The RDF node has
three properties (stated here). The person Albert has two children. What so we
refer to is we refer to "#foo"? Of course we refer to the element - but when
we make RDF statements, we normally want to refer to the RDF node, or rather
the object described by the node, in RDF terms the _resource_.

Of course, in a typical unix programming language we would simply add a syntax
character to distinguish the forms of reference: #foo would be the node, and
@#foo (or something) would be the object refered to. But in this case we are
trying to do everthing with RDF, and what is left with XML, and so we would
lose a few points by adding instead some totally new syntax. What we _can_ do
is to use different attribute names for the different forms of reference. The
attribute names I used above are as follows:

Forms of reference to the object of a property  `value` |  litteral string  
---|---  
`href` |  taking the string as a URI with or without fragment identifier, the
text (or XML fragment or whatever medium) to which it refers.  
`resource` |  taking a string as a URI with fragment idenifier, the abstract
RDF object (rdf:resource) corresponding to the identified XML document
fragment.  
  
Here I have used "href"to allow RDF to refer to the XML model. This is
important, as for example it is bits of XML which one digitaly signs, not (in
sigend XML) bits of RDF. Also, it is useful for RDF to be able to talk about
XML elements. It brings up the question of what an RDF fragment identifier
means.

##  RDF and XML fragment identifiers clash

_This highlights (2000/02) a bug in the relationship between XML and RDF_

Consider what is identified by

`http://.../foo.rdf#bar`

when `...foo.rdf` contains among other things the following:

    
    
    <rdf:description rdf:id="bar">
       <rdf:type resource="...#person">
       <y:common-name>Ora Lassila</y:common-name>
       <y:mailbox>ora.lassila@research.nokia.com</y:mailbox>
    </rdf:description>
    

The meaning of the fragment identifier is taken from the specification
assocaitedwith the MIME type.

Therfore, if this is takes as a document of type application/rdf, then the
fragment identifier identifies the thing (person in this case, Ora) described
RDF node. This is how refernces are used in RDF.

However, if its considered to be of type text/xml then the fragment identifier
is defined bythe XML spec, and so references an element whose attrubute
XML:ID. has value "bar". It happens that the `rdf:id` is _not_ defined to be
an xml:id but is defined to "act like one", whatever that means, by the RDF
spec. So it isn't clear whether the reference to this would be to the XML
subtree (consisting of the rdf:description element and its contents) or would
be undefined or possibly a refernce to some other element which happened to
have id="bar".

To have a different interpretation of a URI as a function of the notional type
of the document belies the fact the point of using XML syntax for RDF was that
RDF documents should be XML documents! Of course we embed RDF in regular XML
documents. So this distinction is nonsense.

Of course, the RDF spec can simply use the XML definition indirectly and refer
to the RDF ndoe described by the XML element. Howvere, this is not powerful
enough for RDF. This is because RDF needs to be able to make statements about
XML documents and XML elements. So for example, I might want to state that I
wrote the above snipet. It would be very tempting to write that I am the
author of foo.rdf#bar. But I am not the author of Ora Lassila. RDF uses and
parseType to resolve this for inline data: parseType=Resource indicates that
the reference is to the RDF object, and parseType=Literal indicates that it is
to the XML. The thing could be resolved with an interpretion property which
expresses relationship between an XML subtree and an RDF object which it
describes. While it would be good to define that property, RDF syntax needs a
shortcut. I would propose that "resource=" which is used to point to a
resource be also used for a resource fragment id, and that a new syntax be
introduced to refer to the actual RDF node. maybe "object=" which happens here
to correspond to the (subject, predicate, object) sense -- as well as a
"thing" sense. (The former is what is the reason for chosing it - the
attribute should express the relationship, not the class of the thing refered
to in general!).

##  Naming properties and elements

We have a similar problem in the XML-RDF relationship looking atthe identity
oat the schema level.

In RDF M&amp;S 1.0, a property name defined in a namespace is formed by
directly concatenating the namepsace URI with local tag name of the XML
element.

One natural way to use this is to end the namespace URI with "#" so that the
local tag name becomes the fragment identifier. When the schema is written in
XML, this implies that the tag name, being a simple alphanumeric, will
identify something in the document by its XML ID. This is a constraint on the
schema language: the XML ID of an element must be usable as a reference to the
thing being defined.

When there is a 1:1 mapping netween RDF properties and XML element types,
there is a choice of

  1. giving them the same URI and distinguishing which is refereed to by context (as in resource= and object= above), or 
  2. giving the different URIs algorithimically related, like assuming that #foo-element means the element defining #foo, using a convention specified in eth schema languages, or 
  3. giving them totally distinct URIs which can be connected by an assertion in the schema, or an in 

Given that it is interesting to use RDF to make statements about XML element
types, having different names it appealing. As writing down the relationship
every time the algorithmic link is un appealing.

###  A generic problem with XML identifiers

(I notice in passing that XML has currently a mixture of identifier paces
which is a little confusing.

The element and attribute namespace is very well handled in terms of
abbreviations, and is grounded in URI space, using the XML namespaces spec.

The URI space is of course the same space, but when value is typed as a URI,
then it cannot use the abbreviation system of the elelemnt namespace.)

###  IDREF considered harmful

The local identifier space is a subset of URI space. When an attribute is
defined as a URI, the simple "#" prefix gives access to the local ID space -
while still allowing great pwer of expression by reference to anything else on
the Web. When the "idref" form is used, this is not possiible. The idref form
is a weak form IMHO and not wise for new designs which are not to be
deliberately constraining.

Others have noticed this problem and there have even been suggestions which
confused the URI prefix and the namespace prefix. In fact the problem can be
solved [ref eric whiteboard] with an escape of some sort. One prossibility is
ambushing a void URI schme name by using a colon prefix (suggested by Eric
Prud'hommeaux)

`href=":rdf:description"`

would be a perfectly valid URI (in an XML context) which referenced the
rdf:description URI using the defined rdf: namespace. I feel this is messy, as
it would have to be subject to different handling than any other URI: its
expansion would be done in an XML-specific way.

The other link you need is the ability, when using an element name which only
occurs once, and without changing the default namespace, it would clearly be
logical to be able to just write

`<http://foo.com/schemas/memo6.2#priority>a</[...]>`

Because what follows uses the full power of what precedes with generality, we
may need to see the first in use before the paper is over. But I can't see
making the second change to XML.)

* * *

[We could derive _resource_ as a shorthand for indicating that the object
refeerred to is that refered to by the given element, with an explicit
coersion

    
    
    <z:person id=foo>
       <head>
          <z:author>Zoe</z:author>
       </head>
       <z:name>Albert</z:name>
       <z:mailbox>mailto:adoe@bar.com</z:mailbox>
       <z:son-name>Bill</z:son-name>
       <z:daughter-name>Claire</z:daughter-name>
       <z:father>
          <z:name value="Joe"/>
          <z:wrote href="#foo">
          <z:friend>
             <rdf:node href="#foo">
          </z:friend>
       </z:father>
    </z:person>
    

This could fromally model what is going on but it a mess: every rdf arc has to
be doubled!. Rref is in fact more fundamental and basic to RDF, and href is an
added level-breaker for breaking levels.]

In my opinion, when you look at this analysis, the fact that the abstract
object in RDF is known as a resource and that that is different from the
"Resource" which is the R in URI, this is very confusing.

RDF M&amp;S solvesa similar problem to this with ID for the object and BAGID
for the container if statements.

RDF uses the "resource" to indicate an object described by a node in the RDF
graph. In the above example, "#foo" in the XML lamnguage idenifies the element
&lt;z:person ... Hwoever, in RDF #foo refers (I understand) to the person
themselves. This means that the

_@@@ - Note the relationship between an object and a URI is non-perfect except
for an abstract resource.... give examples (home page, mailbox, common
name).... Compare with SQL - no identifiers, only use properties.@@@_

##  Expressing Identity of real things

Resources (as in Universal Resource Identifer) are precisely that identified
by URIs. Web pages and email messages are thought of as resources. RDF
unfortunately uses the term for anything which can be talked about - any
concept no matterhow abstract. RDF was originally designed as a solution for
metadat - information about information - where the subject of discourse was
by defintion a Web resource. There was no problem with terminology. As we use
RDF to describe things other than web pages, we in fact use properties to
identify them, for example we use email addresses to idnetify people. We must
not muddle the email address with the person.

Consider this example

    
    
    <rdf:description>
       <rdf:type>http://www.people.org/types#person</a>
       <play:name>Ora Yrjo Uolevi Lassila</play:name>
       <play:mailbox resource="mailto:ora.lassila@research.nokia.com"/>
       <play:homePage resource="http://www.w3.org/People/Lassila"/>
    </rdf:description>
    

Now that represents five nodes in the RDF graph: the anonymous node for Ora
himself (who has no web address) and the four arcs sepcifying that this thing
is of type person, and has a commin name, email address and home page as
given.

Some of the properties are unambiguous in some way: two people which have the
same mailbox may be assumed to be the same person. (I won't get into the rat-
hole of what identity properties should be assumed for what identifiers - that
is not core to the discussion)

I imagine that many processors will use their knowledge (preprogrammed or from
a schema) about uniqueness of such properties to make conclusions. For
example, if we define _play:mailbox_ to be such that no two people are allowed
to share the same play:mailbox property. Then, the information

    
    
    <rdf:description>
       <rdf:type resource="[...]book"/>
       <play:author parseType="Resource">
           <play:mailbox
         resource="mailto:ora.lassila@research.nokia.com"/>
       </play:author>
    </rdf:description>
    
    <rdf:description>
       <play:name>Ora Lassila</play:name>
       <play:mailbox resource="mailto:ora.lassila@research.nokia.com"/>
       <play:homePage resource="http://www.w3.org/People/Lassila/"/>
    </rdf:description>
    

allows the system to conclude that the name of the author of the book is Ora
Lassila.

This actually exposes what is really happening when we say as a short cut that
"the author is ora.lassila@research.nokia.com". What we mean is that the
author is somebody with that internet mailbox. To expose such a two-step
process exposes the actual nature of the identity relationships, and also
their limitations. This is, in my opinion, a much cleaner way to model the
data. Sometimes we need a shortcut:

    
    
    <rdf:description rdf:type="[...]book">
       <rdf:type>[...]book<rdf:type/>
       <play:author-mailbox
         resource="mailto:ora.lassila@research.nokia.com"/>
    </rdf:description>
    

RDF treats people as "resources" and in using this terminolgy which normally
means tautologically "things with URIs" makes people expect Ora to be
synonymous with his web page or his mailbox. This is not of course good
design. When a shortcut is made such as author-mailbox it is important to to
realize what is happening. In this model, there is no RDF node for the author
himself. The fact that there is a person involved who wrote the book and has
the mailbox has to be expressed elsewhere. The RDF schema may indeed be a good
place for that, once we have the vocabulary, as that will make the expansion
of the short cut evident to any processing machinery.

The unambiguous nature of the _play:mailbox_ meant that it could be used as a
way of identifying something. As a raw URI,
`mailto:ora.lassila@research.nokia.com` idenifies the abstract mailbox to and
from which email can be sent. However, the _play:mailbox_ property allows one
to identify a person. Its unambiguousness allows us to step from the literal
"written by **a** person whose email is ora@w3.org" to the more useful
"written by **the** person whose mailbox is ora@w3.org".

* * *

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

