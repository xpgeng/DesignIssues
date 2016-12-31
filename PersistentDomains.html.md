![W3C](http://www.w3.org/Icons/WWW/w3c-home)

Things get written under Design Issues when I have expressed them several
times in various contexts. This idea hit that criterion in a W3C staff meeting
in October 2000, as I had suggested it in various contexts and various times,
including backstage to Ether Dyson at the Harvard Internet Society conference.

####  Persistent Domains - Strawman ideas on Web Architecture

Up to [Design Issues](https://www.w3.org/DesignIssues/Overview).

* * *

#  Persistent Domains

This is a proposal to address the problems with the persistence of HTTP URIs.
It introduces the concept of a datestamped domain name with associated rights
and obligations of ownership.

##  Introduction

 The problems of the lack of persistence of URIs lead to many well-known
problems, including

  * user frustration and social dysfunction with Error 404 messages; and 
  * (worse) the dereferencing of a URI using HTTP/DNS leading to completely different resource to that intended by the referring person. 

 A second-order symptom of the problem is that there is a constant stream of
proposals for new URI schemes with different, incompatible, name-lookup
technology. These are often made with less attention to the real social issues
surrounding persistence than HTTP/DNS, but propose to be systems otherwise
similar except in having greater persistence.

##  The analysis

The persistence of HTTP URIs can be factored into two issues:

  1. The persistence of the opaque string which follows the domain name, and 
  2. the persistence of the domain name  itself. 

The first of these is an issues is of course under the control of the domain
owner.  This, combined with a dearth of tools which help one run a web server
with persistent URIs, has led to a vastly varying level of persistence.  Some
sites understand and construct their URIs carefully, while some obviously have
not thought about the problem and end up changing URIs out of thoughtlessness
rather than malice. I have summarized some aspects of this problem in "[_Cool
URIs Don't Change_](http://www.w3.org/Provider/Style/URI)" .  This relies on
publishers making an institutional commitment to persistence.  I have tried to
lead the way with W3C's draft [Persistence
Policy](http://www.w3.org/Consortium/Persistence). However, this only
addresses the first element.

The second issue is summarized by ICANN chair Ester Dyson's line, _You don't
buy domain names, you rent them_. This single meme instantly undermines any
public expectation that domain names should be persistent. In principle, if
<http://www.example.com/downloads> today points to example.com's download
page, tomorrow, it could point to anything as defined by a company which has
bought, acquired though law suit or accidental expiry the domain name
"example.com".   In fact, however, huge numbers of links are being made with
HTTP. The planet's investment in domain names in references is huge. The
technology which actually is involved in dereferencing such identifiers has
become more and more sophisticated.  In practice, also, the legal weight
behind a significant organization's ownership of a domain name is
considerable.  No one would dream that a legal battle _microsoft.com_ or
_ietf.org_ would be lost to some sneaky entrepreneur.  Through the rift
between trademark law and domain names is a problem, there in fact is strong
legal support for an organization's ability to keep its name. But is this
enough?

##  The Solution

I think we can do better. We can do better, if this scheme works out, on both
issues.  To tackle the second, we can create domain names which are allocated
once and once only, which are bought, not rented. We can simultaneously set
expectations that such data will endure, that names will not be reused, and
that information will be available even after organizations involved have
disappeared.  The trick is the same one as used in W3C's datespace URIs (such
as <http://www.w3.org/2000/01/sw>) and British car registration plates: to
date code them. For example, let us create a series of top-level **persistent
domains** y2000, y2001 and so on. One would only be able to acquire a .y2000
domain name  during the year 2000. Once acquired one would have it forever. In
fact, the domain name would correspond forever to the information published in
it.

We could take the precaution of inserting a few rules for sanity here.  There
should be some combination of due diligence to ensure you are not infringing
trademark when applying for an alphanumeric name. I would like to put a limit
on the number of persistent domains any company could own - or at least put
those who have n in the queue ahead of those who have k&lt;n.  There could be
a convention that if you are happy with a random numeric domain 6872364.y2000
you can have one immediately and automatically.  It would be great to put some
constraint on sitting on a domain without using it, and maybe on transfer of
domain ownership.

To tackle the first issue, an organization wishing to enter the scheme makes
necessarily a few commitments. One is that it must partake in some cooperating
mirroring scheme in which other organizations or commercial services take on
running mirrors of the site.  I can imagining this working, for example, as a
for-pay service for consumers, or a mirror-ring system for academic
institutes. There must be some form of contract which, in the event of the
original publisher of the information coming to a voluntary or involuntary
demise, the mirror sites will continue the service.  The documents then enter
an **archive state** in which the original publisher loses authority to evolve
the domain and the public gain rights of access. The actual contractual
arrangements will in fact have to be skillfully set up. For example, there
will be some information which will be just so uninteresting that no one will
be prepared to pay for it in the long run, but there must be some way to give
serious archival institutions (the major national libraries for example) the
right to take over an archive for the public good.  However, it would be best
to start with simple conditions, but allow them to be modified with experience
(real and imagined - _gedanken_) of the system.  Other interesting things
which come to mind include the mirroring of confidential access controlled
documents with a 30 year timeout on the confidentiality.

I don't know how best to enforce that a URI is never reallocated to something
else by a publisher. Actually, I don't think it will be a long term problem,
as the tools will be made such that it is not a function. ("Rename: command
not known"!).  Obviously re-use would cause a big mess, as caches across the
globe would run out of sync, and assumptions made by mirrors and proxies would
become invalid.  Perhaps a suitable disposition for a domain whose publisher
consistently flaunts the rules would be for it to be more or less
automatically declared dead, and for it to pass into archive state just as
though the organization had passed away. The organization can then ask for a
new domain and start again - at least the first time.

A clarification of what re-using a URI means.  As I have pointed out many
times, most URIs are [Generic URIs](http://www.w3.org/DesignIssues/Generic).
They refer to, not a fixed set of bits, but a conceptual resource whose
representation may vary with (for example) time, technology, language, and so
on.  This is fine, even in a persistent domain. It is in my opinion important
to distinguish (and ideally independently identify with separate URIs) generic
resources and any specific representation in use in a specific case.  The
contractual obligations of ownership of a persistent domain could usefully
include the provision of such metadata, and the allocation of a persistent URI
to the actual (mime-type, octet-string) specific entity.

Obligations of persistence would have to apply across the transfer of the
persistent domain. The persistent domain would be property, with (like land)
rights and obligations. Transfer of the domain name would carry within it
both.  Fleet Bank would not be able to buy BankBoston and simply drop support
for documents bankboston.y2000 - without all public documents falling into
archive state.

Another clarification.  A document in archive state has a certain general
license to mirror and reproduce in unmutilated form, but the intellectual
property rights remain as ever with the author. A very tempting rule (which I
am not convinced of yet) is that once the original domain owner has defaulted
on publishing the material, that it acquires some limited redistribution
license*.  This is the Web equivalent of an implicit right to photocopy any
book out of print: the publisher has deigned not to make copies, and it
impedes the operation of society to prevent this erstwhile public information
from being accessible.

##  Summary

Here is a collection of simplified rules which would form the protocol of
persistent domains.

  1. Domain names *.y2000 only allocated in 2000, and so on; 
  2. Some level of trademark due diligence before registration for alpha numeric names 
  3. Random numeric names   123678.y2000 issued immediately but not transferable 
  4. A limit on the number of persistent domain per organization would be useful 
  5. Domain names owned for life and persist forever 
  6. URIs may be live or frozen but not reused arbitrarily 
  7. Implicit irrevocable license for 3rd parties to mirror public info now and after death 
  8. The registry(-ar - whatever is the controlling authority, I forget the terminology) would be a neutral non-profit cooperative. 
  9. ICANN's delegation of .y[1-9]* would be irrevocable in all time. 
  10. Anyone using it would pay me $1 (just kidding! :-) 

Provided these are put together with sufficient care, the system should run
itself in such a way as to preserve our information world for posterity, be it
represented by a consumer in a decade searching for instructions from the now-
defunct manufacturer of an appliance, or by a historian in a millennium trying
to figure out what on earth made us all tick way back then.

* * *



Tim Berners-Lee

  

First Written: 2000/10/04



##  Footnotes

###  Out of Print Books

Joseph Reagle points out a
[passage](http://www.usg.edu/admin/legal/copyright/copy.html#part2a4) in
_[University System of Georgia]_ _Regents Guide to Understanding Copyright and
Educational Fair Use_ which explains:

> 4\. Out-of-Print-Book SCENARIO D: A library has a book that is out of print
and unavailable. The book is an important one in the professor's field that
she needs for her research. QUESTION a: May the professor copy the book for
her files? ANSWER: Yes. This is another example of personal use. If one
engages in the fair use analysis, one finds that: (1) the purpose of the use
is educational versus commercial; (2) the professor is using the book, a
creative work, for research purposes; (3) copying the entire book would
normally exceed the bounds of fair use, however, since the book is out of
print and no longer available from any other source, the copying is
acceptable; (4) finally, the copying will have no impact on the market for the
book because the book is no longer available from any other source. QUESTION
b: Using the same facts as explained in SCENARIO D, could the professor copy
the book and place the book on reserve in the library? Could the professor
scan the book into her computer and place the book onto the World Wide Web?
ANSWER: If the professor placed the book on reserve in the library, the use
would be considered a fair use. However, if the professor placed the book on
the Web, then the use is not a fair use. Placement on the Web allows unlimited
access to the book. This would affect the copyright holder's public
distribution of the book. See SCENARIO R, SCENARIO T, and SCENARIO U.

Joseph points out that the courts would not necessarily accept a parallel
between Web and paper distrbution. My purpose in drawing a parallel was to
explain the intent, not to suggest that either action was in fact admissable
under any particular jurisdiction.

###  Note for readers after 2100

> Note for readers after 2100.  To understand this document you must first
understand the situation which pertained at the dawn of M3. The anarchic chaos
which reigned over the embryonic Web is often hard for students to grasp, and
the fact that today's Web grew from these chaotic beginnings is a constant
marvel. The reader would do well to consult McKinley's "Chaos and
Fortune:Civilization from the Robber Barons to Domain Sharks" [Time-Microsoft-
Murdock, 2057] for a simple sketch, and Deaton and Plim's "Social Anthropology
of the pre-fusion Human" [UNArchivePress, 2068] for a more detailed analysis.



