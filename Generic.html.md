[![W3c](https://www.w3.org/Icons/WWW/w3c_home.gif)](https://www.w3.org/TheProject.html)

_This is a statement of achitectural principles behind my thinking on web
design. This was the thinking behind the original HTTP content negotiation of
1992, and the vary= fields in the URI: headers for example. It has been behind
W3C thinking on the OBJECT header for HTML and other issues. \- TBL, 1996_

_This is an important axiom of web design, which must be understood for new
designs to use URIs and HTTP properly. - TimBL, 2000_

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

Axioms of Web Architecture: 3

* * *

See also:

  * [A proposal for an HTML "Resource" element](https://www.w3.org/MarkUp/Resource/Specification)
  * [Historical web design note on formats](https://www.w3.org/DesignIssues/Formats.html)
  * [HTTP overview by W3C](https://www.w3.org/Protocols/)

#  Generic Resources

A URI represents a **resource**

A "resource" is a conceptual entity (a little like a Platonic ideal). When
represented electronically, a resource may be of the kind which corresponds to
only one posisble bit stream representation. An example is the text version of
an Internet RFC. That never changes. It will always ha the same checksum.

On the other hand, a resource may be **generic** in that as a concept it is
well specified but not so specifically specified that it can only be
represented by a single bit stream. In this case, other URIs may exist which
identify a resource more specifically. These other URIs identify resources
too, and there is a relationship of genericity between the generic and the
relatively specific resource.

As an example, successively specific resources might be

  1. The Bible 
  2. The Bible, King James Version 
  3. The Bible, KJV, in English 
  4. A particular ASCII rendering of the KJV Bible in English 

Each resource may have a URI. The authority which allocates the URI is the
authority which determines wo what it refers: Therefore, that authority
determines to what extent that resource is generic or specific.

This model is more of an observation of a requirement than an implementation
decision. Multilevel gnericity clarly exists in all our current life with
books and electronic documents. Adoption of this model simply follows from the
rule that Web design should not arbitrarily seek to constrain life in general
for its own purposes.

##  Dimensions of genericity

When we discuss electronic resources, an interesting fact is that a small
number of dimensions of genericity emerge.

Time  |  A resource may vary with time. For example, "The Wall Street Journal"
varies with time. Each issue is a time-specific resource, which does not
change with time. Most home pages on the Web change with time, in a less
periodic way.  
---|---  
Language  |  When a document is translated, it is useful to be able to refer
to it either in the generic, or to a particular specific translation.  
Content-Type  |  A given resource may have mny ways in which it can be
represented on the wire, using different `Content-type`s (in HTTP terms). As
an example, an image may be represented in PNG or JFIF format.  
Target medium  |  A given resource may be targetted specifically to a specific
medium, such as a printer, being displayed on laptop screen, being displayed
on a cellphone, or being projected onto a large screen for an audience. (This
is currenltly available for selecting CSS stylesheets, but is not done at the
HTTP content negotiation level)  
  
The fact that there are such a small number of dimensions currently apparent
sugests that Web software should handle them individually in its interface
with the user, even though the architecure should handle them as a single
concpet.

##  Derivation

When a document is translated, one of the language-specific resources may have
been the original source. However, this need not always be the case. Specific
resources may have been derived from unrelated sources, or multiple sources.
Therefore, though it is interesting to be able to describe the "derived-from"
relationship, this is _not_ part of the genericity relationship. It is not
discused further here.

##  Genericity Metadata

When making statements about resources, genericity leads two types of
statement. The examples use imaginary HTML elements or HTTP headers as
illustrations of the meaning.

###  Dimensions

A statement about the genericity of an object is important both for the user,
and also for example for a cache manager. This statment takes the form of a
list of dimensions in which the resource for a given URI is generic.

One proposal was the `vary` field in the `URI:` header in HTTP:

`URI: http//foo.com/bar/baz vary=time,language` This is a statement about the
relationship between the URI and the resource. (See also [Quality of service
of names](https://www.w3.org/DesignIssues/NameMyth.html#QoS))

###  Relationships

The other statement which can be made is about a genericity relationship
between two resources. Typed links provide this kind of statement. One
proposal was

    
    
     
             <link rel="language-specific" href="baz.fr">
     
     
    

which means "This resource is a language specific version of this resource
identified by baz.fr" This needs to be combined in with information about the
particualar language.

    
    
     
             <resource uri="baz.fr" vary="type, time">
                     <meta htp-equiv="content-language" value="Fr">
             </resource>
     
    

So much for the architectural ideas. In practice one would use a shorthand
form for all this information such as

    
    
             <specific language="fr" uri="baz.fr">
     or
             <specific language="fr" ct="text/html" uri="baz.fr.html">
    
    

##  Using RDF to model this

There is now an RDF ontology for these concepts,
<http://www.w3.org/2006/gen/ont>. The ontology does not describe the target-
medium dimension. (Please use that instead of the old one desribed here in
2000-09.)

* * *

[![](https://www.w3.org/Icons/WWW/w3c_48x48)](https://www.w3.org/)

[(c)Tim BL 1996](https://www.w3.org/People/Berners-Lee)

