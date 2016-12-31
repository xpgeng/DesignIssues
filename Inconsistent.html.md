Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Semantic Web

* * *

##  Inconsistent data

What, many people ask, will happen when this huge mass of classical logic
meets its first inconsistncy? Surely, once you have one staement that A and
another somewhere on the web that not A, then doesn't the whole system fall
apart? Surely, then you can deduce anything you want?

This fear of course is quite valid - or would be if all assertions in the
whole world were regarded as bing on equal footing. Some imagine that an RDF
parser will simply search all XML documents on the web for any facts, and add
them to a massive set of belived assertions. This is not how realisic systems
will actually work.

On the web, a fact may be asserted in an expression. That expression may be
part fo a formula. The formula may ivolve negation, and may invove quotation.
The whole formula is found by parsing some document . There is no a priori
reason to believe any document on the web. The reason to believe a document
will be found in some information (metadata) about the document. That metadata
may be an endosement of the document - another RDF statement, which in turn
was found another document, and so on.

_[@@need picture here]_

A real system may work backwards or forwards (or both). I would call working
forwards a system which is given a configuartion page to work from which in
turn points to other pages which in turn are used as valid data. I would call
working backwards a system which, when looking for an answer to a query, looks
at a gloal index to find any document at all which mentions a given term. It
then searches thes documents turned up for answers to the query. Only when it
has found an answer does t check back to see whether the data can be deriveded
directly or indirectly from sources it has been set up to trust.

Digital sgnature (see trust) of course adds a notion of secuirty to the whole
process. The first step is that a document is not endorsed without giving the
checksum it had when believed. The second step is to secify more powerful
rules of the form

> "whatever any document says so long it is signed with key 57832498437".

In prcatice, particular authroities are trusted only for specific purposed.
The semantic web must support this. You must be able to restrict the
information believed along the lines of,

> "whatever any document says of the form xxxx is a meber of W3C so long as it
is signed wiht key 32457934759432".

for example

> "whatever any document says of the form "a is an employee of IBM" so long as
it is signed by with key 3213123098129".

###  Limiting inference

There is a choice here, and I am not sure right now which appeals to me most.
One is to say precicely,

> "whatever any document _**says**_ of the form xxxx is a member of W3C so
long as it is signed with key 32457934759432".

The other is to say,

> "whatever is of form xxxx and _**can be inferred**_ from information signed
with key 32457934759432"

In the first case, we are making an arbitrary requirement for a statement to
be phrased in a particular way. This seems unnecessarily bureaucratic, and
more difficult to treat constently. Normally we like to be able to replace any
set of forumlae with another set which can be deduced from it. However, in
this case we have to preserve the actual form in case we need to match it
against a pattern. This is very messy.

In the second case, we fall prey to the inconsistency trap. Once any pair of
conflicting statements can be deduced from information signed with a given
key, then anything can be deduced from information signed with the key: the
key is completely broken. Of course, only that key is broken, so a trust
system can remove any reason it has to trust that key. However, the attacked
system may not realize what has happened before it has been convinced that the
sun rises in the west.

Is there a way to limit the domain of trust in a key while allowing
inmformation to be processed in a consistent way throughout the system? Yes -
maybe - there are many. Each KR system which uses a limited logic does do in
order (partly) to solve this problem. We just qulaify "can be inferred" be the
type of inference rules which may be used. This means the generic proof engine
eitehr has to work though a reified version of the rules or it has to know the
sets - incorporate each proof engine. Maybe we only need one.

###  Expiry

> Tortoise: What's the time, Achilles?

>

> Achilles: Five past ten, my friend. [They chat for a minute]

>

> Tortoise: What is the time, Achilles?

>

> Achilles: Six minutes past ten, Mr. Toroise.

>

> Tortoise: But Achilles, you just told me just a minute ago it was **five**
minutes past ten. How can I ever believe you again?

Time-varying information is one cause of apparent contradiction. People and
documents change status. How does one base inference on information which may
be out of date?

One part of this is to put explicit or implcit expry dates on everything.
Whenever a server sends resource to an HTTP client, it can give an expiry
date. The client can track this, and ensure that all deductions from that
document are cancelled when the date arrives, unless a more recent copy can be
optained which says the same thing. In human language you might say "It is
rainy" but on the semantic web that woudl be exported in a fully qualified
way, more like "at Mon Jan 24 09:41:06 EST 2000 the measurement guage 5 at
Dubin Airport read rain as having fallen in the last hour". (A fuzzy system
would conclude "Dublin is wet" and a clasic logic system "at least once it
rained at at least one place in Dublin"!)

I understand [Lehrmann, SW meeting in DC] (sp?) that the KIF folks developed a
complete vocabulary for time-variance.

Another tchnique is to make any looseness which exists in the real system
visible. Instead of saying

> Any employee of any member orgainzation of W3C may register

you say formally to the registration engine

> Any person who was some time in the last 2 months an employy of an
organization which was som etim ein the last 2 montsh a W3C member may
register.

In other words, if an organization were to drop its membership, the system
doesn't have to support propagating that information instantly.

I think there will be time-aware reasoning systems, and time-unaware raesoning
systems which are fed data with expiry dates and whose results are used within
the intersection period of the validity periods of the incomming data. Indeed,
time-aware systems may contain nested time-unaware systems, and probably vice-
versa.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

