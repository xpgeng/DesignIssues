Tim Berners-Lee  
Created: 2002/02/14, last change: $Date: 2007/09/03 23:41:55 $  
Status: personal view only, following from TAG and ww-tag and other mailing
list discussions. Editing status: draft.

This issue is sometimes termed the XML Processing Model problem. There was in
fact an [XML Processing Model Workshop](https://www.w3.org/DesignIssues//XML/2001/07/XMLPM.html). In the light
of lack of consensus result from the workshop, and specifically prompted by a
question about the relationship of XEncryption to other specs, occurring as
XEnc made its way to Candidate Recommendation status in W3C, this document was
eventually started as an [action item](http://www.w3.org/2002/02/25-tagmem-
irc#T17-03-57) from a TAG meeting, to open discussion on a new issue
mixedNamespaceMeaning-13. That issue was then split into several other issues,
one of which,
[xmlFunctions-34](http://www.w3.org/2001/tag/issues.html?type=1#xmlFunctions-34),
is the main import of this document.  In June 2005, this was revised as the
XML Processing Model working group charter was being discussed.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  The Interpretation of XML documents

###  Abstract:

It might seem that the specifications of different XML namespaces can make
inconsistent claims such that the semantics of a mixed namespace documents are
inconsistent. The solution sometimes proposed is a "processing model language"
such that there is no default meaning of an XML document without such an
external processing definition. This article argues that there is only one
basic generic processing model (or rather, algorithm for allocating semantics)
for XML documents which preserves needed properties of a multi-namespace
system. These properties include the need to be able to define the semantics
of an XML element without clashes of different specifications. This introduces
the concept of an on of an XML document is defined starting at the document
root by the specifications of the element types involved. A common class of
foreign element name, called here _XML function_, has to be recognized in
default processing by any supporting application, and returns more XML when it
is elaborated.

##  The problem

If one party sends another an XML document, how does one say what it means?
Or, if you don't like the _meaning_ word, what specs are invoked in what way
when an XML document is published or transmitted? This question is sometimes
posed as: What are is the processing model for XML?

The interpretation of a plain XHTML document is fairly well understood. The
document itself is a human language document, and so the conventions - sloppy
and wonderful - of human language define how it is understood and interpreted.
And the interpretation of tags such as H1 is described in a well-thumbed
standard and many books, and is implemented more or less consistently in many
devices.

But what happens when we start to mix namespaces? When SVG is embedded within
XHTML, or RDF or XSLT for that matter, what are the rules which ensure that
the receiver will understand well the intent, the client software do the right
thing -- and the person understand the right thing? The same issues obviously
apply when the information has machine-readable semantics.

As Paul Prescod [ points out](http://lists.w3.org/Archives/Public/www-
tag/2002Feb/0123.html), there are plenty of places one might think of looking
for information about how to process a document:

  1. DOCTYPE statement 
  2. top-level namespace 
  3. schema reference declaration 
  4. other root-level declared namespaces 
  5. any attribute on the root element 
  6. anything in the document 

In fact the general problem is that without any overall architecture, one can
write specs which battle each other. "The X attribute changes the meaning of
the Y attribute", "The Z attribute restores the meaning of the X attribute
irrespective of any Y attribute" and so on. In such a world, one would never
know whether one had correctly interpreted anything, as there might be
somewhere something deemed to change the meaning of what we have. Clearly this
way lies chaos. A coherent architecture defines which specs to look at to
determine the interpretation of a document. We don't have this yet (2002) for
XML.

However, in practice if a person were to look at a document with a mixture of
XHTML and SVG, they would probably find its meaning unambiguous.

In the same message, Paul opines, _Top-down self-descriptiveness is one of the
major advantages of XML and I think that doing otherwise should be
deprecated_. I completely agree with this conclusion. He concludes correctly
that the root namespace (the namespace of the document element) [or a DOCTYPE,
which I will not discuss further] is the only thing one must be able to
dispatch on.

###  The Pipeline Processing model

However, he secondarily concludes that, because it is important to define what
processing to be done first, one should use wrapper elements, so that if there
are any XSLT elements within a document, a wrapper causes XSLT processing to
be done, and so on. The discussion about documents with more than one
namespace has often made an implict assumption that the XML is to be processed
in a pipeline, in which each stage implements one XML technology, such as
include processing, style sheet processing, decryption, and so on.  The point
of this article is that  while this works in simple cases, in the general case
the pipeline model is basically broken.  Once you have things arbitraryily
nested inside each other, there is no single pipeline which will do a general
case.  And nesting things inside each other in arbitrary ways is core to the
power of XML.

###  Specific cases: XML functions

The pipline model makes it very messy to address a situation which is
increasingly common. This is of an XML document which contains a large numbers
of embedded elements from namespaces such as

  * XSLT, in "[Literal Result Element as Stylesheet](http://www.w3.org/TR/1999/REC-xslt-19991116#result-element-stylesheet)" mode. 
  * XInclude 
  * XMLEncryption 
  * XQuery (?) 
  * Internationalization tags such as "do not translate this phrase when translating this document" 

These namespaces share common properties:

  * They are the sort of thing you want to use with any sort of document, without it having to be foreseen in the schema for the original document 
  * The content of these elements is not the final form, but will be replaced with other content 
  * The resulting content may recursively have invocations of the same or different things from the list 
  * The effect of processing the element in this namespace is constrained such that it can only elaborate the contents of that branch of the tree. The element is replaced with its result of processing, but none of its ancestors or siblings may be affected. 
  * There are certain very special cases in which you want to be able to mention one without it being expanded. 

To treat these as a group, I will call these elements **XML functions**. The
term is not picked randomly. Let's look at some examples, each of which has
its peculiarities.

####  XSLT Literal Result Element as Stylesheet (LRES)

Let me clarify this way of looking at XSLT. The XSLT spec defines an XSLT
namespace and how you make an XSLT document (stylesheet) out of it. Normally,
the style sheet has xsl:stylesheet as its document element. However, there is
a special "Literal result element as Stylesheet" (LRES) form of XSLT, in which
a template document in a target namespace (such as XHTML) has XSLT embedded in
it only at specific places.  Here is an example from the spec.

    
    
    <html xsl:version="1.0"  
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
          xmlns="http://www.w3.org/TR/xhtml1/strict">  
      <head>  
        <title>Expense Report Summary</title>  
      </head>  
      <body>  
        <p>Total Amount: <xsl:value-of select="expense-report/total"/></p>  
      </body>  
    </html>
    

The XSLT spec formally defines the LRES form as an abbreviation for the full
form. In doing so it loses the valuable fact that in the LRES form, XSLT
elements behave as XML functions. They actually adhere to the constraints
above. This is is very valuable. The XSL spec says that the interpretation be
that an XSLT document be generated and processed to return the "real"
document. However, this does not scale in design terms. As the XSLT
specification itsels notes,

"In some situations, the only way that a system can recognize that an XML
document needs to be processed by an XSLT processor as an XSLT stylesheet is
by examining the XML document itself. Using the simplified syntax makes this
harder.  
  
NOTE: For example, another XML language (AXL) might also use an axl:version on
the document element to indicate that an XML document was an AXL document that
required processing by an AXL processor; if a document had both an axl:version
attribute and an xsl:version attribute, it would be unclear whether the
document should be processed by an XSLT processor or an AXL processor.  
Therefore, the simplified syntax should not be used for XSLT stylesheets that
may be used in such a situation"

It does not work when other namespaces use the same trick. It also prevents
applications from using optimizations which result from the constraints above.
So, while the spec formally defines a template document in that way, one can
make, it seems, a completely equivalent definition in terms of XML functions.

Imagine a document in which at various different parts of the tree different
forms occur, and in which these xml functions are in fact nested: you resolve
an XInclude and it returns something with XSLT bits in.

It is essential primarily to define what such a document should actually be
when (for example) presented to a user. It is an extra plus to have some
visibility from outside the document as to what functionality will be
necessary to have to fully process the document, such as from the MIME header,
but we can get to that later.

####  XInclude

This is probably a simple function. The include element is replaced by the
referenced document or part of document. This is straightforward and obviously
nests.

It is also obvious that it doesn't actually matter , when xincludes are
nested, that it doesn't make any difference whether you consider the inner
ones to be expanded before or after the outer ones. (The base URI of a
reference always has to be taken as that of the original source document, no
matter where the refernce ends up being expanded)

##  Top-down Processing model

I think that the battle over the order of processing of XML functions is often
an ill-formed question. XML is a tree. It is appropriate for the
interpretation of the tree to be defined from the top down. This does not
determine the order in which the leaves of the tree have to be done.

Here are some ways in which processors could handle an XHTML document
containing XML functions:

  * Noting that XHTML is a plain vanilla language, but that this document contains other things, first pipeline it through an XSLT processor, then an XInclude processor (the order being arbitrary), then a an XML decryption processor, and again in a cycle, until there are no functions left. 
  * Invoke an XML support class which then parses the document recursively. This more powerful XML parser has the ability to dispatch to the support class for an XML function whenever it finds one. 
  * Invoke an XHTML support class which then parses the document as it needs to in order to display it.. This more powerful XML parser has the ability to dispatch to the support class for an XML function whenever it finds one. However, the XHTML parser uses the constraint that in certain cases the front of an XHTML document can be displayed before the last has been parsed, and it actually delays evaluation of functions until the user's use of scroll keys makes it necessary. It turns out that certain things never need to be evaluated at all, saving time and bandwidth. 

This is NOT supposed to be a definitive list of ways of parsing XML documents
with functions - it is only supposed to illustrate the fact that many
approaches are possible which can be shown to be mathematically equivalent in
their effect. (This is why I tend to talk about the meaning, or
interpretation, of a document, rather than the processing model)

###  The need to quote

That said, it may be necessary to define a reference processing model, just
because one has to have a way of describing what the document means. In this
case note that the first model above is not appropriate. It uses the fact that
XHTML contains no tricks - it is "plain vanilla" in that everything in the
document is part of the document in the same way, modulo styling. (I
simplify). This does not apply to other sorts of document. Take an XML package
for example: the contents of the packages are quoted and is not appropriate
just to expand the contents of them. Only the cover note, the defining
document contains the import of the package as a whole, and the interpretation
of the other packaged things is only known in as much as the cover note
defines it. it is essential that languages such as XML packaging can be
defined in XML. It is essential that one can, if you like, quote a bit of XML
literally, and make up a new tag which says something quite new about the
contents. Therefore, while it works with XHTML, and as Tim Bray says (TAG
2002/02/14) there are many applications which do "generic XML processing" such
as trawling documents for links and use of language, there will be certain
namespaces such as HTML and SVG for which that makes sense and and other such
as XML packaging and Xml encryption, in which it won't. _(On the semantic web
case, the same applies, and was the cause in 2002 of much discussion in RDF
groups because RDF does not have quotes, and the informal use of
rdf:parseType="log:quote")_

If you need another example, think about the XSLT insert which generates and
XInclude element: It may contain what seems to be and even is an XInclude
element, but should not be expanded as contents of the XSLT element.

The reference processing model must be then, that parsing of an XML document
conceptually involves elaboration of any functions, and that processors must
be able to dispatch based on namespace at any point in the tree.

The result of such processing is the document which should correspond to the
XML schema, if the. There is normally no call for schema validation of the
document which still contains XML functions. Systems which claim to be
conformant to the spec of a given XML function mean that they can, in any XML
document, elaborate the function according to the specification. As Jacek
Kopecky says (2002/02/21), _[...] by saying on the sender: "We expect the
XHTML processor to be able to handle XInclude and therefore this thing is an
XHTML document all right"_. We can't of course expect old XML processors to
handle XInclude, but we can expect anything which claims conformance with
Xinclude to do so.

###  Software designs for top-down processing

In object-oriented software terms, one imagines handing an XML tree to an
instance of an object class which supports the element type of the document
element. This then returns something as defined by the spec. (An HTML document
conceptually returns a hypertext page, an SVG document a diagram, an RDF
document a conceptual graph (small c small g)). The object may itself call out
to a parser to get the infoset for its contents, and it may or may not call
out to the XML function evaluator but whether it does or not is defined by its
own specification. But XML functions just return XML which replaces them. And
any XML applications which claim conformance to the XML function's spec should
be able to accept this.

Similarly, in an event-oriented architecture, an event stream which is being
fed to an HTML handler would, when a foreign namespace such as XSLT is found,
be vectored to an XSLT handler. The software design has to allow the XSLT
handler to hand back a new set of events, a serialization of the resultant
tree, to the HTML handler.  
  
The software design in either vase also has to allow enough context to be
shared between the applications so that they can perform their function:
embedded SVG needs a display context such as part of a drawing space which
corresponds to the space in the rendering of the HTML document, and so on.  

###  Unresolved issue: references to siblings

This note does not address many of the issues around the XML processing model.

There is a possible ambiguity when a function refers to the current document.
In other words, though it is not allowed to change things outside itself, it
may read outside itself. This (if allowed) would clear raise the question of
whether it references the document before or after its own or other function's
elaboration.

A related question is whether an XPointer fragment identifier should refer to
the document before or after elaboration of functions. My inclination is to
say after, because then you know that an XPointer into an SVG object will
resolve to a bit of SVG. But there may be arguments the other way.

XML Digital Signature (I am told) specifically requires that the signature is
done on the raw source of the document before XInclude. Without going into the
relative merits of signature before and after XInclude and other functions, it
is clear that there are cases when either would be useful.

The ambiguity of these references, like the problems in XSLT of generating
XSLT stylesheets with XSLT stylesheets, stem from the lack of quoting syntax
in XML.

###  MIME content-type labeling

_@@This section is not complete. It has been covered more thoroughly by TAG
discussions already. @@ link_

An XML document is in most cases self-describing. That is, you don't need to
know anything more that it is XML to interpret it. In email and HTTP
applications, it is useful for the RFC822-style message to define how the body
should be interpreted using the `content-type` header. All that is necessary,
then, is that the content-type should indicate XML (`text/xml` or
`application/xml` or anything with `+xml)` and a top-down generic processing
is valid. (The algorithm for determining the character encoding is not
addressed here @@ link)

While this is sufficient, it is however useful to be able to provide more
visibility as to what is contains [Roy Fielding, Dissertation, Ch4 @@link].
The document element gives, in many cases, fundamental information about the
resulting type of the whole document, irrespective of functions elaborated or
plugins plugged in. For example, whatever the content, an `xhtml:html`
document is a hypertext page. This means that some systems will represent it
in a window and allows certain functionality. The operating system, if it
knows this, can use icons to tell the user, before they open an email or
follow a link, what sort of a thing it contains or leads to. Similarly, an SVG
document will return a diagram, and an RDF document body of knowledge -- a set
of relational data. So more than any other namespace used in the document, the
document element namespace is crucial.

This is why the best practice is to publish documents with standard and
therefore well-known document element types as a special MIME type. This
allows an XHTML page to be visible as such from the HTTP headers alone. This
allows smarter processing by intermediates, decisions about proxy caching,
translation, and so on. It allows the content negotiation of HTTP to operate,
allowing a user for example to express a preference for audio rather than
video. This also allows systems which want to to optimize the dispatching of a
handler for the document from the MIME type alone. A "+xml" prefix as defined
by RFC____@@ should be used whenever the document is also a self-describing
top-down XML document for which the top-down processing model applies. (The
fact that a document is a well-formed XML1.0 document alone does _not_
constitute grounds for adding the "+xml")

Simon St Laurent has suggested [@@ his Internet-draft, possibly timed out]
that all namespaces used in the document be listed as parameters to the MIME
type. This makes sense on the surface. It may not be practical or worth the
effort. It is a lot of bits, and in any case exactly what will be required
cannot be determined until the document has been interpreted top-down.
However, it or something equivalent is necessary if one is to specify the
software support which is necessary.

  * The top element can in fact be such that the other elements are to interpreted in arbitrarily weird ways 
  * For many document element types, there is a guarantee of the sort of object which is being represented. 

So the best form of visibility would be state (and possibly negotiate) the set
of XML deatures which must be supported to properly process the document.

###  Related notion: implied namespace

When a namespace-specific content-type has been specified, is it also
necessary to specify the document namespace, or could that be assumed? That
would mean that a plain XHTML file would not need an explict namespace. It is
tempting to say that the default namespace should default to that associated
with the content type, but in fact the logical thing is for the document
namespace.

@@Decision tree diagram - add

###  User-defined processing of documents

This document defines the basic interpretation of an XML document. There have
been many suggestions of ways in which a complex and different order of
processing could be specified, many of these mentioned at the workshop, and
including Sun's XML pipeline submission. My current view is that such
languages should be regarded themselves the top-level document which then
draws in the rest of the document by reference as it is elaborated.

###  Server-side processing of documents

In the HTTP protocol, or email for that matter, the important interface which
is standardized is the one between the publisher (or sender) and receiver. We
concern ourselves with what a receiver can do by way of interpretation of an
XML document published or sent. Any processing which has happened on the
server or sender side in order to process that document is not part of the
protocol. While XML functions may indeed be elaborated to form a document for
transmission from another one, that is something for control within the server
and so is not a primary concern for standardization.

When a document is in a pure fucntional form, it actually is an opmization
whether the functions are elaborated by the server or or the client.

##  The requirements on Schema languages

This tree-oriented architecture for XML puts requirements on schema languages.
With DTDs, and with current XML schema, there was no natural way to describe
how namespaces fit together. There have been many rather unnatural attempts to
create a modular system, such as the HTML modularization @@link. The way this
has been done has basically been to make one great big schema for the combined
language, in such a way that the new schema constrains the way the elements
from different namespaces can fit together.  
The problem is to avoid making this an n2 problem. Will the working group
which integrates n specs (such as 4 for XHTML, SVG, XForms, MathML) take n2
years to make the schema? It would be far preferable if one could just write a
scheme for each new facility,  
  
Conversely, what would a schema language would have to allow us to say:  

  * &lt;its:info translate="no"&gt;x&lt;/its:info&gt; can occur anywhere x can occur (for systems which support ITS) 
  * &lt;its:info translate="no"&gt;x&lt;/its:info&gt; can occur anywhere x can occur, so long as x is human-presentable content. 
  * &lt;xenc:encrypted&gt; ...&lt;/&gt; is a function: it can occur anywhere, so long as XEnc is supported. It's processing will return XML mixed content which will replace this element. 
  * &lt;svg:drawing/&gt; can occur anywhere &lt;xhtml:img /&gt; can occur. 

This way of specifying n independent schemas, or rather schemas which have
back-references to earlier schemas in some cases, allows a product to simply
quote the set of XML technologies which it supports. This has to be negotiated
between the sender and receiver of XML. It is not the same in the general case
to the set of namespaces used in the document, because function elaboration
may change that. All the same, the namespaces may be a useful way of
indirectly referring to the features.

Because the mode of operation in which the content is evaluated with function
processing is very common, it would be useful in a schema for example to
indicate this mode, or, more practically, to indicate the exceptions. There
are very few elements which don't elaborate their contents at the moment in
the markup world, and so they should be the exception. (Many computing
languages of course reserve special punctuation for this quoting but adding
punctuation at this stage isn't the XML style!)

##  Conclusion

The top-down processing model for XML as an architectual principle resolves
many of the questions which remain unanswerable with pipelined processing. In
fact, consideration of the example shows that pipeline processing could be
actually dangerious, producing errors and possibly security issues, in the
case of generally nested XML technologies of the types discussed.

##  References

  * Discussion on www-tag@w3.org list 
    * [ 19 Feb 2002, Paul Prescod Namespace Dispatching](http://lists.w3.org/Archives/Public/www-tag/2002Feb/0123.html)
  * [ The archive of the XML-MIME list relevant](http://www.imc.org/ietf-xml-mime/mail-archive/threads.html) to MIME dispatching of XML documents 
  * [XML processing model workshop](http://www.w3.org/XML/2001/07/XMLPM.html)
  * TAG Issue [XMLFunctions-34](http://www.w3.org/2001/tag/issues.html#xmlFunctions-34)
  * W3C Specifications: [XML spec](http://www.w3.org/TR/REC-xml/); [Namespaces in XML](http://www.w3.org/TR/REC-xml-names/)
  * [XML pipeline definition language](http://www.w3.org/TR/2002/NOTE-xml-pipeline-20020228/), Sun Microsystems 
  * [ XML Processing Model discussion list](http://lists.w3.org/Archives/Member/xml-pm-ws/2001Jul/thread.html) (W3C members archive) 

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

