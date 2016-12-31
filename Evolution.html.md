Tim Berners-Lee

Date: March 1998. Last edited: $Date: 2009/08/27 21:38:07 $

Status: . Editing status: incomplete first draft. This explains the rationale
for XML namespaces and RDF schemas, and derives requirement on them from a
discussion of the process by which we arrive at standards.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Commentary

_(These ideas were mentioned in a [keynote on
"Evolvability"](https://www.w3.org/Talks/1998/0415-Evolvability/slide1-1.htm) at WWW7 and this
text follows closely enough for you to give yourself the talk below using
those slides. More or less. If and when we get a video from WWW7 of the talk,
maybe we'll be able to serve that up in parallel.)_

* * *

#  Evolvability

###  Introduction

The World Wide Web Consortium was founded in 1994 on the mandate to lead the
**Evolution** of the Web while maintaining its **Interoperability** as a
universal space. "Interoperability" and "Evolvability" were two goals for all
W3C technology, and whilst there was a good understanding of what the first
meant, it was difficult to define the second in terms of technology.

Since then W3C has had first hand experience of the tension beween these two
goals, and has seen the process by which specifications have been advanced,
fragmented and later reconverged. This has led to a desire for a technological
solution which will allow specifications to evolve with the speed and freedom
of many parallel deevlopments, but also such that any message, whether
"standard" or not, at least has a well defined meaning.

There have been technologies dubbed "futureproof" for years and years, whether
they are languages or backplane busses.  I expect you the reader to share my
cynicism when encountering any such claim.  We must work though exactly what
we mean: what we expect to be able to do which we could not do before, and how
that will make evolution more possible and less painfull.

##  Free extension

A rule explicit or implcit in all the email-like Internet protocols has always
been that if you found a mail header (or something) which you did not
understand, you should ignore it. This obviously allows people to add all
sorts of records to things in a very free way, and so we can call it the rul
of free extension. It has its advatage of rapid prototyping and incremental
deployment, and the disadvantage of ambiguity, confusion, and an inability to
add a mandatory feature to an existing protocol. I adopeted the rule for HTML
when initially designing it - and used it myself all the time, adding elements
one by one. This is one way in which HTML was unlike a conventional SGML
application, but it allowed the dramatic development of HTML.

###  The HTML cycle

The development of HTML between 1994 and 1998 took place in a cycle, fuelled
by the tension between the competitive urge of companies to outdo each other
and the common need for standards for moving forward. The cycle starts simply
simply bcause the HTML standard is open and usable by anyone: this means that
any engineer, in any company or waiting for a bus can think of new ways to
extend HTML, and try them out.

The next phase is that some of these many ideas are tried out in prototypes or
products, using the fact free extension rule that any unrecongined extensiosn
will be ignored by everything which does not understand them. The result is a
drmatic growth in features. Some of these become product differentiators,
during which time their originators are loth to discuss the technology with
the competition. Some features die in the market and diappear from the
products. Those successful features have a fairly short lifetime as product
differetiators, as they are soon emulated in some equivalent (though
different) feature in competeing products.

After this phase of the cycle, there are three or four ways of doing the same
thing, and engineers in each company are forced to spend their time writing
three of four different versions of the same thing, and coping with the
software architectural problems which arise from the mix of different models.
This wastes program size, and confuses users. In the case for example, of the
TABLE tag, a browser meeting one in a document had no idea which table
extension it was, so the situation could become ambiguous. If the
interpretation of the table was important for the safe interpretation ofthe
document, the server would never know whether it had been done, as an unaware
client would blithely ignore it in any case. This internal software mess
resulting from having to implement multiple models also threatens future
deevlopment. It turns the stable consistent base for future development into
something fragmented and inconsistent: it is difficult to design new features
in such an environment.

Now the marketting pressure is off which prevented discussions, and there is a
strong call for the engineers to get around the W3C table, and iron out a
common way of doing things. As this happens, a system is designed which puts
together the best aspects of each other system, plus a few weeks experience,
so everyone is in the end happier with the result. The companies all go away
making public promises to implement it, even though the engineering staff will
be under pressure to add the next feature and startthe next cycle. The result
is published as a common specification opene to anyone to implement. And so
the cycle starts again.

This is not the way all W3C activities have worked, but it was the particular
case with HTML, and it illustrates some of the advantages and disadvantages
with the free extenstion rule.

###  Breaking the cycle

The HTML cycle as a method of arriving at consensus on a document has its
drawbacks. By 1998, there were reasons to change the cycle.The work in the
W3C, which had started off in 1994 with several years backlog of work, had
more or less caught up, and was begining to lead, rather than trail,
developments. The work was seen less as fire fighting and more as
consolitation. By this time the spec was growing to a size where the principle
of modularity was seriously flaunted. Any new developments clearly had to be
seperate modules. Already style information had been moved out into the
Cascading Style Sheets language, the programming interface work was a seperate
Document Object Model activity, and guidelines for accessibility were tackled
by a seperate group.

Inthe future it was clear that we needed somehow to set up a modular system
which would allow one to add to HTML new standard modules. At the same time,
it was clear that with XML available as a manageble version of SGML as a base
for anyone to define their own tag sets, there was likely to be a deluge of
application-specific and industry-specific XML based languages. The idea of
all this happening underthefree extension rule was frightening. Most
applications would simply add new tags to HTML. If we continued the process of
retrospectively roping into a new bigger standard, the document would grow
without limit and become totally unmanageble. The rule of free extesnion was
no longer appropriate.

#  Well defined interfaces

Now let us compare this situation with the way development occus in the world
of distributed computing, specifically remote rpocedure call (RPC) and
distributed object oriented systems. In these systems, the distributed system
(equivalent to the server plus the client for the web) is viewed as a single
software system which happens to be spread over several physical machines.
[nelson - courier, etc]

The network protocols are defined automatically as a function of the software
interfaces which happen to end up being between modules on different machines.
Each interface, local or remote, has a well documented structure, and the list
of functions (procedures, methods or whatever) and parameters are defined in
machine-processable form. As the system is built, the compiler checks that the
interfaces required by one module is exactly provided by another module. The
interface, in each version of its development, typically has an identifying
(typically very long) unique number.

The interface defines the parameters of a remote call, and therefore defines
exactly what can occur in a message from one module to another. There is no
free extension. If the interface is changed, and a new module made, any module
on the other side of the interface will have to be changed too, or you can't
build the system.

The great advantage of this is that when the system has been built, you expect
it to work. There is no wondering wether a table is being displayed - if you
have called the table module, you know exactly what the module is supposed to
do, and there is no way the system could be without that module. Given the
chaos of the HTML devleopment world, you can imagine that many people were
hankering after the well defined interfaces of the distributed computing
technology.

With well-defined interfaces, either everything works, or nothing. This was in
fact at least formally the case with SGML documents. Each had a document type
definition (DTD) refered to at the the top, which defiend in principle exactly
what could and could not be in the document. PICS labels were similar in that
thet are self-describing: they actually have a URI atthe top which points to a
machine-readable description of what can and can't be in athat PICS label.
When you see one of these documents, as when you get an RPC mesaage with an
interface number on it, you can check whether you understand the interface or
not. Another intersting thing you can do, if you don't have a way of
processing it, is to look it up in some index and dynamically download the
code to process it.

The existence of the Web makes all this much smoother: instead of inventing
arbitrary names for inetrfaces, tyou can use a real URI which can be
dereferenecd and return the master definition of the interface in real time.
The Web can become a decentralised registray of interfaces (languages) and
code modules.

The need was clearly for the best of both worlds. One must be able to freely
extend a language, but do so with an extension language which is itself well
defined. If for example, documents which were HTML 2.0 plus Netscape's version
of tables version 2.01 were identified as such, mcuh o the problem of
ambiguity would have been resolved, but the rest ofthe world left free to make
their own table extensions. This was the goal of the namespaces work in XML.

###  Modularity in HTML

To be able to use the namespaces work in the extension of HTML, HTML has to
transition from being an SGML application (with certain constraints) to being
an XML based langauge. This will not only give it a certain ease of parsing,
but allow it to build on the modularity introduced by namespaces.

In fact, already in April of 1998 there was a W3C Recommendation for "MathML",
defined as as XML langauge and obviously aimed at being usable in the context
of an HTML document, but for which there was no defined way to write a
combined HTML+MathML document. MathML was already waiting for XML namespaces.

XML namespaces will allow an author (or authoring tool, hopefully) to declare
exactly waht set of tags he orshe is using in a document. Later, schemas
should allow a browser to decide what to do as a fall back when finding
vocabulary which it does not understand.

It is expected that new extensions to HTML be introduced as namespaces,
possibly languages in their own right. The intent is that the new languages,
where appropriate, will be able to use the existing work on style sheets, such
as CSS, and the existing DOM work which defines a programming interface.

##  Language mixing

Language mixing is an important facility, for HTML, for the evolution of all
other Web and application technology. It must allow, in a mixed labguage
document, for both langauges to be well defined. A mixed langage document is
quiote analogous to a program which makes calls to two runtime libraries, so
it is not rocket science. It is not like an RPC message, which in most systems
is very strongly ytped froma single rigid definition. (An RPC message can be
represented as a structured document but not, in general, vice-versa)

Language mixing is a realtity. Real HTML pages are often HTML with Javascript,
or HTML plus CSS, or both. They just aren't declared as such. In real life,
many documents are made from multiple vocabularies, only some of which one
understands. I don't understand half the information in the tax form - but I
know enough to know what applies to me. The invoice is a good example. Many
differet coloured copies of the same document used to serve as a packing list,
restocking sheet, invoice, and delivery note. Different parts of a company
would understand different bits: the financial dividion woul dcheck amounts
and signatures, the store would understand the part numbers, and the sales and
marketting would define dthe relationship betwene the part numbers and prices.

No longer can the Web tolerate the laxness which HTML and HTTP have been
extended. However, it cannot constrain itself to a system as rigid as a
classical disributed object oriented system.

The [note on namespaces](https://www.w3.org/DesignIssues/Extensible.html) defines some requirements of a
language framework which allows new schmata to be developed quite
independently, and mixed within one document. This note elaborates on the
sorts of things which have to be possible when the evolution occurs.

###  The Power of schema languages

You may notice than nowhere in the architecture do XML or RDF specify what
language the schema should be written in. This is because much of the future
power of the system will lie in the power of the schema and related documents,
so it isimportant to leave that open as a path for the future. In the short
term, yo can think of a schema being written in HTML and english. Indeed, this
is enough to tie the significance of documents written in the schema to the
law of the land and mkae the document an effective part of serious commercial
or other social interaction. You can imagine a schema being in a sort of SGML
DTD language which tells a computer program what constraints there are on the
structure of documents, but nothing about their meaning. This allows a certain
crude validity check to be made on a document but little else.

Now let us imagine further power which we could put into a schema language.

##  Partial Understanding

A crucial first milestone for the system is partial understanding. Let's use
the scenario of an invoice, like the [scenario in the "Extensible languages"
note](https://www.w3.org/DesignIssues/Extensible.html#Scenario). An invoice refers to two schemata: one is a
well-known invoice schema and the other a proprietory part number schema. The
requirement is that an invoice processing program can process the invoice
without needing to understand the part description.

Somehow the program must find out that the invoice is from its point of view
just as valid as an invoice with the details fo the part description stripped
out.

###  Optional parts

One possibility is to mark the part description as "optional" on the text. We
could imagine a well-known way of doing this. It could be done in the document
itself [as usual, using an arbitrary syntax:]

    
    
    <item>
    <partnumber>8137498237</>
    <optional>
     <xml:using href="http://aeroco.com/1998/03/sy4" as="A">  
    
       <a:partdesc>
            ...
       <a:partdesc>
     </xml:using>  
    
    </opional>
    </item>
    

There are problems with this. One is that we are relying on the invoice schema
to define what in invoice is and isn't and what it means. It would be nice if
the designer of the invoice could say whether the item should contain a part
description of not, or whether it is possible to add things into the item
description or not. But in general if there is something to be said we like to
allow it to be said anywhere (like metadata). But for the optionalness to be
expressed elsewhere would save the writer of every invoice the bother of
having to explicitly.

###  Partial Understanding

The other more fundamental problem is that the notion of "optional" is
subjective. We can be more precise about "partial understanding" by saying
that the invoice processing system needs to convert the document which
contains things it doesn't understand into a document which it does completely
understand: a valid invoice. However, another agent may which to convert the
same detailed invoice into, say, a delivery note: in this case, quite
different information would be "optional".

To be more specific, then, we need to be able to describe a transformation
from one document to another which preserves "valididy" in some sense. A
simple form of transformation is the removal of sections, but obviously there
can be all kinds of level of transformation language ranging from the cudest
to theturing complete. Whatever the language, statement that given a document
x, that some f(x) can be deduced.

###  Principle of Least Power

In practice, this suggest that one should leave the actual choice of the
transformation language as a flexibility point. However, as with most choices
of computer language, the general "principle least power" applies:

When expressing something, use the least powerful language you can.  
---  
  
_(@@justify in greater depth in footnote)_

While being able to express a very complex function may feel good, the result
will in general be less useful. As Lao-Tse puts it, "[Usefulness from what is
not there](https://www.w3.org/DesignIssues/Evolution.html#within)". From the point of view of translation
algorithms, one usefulness is for them to be reversible. In the case in which
you are trying to prove something (such as access to a web site or financial
credibility) you need to be able to derive a document of a given form. The
rules you use are the pieces of the web of trust and you are looking for a
path through the web of trust. Clearly, one approach is to enumerate all the
things which can be deduced from a given document, but it is faster to have an
idea of which algorithms to apply. Simple ones have input and output patterns.
A deletion rule is a very simple case

s/.*foo.*/\1\2/

This is stream editor languge for "Remove "foo" from any string leaving what
was on either side". If this rule is allowed, it means that "foo"is optional.
@@@ to be continued

Optional features and Partial Understanding

  * Goal: V1 software partially understands V2 document 
  * Optional features visible as such 
  * Example: "Mandatory" Internet Draft 
  * Example: SMIL (P.Rec. 1998/4/9) 
  * Conversion from unknown language to known language. 

#  Test of Independent Invention

The test of independent invention is a thought experiment which tests one
aspect of the quality of a design. When you design something, you make a
number of important architectural decisions, such as how many wheels a car
has, and that an arch will be used between the pillas of the vault. You make
other arbitrary decisions such as the color of the car, the side of the road
everyone will drive, whether to open the egg at the big end or the little end.

Suppose it just happens that another group is designing the same sort of
thing, tackling the same problem, somewhere else. They are quite unknown to
you and you to them, but just suppose that being just as smart as you, they
make all the same important archietctural decisions. This you can expect if
you believe hat these decisions make logical sense. Imagine that they have the
same philosophy: it is largely the philosophy which we are testing. However,
imagine that they make all the arbitrary decisions differently. They
complement bit 7. They drive on the other other side of the road. They use red
buoys on the starbord side, and use 575 lines per screen on their televisions.

Now imagine that the two systems both work (locally), and being usccessful,
grow and grow. After a while, they meet. Suddenly you discover each other.
Suddenly, people want to work across both systems. They want to connect two
road systems, two telephone systems, two networks, two webs. What happens?

I tried originally to make WWW pass the test. Suppose someone had (and it was
quite likely) invented a World Wide Web system somewhere else with the same
principles. Suppose they called it the Multi Media Mesh (tm) and based it on
Media Resource Identifiers(tm), the MultiMedia Transport Protocol(tm), and a
Multi Media Markup Language(tm). After a few years, the Web and the Mesh meet.
What is the damage?

  * A huge battle, involving the abandonment of projects, conversion or loss of data? 
  * Division of the world by a border commission into two separate communities? 
  * Smooth integration with only incremental effort? 

(see also [WWW and Unitarian Universalism](https://www.w3.org/People/Berners-Lee/UU.html))

Obviously we are looking for the latter option. Fortunately, we could
immediately extend URIs to include "mmtp://" and extend MRIs to include
"http:\\\". We could make gateways, and on the better browsers immediately
configure them to go through a gateway when finding a URI of the new type. The
URI space is universal: it covers all addresses of all accessible objects. But
it does not have to be the only universal space. Universal, but not unique. We
could add MMML as a MIME type. And so on. However, if we required all Web
servers to synchronise though one and only one master lock server in Waltdorf,
we would have found the Mesh required synchronisation though a master server
in Melbourne. It would have failed.

No system completely passes the ToII - it is always some trouble to convert.

###  Not just a thought experiment

As the Web becomes the basis for many many applications to be build on top of
it, the phenomenon of independent invention will recur again and again. We
have to build technology so as to make it easy for systems to pass the test,
and so survive real life in an evolving world.

If systems cannot pass the TOII, then we can only achieve worldwide
interoperability when one original design has originally beaten the others.
This can happen if we all sit down together as a worldwide committee and do a
"top down"design of the whole thing before we start. This works for a new idea
but not for the automation of something which, like pharmacy or trade, has
been going on for centuries and is just being represented in the Semantic Web.
For example, the library community has had endless trouble trying to agree on
a single library card format (MARC record) worldwide.

Another way it can happen is if one system is dropped completely, leading to a
complete loss of the effport put into it. When in the late 1980s Europe
eventually abandoned its suite of ISO protocols for networking because they
just could not interwork with the Internet, a huge amount of work was lost.
Many problems, solved in Europe but not in the US (including network addresses
of more than 32 bits) had to be solved again on the Internet at great cost.
Sweden actually changed from driving on the left to driving on the right. All
over the world, people have changed word processor formats again and again but
only at the cost of losing access to huge amounts of legacy information. The
test of independent invention is not just a thought experiment, it is
happening all the time.

#  From philosophy to requirement

So now let us get more specific about what we really need in the underlying
technology of the Semantic Web to allow systems in the future to pass the test
of independent invention.

###  We will be smarter

Our first assumption is that we will be smarter in the future. This means that
we will produce better systems. We will want to move on from version 1 to
version 2, from version n to version n+1.

What happens now? A group of people use version 4 of a word process and share
some documents. One touches a document using a new version 5 of the same
program. Oen of the other people tries to load it using version 4 of the
software. The version 4 program reads the file, and find it is a version5
file. It declares that there is no way it can read the file,as it was produced
in the future, and there is no way it can predict the future to know how to
read a version 5 file. A flag day occurs: everyone in the group has to upgrade
immediately - and often they never even planned to.

So the first requirement is for a version 4 program to be able to read a
version 5 file. Of course there will be some features in version 5 that the
version 4 program will not be able to understand. But most of the time, we
actually find that what we want to achieve can be done by partial
understanding - understanding those parts of the document which correspond to
functions which exist in version 4. But even though we know partial
understanding would be acceptable, with most systems we don't know how to do
even that.

###  We are not the smartest

The philosophical assumption that we may not be smarter than everyone else (a
huge step for some!) leads us to realise that others will have gret ideas too,
and will independently invent the same things. It forces us to consider the
test of independent invention.

The requirement for the system to pass the ToII is for one program which we
write to be able to read somehow (partially if not totally) data written by
the program written by the other folks. This simple operation is the key to
decentralised evolution of our technology, and to the whole future of the Web.

So we have deduced two requirements for the system from our simple
philosophical assumptions:

  * We will be smarter in the future 
    * Technology: Moving Version 1 to Version 2 
  * We are not smarter than everyone else 
    * Decentralized evolution 
    * Technology: Moving between parallel Version A and Version B 

###  The story so far

We are we with the requirements for evolvability so far? We are looking for a
tecnology which has free but well defined extension. We want to do it by
allowing documents to use mixed vocabularies. We have already found out (from
PICS work for example) that we need to be abl eto know whether extension
vocabulary is mandatory or can be ignored. We want to use the Web for any
registry, rather than any central point. The technology has to be allow an
application to be able to convert the output of a future version of itself, or
the output of an equivalent program written indpendently, into something it
can process, just by looking up schema information.

##  Evolution of data

Now let us look at the world of data on the Web, the [Semantic
Web](https://www.w3.org/DesignIssues/Semantic.html), which I expect we expect to become a new force in the
next few years. By "data" as opposed to "documents", I am talking about
information on the Web in a form specifically to aid automated processing
rather than human browsing. "Data" is characterised by infomation with a well
defined strcuture, where the atomic parts have wel ldefined types, such as
numbers and choices from finite sets. "Data", as in a relational database,
normally has well defined meaning which has rarely been written down. When
someone creates a new databse, they have to give the data type of each column,
but don't have to explain what the field name actually means in any way. So
there is a well defined semantics but not one which can be accessed. In fact,
the only time you tells the machine anything about the semantics is when you
define which two columns of different tables are equivalent in some way, so
that they can be used for example as the basis for joining the two databases.
(That the meaning of data is only defined relative to the meaning of other
data is of course quite normal - we don't expect machines to have any built in
understanding of what "zip code" might mean apart from where you can read it
and write it and what you can compare it with). Notice that what happens with
real databases is that they are defined by users one day, and they evolve.
They are rarely the result of a committee sitting down and deciding on a set
of concepts to use across a company or an industry, and then designing the
data schema. The schema is craeted on the fly by the user.

We can distinguish two ways in which tha word "schema" has been used:

Syntactic Schema: A document, real or imagined, which constrains the structure
and/or type of data. _(pl.: Schemata)_.  
---  
Semantic schema: A document, real or imagined, which defines the infereneces
from one schema to another, thus defining the semantics of one syntactic
schema in terms of another.  
---  
  
I will use it for the first only. In fact, a syntactic schema dedfines a class
of document, and often is accompanied by human documentation which provides
some rough semantics.

There is a huge amount ("legacy" would unfairly suggest obsolescence) of data
in relational databases. A certain amount of it is being exported onto the web
as virtual hypertext. There are many applications which allow one to make
hypertext views of difeferent aspects of a database, so that each server
request is met by performing adatabse query, and then formatting the result as
a report in HTML, with appropriate style and decoration.

##  Data about data: Metadata

Information about information is interesting in two ways. Firstly, it is
interesting because the Web society desperately needs it to be able to manage
social aspects of information such as endorsement (PICS labels, etc),
ownership and access rights to information, privacy policies (P3P, etc),
structuring and cataloguing information and a hundred otehr uses which I will
not try to ennumerate. This first aspect is discussed elsewhere. (See
[Metadata architecture](http://www.w3.org/DesignIssues/Metadata.html) about
general treatment of metadata and labels, and the [Technology and Society
domain](https://www.w3.org/TandS/Overview.html) for overveiw of many of the social drivers and
related projects and technology)

The second interest in metadata is that it is data. If we are looking for a
language for putting data onto the Web, in a machine understandable way, then
metadata happens to be a first application area. Also, because metadat ais
fundamental to most data on eth web, it is the focus of W3C effort, while many
other forms of data are regarded as applications rather than core Web
archietcure, and so are not.

###  Publishing data on the web

Suppose for example that you run a server which provides online stock prices.
Your application which today provides fancy web pages with a company's data in
text and graphs (as GIFs) could tomorrow produce the same page as XML data, in
tabular form, for machine access. The same page could even be produced at the
same URL in two formats using content negotiation, or you could have a typed
link between the machine-understandable and person-understandable versions.

The XML version contains at the top (or soemewhere) a pointer to a schema
document. This poiner makes the document "self-describing". It is this pointer
which is the key to any machine "understanding" of the page. By making the
schema a first class object, in other words by giving its URL and nothing
else, we are leaving the dooropen to many possibilities. Now it is time to
look at the various sorts of schema document which it could point to.

##  Levels of schema language

Computer languags can be classified into various types, with various
capabilities, and the sort we chose for the schema document, and information
we allow the schema fundamentally affects not just what the semantic web can
be but, more importantly, how it can grow.

The schema document can, broadly, be one of the following:

  1. Notional only: imaginary, non-existent but named. 
  2. Human readable 
  3. Machine-understandable and defining structure 
  4. Machine-understandable and slo which are optional parts 
  5. A Turing-complete recipe for conversion into othr langauges 
  6. A logical model of document 

We'll go over the pros and cons of each, because none of these should be
overlooked, but some are often way better than others.

###  Schema 1: URI only

  * No supporting documentation 
  * Allows compatibility yes/no test 

This may sound like a silly trivial example, but like many trival examples, it
is not silly. If you just name your schema somewhere in URI space, then you
have identified it. This deosn't offer a lot of help to anyone to find any
documentation online, but one fundamental function is possible. Anyone can
check compatability: They can compare the schema against a list of schemata
they do understand, and return yes or no.

In fact, they can also se an idnex to look up information about the schema,
including ifnromation about suitable software to download to add understanding
of the document. In fact this level is the level which many RPC systems use:
the interface is given a unique but otherwise random number which cannot be
dereferenced directly.

So this is the level of machine-understanding typical of distributed ocmputing
systems and should not be underestimated. There are lot sof parts of URI space
you can use for this: yo might own some http: space (but never actually serve
the document at that point) , but if you don't, you can always generate a URI
in a mid: ro cid: space or if desperate in one of the hash spaces.

###  Schema option 2: Human readable

The next step up from just using the Schema identifier as a document tyope
identifier is to make that URI one which will dereference to a human-readable
document. If you're a computer, big deal. But as well as allowing a strict
compatiability test (test for equality of the schema URI), this also allows
human beings to get involed if ther is any argument as to what a document
means. This can be signifiant! For example, the schema could point to a
complete technical spec which is crammed with legalese about what the document
does and does not imply and commit to. At the end of the day, all machine-
understandable descriptions of documents are all very well, but until the day
that they bootstrap themselves into legality, they must all in the end be
defined in terms of human-readable legalese to have social effect. Human
legalese is the schema language of our society. This is level 2\.

###  Schema option 3: Define structure

Now we move into the meat of the schema system when we start to discuss schema
documents which are machine readable. now we are satrting to enable some
machine understanding and automatic processing of document types which have
not been pre-programmed by people. Ça commence.

The next level we conside is that when your brower (agent, whatever)
dereferences the namespace URI, it find a schema which defines the structure
of the document. this is a bit like an SGML Doctument type Definition (DTD).
It allows you to do everything which the levels 1 and 2 allowed, if it has
sufficient comments in it to allow human arguments to be settled.

In addition, a system which has a way of defineing structure allows everyone
to have one and only one parser to handle all manner of documents. Any
document coming across the threshold can be parse into a tree.

More than that, it allows a document o be validated against allowed strctures.
If a memeo contains two subject fields, it is not valid. Tjis is one fo the
principal uses of DTDs in SGML.

In some cases, there maybe another spin-off. You canimagine that if the schema
document lists the allwoed structrue of the document, and the types (and maybe
names) of each element, then this would allow an agent to construct on the fly
a graphic user interafce for editing such a document. This was theintent with
PICS rating systems: at least, a parent coming across a new rating system
would be be given a ahuman-readable descriptoin of the various parameters and
would be able to select

###  Schema option 4: Structure + Optional flags

The "optional" flag is a term I use here for a common crucial step which can
make the difference between chaos and smooth evolution. All you need to do is
to mark in the schema of a new version of the language which elements of the
langauge can be ignored if you don't understand them. This simple step allows
a processor which handled the old language, giventhe schema of the new
langauge, to filter it so as to produce a document it can legitimately
understand.

Now we have a technology which ahs all the benefits to date, plus it can
handle that elusive **version 2 to version 1 conversion** problem!

###  Schema option 5: Turning complete language

Always in langauges there is the balance between the declarative limited
langauge, whose foprmulae can be easily manipulated, and the powerful
programming language whose programs cannot be analyzed in general, but which
have to be left to run to see what they do. Each end of the spectrum has its
benefits. In describing a lanuage in terms of another, one way is to provide a
black box program, say in Java or Javascript, which will convert from one to
the other.

Filters written in turing-complete languages generally have to be trusted, as
you can't see what rules they are based on by looking at them. But they can do
weird and wonderful things. (They can also crash and loop forever of course!).

A good language for conversion from one XML-based language to another is XSL.
It lstarted off as a template-like system for building one document from
another (and can be very simple) but is in fact Turning-complete.

When you do publish a program to convert language A to language B, then anyone
who trusts it has that capability. A disadvantage is that they never know how
it works. You can't deduce things about the individual components of the
languages. You can't therefore infer much indirectly about relationships to
other languages. The only way such a filter can be used is to get whatever you
have into language A and then put it though the filter. This might be useful.
But it isn't as fascinating as the option of blowing language A open.

###  Schema option 6: Expose logic of document

What is fundamentally more exciting is to write down as explicitly as posible
wahteth new language means. Sorry, let me take that back, in case you think
that I am talking about some absulte meaning of meaning. If you know me, I am
not. All I mean is that we write in a machine-processable logical way the
equivalences and conversions which are possible in and out of language A from
other languages. And other languages.

A specific case of course, is when we document the relationship betwen version
2 and version 1. The schema document for version 2 could explain that all the
terms are synonyms, except for some new terms which can be converted to
nothing (ie are optional) and some which affect the meaning of the document
completely and so if you don't understand them you are stuck.

In a more general case, take a language like iCalendar in RDF (were it in
RDF), which is for describing events as would be in a personal organizer. A
schema for the language might declare equivalences betwen a calendar's concept
of group MEMBER ship and an access control system's concept of group
membership; it might declare the equivalence of eth concept of LOCATION to be
the text description of a Geographical Information Systems standard's
location, and it may declare an INDIVIDUAL to be a superset of the HR
department's concept of employee. These bits of information of the stuff of
the semantic web, as they allow inference to stretch across the gloabe and
conclude things which we knew as whole but no one person knew. This is what
RDF and the Semnatic Web logic built on top of it is all about.

* * *

So, what will semantic web engine be able to do? They will not all have the
same inference abilities or algorithms. They will share a core concept of an
RDF statement - an assertion that a given _resource_ has a _property_ with a
given _value_. They will use this as a common way of exchanging data even when
their inference rules are not compatible. An agent will be able to read a
document in a new version of a language, by looking up on the web the
relationship with the old version that it can natively read. It will be able
to combine many documents into a single graph of knowledge, and draw
deductions from the combination. And even though it might not be able to find
a proof of a given hypothesis, when faced with an elaborated proof it will be
able to check its veracity.

At this stage (1998) we need relational database experts in the XML and RDF
groups, [2000 -- include ontology and conceptual graph and knowledge
representation experts].

##  Evolvability in the real world

Examples abound of language mixing and evolution in the real world which make
the need for these capabilities clear. There is a great and unused overlap in
the concepts used by, for example, personal information managers, email
systems, and so on. These capabilities would allow information to flow between
these applications.

You just have to look at the history of a standard such as MARC record for
library information to see that the tension between agreeing on a standard
(difficult and only possible for a common subset) and allowing variations
(quick by not interoperable) would be eased by allowing language mixing. A
card could be written out in a mixture of standard and local terms.

The real world is full of times when conventions have been developed
separately and the relationships have been deduced afterward: hence the market
for third party converters of disk formats, scheduler files, and so on.

#  Engines of the future

I have left open the discussion as to what inference power and algorithms will
be useful on the semantic web precisely because it will always be an open
question. When a language is sufficiently expressive to be able to express teh
state of the real world and real problems then there will be no one query
engine which will be able to solve real problems.

We can, however, guess at how systems might evolve. No one at the beginning of
the Web foresaw the search engines which could index almost all the web, so
these guesses may be very inaccurate!

We note that logical systems provide provably good answers, but don't scale to
large problems. We see that search engines, remarkably, do scale - but at the
moment produce very unreliable answers. Now, on a semantic web we can imagine
a combination of the two. For example, a search engine could retrieves all the
documents which reference the terms used in the query, and then a logical
system act on that closed finite world of information to determine a reliable
solution if one exists.

In fact I thing we will see a huge market for interesting new algorithms, each
to take advantage of particular characteristics of particular parts of the
Web. New algorithms around electronic commerce may have directly beneficial
business models, to there will be incentive for their development.

Imagine some questions we might want to ask an engine of the future:

  * Can Joe access the party photos? 
  * Who are all the people who can? 
  * Is there a green car for sale for around $15000 in Queensland? 
  * Did someone driving a blue car send us an invoice for over $10000? 
  * What was the average temperature in 1997 in Brisbane? 
  * Please fill in my tax form! 

All these involve bridging barriers between domains of knowledge, but they do
not involve very complex logic -- except for the tax form, that is. And who
knows, perhaps in the future the tax code will have to be presented as a
formula on the semantic web, just as it is expected now that one make such a
public human-readable document available on the Web.

##  Conclusion

There are some requirements on the Semantic Web design which must be upheld if
the technology is to be able to evolve smoothly. They involve both the
introduction of new versions of one language, and also the merging of two
originally independent languages. XML Namespaces and RDF are designed to meet
these requirements, but a lot more thought and careful design will be needed
before the system is complete.

* * *

> ####  The Space Within

>

> Thirty spokes share the wheel's hub;  
>  It is the center hole that makes it useful.  
>  Shape clay into a vessel;  
>  It is the space within that makes it useful.  
>  Cut doors and windows for a room;  
>  It is the holes that make it useful.  
>  Therefore profit comes from what is there;  
>  Usefulness from what is not there.

Lao-Tse

(UU-STLT#600)

...

Imagine that the EU and the US independently define RDF schemata for an
invoice. Invoice are traded around Europe with a schema pointer at the top
which identifies the smema. Indeed, the schema may be found on the web.

* * *

* * *

[Next:  Metadata architecture](https://www.w3.org/DesignIssues/Metadata.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

