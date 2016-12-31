Tim Berners-Lee  
Date: 1999, last change: $Date: 2009/08/27 21:38:08 $  
Status: personal view only. Editing status: first draft. _Written partly when
the Namespace argument came around again and I realized that where there_

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Axioms of Web Architecture: the meaning of a document

_Abstract: The meaning of a document is then the product of some text in some
language) and the meaning of the language. The text is found in a document and
the language defined in a document called a schema._

* * *

#  Meaning

_Grounding the meaning of a document in URI space._

What is the meaning of a document?

The meaning of a document on the Web can be defined more precisely than an
arbitrary paper document. Because we have the benefit of a global namespace
(URIs), things become possible which were not before. One example is global
hypertext; another is the rigid (though rarely absolute) specification of
meaning. Just as a hypertext document can now exactly point to another
document when it makes a reference (instead of making some vague natural
language reference to it), so can a formal document make a precise reference
to the language it uses.

A writer of a document uses the language to convey his intent to the reader.
It is essential that the intent of the writer can be well defined for both
parties and in general for a third party.

The "language" here I means the set of symbols, the syntactic rules which
constrain their combination, and some semantics which are conveyed by defining
their interpretation in one or more other formal language, or in some natural
language.

The meaning of a document is then the product of the text of the document (in
some language) and the meaning of the language.  
---  
  
On the Web, [important things are identified by
URIs](https://www.w3.org/DesignIssues/Axioms.html#Universality2). This should clearly apply both to the
document itself and to the language. The party which defines what a URI refers
to I call the publisher, or owner of the URI. HTTP allows a delegated system
of authority for ownership (DNS) to define ownership of URIs, and it also
provides a network protocol to retrieve documents representing that identified
by the URI. The text a document is defined by its publisher and the meaning of
the language is defined by the publisher of the language.

Natural languages are constantly evolving and rather vague, in that no one
(except _Scrabble_ players) use a particular dictionary as a definitive set of
meanings. In practice, the meaning of a word in a natural language is the sum
of the associations of that word -- logical or poetic -- in the mind of the
reader or writer. Of course society works on the basis of a very strong
similarity of the webs of association in different people's minds.

In the semantic web, however, meaning is not vague: the idea is that languages
must be defined formally and as precisely as possible. The semantic web
consists of some "terminal" languages which are defined solely in natural
language terms, and some languages for which there are machine-readable
interpretations into other formal languages. Whereas programs processing
documents in the first sort of language will typically have to be hand coded,
documents in the second set may be processed automatically to convert them
into languages in the first set.

URIs can be of various sorts, with various properties depending on their
scheme (and, for http URIs, the publisher), but some URIs can be dereferenced
to a definitive document. The document resulting from dereferencing the URI
for a language is a place where the publisher of the language can put
definitive information about the meaning of a language.

###  Language and document subsets

As languages evolve, there can be many languages which are similar.
"Similarity" doesn't mean much, but something which is well defined is when a
document in one language A can be treated precisely as though it had been in
another language B.

###  Meaning in XML

In XML, a language is a "namespace", and the document about the language is
called a "schema". In XML, one document can contain a mixture of languages,
and so the schema if written in XML may contain information about syntactic
constraints (in XML-schema language) and/or RDF properties (in rdf-schema
language), or any combination of the above. (note)

XML puts no constraints on a language apart from syntactic structure. There is
not (without RDF and logic or some other higher level) any overall framework
into which new languages can be introduced. So, the question of **what an XML
document means depends** first upon the fully qualified name of the **document
element**. No semantics can be attached to any of its descendents in the
document tree except in as much as is defined by the specification of that
element type in that namespace. One cannot talk about the "meaning" of a
subtree of a document without understanding the semantics of the language. In
fact, because languages only necessarily define meaning for documents, the
only way one can talk about the meaning of a subset of a document is to define
a how those parts of the document can be reassembled into a second whole
document. This is what must be done when a digital signature is applied to a
document.

###  The Meaning of Digital Signature

The language defines semantics. On the simple philosophy that one place is
enough, It is not the place of a digital signature to define semantics. A
digital signature on a document may give a party reason to use the information
therein for purposes it would not have otherwise. The issuer of a public key
may also put constraints on what sort of guarantees are made by signature with
a given key. But the signature itself must not affect the semantics - the
meaning \- of a document. To allow it to would be to create an inconsistency
between the intent of the writer of the original document and the meaning of
the signed document. So, signatures themselves have no meaning. The meaning
has to be ascibed to them by other documents. For example, I may say, "If an
organization is a member of W3C according to a document signed with this key,
then that organzation is indeed a member". That is a trust statement which
gives the key a connection into the world of meaning of documents.

###  Style as meaning

(Although few people would think of presentation style of a document as its
"meaning", and many of us spend a lot of time emphasising the difference
between style and content and semantics, in fact much of what applies to style
applies to semantics. Therefore the "meaning in terms of presentation" is a
good test case for the architecture of the system. (For many documentation
systems, the only semantics required is "H2 means a big bold block on the
left"!) Style sheets provide an "interpretation"of a document by mapping it
onto another well-defined language of formatting properties. The style sheet
language gives a good definition (in English) of what is needed. This is an
interesting comparison, and I mention it as a place where architectural
conssistency should be maintained, but it isn't what I normally mean by
"meaning".)

###  Logical meaning

When XML is used to encode logic, then a document is a formula and the (see
[Logic on the web](https://www.w3.org/DesignIssues/Logic.html)). Then, the way new predicates and constants
interact is defined by the logic. The way fundamental new parts of the
language (such as quantification) are added is part of a more general question
of how arbitrary languages interact. Examples we have seen are the mixing of
XHTML and XSL. What is the result - XHTML or XSL? A document or a style sheet?
Both?

###  Mixing Languages

XML puts no contarints on a language apart from syntactic structure. There is
not (without for example RDF and logic) some overall framework into which new
languages can be introduced. This means that every language has to define how
it canbe extended by mixing with other languages. Typically it will indicate
the element types which can be subclassed by extensions and therefore
incorporated into documents wherever that element type is allowed.

One particular example of such a type is common to almost all languages. This
is the sentence, the fully qualified assertion or statement, the formula with
no free variables. Almost all whole documents count as such, though an
interesting counterexample is a style sheet which represent a function: it
specified the result document as a functin of an input document, and so itself
cannot be said to be a stand-alone statement. (If I sent you a message
consisting only af a stylesheet with no coverletter, what would it signify?
What would it mean if I digitally signed it?)

With that exception, it clearly makes sense to allow any language which has
the concept of a sentence -- maybe any language at all - to allow sentences
from other languages to be included anywhere where a sentence of its own could
go. **This should be a generic feature of XML schemas**.

(It is would be against the minimalist principle for XML generically to define
other common subclasses. Note that the RDF spec does define properties and
node types and the concept of subclassing in RDF. HTML defines things like
block and inline elements, which can be subclassed in extensions; SVG and SMIL
probably define similar concepts. The significance of this when looking at
downloaded support code would be that, for example, in a set of Java classes
implementing HTML, that any subclass of "Inline element" would export the same
software API to allow it to be justified and line wrapped in a text flow
object. So there is a natural correspondence between element type subclassing
and support class subclassing, but the tow must remain distinct. Language
specifications must always define what a language means without refering to
implementations if they can possibly avoid it)

Note that without the assurances given by such information you cannot just go
around embedding one language in another. Every language has to address the
issue which the concept of RDF transparency potentially solves for RDF. A
surrounding XML context must have the ability to quote, deny, negate or
whatever any element. In fact, nothing in XML says that the menaing of a
fragment is not affected by thing anywhere else in a document. Nothing
suggests that the process of removing sub-trees creates a valid document. (How
does xml fragment deal with this?)

###  Grounded documents

We can say a document is "grounded" if its meaning is completely defined
because every term used is explicitly, directly or indirectly, an explicit
direct or indirect referece to its definition in a document on the Web.
Clearly a definition of "grounding" depends on the set of documents one
considers acceptable definitions. "Grounded in W3C Recommendations" would
imply that the closure under [i.e. set of all the things you can possibly end
up with by repeated applications of] the operation of looking up definitions
would be a subset of the set of W3C recommendations.

This is the basis for the entire web and internet architecture stack today.
(See also: [Stack](https://www.w3.org/DesignIssues/Stack.html)) . All commercial use on the web is largely to
be considered in this light, that the meaning of each messaeg sent across the
Internet is well-defined by a series of specifications.

(A sense of grounding also can be appliyed seperately to different sorts of
"understanding". When "understanding" means presentation to a human for human
understanding, a presentation-grounded documents points to all information
such as schemata and style sheets which will enable it to be presented.)

###  Grounding as a myth: the Web of Meaning

The concept of grounded documents is important for predicatble systems, but it
is a bad model for the web -- or for life -- in the long run. Words in a
_natural_ langauge such as English are not grounded in a unique base set*.
Every time you look one up in the dictionary all you find are more words. The
world is web-like, and any attempt by the Web to constrain it to be tree-like
is bound to force a misrepresentation of realtity. This is the Wittgenstein
view of meaning. Understanding this view sometimes confuses people about the
very systematic way in which meaning in Internet protocols is defined by
layers and layers of specs.

In fact, the two views both apply, one nested inside the other. Yes, meaning
is use - but in the Internet protocols, society has set up social constraints
- laws and other expectations - which constrain use to be according to the
specs. This is a social constraint which your computer is under when you use
the Internet, just as when you fill out a tax form you don't have a choice as
to how to interpret the meaning of "Adjusted Gross Income on line 39 of a US
IRS form 1040". There is a whole department of the government which defines
what it is and which socially owns the term. So while the

What will change with the Semantic Web's development is that its grounding in
legacy systems will fade into history. Right now, the meaning of "Invoice
total vale" is effectively defined by the software which you plug your RDF
document into, and how it treats invoices. This is an important way to
bootstrap the semantic web with useful terms. That will become less important
as many different software poducts share teh same term. In the end, it is
weblike form which will characterize the semantic web. Everyone will be
defining things in terms of other things which they feel are useful and stable
enough. It will be impossible to insist that there be a global ordering
between more basic and less basic specifications -- and to do so would stop
the web scaling. No one will agree on a directed _acyclic_ graph determining
what terms are "more basic" than others. For any set of definitions in one
direction, there can always be some reverse definitions which can be seen by
others as just as valid.

So, while the concept of documents grounded in a given base set is important
for interoperability, it must not be seen as a goal to force the semantic web
into an acyclic structure. There will be no single Dewy decimal system for the
semantic web. The concepts of well-defined stable specifications will still be
essential. So will respect for the definitions of terms. The difference will
be that any one will chose their own set of langauges they consider "basic",
and find ways of defining other languages they come across in terms of those.
A rich web of conversions, translations will grow up to support this. The web
of trust will provdie tools for navigating within and selecting from this web
in a safe way. And of course, global standarsdw il wlways make like much
easier where they can be made.

###  FAQ: Surely meaning is only defined by use?

_This is all very well_, runs a popular line, _except that to talk about
"meaning" at all is basically bogus_. _The meaning of words, and therefore
languages, is defined by use - by how people actuall respond to them, by how
they are processed. Surely the only way I can guarantee that someone will
interpret a document in a particular way is to have some out-of-band agreement
with them first?_

Philosophically, it is indeed the case that you need some out-of-band (not in
the message itself) agreement. In real life, though, in fact there a lot of
widely-held agreements. In fact, the law is a set of agreements which you are
deemed to accept whether you formally agree or not. So when you are sent a tax
form, you can't argue that the language of the tax form is not one you
interpret in that way. they just stick you in jail.

The web works like one big agreement. By connecting your computer to it and
getting email from POP and IMAP ports, there is an understanding that what you
get are MIME messages, and the same thing when you pick up web page using
HTTP. So by using the web you are entering a world where the assumption can be
made that messages are to be interpreted by a set of specifications. the
specifications are (currently) generally written in english, and imperfect,
but basically debate about them is practically about details, not aboutteh
philosophy as to whether they apply. So that is why one can in practice talk
about meaning.

###  FAQ: Doesn't the meaning of a document depend on its context?

Of course it does. If i exclose a phtocopy of a document as an attachment, it
doesn't mean I am sending you that letter.

However, theer are a lot of contexts for a document which have the same
implication for the meaning of that document. Publication, by email to a
public list, or HTTP, or FTP, or printing on paper and nailing to a tree, in
each case leaves the meaning of a document defined in the same way. These
contexts, in which a document is published by a party, or a message converyed
from one party to another, are so common and basic that the meaning of the
document in these contexts is referred to simply as the meaning of the
document (or message).

The webarchitecture separately enumerates the ways in which these contexts
actually work under he hood (publication using HTTP, etc) and teh way
documents are interpreted and dealt with once published. That way, XML
langauegs don't ahve to keep referring to "meaning when received with a 200
code in HTTP".

* * *

##  See also

  * [Self-describing information in "Metadata"](https://www.w3.org/DesignIssues/Metadata.html#Self-descr)
  * [Evolvability](https://www.w3.org/DesignIssues/Evolution.html)

##  Footnotes

###  Name-less and Address-less systems

(Technically, it is possible to create a network with "source-based routing"
in which everything whether server or document is identified by an md5
checksum or other random unique ID, and network nodes learn to send packets
with full routing instructions. This is a little like the old email addresses
which specified a routing path like timbl@cernvax!mcvax!mitmail!whatever. The
process of hypertext link involves the client A contacting the server B of the
source document of the link and finding the path which B had stored as a way
to get from B to the server C of the link's destination document. Then the
client A can contact C first through the root ABC but then from local
information and information from B and C can maybe derive a more efficient
route AC. Such a system has different scaling properties as a subset of teh
information about the network must reside in the network hosts rather than in
the routers. Its efficeny and scaling properties rely on features of the
topology of the web such as locality of reference.)

###  Language identity crisis in XML

(There is currently (1999/9) much debate in the XML world over exactly what
defines a language, the proposed answers ranging though: the publisher of the
namespace including any information in the definitive schema; a separate note
of a schema; a schema plus a different namsepcae URI document plus a version
plus an HTML profile; and "nothing". If this debate resolves itself such that
athe identity of a language is not clearly defined. In that case the XML
namespace mechanism may prove an insufficiently firm foundation for the
semantic web, or any application of data on the web.)

###  Grounding of words in English

(Distracton: Is there a set of english words in the OED which, if understood,
allow one to understand any definition by sufficient recursive dereferencing?)

###  References:

DNS mess: Weaving the Web p126, etc.

[ Carpenter, Brian, et. al , "IAB Technical Comment on the Unique DNS Root",
IETF-announce, 1999/9/27.](http://www.ietf.org/mail-archive/ietf-
announce/msg05299.html)

##  Fodder

[@@ Dan's quote (Ted N?) about all things being hopelesly? intertwigled@@ :-)
.. maybe some Bhuddist quotation about interconnectedness...]

"I'm very glad you asked me that, Mrs Rawlinson. The term `holistic' refers to
my conviction that what we are concerned with here is the fundamental
interconnectedness of all things. I do not concern myself with such petty
things as fingerprint powder, telltale pieces of pocket fluff and inane
footprints. I see the solution to each problem as being detectable in the
pattern and web of the whole. The connections between causes and effects are
often much more subtle and complex than we with our rough and ready
understanding of the physical world might naturally suppose, Mrs Rawlinson.
Let me give you an example. If you go to an acupuncturist with toothache he
sticks a needle instead into your thigh. Do you know why he does that, Mrs
Rawlinson? No, neither do I, Mrs Rawlinson, but we intend to find out. A
pleasure talking to you, Mrs Rawlinson. Goodbye." -- Douglas Adams, _Dirk
Gentley's Holistic Detective Agency

[quoted in Fork](http://www.xent.com/nov99/0596.html)

@@ Statistiscs from OED

[Mark Bernstein, "Everything is
intertwingled"](http://www.eastgate.com/ht99/slides/Welcome.htm).Opening
Keynote, Hypertext '99, Darmstadt, Germany. February 23, 1999.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

