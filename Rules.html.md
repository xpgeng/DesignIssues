Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:09 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Axioms of Web Architecture: n

* * *

#  Rules and Facts: Inference engines vs Web

At at attempt to explain explain part of the relationship between the Semantic
Web and inference engines, either existing or legacy, and discuss the
relationship between inference rules and logical facts.

The Semantic Web is a universal space for anything which can be expressed in
classical logic. In the world of knowledge Representation (KR) there are many
different systems, and the following is an attempt to generalize.

Each system typically has a distinction between data and rules. The data is a
pool of information in one language (sometimes very simple without negation
like basic RDF) . The rules control the inference steps which the inference
engine makes. The rules are written in a restricted language so as to preserve
some property computability property. Algernon restricts its rules to forward
chaining but assures Socratic completeness.

When integrating rules with the semantic web, one must realize that a rule
contains two separate pieces of information. Take a rule in a certain
inference system

g(a,c) |= d(a,b) &amp; d(b,c)

which is defined to mean "whenever you find a new relationship where any a is
the daughter of some b, then if for that b there is any c for which b is the
daughter of c, then conclude that a is the granddaughter of c". Here,
"conclude" means add to the database. This is a procedural instruction.

It involves an out-of band decision (may by a person) as to whether all
granddaughter relationships should be added to the database the moment they
can be, or whether the relationship would only be used at a time when a query
is made. This rule can be exchanged between two inference engines of the same
type, but it does not as a rule make sense to anyone else.

In fact, of course, this rule would be nonsense if it were not for the fact in
classical logic that

Va,b,c g(a,c) &lt;= d(a,b) &amp; d(b,c)

This fact, unlike the rule, can be directly expressed in the semantic web
language. When the rule is used in deducing something, it is this fact which
is a step input to the proof. Every semantic web proof validator will be able
to handle it.

Exposing rules as classic logic facts strips the (pragmatically useful) hint
information which controls the actual sequence of operation of a local
inference engine. When the facts corresponding to all the rules of all the
inference engines are put onto the web, then the great thing is that all the
knowledge is represented in the same space. The drawback is that there is no
one inference engine which can answer arbitrary queries. But that is not a
design goal of the semantic web. The goal is to unify everything which can be
expressed in classical logic (including more mathematics when we get to it)
without futher constraint. We must be able to describe hte world, and our
hopes and needs and terms and conditions. A system which tries to constrain
the expressive power cannot be universal.

##  Non-monotonic "logics"

Now there are some systems which in fact use classical logic directly, and
others, "non-monotonic logics" in which adding a fact can change something
which was previously "believed true" to being "believed false". (Describing
them as logics may be regarded by some as questionable). For example, given
that "birds can fly", the system will believe that Pingu can fly because Pingu
is a penguin and a penguin is a bird, unltill it is told that penguins can't
fly. Then it will assume that all birds can fly excpt for penguins. Such
systems use concepts of "defaults" -- things to be assumed unless one is told
otherwise. They are fundamentally closed-world systems, in that the concept of
"belief" is alway implicitly make with respect to a given closed set of facts.

One can export such information into the semantic web in two ways. One can
export the rule system specifically, ending up with a statement of the form
"there is as assertion of birds being able to fly which is is unchallenged in
the xxxx corpus by any assertion contradicting that which applied to birds or
any otehr superclass of penguins". This effectivly is a reification of the
non-monotonic system, an analysis not of penguins but of the inferenc system
and what its state is. This may be so unweildly that it is only useful by
systems which use th same inference system. The second way to export the data
is to just record the classical logic statement as the output of the inference
engine. "The xxxx system has output that Pingu can fly.". In certian cases, a
system might risk incorporating such statements into a classic inference
system. This is the logical equivalent of declaring, "Well, I don't think such
a book exists becase it wasn't in Blackwell's catalog". We do things all the
time, but a secure system is unlikely to be set up to incorporate such
information. (A more secure system would for example, given the publisher and
year, find a definitive list from the publisher of books published in that
year, which would allow it to proove that such a book did not exist.)

The choice of classical logic for hte Semantic web is not an arbitrary choice
among equals. Classical logic is the only way that inference can scale across
the web. There are some logics which simply do not have a consistent set of
axioms - fuzzy logic, for example, tends to believe something to a greater
extent as a funcion of how often evidence for it has been presented. Closed
world systems don't scale because the refernce to the scope of a defualt is
typically implicit, and different from one fact to another. When a fact is
presented as a fact, the "Oh yeah?" function of demanding justification can be
satsfifed by a roof in a universal language of proof. non-classical heuristic
systems may have been used to discover the proof, but onec the proof has been
found it can by checked as valid by any semantic web system.

In the diagram, I have put heuristic systems above the semnatic web bus, and
classical systems below. In Weaving the Web later chapters I try to describe
the importanc of the web in supporting both types of system.

* * *

[thanks to Lynn Stein/LCS for raising and largely answering the question of
non-monotonic logics]

##  Inconsistent data

What, they say, will happen when this huge mass of classical logic meets its
first inconsistncy? Surely, once you have one staement that A and another
somewhere on the web that not A, then doesn't the whole system fall apart?
Surely, then you can deduce anything?

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

A real system may work backwards or forwards (or both). I would call working
forwards a system which is given a configuartion page to work from which in
turn points to other pages which in turn are used as valid data. I would call
working backwards a system which, when looking for an answer to a query, looks
at a gloal index to find any document at all which mentions a given term. It
then searches thes documents turned up for answers to the query. Only when it
has found an answer does t check back to see whether the data can be deriveded
directly or indirectly from sources it has been set up to trust.

Digital sgnature (see trust) of cours adds a notion of secuirty to the whole
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

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

