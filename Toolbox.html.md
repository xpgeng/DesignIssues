[![W3](https://www.w3.org/DesignIssues//Icons/WWW/w3c_home)](https://www.w3.org/)

_Status: Personal ramblings, unfinished in many places. Abandon requiements
for consistency all ye who enter in.Created: 1999/06/18_

This document was an attempt to build logical formulaue as closely as possible
on top of the RDF triple abstract syntax. Another more recent investigation in
this direction is [Notation3](https://www.w3.org/DesignIssues/Notation3). It investigates using XML for logic.

* * *

In this document:

  * Assumed Syntax
  * Semantic Context
  * Assetion of another document (`include`, assert, truth)
  * Logical expressions: (not)

Example of trust statemement

Quantification (for all, exists)

# The Semantic Toolbox: Building Semantics on top of XML-RDF

The XML syntax [] and the RDF model [] give the basics for semantics of the
Web, but it seems to me we need some conective tissue to work towark the
semantic web. Basically, everything we think of as "data" on the Web forms a
set of logical statements. We need a unifying logical langauge for data - for
the machine interfaces to data systems -- in the same way that HTML was a
unifying language for human interfaces to information systems. This document
is an attempt at an existence proof to reassure one that the XML/RDF model
will be able to meet a number of requirements which have been proposed in the
community. These include

  * Stating that a list is definitive;
  * Making a reference contingent on a digital signature of the destination;
  * Writing inference rules for linking old and new schemata;
  * Expressing the equivalence of terms in different database schemas;
  * ...

The need, of course, is to build a logic out of RDF, as naturally as possible.
We fail if the syntax becomes drmatically more cumbersome as we add features;
we win if we find that higher-oder statements look like natural XML just as
simple metadata assertions do. We fail if at every stage we have introduced
special XML syntax whose semantic is expressed in English; we win if we find
that we can build up the language by introducing new RDF properties -
especially those whose semantics can be expressed in RDF and the preceding
properties.

(Within this document, XML elements with namespace prefix are assumed to be
defined as pointing to something the reader can figure out, and unprefixed
element names are used for new features which are introduced in this document.
).

## Assumed syntax

I assume for the purposes of this paper a syntax for data in XML which is now
described in a [separate note on syntax](https://www.w3.org/DesignIssues/Syntax.html).

## Semantic Context

Assertions are not all equal. They are made in different documents by
different people with different guarantees. They may be refered to, and even
denied explicitly. The context of an assertion is therefore indispensible to
its use.

Context is inherited though nested XML elements unless an element of the
following forms changes that.

When an assertion is verified, evidence as to its veracity is accumulated and
submitted to subjective criteria of trust assesment. While the eventual trust
criteria are subjective, the logic of what is meant when data is put on the
Web must be very well defined and unambiguous.

### On reification

The RDF model currently is that of an (unordered) set of assertions. We will
demonstrate that this remains all that is needed to represent the new langauge
features. Every new feature can be introduced as a new RDF property. However,
we will see that this is an impractical way of actually processing
information, as it involves using RDF indirectly to describe the parts of a
statement instead of making it directly. This process (called reification) is
described in the RDF Model &amp; Syntax document. An RDF statement in a what
RDF called a model, but I call a Formula, can be reified by four triples.
Three are needed to assert the subject, object, and predicates of the
assertion. One to assert that the triple is part of the given model (set of
triples) -- where more than one model can exist. Reification therefore blows
up the storage requirement by a factor of four.

There is also a problem when using a simple link between the context formula
and the statement, that it is necessary to specify definitively the set of
statements in a formula. There are a number of ways of doing this, incluing
the DAML list "first/rest" method, giving the number of statements, and giving
the relationship as for example "item_2_of_5". As these are inter-convertible,
the choice is not fundamental.

We will see how reification ends up being replied successively, making the
verbosity become quite unnacceptable as a practical technique for repreenting
formulae. Therefore, while we will derive each language feature simply by
defining a new RDF property, to make it practically useful we will also need a
syntax which allows the new langauge to be written less verbosely

Reification turns what is an explict statement into a description of a
statement which is not specifically asserted, but which is described and can
be talked about. In languages this is typically done by quotation. In RDF
synatax to date there is now way of doing this, so let as start with that as
then we can do anything.

### Quotation

There is no specific element for this yet, so let's assume an QUOTE which,
which allows one to talk about assertions without asserting them. In the
"Ralph said Ora wrote the book" example, "Ora wrote the book" is obviously
quoted. We need a away of distinguising between things we said and we stand
by, and statements we wish to discuss. This is going to be of primary
importance on the Web in which information from many sources is combined. It
is a fundamental part of language design. (The PICS label system uses it for
example. In metadata, information about information, quotation is obviously
essential.).

One way would be

    
    
    <quote id=foo about="theBook">
              <dc:author>Ora</dc:author>
    </quote>
    <rdf:description href="#foo">
       <dc:author>Ralph</dc:author>
       <http:from>swick@w3.org</http:from>
    </rdf:description>

Here the quoted part says that Ora wrote the book, and then the description
following it assert that Ralph made the assertion. This not to be confused
with a quote which maintains that it itself was written by Ralph, but for
which the present author makes no claim of truth or anything else:

    
    
    <quote id=foo about="theBook">
        <rdf:description href="#foo">
           <dc:author>Ralph</dc:author>
           <http:from>swick@w3.org</http:from>
        </rdf:description>
        <dc:author>Ora</dc:author>
    </quote>

If it becomes common, would be even simpler is we defined a shortcut element
&lt;head&gt; to mean "about my enclosing parent element":

    
    
    <quote about="theBook">
        <head>
           <dc:author>Ralph</dc:author>
           <http:from>swick@w3.org</http:from>
           <follows-from>http://www.org/catalog</follows-from>
        </head>
        <dc:author>Ora</dc:author>
    </quote>

In fact one could make &lt;quote&gt; basically identical to
&lt;rdf:Description&gt; except disavowing of the assertions contained. [This
was, I understand, considered by the RDF working group].

## Assertion of another document

(see also [daml:imports](http://www.daml.org/2000/12/reference.html#imports-
def) of Oct 2000 and and [Dan's GET/PUT model](https://www.w3.org/DesignIssues//2000/07/document-
maintenance/))

Just as it is important to be able to exclude assertions within a document
from the set asserted directly by the document, it is equally as important to
be able to include assertions which are in fact not in the docoument. This is
easy to do with another property. It is, after all, a single assertion
indiacting that B should be believed to the extent that you believe A.

    
    
    <foo:bar>
        <head>
          <include rdf:value="part1.rdf" />
          <include rdf:value="part1.rdf" />
          <include rdf:value="part1.rdf" />
        </head>
    </foo:bar>

This document, of some type we need not worry about, from the semantic point
of view is deemed to include the information in part1.rdf, part2.rdf, and
part3.rdf. We use HEAD here as a shortcut for setting the subject to be the
current document.

(This is NOT a textual inclusion - it only brings across the semantics of the
other document, parsed with no context from this one. If the destination
document inlcldues HTML for SMIL, the text and graphics for human consumption
are NOT invoked in any way!)

There is no information provided as to how or why to trust those documents.
The statememnt is only about the meaning of this document. It is importrnat to
separate in the language the meaning and the trust.

(Deciding on a name for this is really diffictl, to get people to follow this
very basic logical function. "Vouch"is a a nice word, meaning "asserts the
truth of". "Imply" is nice word as it contains the fact that it is a
relationship between one document and another: if you don't believe the first
you don't have to believe the second. "Assert" or "IsTrue" are other
possibilites.)

It is overcomplicated to represent this as a binary relationship between the
current document and the document vouched for. It realy is a unary
relationship true(f) expressed in the current document. That would need an XML
shortcut rather than an RDF property, though, which would score less on
cleanliness. But it is simpler:

    
    
    <foo:bar>
          <assert href="part1.rdf" />
          <assert href="part1.rdf" />
          <assert href="part1.rdf" />
    </foo:bar>

Alternatively you can make a statement of the truth of the document:

    
    
    <rdf:description about="part1.rdf">
       <truth>1</truth>
    </rdf:description>

This is strightforward too - and begs the question of what happens if you say
"0" instead of "1"

    
    
    </quote>
    <rdf:description about="#foo">
       <truth>0</truth>
    </rdf:description>

## Logical expressions: NOT

We don't have a form for logical expressions for the semantic web, although of
course logical expression in human readers documents are covered by MathML.
The practical need for logical expressions has been apparent in the IETF's
work on profiling in the "conneg" group, and in the W3C's internal work on
access control.

(No comment needs to be made about the huge number of languages which allow
logical expression. In the classification of languages, normally logic is
introduced before the ability to make statements about statements -- or
rather, it was until Goedel. Here, the "first order" question is taken
backwards, in that RDF statements already break the "first order" assumptions
before basic logic has been introduced. _Not_ extends the toolbox to
propositional logic.).

Of course we already have the logical "**AND**" construction by juxtaposition.
Two statements one after the other are both to be trusted to the same extend
as the context. It is difficult contemplate a logical system in which two
statements cannot be considered together, so

{ S1, S2 } == S1 &amp; S2

more or less defines "&amp;", and juxtaposition already exists, we already
have it.

One of the simplest forms of expression is NOT(x), which maps onto XML most
naturally as a single XML element:

    
    
    <bar id="foo" about="http://ww.w3.org/">
    
    
        <w3c:member>http://www.ibm.com/</w3c:member>
        <not>
            <w3c:member>http://www.soap.com/</w3c:member>
        </not>
    
    
    </bar>

The _not_ is transparent when it comes to the subject, but clearly not when to
comes to the trust! It is an explicit assertion that the contained assertion
is false.

### _Not_ by reification

I am not proposing that the best machine in practice to process the language
we are building is based directly on RDF triplets - but it is important to
ground new features in basic RDF. As RDF has little power at its basic level,
anything new has to be introduced by reification - by describing it in RDF.
Hence, to say "not(node, property, value)", you have to say, for example,
"there is something which is an RDF property and has a subject of A and whose
B property has vale C and is false". So in RDF, not can be introduced by a new
property which associates a boolean truth value with another node. Actually
manipulating the information in this way is of course not very efficient.

    
    
    <quote id="foo" about="http://www.w3.org/">
    
    
        <w3c:member>http://www.soap.com/</w3c:member>
    
    
    </quote>
    <rdf:description about="#foo">
       <truth>0</truth>
    </rdf:description>

There is an overlap of semantics with &lt;include&gt;.

There are therefore two ways of representing an expression containg not. The
strict RDF way, in which the only data is a set of triples, involved the
reification above.The way using the enhancd model simply encodes each

Before _not_, every assertion in an RDF database could be handled
independently, and deletion of a facts did not create untruth. However, with
_not_, it can, because we need to know the full set of terms in a negated
_and_ expression to be able to deduce anything.

_Not_ is very powerful. Given _not_ and _and_, as logicians and gate designers
know, you can construct many things. Immediately, given that the contents of a
_not_ element are _and_ed, we have a "nand" function. ["Nand" is the Sheffer
stroke which was shown in 1913 to be the only operator needed to construct for
a complete propositional logic system, and which lin the 1970s was the basic
building block unit of the 7400 series logic].

With nand, you can construct, for example, _or_:

    
    
    <not>
        <not>
            <w3c:member>http://www.ibm.com/</w3c:member>
        </not>
        <not>
            <w3c:member>http://www.soap.com/</w3c:member>
        </not>
    </not>

is equivalent to "either IBM is a member of W3C or soap.com is a member of
W3C". It is a little clumsy, but looks more natural if you use synonyms:

    
    
    <alternatives>
        <or>
            <w3c:member>http://www.ibm.com/</w3c:member>
        </or>
        <or>
            <w3c:member>http://www.soap.com/</w3c:member>
        </or>
    </alternatives>

Implication can also be constructed using _not_. "If soap.com is a member then
IBM is a member" can be written as "it is not true that soap.com is a member
and IBM is not a member", or:

    
    
    <not>
        <w3c:member>http://www.ibm.com/</w3c:member>
        <not>
            <w3c:member>http://www.soap.com/</w3c:member>
        </not>
    </not>

This similarly can be made more palatable to the human reader by using
synonuyms for _not_:

    
    
    <if>
        <w3c:member>http://www.ibm.com/</w3c:member>
        <then>
            <w3c:member>http://www.soap.com/</w3c:member>
        </then>
    </if>

### Example of trust statemement

Above we had an example in which we invoked using &lt;include&gt; the meaning
in another document. In same cases one might want to constrian the simple
invokation to protect the reader. We can use a conditional, for example, to
require a partiuclar checksum or digital signature:

    
    
    <foo:bar>
      <head>
        <if>
          <ds:hash rdf:about=part1.rdf">
             md5:1287129371237..12738127398712</ds:hash>
          <then>
              <include rdf:value="part1.rdf" />
          </then>
        </if>
        <if>
          <ds:signed-by rdf:about=part2.rdf">
             rsa:a/1024/123hg1238912whh3983yd2734dg
          </ds:signed-by>
          <then>
              <include rdf:value="part2.rdf" />
          </then>
        </if>
      </head>
    </foo:bar>

Here the document asserts the contents of part1 only if it has a certain hash,
and asserts the content of part2 only if it has a digital signature which
verifies with a partuclar public key. (the ds namespace is assumed to exist to
define hash and signed-by and is not frther discussed here apart from to pint
out that the hash value is an existing URI md5 scheme and that the RSA key is
just regarded as a URI too).

What is nice about this section is that this functionality has been achieved
using existing features. The two statements may be a little verbose, though it
isn't obvious how one can make them very much more compact.

##  Quantification

Examples above are very specific, when in fact many rules are made about
generalities. How would we add quantification to XML, the "for all" or "there
exists some"? Like anything else, you can introduce it into RDF by reifiying
it (to descibe the expression's structure and then assert something about the
structure). Formally, then, to build it by tedious reification, one would

    
    
    <quote id="foo" about="http://www.w3.org/">
    
    
        <w3c:member>http://www.soap.com/</w3c:member>
    
    
    </quote>
    <rdf:description about="#foo">
       <true-for-all>http://www.soap.com/</true-for-all>
    </rdf:description>

In this example (compare with the _not_ reification above) the element
expressing "W3C has a member soap" statement is given the identifier #foo, and
then the assertion is made that the statement represented is true even when
"http://www.soap.com/" is replaced with any other value. This may not be an
inutitive way of quantifying things, and the variable name may seem bizare,
but it shows that we can derive quantification from a single added RDF
property, "true-for-all" [note].

Quantification syntax for logic in XML

It is not obvious how to add this to a practical XML-based toolbox. One can
either try to layer it on to of XML, or extend XML. Here is one example of
layering it on top of XML. We use an XML element for the forall clause,
defining a variable at the same time in the ID space of the XML document. Any
reference to that variable within the clause is to be taken torefer to the
variable.

    
    
    <forall id="baz" var="x" rdf:about="#x">
      <if>
        <w3c:memberOf>http://www.w3.org/</w3c:memberOf>
        <then>
            <w3c:canAccess>http://www.w3.org/Member</w3c:canAccess>
            <exists var="rep">
               <w3c:acMember>#rep</w3c:acMember>
               <w3c:employee>#rep</w3c:acMember>
            </exists>
        </then>
      </if>
    </forall>

which, translated, means: For any X, if X is a member of W3C, then X has
access to the member page, and there is some rep which is an advisory commitee
representative for X and also is an employee of X.

It is messy compared with mathematical symbols, but not compared with typical
XML.

The var attribute defines a variable in ID space (a subset of URI space), so
must have type IDREF because to have type ID in XML has the secondary meaning
of being an identifier for the element.

(An alternative might be to use XML enities in a magic new form of entity
&amp;x; or to simply make a new syntax which declared $x to be a variable even
tough you get really fed up with the dollar signs; or if you want in
interesting one to make a namespace which is defined to consist of varibles.
This latter would maybe confuse engines which didn't understand it.)

(Note that the XML namespaces don't use scoping, but a "forall" clause
necessarily introduces a variable which only has sitgnficance within the scope
of the clause, element in this syntax. However, it may be referred to from
outside when a substitution is defined. You will want to say for example
"substituing "John Doe" for the variable foo.rdf#name in foo.rdf#rule1 yeilds
..." so the fact that the variable is afirst class object may possibly be
useful. Beware of course that you may want in one forumula to use the
quantified expression more than once using different subsitutions)

In the 1.0 syntax spec there is a special syntax for a particular form of
quantification

    
    
     <rdf:Description aboutEach="#pages">
    
        <s:Creator>Ora Lassila</s:Creator>
    
    </rdf:Description>  

This we can now explain as meaning

    
    
    <forall var="x">
     <if>
       <rdf:li for="#pages" value="#x">
       <then> 
           <s:Creator for="#x">Ora Lassila</s:Creator>
       </then>
     </if>
    </forall>

### Definitive lists

A very common thing we need to express is a definitive set of things.

(Examples of definitive lists:

  * A definitive list of requirements for a document to be valid - validatable schema.
  * An access control list (ACL) for a resource.
  * A bank statement
  * and so on...)

When W3C gives a list of W3C members, it can not only tell you that if someone
is on the list they are a member, but also that if they are not on the list
they are not. The exclusivity of a list is a statement about a document or
part of a document. Here is a statement about the definitive nature of a list,
followed by a list:

    
    
    <forall var="x">
      <if rdf:about="#list">
        <w3c:member "id=statement"
           about="http://www.w3.org/"><var ref="#x">
        </w3c:member>       
        <then>
          <implies rdf:value="#statement" />
        </then>
      </if>
    </forall>
    <foo:container id="list"
       rdf:about="http://www.w3.org/">
       <w3c:member>http://www.ibm.com/"</w3c:member>
       <w3c:member>http://www.hp.com/"</w3c:member>
       <w3c:member>http://www.netscape.com/"</w3c:member>
       <w3c:member>http://www.sun.com/"</w3c:member>
       <w3c:member>http://www.acme.com/"</w3c:member>
    </foo:container>

Note that just as in normal algrebra one almaost always uses "For all" with
"such that", here one will almsot always use &lt;forall&gt; with &lt;if&gt;
and so the two could be combined to save space into, say, &lt;ifany&gt;

    
    
    <ifany var="x" rdf:about="#list">
        <w3c:member "id=statement"
           about="http://www.w3.org/"><var ref="#x">
        </w3c:member>       
        <then>
          <implies rdf:value="#statement" />
        </then>
    </ifany>
    <foo:container id="list"
       rdf:about="http://www.w3.org/">
       <w3c:member>http://www.ibm.com/"</w3c:member>
       <w3c:member>http://www.hp.com/"</w3c:member>
       <w3c:member>http://www.netscape.com/"</w3c:member>
       <w3c:member>http://www.sun.com/"</w3c:member>
       <w3c:member>http://www.acme.com/"</w3c:member>
    </foo:container>

This is done using features defined to date.

(It is a little verbose, but we could make a shorthand for the expression
"list A is object-definitive for B", meaning "If list A implies the statement
&lt;B about=x value=V&gt; for some (x,V) then it will also imply any statement
&lt;B about=y value=V&gt; which is true. In other words, "ibm is a member of
w3c" in a object-definitive list means that the list will include all members
of w3c, wheras in a subject-definitive list it implies that the list contains
all things ibm is a member of

    
    
    <foo:container id="list"
       rdf:about="http://www.w3.org/">
       <w3c:member>http://www.ibm.com/"</w3c:member>
       <w3c:member>http://www.hp.com/"</w3c:member>
       <w3c:member>http://www.netscape.com/"</w3c:member>
       <w3c:member>http://www.sun.com/"</w3c:member>
       <w3c:member>http://www.acme.com/"</w3c:member>
    </foo:container>
    
    <object-definitive about="#list">:w3c:member
          </object-definitive>

)

* * *

### Functions

A function is the ability to encapsulate meaning with the extraction of
parameters to be specified later. This could map onto RDF and XML in a number
of ways, just as practical languages have various forms of function.

When looking at the expoesion of data, a function becomes a compact expression
of a common expression. The shorthand expression can take many forms
(positional or names parameters) but a clear choice for RDF is an RDF node,
whose actual arguments [the things which at function invokation replace the
formal parameters] are provided by a set of properties of that node.

The equivalent of the function "body" is then a set of information which can
be deduced from the node. An interesting point of the semantic web philosophy
is that, while one might think of "the" meaning of a function, in fact the
inference rules which express that are those provided by the functions
creator, but any other document might add its own rules. In other words, the
function body is not a very useful term, and any expression about the function
will do. The example above

    
    
    <forall id="baz" var="x" rdf:about="#x">
      <if>
        <w3c:memberOf>http://www.w3.org/</w3c:memberOf>
        <then>
            <w3c:canAccess>http://www.w3.org/Member</w3c:canAccess>
            <exists var="rep">
               <w3c:acMember>#rep</w3c:acMember>
               <w3c:employee>#rep</w3c:acMember>
            </exists>
        </then>
      </if>
    </forall>

in fact is an example. It states some implications of the concept of
membership of W3C. You could take this to be definitive, but that is really
part of the trust model rather than the language. In other words, W3C might
say that if an organization is a member of W3C then it has an AC
representative who is an employee. Another may maintian that any organization
which is is a member of W3C conmtains at least one smart employee.

I would expect that, where particular RDF nodes are intended to express
particular things by their creators, that the schema would have at least a
pointer to those things.

In the above example, the inference was just from a property of membership: a
property is used as binary predicate, but in general n-ary form with multiple
parameters could look like:

    
    
    <forall var="x" v2="y" v3="z" rdf:about="#x">
      <if>
        <employee>
           <name>#y</name>
           <street>#s</name>
           <zip>#z</zip>
        <employee>
        <then>
           _ [...]
    _    </then>
      </if>
    </forall>

The basic RDF utility allows us to write all kinds of forms, and it may be
useful to pick one to make a common form. In the example above, the rule
applied to any node which is the employee (of anything) and has a name and a
street. The property name "employee" is used like a function name. We can use
types for this instead:

    
    
    <forall var="x" v2="y" v3="z" rdf:about="#x">
      <if>
        <rdf:type>http://www.w3.org/1999/a/empType</>
        <z:name>#y</>
        <z:street>#s</>
        <z:zip>#z</>
        <then>
           _ [...]
    _    </then>
      </if>
    </forall>

Here the rule applies to any node which has been explicitly given the type
empType and has the given parameters.

Of course, these two things are linked by the RDF schema type properties.

    
    
    <rdfs:range about="#employer">http://www.w3.org/1999/a/empType</a>

(sp?) is a way of saying

    
    
    <forall var="x" v2="y" rdf:about="#x">
      <if>
        <employer>#y</employer>
        <then>
           <rdf:type>http://www.w3.org/1999/a/empType</rdf:type>
    __    </then>
      </if>
    </forall>

In fact, while we are talking about functions we can use what we have now to
define bits of RDF Schema specification: we can start by defining what "range"
of a property means:

    
    
    <forall var="aPropertyName" v2="y" v3="aType" rdf:about="#x">
      <if>
         <rdfs:range about="#aPropertyName">#aType</a>
         <then>
           <if>
              <#aPropertyName>#y</>     <!-- oops!  ->
           <then>
              <rdf:type about="#y">http://www.w3.org/1999/a/empType</rdf:type>
    __       </then>
         </then>
      </if>
    </forall>

I knew we would need a way of invoking an RDF assertion by its full ID. This
is the identifier problem introduced above.

    
    
    <#aPropertyName>#y</>     <!-- oops!  ->

is what we need, and we can't in XML but we can instread define in the basic
RDF syntax an XML element to do that

    
    
    <rdf:property pname="#aPropertyName">#y</>     <!-- better!  ->

which is not as clean in the sense of a consistent language but is but good
XML.

@@@

### Skolem functions.

There are times when you may know that every person has a mother and you may
know that a person's mother is unique and so it is convenient to save the
bother of writing "for any x such that x is a's mother" and simply refer to
a's mother. (This is similar in concept to skolem functions used to remove
quantifiers from expressions in symbolic logic.)

Maybe time for an XML shortcut:

&lt;the pname="#mother" of="#a"&gt;

can be thought of as a query as well. It is well defined when the property is
unique, but when a property is not unique then it is not obvious what sort of
implicit quantification should be implied, and what the scope of it would be
... not obvious. Two choices appear to match the choice of definite and
indefinite article in natural languages:

  1. Make the use of the phrase within any forumula imply an assertion that the mother is unique: F(..., THE(prop,x)...) -&gt; (exists(w). prop(w,x)) &amp; ((prop(x,y) &amp; prop(z,y)) -&gt; x=z). Here THE(prop) is in caps as it is a special kind of function: in skolemization., the(prop) is a new function added to the language to make a new langauge. THE not a first order function as it takes a predicate as an argument. Nor is it a function at all in that one can only generate a skolem sunction from the xistence statement.
  2. Make the use equivalent to an existence assertion but no uniqueness assertion. Here F(.., A(prop,x)..) -&gt; (exists(w. prop(w,x)).

The latter is the way it is usd in Skolemization, and I think we should stick
to that. Note that are NOT functions. They are not part of the language. They
are shortcuts.

## Proof

This is not about constructing a proof, but about transmitting a proof to be
validated. To define the proof language, one must define the powers of the
proof checking machine. In other words, do you have to spoon-feed it every
atomic step, or is there a certain jump which it can make? This decision does
not have to be fundamental, in that you can imagine different vocabularies for
expressing a proof to different engines which have different capability. At
one extreme is the simplest logical engine for which everything must be
reduced to a connonical form of binary operators. At the other extreme is the
proof "A follows-indirectly-from B" which involves the proof checker in
extensive (but bounded, or we don't call it a proof) searches. In between lies
the sound engineering compromise.

This will not be rigorous derivation, but a .

  1. Canonicalization: The proof engine can be assumed to deduce one statement from another where the URIs involved (etc?) have the same value when canonicalized (equivalent values).
  2. Extraction: If an RDF assertion is made in an AND list (a normal list of RDF statements), then the proof engine can deduce it. (Does it need to b told the index of the ietm within the list? Or ID of the element?)
  3. Substitution: If a substitution is specified, the proof engine can generate the document which results from that subsitution. substitute(expression, variable)
  4. Implication: Given a proof of all the items in an AND list except for one, and given the negation of the AND list, can deduce the negation of the remaining item.
  5. Dereference: Given the statement that A follows-from B, and given B, deduce A.
  6. ... and so on.

[@@ref]

Now we need an expression to lead the proof-checker through a proof. Let's
assume taht canonicalization isimplciit in that it just involves resolving
relative URIs, and that otherwise exact string commparison implies
equivalence. (In practice there are often different URIs which yield the same
result but that can be an equivalence statement we can explicitly make if ever
we need to)

In the case that a given document [fragment] allows the proof checker to
deduce the required result directly, then all one needs is a single RDF
assertion to point it at the source from which it follows. We therefore
introduce the &lt;follows-from&gt; assertion

### Follows-from

#### Semantics:

All the information A was derived from information in B.

#### Comment:

This is a tool for the "oh, yeah?" button. It allows one to trace back to the
origin of an assertion or assertions. In order to verify the assertions, the A
is abandoned as being only a hint, and B is parsed to extract the same
meaning, and then verified. No representation is made about the language in
which B is written or why B should be believed.

#### Example:

    
    
    <a:record id="foo" about="http://ww.w3.org/">
    
    
        <w3c:member>http://www.ibm.com/</w3c:member>
    
    
    </a:record>
    <rdf:description about="#foo">
        <follows-from>http://www.w3.org/MemberList</follows-fromsource>
    </rdf:description>

The assertion that IBM is a member of W3C is implied by the W3C membership
list.

(Does the document assert that you can _still_ deduce the statements from the
document? Yes, formally - an assrtion is an assertion. However, if you don't
trust the current document, typically you treat it as an invitation to check
the URI given. Later we must deal with expiry with time and "I found yyy in
xxx but don't trust me: you check" statements which do not lend explicit
credance.)

### Specific derivation syntax

...... @@@@@@

### Digital Signature and Trust

The above deals with logic, when in fact any deducion in the real world or on
the Web is in fact made according to rules of trust. On the Web, trust is
enhanced by the power of public key cryptography, and in particular, digital
signature. The W3C Signed XML activity defines ways of signing an XML document
so that it can be shown to have been signed by the private key corresponding
to a give public key.

The following is a model of trust which seems powerful and seems general. The
basic concept is that of a statement being "assured by" a set of keys. This is
a new word and if you can thing of a better one, let me know. It means that
the statement either has been made in a document (or part of a document) whose
signature has been verified with the key, or it has been logically derived
from such statements. When it is logically derived from a combination of
statements assured by different sets of keys, then it is assured by the union
of the sets.

(You can think about it in terms of _belief_ if you like, that if you
_believe_ all the keys in the set you will _believe_ the statement, but that
is not a useful analogy, as the model does not require agents to actually
"_believe_" anything).

While from the rules defining assurance you might expect a logical processor
to accumulate a larger and larger key set as information is drawn in from more
and more sources, in fact the key set can reduce too. Suppose you have found
on the web statment A signed by key Ka, and statment B signed with key Kb. If
a third statement, signed with key K, says, "If A is signed with Ka it is
true, and if B is signed by Kb it is true," then you can deduce A and B
assured by K. I would expect a typical trust engine to have one key which it
trusts basially from installation. For a webserver, for example, the webmaster
holds the key. The server will only act on something which is assured by that
key. The various configuration files then contain trust rules which delegate
responsability for particular aspects of operation.

Many trust engines (whether or not they think of themselves as trust engines)
use simpler rules which are specicializations of this general model. One is
the simple trust boundary: "Trust the following keys for anything, anything
else for nothing". This is typical of the configuration of a web browser for
trusting applets. It obviously works because it is only reposible for a
certain decisions, and in fact the user is also involved with every one as
well - before the downloaded code is executed. (This binary model of trust
leads to that binary concept of "_belief_")

The most general rule I can think of is of the form "if a statement of the
form x follows from key set y then deduce f(x)." This would, of course,
typically be signed with another key.

(If we assume a key is a URI then we can declare keysets as URIs too, by just
using unique identifiers. This means that the problem of dealing with sets can
be hidden from the logic if we need to simplyify it. We just declare a key
set, give it mid: URI, and declare which RSA (say) keys it contains. I don't
think the key set idea is very fundamental - we just seem to need it for
completeness, so that we can extract the assuring keys from sperate
statements: from "A assues S and B assureds T", deduce "set {A B} assures S
and T". Maybe we can get away without that extraction, using nesting instead,
`A assures `B assures S &amp; T' ')

@@ homework: express published trust models in this general trust model.

Examples of trust rules

"If K assures that y is a member of w3c then they are"

Doing this without any extra

    
    
    <ifany varid="x'>
       @@@@@@
       <then>
       </then>
    </ifany>

## Conclusion

XML is clearly a (terrible, great) way of representing formal logic and trust.

* * *

## Assertions about topology - appendix

These are some random assertions about assertions, in particular the ropilogy
of th DLGs which they make and the inferences which can be directly made.
Within this list, the semenatics are expliand for when the assertion is made
about A and the property is given as having value B.

### A Implies B

Semantics: Any assertion using the property type A implies an assertion with
the same subject node and value but with property type B.

Comment:

Domain and Range: The subject and object must both identify RDF assertions.

Example

    
    
    <implies rdf:about="#from" rdf:value="#responsible">

If A is "from" B then A is repsonsible for B in this vocabulary.

### A Inverse B

Semantics: Any assertion using the property type A implies an assertion with
property type B in the reverse direction - ie whose subject was the value of A
and whose value was the subject of A.

Comment:Domain and Range: The subject and object must both identify RDF
assertions.

Note some relations are self-inverse. "Inverse" is self-inverse.

&lt;implies rdf:about="#part-of" rdf:value="#includes"&gt;If A is "part-of" B
then A "includes" B in this vocabulary.

### Acyclic, etc

...@@@

## Terms introduced - A summary

Toolbox terms Term | Language role | axiomatic status | semantics  
---|---|---|---  
rdf:about | xml attribute | syntactic sugar | set defualt rdf subject for
element contents  
rdf:for | xml attribute | syntactic sugar | override rdf subject for this
element  
head | xml element | syntactic sugar | set default rdf subject to parent
element's node  
not | xml element | fundamental addition | implies (reifiation and) denial of
contents  
truth | rdf property | strict alternative to _not_ | asserts boolean
truth/falsity of document part  
if | xml element | synonym sugar | synonym of not to create conditional  
then | xml element | syntactic sugar | synonym of not to create conditional  
forall | xml element | fundamental | quantification  
exists | xml element | syntactic sugar | there exists - derivable from
not(forall(not ...))  
  
[Notes

Thanks to Dan Connolly for pointing this out.

## References

these always seem to diappear... theer are many small lists of these, all
different.

Ban logic@@

[Appel](http://www.cs.princeton.edu/faculty/appel/)'set al. work at Princeton
on [Proof-Carrying
Authentication](http://www.cs.princeton.edu/sip/projects/pca/): Proof-Carrying
Authentication. Andrew W. Appel and Edward W. Felten, 6th ACM Conference on
Computer and Communications Security, November 1999.

* * *

Last change $Id: blank.html,v 1.1 1999/05/24 14:24:19 timbl Exp $ Tim BL

