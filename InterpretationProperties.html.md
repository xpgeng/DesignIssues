Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Design Issues - Ideas about Web Architecture

_This page assumes an imaginary namespace referred to as play: which is used
only for the sake of example. The readers is assumed to be able to guess its
specification._

* * *

#  Interpretation properties

_Abstract: Natural languages, encodings, and similar relationships between one
abstract thing and another, are best modeled in RDF as properties. I call
these Interpretation properties in that they express the relationship between
one value and that value interpreted (or processed in the imagination) in a
specific way._

##  The problem of annotating natural language

There has to date (2000/02) been a consistent muddle in the RDF community
about how to represent the natural language of a string. In XML it is simple,
because you never have to exactly explain what you mean. You can mark up span
of text and declare it to be French.

> His name was &lt;html:span xml:lang="fr"&gt;Jean-
Fran&amp;ccedilla;ois&lt;/html:span&gt; but we called him Dan.

Under pressure from the XML community to be standard, the RDF spec included
this attribute as the official RDF way to record that a string was in a given
language. This was a mistake, as the attribute was thrown into the syntax but
not into the model which the spec was defining.

Consider the [example](https://www.w3.org/DesignIssues/Identity.html#this) in the [identity
section](https://www.w3.org/DesignIssues/Identity.html),

    
    
    <rdf:description>
       <rdf:type>http://www.people.org/types#person</a>
       <play:name>Ora Yrjo Uolevi Lassila</play:name>
       <play:mailbox resource="mailto:ora.lassila@research.nokia.com"/>
       <play:homePage resource="http://www.w3.org/People/Lassila"/>
    </rdf:description>
    

Now that represents five nodes in the RDF graph: the anonymous node for Ora
himself (who has no web address) and the four arcs specifying that this thing
is of type person, and has a common name, email address and home page as
given.

Where to we add the language property? Of course we could add a language
attribute to the XML, but that would be lost on translation into the RDF
model: no triple would result.

###  Attempt 1: a property of the person?

Many specifications such as iCalendar (see my notes@link) would add another
property to the definition of the person.

    
    
    <rdf:description>
       <rdf:type>http://www.people.org/types#person</a>
       <play:name>Ora Yrjo Uolevi Lassila</play:name>
       <play:namelang>fi</play:namelang>
       <play:mailbox>ora.lassila@research.nokia.com</play:mailbox>
       <play:homePage>http://www.w3.org/People/Lassila/</play:homepage>
    </rdf:description>
    

Here, the property _play:namelang_ is defined to mean "A has a name which is
in natural language B". In the iCalendar spec, the definition more complex in
that the _lang_ property is in same cases the language of a name and in other
cases that of the object's description. This is a modeling muddle. The nice
thing about doing it this way is that the structure is kept flat, and pre-XML
systems such as RFC822 (email etc) headers have a syntax which can only cope
with this.

There are many drawbacks to this muddle. Ora may have two names, one in Finish
and another in English, and the model fails to be able to express that.
Because the attribute is apparently tied to the person and not obviously
attached to the name, automatic processing of such a thing is ruled out.
Clearly, the structure does not reflect the facts of the case.

###  Attempt 2: a property of the string?

The second attempt is to make a graph which expresses the language as a
property of the string itself. Clearly, "Ora Yrjo Uolevi Lassila" is Finnish,
is it not? Yes, Ora is Finnish, but that is different. What we need to say is
that the string is in the Finnish language. The problem, then, becomes that
RDF does not allow literal text to be the subject of a statement. Never mind,
RDF in fact invents the _rdf:value_ property which allows us to specify that a
node is really text, but say other things about it too. This is done by
introducing an intermediate node.

    
    
    <rdf:description>
       <rdf:type resource="http://www.people.org/types#person" />
       <play:name rdf:parseType="Resource">
           <rdf:value>Ora Yrjo Uolevi Lassila</rdf:value>
           <play:lang>fi</play:lang>
        </play:name>
       <play:mailbox resource="mailto:ora.lassila@research.nokia.com"/>
       <play:homePage resource="http://www.w3.org/People/Lassila">
    </rdf:description>
    

There we have it, and in an RDF graph at least very pretty it looks. And
indeed, we could work with this, apart from the fact that we have made another
modeling error. It is not true that the language is a property of the text
string. After all, the string "Tim" - is that English (short for Timothy? or
French (short for "Timothe")? I don't need to add a long list of text strings
which can be interpreted as one language or as another. A system which made
the assertion that the string itself was fundamentally English would simply be
not representing the case.

###  Attempt 3: a relationship between them.

In fact, the situation is that Ora's name is a natural language object, which
is the interpretation according to Finnish of the string "Ora Yrjo Uolevi
Lassila". In other words, Finish the language is the relationship between
Ora's name and the string. In RDF, we model a binary relationship with a
property.

    
    
    <rdf:description>
       <rdf:type>http://www.people.org/types#person</a>
       <play:name>
           <lang:fi>Ora Yrjo Uolevi Lassila</lang:fi>
        </play:name>
       <play:mailbox>ora.lassila@research.nokia.com</play:mailbox>
       <play:homePage>http://www.w3.org/People/Lassila/</play:homepage>
    </rdf:description>
    

This works much better. Ora has a name which is the Finnish "Ora". This allows
an RDF system to create a node for that string, and a "Finish" link from the
concept of Ora the person, maybe a Danish link from the concept of the
currency, and an old english link from the concept of weight (1/15 pound), not
to mention a Latin link from the concept of the shore.

A problem we may feel is we would like the language to be a string, so that we
can reference the ISO spec for all such things, but there is of course no
reason why the spec for the lang: space should not reference the same spec.

Another problem we might feel is that it is reasonable for the play:name to
expect a string, and in most cases it may get a string: what is the poor
system supposed to do in order to accommodate finding a natural language
object in place of a string? I guess making a class which includes all strings
and all natural language objects is the best way to go. Any use of string
which did not allow also such natural language object makes life much more
difficult for multilingual software- so this is serious problem.

_[[This leads us on to another interesting question of packaging in RDF. There
is a requirement in XML packaging and in email packaging and it seems quite
similarly in RDF that when you ask me for something of type X I must be able
to give you something of type package which happens to include the X you asked
for and also some information for your edification. But that is another
story.@@@ eleborate and define properties or syntax@@@]]_

What is really important is that we are using the ability of RDF to talk about
abstract things, just as when we identified people by the resources they were
associated with, but avoided pretending that any person had a definitive URI.

##  Datatypes as interpretation properties*

_Datatypes_ here I mean in the sense of the atomic types in a programming
language, or for example XML Datatypes (XML schema part 2). Defining datatypes
involves defining constraints on an input string (for example specifying what
a valid date is as a regular expression) and specifying the mathematical
abstract individuals which instances of a type represent. One can model the
relationship between the representation and the abstract value and the string
using a property.

    
    
    <rdf:Description about="#myshoe">
       <shoe:size>10</shoe:size>
    </rdf:Description>
    

|  &lt;#myshoe&gt; shoe:size "10".  
---|---  
  
This doesn't tell us what it is 10 of. We could go through life without any
model of types: we could define a shoe size as being a decimal string for a
number inches. There are many questions and tradeoffs which datatype designers
make (for example,

  * Can you tell the type of a value from the string representation in every case? (eg 1.4e4 vs 1.4d4 for precision) 
  * Are the values of different datatypes distinct? (Eg, is 1 = 1.0?) 
  * Are the set of datatypes extensible? (Eg, can you add complex numbers or prime numbers?) 
  * Does representation equality imply value equality? 
  * Does value equality imply representation equality? (Is the only allowed representation the canonical one?) 

It would be nice to be able to model these questions in general in the
semantic web, in order describe the properties of dat in arbitrary systems. We
can introduce interpretation properties which link a string to its decimal
interpretation as number, or a length including units. The problem is that the
RDF graph which most folks use is the one above. The object of shoe:size is
"10".

The simplistic system corresponding exactly to the Attempt 1 above, is to
declare that shoe:size is of class integer. This implies (we then say) that
any value is a decimal string. Given the string and the type we can conclude
the abstract value, the integer ten. This works. It is the system used by XML
datatytpes whose answers for the questions above are as I understand it [No,
Yes, Yes, Yes, No]. A snag is that you can't compare two values unless you
know the datatypes.

To model the representation explicitly in the RDF it seems you have to
introduce another node and arc, which is a pain.

    
    
    <rdf:Description about="#myshoe">
       <shoe:size>
          <rdf:value>10</rdf:value>
       </shoe:size>
    </rdf:Description>
    

|  &lt;#myshoe&gt; shoe:size [ rdf:value "10" ].  
---|---  
  
We can then define rdf:value to express that there is some datatype relation
which relates the size of the shoe to "10". All datatype relations are
subProperties of rdf:value with this system. Once it is that form, the
datatype information can be added to the graph. You have the choice of
asserting that the object is of a given class, and deducing that the datatype
relation must be a certain one. You can nest interpretation properties -
interpreting a string as a decimal and then as a length in feet. But this is
not possible without that extra node. One wonders about radically changing the
way all RDF is parsed into triples, so as to introduce the extra abstract node
for every literal -- frightful. One wonders about declaring "10" to be a
generic resource, an abstraction associated with the set of all things for
which "10" is a representation under some datatype relation. This is frightful
too you don't have "equals" any more in the sense you used to have it.

Instead of adding an extra arc in series with the original, we can leave all
Properties such as shoe:size as being rather vague relations between the shoe
and some string representation, and then using a functional property (say
`rdf:actual)` to relate the shoe:size to a (more useful) property whose object
is a typed abstract value.

    
    
    { <#myshoe> shoe:size "10" } log:implies
    { <#myshoe> [is rdf:actual of shoe:size] [rdf:value "10"] } .
    

_@@@ No clear way forward for describing datatypes in RDF/DAML (2001/1) @@_

##  More examples

Interpretation properties was the name I have arbitrarily chosen for this sort
of use. I am not sure whether it is a good word. But I want to encourage their
use. Base 64 encoding is another example. It comes up everywhere, but XML
Digital Signature is one place.

    
    
    <rdf:description>
       <play:name parseType="Resource">
          <lang:fi  parseType="Resource">
            <enc:base64>jksdfhher78f8e47fy87eysady87f7sea</enc:base64>
          </lang:fi>
        </play:name>
    </rdf:description>
    

Another example is type coercion. Suppose there is a need to take something of
datetime and use it as a date:

    
    
    <rdf:description>
       <play:event parseType="Resource">
           <play:start parseType="Resource">
              <play:date>2000-01-31 12:00ET</play:date>
           </play:start>
           <play:sumary>The Bryn Poeth Uchaf Folk festival</play:summary>
       </play:event>
    </rdf:description>
    

Such properties often have uniqueness and/or unambiguity properties.
_enc:base64_ for example is clearly a reversible transformation. It it relates
two strings, on printable and the other a byte string with no other
constraints. The byte string could not in general be represented in an XML
document. The definition of _enc:base64_ is that A when encoded in base 64
yields A. This allows any processor, given B to derive A. The specification of
the encoding namespace (here refereed to by prefix _enc:_) could be that any
conforming processor must be able to accept a base64 encoding of a string in
any place that a string is acceptable.

Interpretation properties make it clear what is going on. For example,

    
    
    <rdf:description about="http://www.w3.org/">
       <play:xml-cannonicalized parseType="Resource">
          <enc:hash-sha-1 parseType="Resource">
             <enc:base64>jd8734djr08347jyd4</enc:base64>
          </enc:hash-sha-1>
       </play:xml-cannonicalized>
    </rdf:description>
    

clearly makes a statement, using properties quite independently defined for
the various processes, that the base64 encoding of the SHA-1 hash of the
canonicalized form of the W3C home page is jd8734djr08347jyd4. Compare this
withe the HTTP situation in which the headers cannot be nested, and the
encodings and compression and other things applied to the body are mentioned
as unordered annotations, and the spec has to provide a way of making the
right conclusion about which happened in what order.

##  Units of Measure (2006)

This pattern applies very well to units of measure.

See, for example a simple ontology <http://www.w3.org/2007/ont/unit> of units
of measure.

##  Conclusion

Representing the interpretation of one string as an abstract thing can be done
easily with RDF properties. This helps make a clean accurate model. However,
using the concept for datatypes in RDF is incompatible with RDF as we know it
today.

* * *

See also:

  * [Expressing the identity of real things](https://www.w3.org/DesignIssues/Identity.html)

_@@@Needs circle-and-arrow pictures for each attempt._

Note. This section followed a discussion about "_[Using XML Schema Datatypes
in RDF and DAML+OIL](https://www.w3.org/DesignIssues//2001/01/ct24)_ with DWC.

[Thomas R. Gruber](https://www.w3.org/DesignIssues/mailto:gruber@ksl.stanford.edu) and Gregory R. Olsen, KSL [
"An Ontology for Engineering Mathematics"](http://www-ksl.stanford.edu
/knowledge-sharing/papers/engmath.html) in Jon Doyle, Piero Torasso, &amp;
Erik Sandewall, Eds., _Fourth International Conference on Principles of
Knowledge Representation and Reasoning_, Gustav Stresemann Institut, Bonn,
Germany, Morgan Kaufmann, 1994. _A non-RDF but thorough treatement including
units of measure as scalar quantities._

Compare with [ SUMO units of Measure](http://icosym-nt.cvut.cz/kifb/en/ont
/sumo-units-of-measure.html) which seems have units as instances, and
multupliers such as kilo, giga, etc as functions.

A ittle off-topic, On linear and area memasure, John Baez's ["Why are there
63360 inches per mile?"](http://www.math.ucr.edu/home/baez/inches.html) is
good reaing.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

(names of certain characters may have been misspelled to protect the innocent
;-)

