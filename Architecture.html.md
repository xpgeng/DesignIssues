  
Status: An attempt to give a high-level overview of the architecture of the
WWW. This been presented to and discussed at the IWWW conferences, the W3C
chairs forum and the W3C Advisory Committee. Editing status: Being updated for
October 1999. More verbose in new areas. Comments welcome

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

* * *

#  Web Architecture from 50,000 feet

This document attempts to be a high-level view of the architecture of the
World Wide Web. It is not a definitive complete explanation, but it tries to
enumerate the architectural decisions which have been made, show how they are
related, and give references to more detailed material for those interested.
Necessarily, from 50,000 feet, large things seem to get a small mention. It is
architecture, then, in the sense of how things hopefully will fit together. I
have resisted the urge, and requests, to try to write an architecture for a
long time: This was from a feeling that a dead and therefore less valuable
document must any attempt to select which, of all the living ideas, seem most
stable, logically connected and essential. So we should recognize that while
it might be slowly changing, this is also a living document.

The document is written for those who are technically aware or intend soon to
be, so it sparse on explanation and heavy in terms of terms.

###  Goal

The W3C Consortium's broadly stated mission is to lead the Web to its "full
potential", whatever that means. My definition of the Web is a universe of
network-accessible information, and I break the "full potential" into two by
looking at it first as a means of human-to-human communication, and then as a
space in which software agents can, though access to a vast amount of
everything which is society, science and its problems, become tools to work
with us.

_(See keynote speeches such as "[Hopes for the
future](https://www.w3.org/Talks/1998/0227-WebFuture/slide1-1.htm)" at the Quebec Internet
Forum, and have written up in outline for example in short essay "[Realizing
the full potential of the Web](https://www.w3.org/1998/02/Potential.html)")_

In this overview first I will deal with the properties of the space itself,
and then look it is use as a human medium and then as a medium for machine
reasoning.

This article assumes that the goals of interoperability, and creating an
evolvable technology, are taken for granted and assumed throughout. The
principles of universality of access irrespective of hardware or software
platform, network infrastructure, language, culture, geographical location, or
physical or mental impairment are core values in Web design: they so permeate
the work described that they cannot be mentioned in any one place by will
likewise be assumed throughout. _(See [Internationalization
Activity](https://www.w3.org/International) and the [Web Accessibility
Initiative](https://www.w3.org/WAI/Overview.html))_

###  Principles of Design

Similarly, we assume throughout the design process certain general notions of
what makes good design. Principles such as
**[simplicity](https://www.w3.org/DesignIssues/Principles.html#KISS)** and
**[modularity](https://www.w3.org/DesignIssues/Principles.html#Modular)** are the stuff of software
engineering; **[decentralization](https://www.w3.org/DesignIssues/Principles.html#Decentrali)** and
**[tolerance](https://www.w3.org/DesignIssues/Principles.html#Tolerance)** are the life and breath of
Internet. To these we might add the principles of **[least
powerful](https://www.w3.org/DesignIssues/Evolution.html#Least)** language, and the [**test of independent
invention**](https://www.w3.org/DesignIssues/Evolution.html#ToII) when considering evolvable Web technology. I
do not not elaborate on these here (but see [Principles](https://www.w3.org/DesignIssues/Principles.html)).

###  The fundamentals: The Universal Web

The most fundamental specification of Web architecture, while one of the
simpler, is that of the Universal Resource Identifier, or URI. The principle
that anything, absolutely anything, "on the Web" should identified distinctly
by an otherwise opaque string of characters (A URI and possibly a fragment
identifier) is core to the universality.

Great multiplicative power of reuse derives from the facts that all languages
use URIs as identifiers: This allows things written in one language to refer
to things defined in another language. The use of URIs allows a language
leverage the many forms of persistence, identity and various forms of
equivalence. Each language simply refers to the URI spec - this is a
flexibility point allowing the properties of naming and addressing schemes to
be defined separately.

_(See the [URI specification](http://www.ietf.org/rfc/rfc2396.txt); Footnote;
[Myths of Naming and addressing](https://www.w3.org/DesignIssues/NameMyth.html))_

There are many design decisions about the properties of URIs which are
fundamental in that they determine the properties of the Web, but which I will
not go into here. They include the rules for the parsing and use of relative
URI syntax, the relationship of view identifiers (fragment ids) to URIs. It is
important that these are respected in the design of new URI schemes.

_(See the first few [Design Issues](https://www.w3.org/DesignIssues/Overview.html) articles for detailed
discussions of these)_

###  URI schemes

The Web is by design and philosophy a decentralized system, and its
vulnerabilities lie wherever a central facility exists. The URI specification
raises one such general vulnerability, in that the introduction of new URI
scheme is a potential disaster, immediately breaking interoperability.

Guidelines for new Web developments are that they should respect the generic
definition and syntax of URIs, not introduce new URI schemes without due
cause, not introduce any different scheme which puts itself forward as to be
universal as a superset of URIs which would effectively require information
apart from a URI to be used as a reference. Also, in new developments, all
significant objects with any form of persistent identity should be "first
class objects" for which a URI exists. New systems should use URIs where a
reference exists, without making constraint on the scheme (old or new) which
is chosen.

The principle of minimalist design requires that the URI super-space itself
makes the minimum constraint upon any particular URI scheme space in terms of
properties such as identity, persistence and dereferencability. In fact, the
distinction between names and addresses blurs and becomes dangerously
confusing in this context. (See Name myths). To discuss the architecture of
that part of the Web which is served using HTTP we have to become more
specific.

  * _A URI activity is proposed [Oct 99, member only]_

###  Specific schemes

A few spaces are worthy of note which in which identity is fairly well
defined, but have no defined dereferencing protocol: the message identifier
(mid) and content identifier (cid) spaces adopted from the MIME world, the
md5: hash code with verifiable pure identity, and the pseudo-random
Universally Unique Identifier (uuid) from the Apollo domain system and
followers. These may be underused as URIs.

It is also worth pointing out the usefulness of URIs which define
communication endpoints which do have a persistent identity even for
connection-oriented technologies for which there is no other addressable
content. An example is the "mailto" scheme which should perhaps have been
called "mailbox". This object is the most fundamental and very widely used
object in the email world. It represents conceptually a mailbox - something
you can mail to. It is a mistake to take the URI as a verb: a URI is a noun.
Typical browsers represent a "mailto:" URI as a window for sending a new
message to the address, but opening an address book entry and a list of
messages previous received from or sent to that mailbox would also be a useful
representation.

There is an open question as to what the process should be for formulating new
URI schemes, but it is clear that to allow unfettered proliferation would be a
serious mistake. In almost all other areas, proliferation of new designs is
welcomed and the Web can be used as a distributed registry of them, but not
for the case of URI schemes.

It is reasonable to consider URI spaces which are designed to have greater
persistence than most URIs have today, but not technical solutions with no
social foundation.

##  The HTTP space

The most well-known URI space is the HTTP space, characterized by a flexible
notion of identity _(See Generic URIs)_, and a richness of information about
and relating resources, and a dereferencing algorithm which currently is
defined for reference by the HTTP 1.1 wire protocol. In practice, caching,
proxying and mirroring schemes augment HTTP and so dereferencing may take
place even without HTTP being invoked directly at all.

_(See the HTTP 1.1 protocol specification.)_

The HTTP space consists of two parts, one hierarchically delegated, for which
the Domain Name System is used, and the second an opaque string whose
significance is locally defined by the authority owning the domain name.

_(See the DNS specification)_

The Achilles' heel of the HTTP space is the only centralized part, the
ownership and government of the root of the DNS tree. As a feature common and
mandatory to the entire HTTP Web, the DNS root is a critical resource whose
governance by and for the world as a whole in a fair way is essential. This
concern is not currently addressed by the W3C, except indirectly though
involvement with ICANN.

The question of improving the persistence of URIs in the HTTP space involves
issues of tool maturity, user education, and maturity of the Web society. The
changing of URIs ("moving" of resources) is strongly discouraged.

  * [See: Cool URIs don't change](https://www.w3.org/DesignIssues//Provider/Style/URI)

Research work elsewhere has included many "naming" schemes variously similar
or dissimilar to HTTP, the phrase "URN" bring used either for any such or one
such scheme. The existence of such projects should not be taken, to indicate
that persistence of HTTP URIs should not also be pursued, or that URIs in
general should be partitioned into "names" and "addresses". It is extremely
important that if a new space is created, that it be available as a sub-space
of the universal URI space, so that the universality of the Web is preserved,
and so that the power of the new space been usable for all resources.

One can expect HTTP to mature to provide alternate more modern standard ways
of dereferencing HTTP addresses, whilst keeping the same (hierarchy plus
opaque string) address space.

###  State distribution protocols

Currently on the Internet, HTTP if used for Web pages, SMTP for email
messages, and NNTP for network news. The curious thing about this is that the
objects transferred are basically all MIME objects, and that the choice of
protocol is an optimization made by the user often erroneously. An ideal
situation is one in which the "system" (machines, networks and software)
decides adaptively which sorts of protocols to use to efficiently distribute
information, dynamically as a function of readership. This question of an
efficient flexible protocol blending fetching on demand to preemptive
transmission is currently seen as too much of a research are for W3C
involvement.

##  Content and Remote Operations

The URI specification effectively defines a space, that is a mapping between
identifiers (URIs) and resources. This is all in theory which is needed to
define the space, but in order to make the content of the space available, the
operation of dereferencing an identifier is a fundamental necessity. In HTTP
this is the "GET" operation. In the Web architecture, GET therefore has a
special status. It is not allowed to have side effects (and it is idempotent)
and HTTP has many mechanisms for refining concepts of idempotency and
identity. While other remote operations on resources (objects) in the Web are
quite valid, and some are indeed included in HTTP, the properties of GET are
an important principle. The use of GET for any operation which has side-
effects (such as unsubscribing from a mailing list, filling a shopping cart,
etc) is incorrect.

The introduction of any other method apart from GET which has no side-effects
and is simply a function of the URI is also incorrect, because the results of
such an operation effectively form a separate address space, which violates
the universality. A pragmatic symptom would be that hypertext links would have
to contain the method as well as the URI in order to able to address the new
space, which people would soon want to do.

_(Example: Instead of defining a new method CVSSTAT to retrieve the code
management status of a document, that status should be given a URI in the
server's space, and headers used to point the aware client to it. Otherwise,
we end up with a class of document which contains interesting information but
cannot be linked to.)_

The extension of HTTP to include an adaptive system for the proactive
distribution of information as a function of real or anticipated need, and for
the location of close copies, is a natural optimization of the current muddle
of push and pull protocols (SMTP, NNTP, HTTP, and HTTP augmented by "channel"
techniques). This is an area in which the answers are not trivial and research
is quite appropriate. However, it is in the interests of everything which will
be built on the Web to make the form of distribution protocols invisible
wherever possible.

HTTP in fact combines a basic transport protocol with formats for a limited
varieties of "metadata", information about the payload of information. This is
a historical inheritance from the SMTP world and as an architectural feature
which should be replaced by a [clearer
distinction](https://www.w3.org/DesignIssues/Metadata.html#MetadataHeaders) between the basic HTTP
functionality and a dramatically richer world of [metadata](https://www.w3.org/DesignIssues/Metadata.html).

_(See [old propagation activity statement](https://www.w3.org/Propagation/Overview.html))_

###  Remote Operations: Web Services

HTTP was originally designed as a protocol for remote operations on objects,
with a flexible set of methods. The situation in which distributed object
oriented systems such as CORBA, DCOM and RMI exist with distinct functionality
and distinct from the Web address space causes a certain tension, counter to
the concept of a single space. The HTTP-NG activity investigated many aspects
of the future development of NG, including a possible unification of the world
of Remote procedure Call (RPC) with existing Web protocols. The study ended
but has not generated the momentum for further work, but the use of XML for
inter-company remote operations becaome prevalent (2001) and became known as
Web Services. See the W3C Web Serices activity.

Both HTTP and XML have come upon the problem of extensibility. The XML/RDF
model for extensibility is general enough for what RPC needs, in my opinion,
and I note that an RPC message is a special case of a structured document. To
take the whole RPC system and represent it in the RDF model would be quite
reasonable. Of course, a binary format (even if just compression) for XML
would be required for efficient transmission. But the evolvability
characteristics of RDF are just what RPC needs.

Web Services differe from previous remote operation work in that the
transactions are less frequent, and slower, and between non-trusted parties.
Such things as proof of delivery become important . while techniques such as
storeing messaegs for years can becoem part of a protocol. The Web Services
Architecture Group was chatered to define the interrelationships betwwn the
required functionality such as Pckaging, Security, Reliability, QoS and so on
discussed as Web Services requirements at the 3C WS wokshop.

###  Level breaking: Messages and Documents.

There has been to date an artificial distinction between the transmission
standards for "protocols"and "content". In the ever continuing quest for
generalization and simplification, this is a distinction which cannot last.
Therefore, new protocols should be defined in terms of the exchange of
messages, where messages are XML, and indeed, RDF documents.

The distinction has been partly historical, and partly useful, in that, with
protocols defined on top of "messages", and defined in order to transport
"documents" (or whatever vocabulary), the confusing but illuminating recursion
of protocols being defined in terms of messages exchanged by protocols defined
in terms of other messages and so on.

In fact this recursion happens all the time and is important. Email messages
contain email messages. Business protocols are enacted using documents which
are put on the web or sent by SMTP or HTTP using internet messages. The
observation that these are in fact the same (historically this almost lead to
HTTP messages being defined in SGML) leads to a need for generalization and a
gain from the multiplicative power for combining the ideas. For example,
regarding documents and messages as identical gives you the ability to sign
messages, where you could only sign documents, and to binary encode documents,
where you could only binary encode messages, and so on. What was level
breaking becomes an architectural reorganization and generalization.

The ideal goals, then, for an evolution of HTTP - would include:

  * A protocol for allowing many concurrent message exchanges; 
  * A data typing and marshalling standard for objects as general and as extensible as XML documents with namespaces; 
  * A schema system which allows any (Corba, DCom, RMI, etc) RPC interface to be defined, with an implied standard efficient format for RPC transmission; 
  * Extensions to the RPC state transition protocols to allow asynchrony needed for web applications (bidirectionality, streaming, asynchronous calls...); 
  * An implementation of a sophisticated socially aware state propagation (Web) protocol on top of the new RPC functionality, but in a modular way making use of the the extensibility to allow a much simpler basic design than HTTP 1.1. 

_(See the old HTTP-NG activity statement, the [HTTP-NG architecture
note](https://www.w3.org/TR/WD-HTTP-NG-architecture/Overview.html))_

Where new protocols address ground which is covered by HTTP-NG, awareness and
lack of duplication is obviously desirable.

###  Extension of access protocols

The ubiquity of HTTP, while not a design feature of the Web, which could exist
with several schemes in concurrence, has proved a great boon. This sunny
situation is clouded a little by the existence of the "https" space which
implied the use of HTTP through a Secure Socket Layer (SSL) tunnel. By making
this distinction evident in the URI, users have to be aware of the secure and
insecure forms of a document as separate things, rather than this being a case
of negotiation in the process of dereferencing the same document. Whilst the
community can suffer the occasional surfacing of a that which should be
hidden, it is not desirable as a precedent, as many other dimensions of
negotiation (including language, privacy level, etc) for which proliferation
of access schemes is inappropriate.

Work at W3C on extension schemes for protocols has been undertaken for a long
time and while not adopted in a wide-scale way in HTTP 1.1, currently takes
the form of the Mandatory specification. Many features such as PICS or RTSP
could have benefitted from this had it been defined in early HTTP versions.

_(See the Mandatory Specification)_

Extension of future protocols such as HTTP-NG is clearly an important issue,
but hopefully the experience from the extensibility of data formats will
provide tools powerful enough to be picked up directly and used by the HTTP-NG
community in due course.

Specifications for protocols or data formats must allow for and distinguish
mandatory and optional extensions. A generic facility for doing this in XML is
clearly called for.

##  Data Formats

###  Format Negotiation

When the URI architecture is defined, and when one has the use of at least one
dereferencable protocol, then all one needs for an interoperable global
hypertext system is at least one common format for the content of a resource,
or Web object.

The initial design of the Web assumed that there would continue to be a wild
proliferation of proprietary data formats, and so HTTP was designed to have a
feature of negotiation common formats between client and server. Historically
this was not used due to, on the one hand, the proliferation of HTML as a
common format, and, on the other hand, the size of the known formats list
which a typical client had to send with each transaction.

As an architectural feature, this is still desirable. The Web is currently
full of user awareness of data formats, and explicit user selection of data
formats, which complicates it and hides the essential nature of the
information.

The discussion of data formats should be seen in this light.

  * See: The CC/PP protocol in development 

###  MIME types

In HTTP, the format of data is defined by a "MIME type". This formally refers
to a central registry kept by IANA. However, architecturally this is an
unnecessary central point of control, and there is no reason why the Web
itself should not be used as a repository for new types. Indeed, a transition
plan, in which unqualified MIME types are taken as relative URIs within a
standard reference URI in an online MIME registry, would allow migration of
MIME types to become first class objects.

The adoption by the community of a tested common recommended data format would
then be a question not of (central) registry but of (possibly subjective)
endorsement.

Currently the Web architecture requires the syntax and semantics of the URI
fragment identifier (the bit after the "#") to be a function of MIME type.
This requires it to be defined with every MIME registration. This poses an
unsolved problem when combined with format negotiation.

###  Common Syntax for Structured documents: XML

While HTML was, partly for political reasons, based upon the generic SGML
language, the community has been quite aware that while sharing a common
syntax for structured documents was a good idea, something simpler was
required. XML was the result.

_(See the [XML Activity Statement](https://www.w3.org/DesignIssues//XML/Activity.html))_

While in principle anyone is free to use any syntax in a new language, the
evident advantages from sharing the syntax are so great that new languages
should where it is not overly damaging in other ways be written in XML. Apart
from the efficiency of sharing tools, parsers, and understanding, this also
leverages the work which has been put in to XML in the way of
internationalization, and extensibility.

###  Namespaces

The extensibility in XML is essential in order to crack a well-known tension
in the software world between free but undefined extension and well-defined
but awkward extension in the RPC world. An examination of the needs for
evolution of technology in a distributed community of developers shoes that
the language must have certain features:

  * It must be possible to precisely define a language (the set of tokens, grammar, and semantics) as a first class object; 
  * It must be possible to make documents in a mixture of languages (language mixing) 
  * Every document should be self-defining by carrying the URI(s) of the language(s) in which it is written; 
  * It must be possible to process a document understanding a subset of the languages (partial understanding). 

_(See [Evolvability Talk](https://www.w3.org/Talks/1998/0415-Evolvability/slide1-1.htm) at
WWW7, and design issues:_ [Evolvability](https://www.w3.org/DesignIssues/Evolution.html))  
(See Note "[Web architecture: extensible languages](https://www.w3.org/TR/NOTE-webarch-
extlang.html), )

These needs lie behind the evolution of data formats whether of essentially
human-targeted or of machine-understandable (semantic) data.

When a new language is defined, XML should in general be used. When it is, the
new language, or the new features extending an existing language, must be
defined as a new namespace. (That is, new non-XML syntaxes, processing
instructions, or tunnelling of functionality within other XML entities etc is
inappropriate). A namespace URI must be used to identify the language. XML
should be considered to include XML 1.0 and Namespaces.

The XML and RDF schema languages are mature now (2002). New namespaces must be
designed assuming the use of schemas, and not relying on DTD functionality.
Where the functionality being introduced maps onto a logical assertion model,
then the mapping onto the RDF model below should be defined, and, normally,
RDF used. An alternative is to define an XML schema and a mapping algorithm
from an XML document using the namespace to RDF.

Language specifications should define the ways in which they can be extended.
This typically involves defining types of element which subtypes can be
created in future languages. The structural constraints of the original
language will then define how the new language may syntactically be mixed with
the old, and the semantics of the old specification will define how the new
elements should be interpreted at the semantic level of that specification.
(Note typically in an object-oriented support class, this will require classes
supporting the new elements to support the same API as the superclass in the
original language). Future work in this area is required to clarify this and
how it is expressed in the schema language.

New languages (namespaces) may, in summary, be introduced in two ways.
Firstly, as a completely new application (such as a downloaded bank transfer),
allowing interoperability where previously formats were proprietary and
indecipherable. Secondly, as an extension to an existing application such as
HTML or RDF. In the latter case languages such as style sheets for human
readable documents and inference rules for logical documents will define the
interpretation of the new language at a given semantic level.

The namespace document (with the namespace URI) is a place for the language
publisher to keep definitive material about a namespace. Schema languages were
the first languages available for this, but could only give syntactic
constraints. More generally, one would expect a more powerful language to
allow all kinds of information to be provided, either inline (like RDF) or by
reference (like RDDL or RDF). There is a huge a mount of value to be gained
from having a document be self-describing in the Web. (This does not preclude
the operation of checking a document against a different schema if one wants
to as a local operation). The first stage in self-describing documents is to
do it at the XML schema (structure) level. Successive stages are to give
semantic information. [See grounded documents]

Languages, like resources may be living or frozen. Making the language a
living language is in my opinion dangerous and asking for HTML-like
divergence. Even when a language is frozen, the namespace document may change
as new languages become available to express different forms of semantics
about the language. The namespace document may for example include or link to:

  * Syntactic constraints (e.g. in xml-schema) 
  * Range and domain of properties (e.g. in rdf-schema) 
  * Default or mandatory style sheet for display of the language to a person (e.g. in CSS or XSL) 
  * and so on... 

A namespace document clearly may have a mixture of languages.

##  Human Readable Information

By **human readable** information I mean documents in the traditional sense
which are intended for human consumption. While these may be transformed,
rendered, analyzed and indexed by machine, the idea of them being _understood_
is an artificial-intelligence complete problem which I do not address as part
of the Web architecture. When I talk about **machine-understandable**
documents, therefore, I mean data which has explicitly been prepared for
machine reasoning: part of a semantic web. (The use of the term "semantics" by
the SGML community to distinguish content from form is unfortunately confusing
and not here).

###  Separation of Form and Content

An architectural rule which the SGML community embraced is the separation of
form and content. It is an essential part of Web architecture, making possible
the independence of device mentioned above, and greatly aiding the processing
and analysis. The addition of presentation information to HTML when it could
be put into a style sheet breaks this rule. The rule applies to many
specifications apart from HTML: in the Math Markup Language (MathML) two
levels of the language exist, one having some connection with mathematical
meaning, and the other simply indicating physical layout.

###  Graphics

The development of different languages for human readable documents can be
relatively independent. So 2D graphic languages such as PNG and SVG are
developed essentially independently of 3D languages such as VRML (handled not
by W3C but by the VRMLC, now Web3D) and text languages such as HTML and
MathML. Coordination is needed when aspects of style, fonts, color and
internationalization are considered, where there should be a single common
model for all languages.

PNG was introduced as a compact encoding which improved on GIF both
technically (color, flexibility and transparency) and politically (lack of
encumbrance). [SVG](https://www.w3.org/DesignIssues//Graphics/SVG/) is required as a common format in response
to the large number of suggestions for an object oriented drawing XML
language.

###  HTML

The value of a common document language has been so enormous that HTML has
gained a dominance on the Web, but it does not play a fundamental key role.
Web applications are required to be able to process HTML, as it is the
connective tissue of the Web, but it has no special place architecturally.

HTML has benefitted and suffered from the "ignore what you don't understand"
rule of free extension. In future, the plan is to migrate HTML from being an
SGML application to being defined as an XML namespace, making future extension
a controlled matter of namespace definition. The first step is a specification
for documents with precisely HTML 4.0 features but which are XML documents.

_(See [W3C Data Formats](https://www.w3.org/TR/NOTE-rdfarch.html) note)_

###  XHTML transition

The transition strategy from HTML as it is practiced today to HTML based on
XML in the future is difficult. It is driven by many constraints:

  1. Currently many web pages are badly formed and do not adhere to the HTML 4.0 standard, nor to SGML; 
  2. Browsers must for a long time be able to read these legacy web pages. 
  3. Many browsers exist which cannot parse XML; 
  4. There is a way, "XHTML" to write a well-formed XML document so that it appears to a typical legacy browser to be HTML and it is parsed correctly; 
  5. One can tell the difference between an old HTML document and an XML document by the namespace declaration; 

The transition strategy is to start using XML internally within a site, and
for internal documents, while formating web pages as XHTML. This will allow
web sites to use as many XML tools, encouraging the market for XML tools.

The second phase is for web sites to convert HTML pages to XHTML pages. An
incentive to do this will be to be able to use XML tools directly on the site
(for reading: a special converter will be needed to write XHTML pages).This
will create a base of well-formed XML pages, which hopefully will encouraging
the inclusion of XML parsing in browsers and search engines. During the
transition phase, any XML-capable browser finding an XML document must assume
that it is well-formed XML with namespaces. The community must be careful to
condemn any lax interpretation of the XML specification, such as nominally
XHTML pages which are not well-formed XML and exactly the XHTML namespace.
Anything which is not XML may be fed by a browser to a legacy HTML engine.
Legacy HTML pages will of course **not** be extendable using other namespaces.
XHTML pages will be extensible bearing in mind that legacy browsers will
ignore any tag they don't recognize. Hopefully the transition will be eased by
the availability of open source code which will take a typical old HTML page
and convert it (with zero loss in most cases) into a completely valid XHTML
page. This will allow all new tools to be built simply to accept XML, and
therefore be ready as the use of XML spreads.

Eventually, the weight of sites which need to use other languages, or other
XML features such as Unicode, will hopefully cause a general upgrade until all
the vast majority of Web clients are capable of handling XML with namespaces,
and sites will be able to insist on it from their readers. At this point, a
web service of translation of legacy pages would be one solution for general
access to the archive of historical badly-formed documents.

_Note: This transition strategy has been the cause of much debate, as some
favor a complete switch from HTML to XML without compatability._

###  Hypertext Link topology

A fundamental compromise which allows the Web to scale (but created the
dangling link problem) was the architectural decision that links should be
fundamentally mono-directional. Links initially had three parameters: the
source (implicit when in the source document), destination and type. The third
parameter, intended to add semantics, has not been heavily used, but XLINK
activity has as one goal to reintroduce this to add richness especially to
large sets of Web pages. Note however that the Resource Description Framework
, introduced below, is a model (based on an equivalent 3-component assertion
onto which a link maps directly), and so link relationships, like any other
relation in future Web architecture, must be expressible in RDF. In this way,
link relationships in HTML, and in future XML hypertext languages, should
migrate to becoming first class objects.

XLINK will also define more sophisticated link topologies, and address the
human interface questions related to them, still using the same URI space and
using RDF as the defining language for relationship specification. (It may be
appropriate for information based on the RDF model to be actually transferred
in a different syntax for some reason,. but the specification must define the
mapping, so that common processing engines can be used to process combinations
of such information with other information in the RDF model.)

###  Style Sheets

The principle of modular design implies that when form and content are
separated the choice of languages for each, if possible, be made an
independent choice. HTML has dominated the text markup (content) language, but
the introduction of XML opened the door for the use of new XML markup
languages between parties which share them. (See the
[Style](https://www.w3.org/Style/Overview.html) activity at W3C).

Style essentially is the mapping between the abstract content of a document
and the physical form in which it is displayed, spoken, performed or in
general presented, to its recipient.

For graphic style, Cascading Style Sheets ([CSS](https://www.w3.org/DesignIssues//Style/CSS/)) provide a way
of declaring the form in which elements of a document should be presented. It
has the advantage of being declarative and so reversible: one can make an
editor which edits a document with the style sheet applied to it.
[XSL](https://www.w3.org/DesignIssues//Style/XSL/)T, by contrast, is a transformation language which can make
an arbitrarily complex mapping from input to output structure. This allows
more powerful processing, but is not in general reversible. For graphic
presentation, XSLT can be used to map to a set of Formating Objects (XSL-FO)
whose formatting properties are to be a superset of those of CSS.

The fact that CSS is not an XML language is largely historical, as it
preceeded XML: A namespace of CSS formatting properties to allow CSS to be
added intuitively to any XML document would be a natural development, but may
be make unnecessary by XSL-FO.

###  Collaboration

The original idea of the Web being a creative space for people to work
together in ("intercreative") seems to be making very slow progress

_[See W3C Collaboration Workshop](https://www.w3.org/Collaboration/Workshop/Overview.html)_

This field is very broad and can be divided into areas:

  1. Asynchronous collaboration tools 
    * Discussion forums 
    * Workflow automata 
    * Annotation systems (see Annotea) 
    * Endorsement (see PICS) 
    * Collaborative filtering 
  2. Integration of real-time audio video collaboration and the Web (, integration of video in HTML, co-presence) 
    * addressing for video - callto: etc 
    * integration of video in HTML (SMIL etc) 
    * Co-presence systems 
  3. Group editors (synchronous hypertext editors, whiteboards etc) 
  4. Asynchronous distributed editing. (Amaya, Jigsaw, Jigedit, WebDAV) 

A precursor to much collaborative work is the establishment of an environment
with sufficient confidentiality to allow trust among its members. Therefore
the Consortium's work on a semantic web of trust addressed below may be a
gating factor for much of the above.

Many of the above areas are research areas, and some are areas in which
products exist. It is not clear that there is a demand among w3C members to
address common specifications in this area right now but suggestions are
welcome.. The Consortium tries to use whatever web-based collaborative
techniques are available, including distributed editing of documents in the
web, and automatic change tracking. The Live early Adoption and Demonstration
(LEAD) philosophy of W3C was introduced specifically for areas like this where
many small pieces need to be put together to make it happen, but one will
never know how large any remaining problems are until one tries. Still,
largely, this section in the architecture is left as a place-holder for later
expansion. It may not be the time yet, but collaborative tools are a
requirement for the Web and the work is not done until a framework for them
exists.

##  Machine-Understandable information: Semantic Web

The Semantic Web is a web of data, in some ways like a global database. The
rationale for creating an infrastructure is given elsewhere [Web future talks
etc] here I only outline the architecture as I see it.

See:

  * [The Semantic Web Roadmap](https://www.w3.org/DesignIssues/Semantic.html) in Design Issues 
  * [The RDF home page](https://www.w3.org/RDF/Overview.html)
  * [RDF Model and Syntax Specification](https://www.w3.org/TR/WD-rdf-syntax/)

When looking at a possible formulation of a universal Web of semantic
assertions, the principle of minimalist design requires that it be based on a
common model of great generality. Only when the common model is general can
any prospective application be mapped onto the model. The general model is the
[Resource Description Framework](https://www.w3.org/RDF/Overview.html).

###  Semantic Web: the pieces.

The architecture of RDF and the semantic web build on it is a plan but not yet
all a reality. There are various pieces of the puzzle which seem to fall into
a chronological order, although the turn of events may change that. (Links
below are into the [Semantic Web roadmap](https://www.w3.org/DesignIssues/Semantic.html#Signature))

  1. XML provides a basic format for structured documents, with no particular semantics. 
  2. The [basic assertion model](https://www.w3.org/DesignIssues/Semantic.html#Assertion) provides the concepts of assertion (property) and quotation. (This is provided by the [RDF Model and Syntax Specification](https://www.w3.org/TR/WD-rdf-syntax/)). This allows an entity-relationship-like model to be made for the data, giving it the semantics of assertions propositional logic. See the [Cambridge Communique](https://www.w3.org/DesignIssues//TR/1999/NOTE-schema-arch-19991007) about the XML-RDF relationship) The RDF syntax was considered in need of a change. 
  3. The [schema language](https://www.w3.org/DesignIssues/Semantic.html#Schema) provides data typing and allows document structure to be constrained to allow predictable computable processing. XML schema's datatypes are used. 
  4. The Ontology layer (WebOnt working group) provides more powerful schema concepts, such as inverse, transitivity, and so on. Uniqueness and/or unambiguousness of properties, when know, allow a system to spot different identifiers which in fact are talking about the same thing. 
  5. A [conversion language](https://www.w3.org/DesignIssues/Semantic.html#Conversion) allows the expression of inference rules allowing information in one schema to be inferred from a document in another. This is part of rules layer. 
  6. An [evolution rules language](https://www.w3.org/DesignIssues/Semantic.html#Inference) allows inference rules to be given which allow a machine with a certain algorithm to do convert documents from one RDF schema into another. This is a fundamental key to [evolution](https://www.w3.org/DesignIssues/Evolution.html) of the technology. There may be more than one rules standard, as different class of rule-based system have different capabilities. 

[Query languages](https://www.w3.org/DesignIssues/Semantic.html#Query) assume different forms of query engine,
but are basically the same problem space as rule systems. (The antecedent of a
rule is a query).. One can imagine standardizing both certain query engines
and a language for defining query engines. See the RDF Interest Group for
discussion of querying logically.

  7. The [logical layer](https://www.w3.org/DesignIssues/Semantic.html#Logical) turns a limited declarative language into a Turing-complete logical language, with inference and functions. This is powerful enough to be able to define all the rest, and allow any two RDF applications to be connected together. However, without being profiled for use, it does not address specific applications. One can see this language as being a universal language to unify all data systems just as HTML was a language to unify all human documentation systems. 
  8. A proof language is a form of RDF which allows one agent to send to another an assertion, together with the inference path to that assertion from assumptions acceptable to the receiver. This allows applications such as access control to use a generic validation engine as the kernel, with very case-specific tools for producing proofs of access according to whatever social rules have been devised for the case. A W3C Recommendation for the language and capabilities of a standard proof engine would be very appropriate. Onc could see this engibe as being based on the logic layer, or being based on a less experssive rules layer - esepcially if the logic layer remains a research issue when proofs in terms of rules are practical need for interchange. 

Once one has a proof language, then the introduction of [digital
signature](https://www.w3.org/DesignIssues/Semantic.html#Signature) turns what was a web of reason into a web
of trust. The development of digital signature functionality in the RDF world
can in principle happen in parallel with the stages above. As more expressive
logical languages become available, then but it requires that the logical
layer be defined as a basis for defining the new primitives which describe
signature and inference in a world which includes digital signature.

A single digital signature format for XML documents is important. The power of
the RDF logical layers will allow existing certificate schemes to be converted
into RDF, and a trust path to be verified by a generic RDF engine.

##  Metadata applications

The driver for the semantic web at level 1 above is information about
information, normally known as metadata. The following areas are examples of
technologies which should use RDF, and which are or we expect to be developed
within the W3C.

  * Information practice labels ([P3 Project](https://www.w3.org/P3P/Overview.html)) 
  * [Synchronized MultiMedia](https://www.w3.org/AudioVideo/Overview.html) (SMIL) 
  * Intellectual Property Rights - Distribution Rights languages 
  * [Micropayment](https://www.w3.org/ECommerce/Micropayments/Overview.html)s (link labeled as "must pay to follow") 
  * Digital Libraries: Catalog: (e.g. [Dublin Core](http://purl.oclc.org/metadata/dublin_core/)) 

This is by no means an exclusive list. Any technology which involves
information about web resources should express it according to the RDF model
The plan is that HTML LINK relationships be transitioned into RDF properties.
We can continue the examples for which RDF is clearly appropriate.

  * Version control information 
  * Relationships between [generic](https://www.w3.org/DesignIssues/Generic.html) and specific URIs 
  * Access control information 
  * Structural information in complex works of many component resources 
  * Relationships between a document and its style sheet 

###  Indexes of terms

Given a worldwide semantic web of assertions, the search engine technology
currently (1998) applied to HTML pages will presumably translate directly into
indexes not of words, but of RDF objects. This itself will allow much more
efficient searching of the Web as though it were one giant database, rather
than one giant book.

The Version A to Version B translation requirement has now been met, and so
when two databases exist as for example large arrays of (probably virtual) RDF
files, then even though the initial schemas may not have been the same, a
retrospective documentation of their equivalence would allow a search engine
to satisfy queries by searching across both databases.

###  Engines of the Future

While search engines which index HTML pages find many answers to searches and
cover a huge part of the Web, then return many inappropriate answers. There is
no notion of "correctness" to such searches. By contrast, logical engines have
typically been able to restrict their output to that which is provably correct
answer, but have suffered from the inability to rummage through the mass of
intertwined data to construct valid answers. The combinatorial explosion of
possibilities to be traced has been quite intractable. However, the scale upon
which search engines have been successful may force us to reexamine our
assumptions here. If an engine of the future combines a reasoning engine with
a search engine, it may be able to get the best of both worlds, and actually
be able to construct proofs in a certain number of cases of very real impact.
It will be able to reach out to indexes which contain very complete lists of
all occurrences of a given term, and then use logic to weed out all but those
which can be of use in solving the given problem. So while nothing will make
the combinatorial explosion go away, many real life problems can be solved
using just a few (say two) steps of inference out on the wild web, the rest of
the reasoning being in a realm in which proofs are give, or there are
constrains and well understood computable algorithms. I also expect a string
commercial incentive to develop engines and algorithms which will efficiently
tackle specific types of problem. This may involve making caches of
intermediate results much analogous to the search engines' indexes of today.

Though there will still not be a machine which can guarantee to answer
arbitrary questions, the power to answer real questions which are the stuff of
our daily lives and especially of commerce may be quite remarkable.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html);

####  Footnote: Universal or Uniform?

Historically, the original term the author used was _Universal Document
Identifier_ in the WWW documentation. In discussions in the IETF, there was a
view expressed by several people that _Universal_ was too strong, in that it
could or should not be a goal to make an identifier which could be applied to
all things. The author disagreed and disagrees with this poisition. However,
in the interest of expediency at the time he bowed to peer pressure and
allowed _Uniform_ to be substituted for _Universal_ in
[RFC2306](http://www.ietf.org/rfc/rfc2396.txt), he has since decided that that
did more harm than good, and he now uses _Universal_ to indicate the
importance to the Web architecture of the single universal information space.

* * *

Tim Berners-Lee  
Created: September 1998.

  
$Id: Architecture.html,v 1.66 2009/08/27 21:38:06 timbl Exp $

