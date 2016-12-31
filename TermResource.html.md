Tim Berners-Lee  
Date: 2009/08/02, last change: $Date: 2009/08/05 20:36:28 $  
Status: Personal view only. This was sent as an email in a discussion on the
TAG list. There had been a lot of discussion of this of course in the TAG, and
in the AWWSW task force, and a proposal to start a new task force in this
space.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  A Short History of "Resource" in web architecture.

There has been a lot of confusion from a wide varying uses use of this term
for various different historical reasons, leading to uses which are sometimes
ambiguous and in places inconsistent. This article attempts to shed light on
the issue.

Historically, URIs were used to point to thinks like web pages and files and
movies, on the web, useful documents, or "online resources" in the sense of
useful things out there. FTP. Gopher and HTTP sites served up various types of
online resources. People got used to http://example.com/ being a web page and
http://example.com/#contact being an anchor within it.

The Online Information community, into whose domain the web stuff was put for
standardization at the IETF, referred to these things like web pages as
resources, and changed the original "D" for "Document" in "UDI" to "R". Some
felt that resource was more appropriate term, maybe because "document" wasn't
wide enough to include things like movies.

Now the URI spec actually allowed URIs for completely different things, such
as telephone end points, and wisely the URI spec does not make any arbitrary
constraint on what a resource should be, especially a resource denoted by a
URI in a new scheme to be invented.

Meanwhile, the HTTP spec was polished and elaborated basically as a document
delivery system, plus other methods for updating documents, plus POST. (POST
started historically as a way of introducing a new web page y posting it to a
list, just as in NNTP. It then almost immediately got used as a catch-all
extension method. I will ignore it in this overview).

There was no real definition of what a resource or document was -- maybe
because it seemed obvious. The HTTP spec did not even specify whether the URI
denoted a person or a document about them, it just explained that the thing
returned representation of the resource.

Roy's REST work then came along to formalize HTTP as REST and declared that a
resource was a time-varying mapping between URI and representation. That was
good enough for HTTP. It didn't have enough for the AWWW, when it came along,
to be able to describe how the web worked.

In fact, the AWWW document, to explain how to use the web properly, had to add
in a bunch of stuff about the social expectations -- things like, yes, the
mapping from URI to representation is a function of time, but not just any old
one -- a random function is not typically very useful. There are expectations
about it can change with time. Persistence, consistency, with various common
patterns which allow the web to be a useful medium. The AWWW decided to use
the term "Information Resource" for a thing like a web page which contains
information, and "Resource" for any old thing at all.

So HTTP and the REST work of was done very much in this space of document
delivery, editing and update. There was no philosophical need to talk about
what he URI denoted (the person, the web page about the person) until RDF came
along, when there was an immediate need.

When RDF was first developed, it was motivated by the need for data about
resources very much in the online information sense: data about documents, or
'metadata'. In fact it was designed to be able to describe anything, but many
early users of RDF referred to it as metadata technology. RDF used the word
"resource" rather awkwardly in fact as it turned out. In the beginning, many
of the things being described were documents, and so the online information
meaning of resource made sense. But in fact in RDF the resource was allowed to
be anything at all. A class, rdf:Resource even used the term as the universal
class of all things. A little later, the Web Ontology Language decided to use
Thing for that.

RDF came along in what I think was a neat way. It used completely existing web
protocol extension devices to introduce a new system which was fundamentally
different from the old HTTP+HTML one. The HTML web was a hypertext model,
which pages and anchors. The RDF model was a knowledge representation one of
arbitrary things. It did this by using the fact that a new language can define
whatever it likes as what a local identifier denotes. A graphic language might
use local identifier to denote lines and points. HTML used local identifiers
to identify hypertext anchors. RDF used them to identify arbitrary concepts,
people, whatever.

The web architecture gave all these languages a common way of building a
global identifier for the thing denoted by a local identifier in a given
document. The semantics of the hash sign are defined web-wide to mean that
"a#b" can be used to denote whatever is denoted by "b" in the document denoted
by "a".

Worked a treat. At the beginning of the century, people played around and gave
all kinds of things URIs like "http://example.com/ foo.rdf#color". Some of us
did lots of work and made all kinds of systems which exchanged and integrated
data in this way.

Two snags occurred, as the years passed. One was that a bunch of RDF users got
the fact that it was good to use HTTP URIs, but didn't get the fact that you
should put the foo.rdf online so that people can look up what #color means in
it. And as they didn't do that, they didn't actually bother with the "#" at
all. The second fly in the ointment was that some people wanting to use RDF
for large systems found that they didn't want to use the "#". This was
sometimes because the number of things defined in the same file was too low
(like 1) or too large (like a million) and it was difficult to divide up the
information into middle-sized chunks. Or they just didn't like the "#" because
it looks weird. But for one reason or another people demanded the right to be
able to use http://example.net/people/Pat to denote Pat rather than a web page
about Pat.

This potentially led to huge failures in the whole RDF world, with systems
already built which just used "http://example.net/people/ Pat" to identify the
document whether you like it or not. I among others pushed back against using
non-hash URIs for arbitrary things his but eventually gave in.

So in response to this, the HTTP protocol was, in fact, changed.

The spec wasn't changed. The spec editors were not brought on board to the new
model. The spec was interpreted. The TAG negotiated in a way a truce between
the existing HTTP spec, RDF systems, and people who wanted to use HTTP URIs
without "#" to identify people. That truce was HTTPRange-14, which said that
yoiu don't _a priori_ know that a hashless HTTP URI denoted a document, but if
the server responded with a 200 then you did, and you had a representation of
the document. If you did a get on one of these new URIs which identified
things were not documents (people, RDF properties, classes, etc) them the
server must not return 200, it can return 303 pointing to a document which
explains more.

So the HTTP protocol was, effectively, changed. The HTTP protocol as extended
now allows HTTP to be used not only for Documents but for arbitrary Things. It
extends the set of things which you can ask a web server about from documents
to anything. It isn't a very bad design, nor very beautiful. Other designs
would have worked, but that one was the only one which didn't have major
problems for some community. It could be extended, but basically it works. It
would be very expensive to reverse it in terms of systems which have been
deployed.

It is also very expensive to go on debating it as though it is an open issue.
It is reasonable to try to make the documents more consistent.

Anyway, that is a simplified version of the history of all this as I saw it.

I would like to see what the documents all look like if edited to use the
words Document and Thing, and eliminate Resource. That's my best bet as to two
english words which mean as close as we can get to what we want. Note however
that the web is a new system, a design in which new concepts are created, so
we can't expect english words to exist to capture exactly the concepts. So we
take those nearby and abuse them as little as we can as far as we can tell at
the time, and then write them in initial caps to recognize that that is what
we have done

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

