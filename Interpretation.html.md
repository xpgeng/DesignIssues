Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $  
Status: personal view only. Editing status: first draft.

(I am sorry that the terms here probably do not correspond to those
conventionally used in the field of philosophy)

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Axioms of Web Architecture: n

* * *

#  Interpretation and Semantics on the Semantic Web

We need some philosophy as a basis for the architecture of digital signature
and the semantic web.

The semantic web is a computer system, a distributed machine which should
function so as to perform socially useful tasks. There will be various
interfaces between the Semantic Web (SW) world and the social world of people,
such as the physical delivery of goods, and the presentation of a document to
a person for signature. However, in general with these important exceptions
the Semantic Web will form a self-sufficient loop. The semantics of anything
on the SW are then defined either in terms of more stuff on the SW, or in
terms of the connection with these real-world connections. So for example I
might initially define a check as something which when fed into the bank's
black box will make it do a certain thing. Then within the SW all definitions
of dollars and transfers can be defined back in terms of the check, and a
self-sufficient system can be made where is necessary the recourse can be made
to sending a check to a bank, but in fact we can etrade using ecurrency and
einvoices and edeliverynotes and so on.

This is a similar relationship with reality that coins originally had with
gold, and bills with coin. (A UK pound used to read "I promise to pay the
bearer on demand the sum of one Pound signed, signed: Bank of England"). From
then on a pound note became what people thought of as a pound, and the notion
of what exactly the "sum of one pound" was originally defined by becomes
irrelevant and the paper money is self-sufficient. So we are making a computer
system which will function as a machine which does a process quite equivalent
to (though perhaps more crisply defined than) a social process such as trade
or endorsement.

We use the applications which tie the SW to what we currently think of as
reality for three reasons:

  1. We need an interface between the SW and the current social systems that is how the SW system will work at least initially. 
  2. The social system machine has legislative backing (and public understanding etc.) which we want to exploit; 
  3. The social system we have works and we only want to change the machine incrementally. 

Our reason is _not_ that the current definitions are fundamental or because
their specification is inherently beautiful (indeed many existing systems are
really crufty). Importantly, we do _not_ define the semantics of something to
the real world in such a way as to break the loop, when the loop can be
completed in the SW. Here is an example of a loop in the semantic web.

  * a. Web server grants access to resource d in response to request is signed with key k1. 
  * b. key k1 is listed in a [employee list] document signed with k2; 
  * c. Key k2 is listed in a [w3c member] list signed with k3; 
  * d. Key k3 is the key with which the web server was set up to trust 

This little system can happily run controlling our web site. Now in fact we
set it up to model the following social system

  * A. A person P1 is allowed to read the member site 
  * B. The person P1 is an employee of company C2 
  * C. C2 is a member of the consortium according to Hugo; 
  * D. Hugo is deemed responsible when it comes to defining member site access. 

Now to represent the SW loop a-d is very simple. The conditions can be written
in math and proved. The social loop A-D as written is always a rough
approximation to the very complex web of trust which is often less dependable
than the simpler SW model.

Security has always been plagued by people trying to connect the SW steps
(such as a-d) at every stage to the social machine (A-D). For example, this
would raises the question of how to identify the person P1 with key k1,
introducing the quite unnecessary x.500 directory system which is really not
part of the trust loop but becomes a security hole, bringing in unnecessary
"trusted" third parties. It drags up endless questions of what "identity"
really is anyway. It would raise the question of whether it is Hugo or the
webmaster or what that is associated with K3. Before we had finished arguing
about identity we would be into arguments about "belief". We would be arguing
as to whether Hugo really _believes_ that the person is a member of the
company - maybe Hugo does not have to but in his webmaster role he does! These
are rat holes. (People don't just belive things to believe to a certain
extent, they trust certain source for certain purposes). It would be best to
use a different term ("interpretation"?) for the mapping between the semantic
and real worlds. (I probably haven't got the philosophical terms right at all
and I haven't said "model" once)

So what happens, after we have installed our web server access protocol based
on digital signature, is that we then relate things to that. We say that
invited experts can get have keys on a given list. The semantic web becomes
the definitive machine, and we just have rules at the edges about how it
related to things like membership payments. An invited expert becomes defined
as someone whose key is on a given list.

What we are looking for from a digital signature spec is the relationship
between a signature and a string of bits, and what we are looking for from a
semantic web toolbox is the language for writing the conditions a-d. We are
NOT looking for either to provide and interpretation language for relating a-d
to A-D, ora legal language for writing the steps A-D.

Now, the much-asked question, what is the "semantics" of the digital signature
in a-d above? From the SW point of view, those rules are the semantics of the
system. The whole thing is self-sufficient from the machine's point of view,
except for the edges where the server has to understand what to "give access"
is, and where the person has to sign a request or a list. The great thing
about the semantic web is that we can make it all work and never actually
answer the questions "invited" in what sense? by whom? and Does this mean an
invitation which has been accepted? and such other rat holes. We must be
careful not to confuse what is said with where it is stored There rare
basically four rules which define the access machine. We could store them
anywhere. They could be sent in an HTTP request, stored on any number of
different web sites, in Java rings and smartcards, send by email or etched in
marble. The SW design must not constrain where things are stored.

Where do the "sematics of the signature" lie?

The semantics in the SW are for me the whole loop a-d, which you see, to be a
loop, and therefore to allow any processing, must eventually be tried down to
the key. When you start to argue something on the basis of a signature by a
key, they only next step can be some knowledge about the key. In the semantic
web, this is a processing rule about things which are signed with that key.
However, that does not mean that the signature has semantics which stored
as/with/about the key. In fact, I do not think it is useful to talk about the
"semantics of the signature.

Documents have meaning. Signatures by themselves do not.

So it is not useful to ask what the semantics of a signature are. Signatures
convey trust, but even that because of a set of statements about keys and
documents. There are in society many rules about the trust which is conveyed
by the signature under various circumstances. We should not attempt to model
those when we make the basic infrastructure of the semantic web.

* * *

Initially created 1999/12/01

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

* * *

####  Reference fodder

[14:31] * DanC goes surfing for BAN logic and surreptitiously finds a hit in
ietf-tls from Oct 1996 http://lists.w3.org/Archives/Public/ietf-
tls/msg02632.html [14:33] &lt;DanC&gt; see also: "A Logic of Authentication"
(aka BAN logic) http://gatekeeper.dec.com/pub/DEC/SRC/research-
reports/abstracts/src-rr-039.html

