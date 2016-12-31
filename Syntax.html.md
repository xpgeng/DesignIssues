[![W3](https://www.w3.org/DesignIssues//Icons/WWW/w3c_home)](https://www.w3.org/)

_Status: Obsolete._

This was written as part of the Semantic Web [Toolbox](https://www.w3.org/DesignIssues/Toolbox.html) page and
spun off. It investigated a syntax for RDF/XML which would be simpler for
users than the 'striped' syntax of RDF M&amp;S 1.0. It also looks at the rules
for extracting RDF semantics from other non-RDF markup. In this sense it
connects with the [Top-down functional interpretation of XML](https://www.w3.org/DesignIssues/XML.html) You
can think of this syntax as Notation 2. A later syntax, [Notation
3](https://www.w3.org/DesignIssues/Notation3.html), was much more successful.

* * *

#  A strawman Unstriped syntax for RDF in XML

(Within this document, XML elements with namespace prefix are assumed to be
defined as pointing to something the reader can figure out, and unprefixed
element names are used for new features which are introduced in this document.
).

The major difference between this syntax and [RDF 1.0 M&amp;S](https://www.w3.org/DesignIssues//TR/REC-rdf-
syntax/) is that RDF edges correspond to elements, and RDF nodes are implicit.
It is basically as the M&amp;S syntax with `parseType=resource` is a default.

###  Syntax requirements

Basically the things which drove this particular syntax are

  1. A requirement to use XML as W3C policy for serialisations (except where excruciatingly painful) 
  2. A non-requirement to have the "striping" of RDF M&amp;S 1.0 where nested elements describe alternately nodes and arcs; 
  3. RDF can be carried within other XML information and can have other XML information inserted within the syntax; 
  4. It should be possible to make a document which efficiently expresses information and allows an RDF parser aware of the syntax to extract the RDF graph without needing to read the namespace schema. 
  5. RDF can carry extensions which can be optional. 

##  Assumed syntax

I assume for the purposes of the [Toolbox](https://www.w3.org/DesignIssues/Toolbox.html) page a syntax for
data in XML in which XML elements be classified into the following categories.

###  RDF-Property element

The element introduces information about an arc in the graph. As nodes in RDF
do not inherently have any information apart from their arcs, properties are
the only way RDF information actually described. Property elements work as
follows:

  1. XML elements may be declared in a schema to be RDF assertions and to therefore be treatable as such. These are known as _property elements_. 
  2. At any point in an XML document there may by a _default subject_ set. This is the subject of any property element where not indicated otherwise. 
  3. An `rdf:for` attribute indicates otherwise for the subject for one property element. (This is a shortcut) 
  4. An `rdf:about` attribute on any element sets the default subject for any contained elements. (Equivalent to RDF M&amp;S) 
  5. An `rdf:fyi` attribute on an element removes any default subject for the element and its descendants unless otherwise specified. The RDF parser may ignore the element and its contents as far as RDF semantics go. 
  6. An `rdf:extend` attribute on any element indicates that the semantics of the element are of relevance to the RDF parser and must be interpreted according to the specification, and where this cannot be done the RDF semantics are undefined (and typically an error condition will result from an attempt at evaluation). The element is known as an RDF-opaque element 
  7. If a property element has an `rdf:value` attribute that indicates the value of the property. This is just a shortcut for having it in the element content. 
  8. If a property element has atomic (string) content then that is the object of the statement. (If this and the previous exist they must match). 
  9. If a property element has child elements then its value is an RDF node which becomes the default subject (unless the parsetype is used to declare the content to be literal XML) 

###  RDF-Transparent

The Semantic context is not changed. And example might be all HTML tags, to
make it simple to include RDF in HTML documents (and extract it).

###  RDF-Opaque

The RDF parser can deduce nothing about the element or its contents, unless it
knows the semantics of the element. Example: &lt;sense:room-temperature/&gt;

RDF-Opaque tags are understood by parsers conforming to the namespace they are
in.

In the [toolbox](https://www.w3.org/DesignIssues/Toolbox.html) we will introduce new features which, while
they indeed be expressed longhand in the existing XML-RDF notation, in
practice need to available in a more concise form at a high level. These are
therefore extensions to the RDF-XML syntax for logic. Example: &lt;not&gt;

RDF-Opaque tags in the RDF space are understood by conforming parsers. Other
tags are assumed to be property elements if there is subject defined (default
or otherwise) and otherwise RDF-Transparent (by default) or Opaque (if
specified). Information as to whether tags are RDF-Opaque may be given in the
document using them or in a schema (or indeed in principle anywhere else). It
may be done element by element, or if applicable, to an en entire namespace.

This syntax was written as have something for examples, and part of the
purpose of this is a feasibility of writing logic in XML. I apologise to the
reader for the effort required to work in a strange syntax. There was later a
call for a simpler syntax and so this was cleaned up a little as a strawman.

* * *

###  Examples for rdf:for and rdf:about

Sometimes the effort of creating an element just in order only to define the
subject for a following assertion is a bit heavy. Making a standard well-known
and mandatory understood attribute would make this easier. Suppose, for
example that `rdf:about=foo` always sets the thing to which a contained
property element refers by default, and `rdf:for=bar` overrode it for the
element itself. (`rdf:for` would also imply that the element was an RDF
property)

    
    
    <dc:author rdf:for="thebook" value="Ora"/>
    

is an easier way of specifying a single property.

    
    
    <frontm rdf:about="theBook">
       <z:date>sdfghjk</z:date>
       <z:title>Makeing more pancakes</z:title>
       <z:obsoletes> 
          <!-- default subject is no longer theBook --!>
          <z:title>Making pankakes</z:title>
          <z:price>$3.00</z:price>
       </z:obsoletes>
       <z:price>$6.00</z:price>
       <z:price for="anotherBook">$78.00</z:price>
    </frontm>
    

(The only problem I have with `rdf:about` and `rdf:for` is that it becomes
mandatory for any semantically aware parser to be able to handle this, as
ignoring it is of course impossible.)

###  RDF:Description

When one wants to introduce information about an RDF node, this is basically
done by any element with an rdf:about attribute. When there is no other
element which conveniently provides a placeholder, the rdf:description element
may be used.

    
    
    <rdf:description rdf:about="theBook">
       <dc:author>Ralph</dc:author>
       <http:from>swick@w3.org</http:from>
    </rdf:description>
    

If the `rdf:about` attribute is present it indicates that the node represents
a resource (document) whose URI is that give. That attribute may be omitted.

###  RDF:Property

There are times when using an XML element name for a property may be difficult
or impossible, such as when there are many properties to be listed, each from
different namespaces, or when the property must take the value of the
variable. (Yes, I understand this takes RDF out of first order logic but our
ability to quote statements and refer to them I think makes that step anyway).

    
    
    <rdf:property pname="http://dc.org/dc1#author"
       rdf:for="theBook"
       rdf:value="Ralph">
    

This is also useful as a serialisation syntax when dumping the output of a
parser, for example.

* * *

##  NOTES

See also

[Identifying things in RDF](https://www.w3.org/DesignIssues/Identity.html)

###  RDF in HTML - Transparent or not?

There are two ways to put RDF into HTML using these conventions. One could
declare that all HTML elements are RDF-transparent, in which case RDF can be
stuck in anywhere.

One could bring them closer, so that the RDF subject is set to appropriate URI
by convention by declaring them (in RDF schema code inserted into the XHTML
schema) to be opaque. In this case, I would propose that HTML's HEAD (or maybe
even the HTML document container) be considered as a Node element whose
context is the document itself. I would propose that A switch context to the
destination of the link - as one often wants a neat way of putting in
information about it.

Examples:

Element  |  RDF subject (URI)  
---|---  
HTML:HTML  |  The document itself ("")  
HTML:HEAD  |  The document itself ("")  
HTML:A  |  The linked document (value of _href_)  
HTML:BLOCKQUOTE  |  The quoted document  
  
References

See also:

  * [Sergy's proposal](http://www-db.stanford.edu/~melnik/rdf/syntax.html)

So much for syntax: on to the [semantic toolbox](https://www.w3.org/DesignIssues/Toolbox.html).

* * *

Last change $Id: Syntax.html,v 1.21 2007/03/22 20:31:40 timbl Exp $ Tim BL

