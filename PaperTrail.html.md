Tim Berners-Lee

Date: February 1999. Last modified: $Date: 2004/04/20 19:21:17 $

Status:

An example of how a social machine can be made without a center. Editing
status: Draft. Comments welcome

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Ideas about future Web architecture

* * *

#  Paper Trail

Here we look at the relationship between documents (living or dead but
basically bits of state) and messages (events with associated data, including
typically but not essentially sender and recipient).

Here is a proposal for a project: "Paper trail" state machine for workflow.
The concept here is that the state of any transaction is in the real world
(and in this formalization in the Web) just a function all the messages which
form part of a protocol.

> ###  Epilogue (2001/05)

>

> The [Web Services workshop](https://www.w3.org/DesignIssues//2001/01/WSWS), in discussing transactios over
the Net, surfaced the need for process flow descriptions

>

> ###  Update (2004/03)

>

> The [Semantic Web Application Platform (SWAP)](https://www.w3.org/DesignIssues//2000/10/swap/) now has
enough functionality to implement these ideas. see [ppt-bank](https://www.w3.org/DesignIssues//2000/10/swap
/ppt-bank/), especially [checking.n3](https://www.w3.org/DesignIssues//2000/10/swap/ppt-bank/checking.n3)

##  Introduction

Social processes look like state machines. However, they don't exist as a
state variable stored in one place, but as a trail of documents. You know the
true state of the machine only if you have access to the latest documents.
(This is not the problem addressed here, this is real life being modelled.)
_Paper-trail_ is a system which allows one to follow a strict process by
creating new documents in a constrained fashion. Every paper-trail document
has a pointer to a "paper-trail schema" which defines its document type (eg
"constitutional amendment") a pointer to its justification documents (maybe) a
notarization of when it was checked against the schema by the paper-trail
program. The schema defines:

  * Prerequisites for a document being valid, in terms of other documents 
  * Hints to other document types you can make from this one (state transitions) 

###  Example

> To make a new W3C working draft, the schema requires pointers to old working
draft new document, and editor's authorization. The editor must be defined as
editor on home page of working group where working group page is pointed to be
by old draft. If all those exist, then the new document is created from all
that and notarized (time stamped) by the software. The human readable part of
the document is created as a (simple macro) function of the input documents. A
document also has a buttons to take you to a form to turn it into another type
of document according to hints in the schema.

###  Example

> A button on a Working Draft takes you to a form for promoting it to a
"proposed recommendation". This requires different things (all the above plus
endorsement of new draft by director or any two members of the management
group.)

##  Technology

If you are considering this as a student project, consider these directions:

  * Use RDF within the document to express its state. 
  * Develop declarative language for defining the prerequisites - ideally in RDF too. 
  * Develop GUI for creating a new document by supplying the prerequisites 
  * Allow hooks for digital signature but don't have to implement it 

##  Generalizing for formal protocols

The concept of a paper trail is common in conventional administration, but the
model can also be applied to well-defined computer protocols.

##  Model

The model is that a protocol P defines a status sn as a function of a message
m and a previous state sn-1, and the time t.

sn= P(mn, sn-1, t)

or for that matter as a function of all the messages to date

sn= P'({mi}i=1..n)

The state could be a logical formula, an RDF graph, or an XML document, or
just a number, in decreasing order of interest. The system can be a any one of
a number of types of machine, including the well-known finite state machine
and push-down automata.

In an XML world, think of the state and the messages all being expressed in
XML, and the protocol maybe being an XSLT script.

The state must record everything necessary for calculating future states for
any new message. It could also record the results of the protocol. For
example, the state of TCP (where IP packets are the {m} ) must hold the state
of the packets unacknowledged in the sliding window, but when the connection
has been successfully closed it could hold either just "terminal state", or
also the ordered set of bytes transferred in the connection.

The protocol function can be seen as an information destroying function. By
specifying what needs to be remembered, it defines what can be thrown away.
This is of course very important. Of course, one might in some cases still
want to spool the messages for security, but the actual information needed to
describe the state of affairs is limited..

Typically, to be valid, messages will link back to previous messages either
directly or though common threading identifiers of some sort. A message
without such a reference will in most cases not have any effect on the state.

There will in general be error states, which the protocol does not allow,
which any message which is invalid in some way will lead to. Functionally
there need only be one error state but in practice one might want t preserve
the state before the error and details of the error. Some protocols model most
errors themselves by sending.

There must obviously be a set M0 of valid ways to start a protocol in the
first case from the generic initial state s0. For example, in TCP one sends a
SYN message; on the telephone one picks up the receiver. For any m in M0, P(m,
s0) will be a valid (non-error) state.

There will in some systems be a set of F final states, in which no further
messages can have any effect on the state. For any s in F, P(m,s) = s for all
m.

For example, in the US, when 7 years have passed since a transaction occurred,
then all records may be discarded as no one even the tax man has the right to
query them. The state is reduced to a minimum. Most systems can be modelled in
a simple of complex way, the simple way ignoring a lot of the auditing
processes for example. A simple model of a loan between two people has a state
which is the balance amount and one final state when that is zero. Other
systems are designed to remain in non-final state: a lifetime warranty is a
protocol which remains in non-final state (until you die!), waiting for any
message that you are dissatisfied with the product.

Real system are part of bigger systems, and so the real protocol will function
as part of a larger protocol. For example, a working group at W3C goes though
many internal state changes, and (on a simple model) the last is when their
work is accepted by the Consortium as a whole as a Recommendation. This is a
message leaving the system, which forms part of the larger protocol. Modeling
this is clearly interesting. (To demonstrate this nesting by an example of it
breaking, think of the case of a working group not arriving at consensus and
passing on not only a final document but also a minority report, basically a
peek into the internal workings of the group which did not in fact arrive in
its final state. ) This would include modelling tasks which can split, and be
recursively delegated, and so on.

##  Cool things

This system can allow well-defined social processes to work eg on a net
newsgroup, or by email. ie, it works in a write-only medium.

It models real life in commerce well, where the state really is an abstract
thing and one's perception of it depends on the set of messages one has had
access to.

Hopefully we can use this model to define systems which are even more
powerfully distributed than any we use at the moment.

##  Linking Remote operations and Data Formats

I must have discussed the relationships between remote operations and data
formats before. Maybe I have made a table with schema languages compared
against interface definition languages, and so on.

Now we have a clear way of expressing the relationship between the two. A
Protocol definition document defines a document as a function of messages,
which can be represented as documents - so we can look at remote operations in
terms of documents. Typically RPC messages are very constrained: this model
allows much more complicated multi-party protocols to be defined.

##  Challenges if you finish early

If making a paper trail machine was fun, here are some more ideas.

  * Add time-aware social processes such as promises and timeouts. 
  * Do you need to be able to prove non-existence of documents? 
  * Locally to an author or globally? 
  * States can split. (draft can go to W3C or IETF process or both). 
  * How can you limit this, when socially undesirable?) 
  * Develop proofs that processes will achieve given ends. 
  * Model processes near you: 
    * auction 
    * peer review journal 
    * presidential impeachment ;-) 
    * internet newsgroup creation 
    * formation of a company 
    * MIT purchasing (possible PhD thesis ;-) 
  * Develop theories in which players are 
    * collaborative 
    * competitive 
    * allowed to create new schemas to achieve their ends 
  * Model existing systems near you: 
    * TCP 
    * HTTP... 
  * Develop a protocol machine, which, acting on behalf of one agent, will determine when that agent has a possible move to make, and when in fact the protocol is acting for that agent. Develop a GUI which helps a human user chose from the set of possible options at that state of the protocol. 

##  Products

The thing which would come out of this idea would I imagine be a standard
language for writing protocols. Of course, it would mainly be something else,
such as an rdf-logic language, or prolog or whatever, but there would have to
be hooks to define it to be a definition of a protocol.

This takes the self-describing web concept into a new area: that messages are
self-describing in that they contain a pointer to the language in which they
are written, and that includes (or points to) the protocol to which they claim
to adhere.

@@ Add pointers to work done with Notation3

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html);

Thanks for some fun discussions with Dan Connolly about these ideas.

