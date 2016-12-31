[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

(part of [Design Notes](https://www.w3.org/Implementation/DesignNotes.html) ) 92.06.11 RC

#  From Version to Version of HTTP

##  Current version of HTTP

I propose 0.9 as the number of the [current version](https://www.w3.org/DesignIssues/HTTP0.9Summary.html) .

##  Compatibility

Today (June 1992) WWW is used in a community of highly computer literate
people. The cost of making all users adopt a new, incompatible version of the
browser and/or the server is not very high, neither in effort nor in
inconvenience.

Nevertheless, I will propose to go to a new version in a compatible way.
[Absolutely -- we can require complete back-compatibility for both clients and
servers - Tim]

##  Imperatives

Browsers and servers must have a few [characteristics](https://www.w3.org/DesignIssues/HTTP0.9Summary.html#1)
that must be kept over all versions.

##  What has a version?

A version is associated with the HTTP protocol used in the exchange between
servers and browsers. Because two agents on two different machines are
involved, there can be two different implementations of the protocol at work.
The version of the browser or the server refers to its capabilities in
displaying or providing, not to the protocol. Perhaps a Browser or server
should be characterised by both numbers: Linemode 3.4/2.0 would mean browser
version 3.4 using HTTP 2.0. [Hang on -- let's not complicate things unduly.
The software has a version number, and so does the protocol but they're
nothing to do with each other]

An HTTP version number consists of

  * an integer indicating the set of features, 
  * a dot, 
  * an integer indicating the level, whereby the differences between, say, 2.01 and 2.02 must be such that ANY two version 2 implementations must be able to communicate without problems. 

[So you require back-compatibility between "major" versions number before the
dot changing] and both-ways compatibility between "minor" versions? -- DEC
jargon]

##  Aims

In a new version of HTTP, there can be added features, but there can also be a
lack of deprecated ones. Communication between a browser using version n and a
server using version m should in some sense be possible.

It is reasonable to require that an agent using version n+1 also still knows
how to handle version n but does not have to know version n-1.

##  Forwards

There are three disjoint elements:

  * the WWW data model, which today consists of documents which may have explicit links and/or be queryable with text-based queries. [Was: maybe I'd prefer to call data bases, since an index is a reference table built from a data base to ease access to it)." An index can be many [things](https://www.w3.org/DesignIssues/WhatIsAnIndex.html) ] There is no reason why other types should not be added, such as time-indefinite communications (eg. a telnet session, TV or process control).[Is this really different from a document?] 
  * the HTTP protocol, which should be defined outside the document contents. It needs to evolve and expand. 
  * the HTML markup which is today the only implemented format we accept for the document contents. Here certainly we want more. 

The next releases should distinguish these cleanly. One way is to talk HTTP
over a control connection and documents over a data connection.

##  Pragmatism

Having suggested a split of control and data, I realise that at present this
is too much, and so we must keep going on one connection. [Ample justification
for this is the difference in reponse time from HTTP servers and FTP servers
-- the latter using 2 connections] That implies though that we must do our own
transmission protocol inside HTTP, ie. when we send, say, binary data, then
because we mix HTTP and data on the same connection, we have to do things
inside HTTP like "here follows 3406 bytes of binary data" because otherwise we
are not guaranteed to be able to distinguish between HTTP controls and
document data.

##  Proposed modifications

###  Version 1.0:

The HTTP version number is sent in every communication, by the browser after
the argument to GET, by the server in a tag at the start. [I don't see the
reason for this version.]

###  Version 2.0:

The HTTP version number is sent at the start of every communication.

The HTTP commands are not in HTML; however, they are mixed in with the data
stream. [I would say they envelop the data stream. I think it is important to
keep the TOEOF style as an option because it is so practical]

See also [problems to solve](https://www.w3.org/DesignIssues/ProtocolProblems.html) , a way of communicating
[with different versions](https://www.w3.org/DesignIssues/Protocolcomms.html) and a
[proof](https://www.w3.org/DesignIssues/CompatibleProof.html) that the new version is backwards compatible.

