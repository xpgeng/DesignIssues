Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $ $Author: timbl $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  The Semantic Web as a language of logic

This looks at the Semantic Web design in the light a little reading on formal
logic, of the Access Limited Logic system, in particular, and in the light of
logical languages in general. A problem here is a that I am no logician, and
so I am am having to step like a fascinated reporter into this world of which
I do not possess intimate experience.

##  Introduction

The [Semantic Web Toolbox](https://www.w3.org/DesignIssues/Toolbox.html) discusses the step from the web as
being a repository of flat data without logic to a level at which it is
possible to express logic. This is something which knowledge representation
systems have been wary of.

The Semantic Web has a different set of goals from most systems of logic. As
Crawford and Kuipers put it in [Crawf90],

> [...]a knowledge representation system must have the following properties:

>

>   1. It must have a reasonably compact syntax.

>   2. It must have a well defined semantics so that one can say precisely
what is being represented.

>   3. It must have sufficient expressive power to represent human knowledge.

>   4. It must have an efficient, powerful, and understandable reasoning
mechanism

>   5. It must be usable to build large knowledge bases.

>

>

> It has proved difficult, however, to achieve the third and fourth properties
simultaneously.

The semantic web goal is to be a unifying system which will (like the web for
human communication) be as un-restraining as possible so that the complexity
of reality can be described. Therefore item 3 becomes essential. This can be
achieved by dropping 4 - or the parts of item 4 which conflict with 3, notably
a single, efficient reasoning system. The idea is that, within the global
semantic web, there will be a subset of the system which will be constrained
in specific ways so as to achieve the tractability and efficiency which is no
necessary in real applications. However, the semantic web itself will not
define a reasoning engine. It will define valid operations, and will require
consistency for them. On the semantic web in general, a party must be able to
follow a proof of a theorem but is not expected to generate one.

(This fundamental change goals from KR systems to the semantic web is loosely
analogous with the goal change from conventional hypertext systems to the
original Web design dropping link consistency in favor of expressive
flexibility and scalability.The latter did not prevent individual web sites
from having a strict hierarchical order or matrix structure, but it did not
require it of the web as a whole.)

If there is a _semantic web machine_, then it is a proof validator, not a
theorem prover. It can't find answers, it can't even check that an answer is
right, but it can follow a simple explanation that an answer is right. The
Semantic Web as a source of data should be fodder for automated reasoning
systems of many kinds, but it as such not a reasoning system.

Most knowledge representation systems distinguish between inference "rules"
and other believed information. In some cases, this is because the rules (such
as substitution in a formula) cannot be written in the language - they are
defined outside the language. In fact the set of rules used by the system is
often not only formally quite redundant but arbitrary. However, a universal
design such as the Semantic Web must be minimalist. We will ask all logical
data on the web to be expressed directly or indirectly in terms of the
semantic web - a strong demand - so we cannot constrain applications any
further. Different machines which use data from the web will use different
algorithms, different sets of inference rules. In some cases these will be
powerful AI systems and in others they will be simple document conversion
systems. The essential this is that the results of either must be provably
correct against the same basic minimalist rules. In fact for interchange of
proof, the set of rules is an engineering choice.

There are many related ways in which subsystems can be created

  * The semantic web language can be subsetted, by the removal of operations and axioms and rules; 
  * The set of statements may be limited to that from particular documents or web sites; 
  * The form of formulas used may be constrained, for example using document schemata; 
  * Application design decisions can be made so as to specifically guarantee tractable results using common reasoning engines. 
  * Proofs can be constructed by completely hand-built application-specific programs 

For example, Access Limited Logic is restricted (as I understand it) to
relations r(a,b) available when r is accessed, and uses inference rules which
only chain forward along such links. There is also a "partitioning" of the Web
by making partitioning the rules in order to limit complexity.

For the semantic web as a whole, then, we do require tractable

  * Consistency, that it must not be possible to deduce a contradiction (without having been given one) 
  * Strength in that all applications must be subsets 

###  Grounding in Reality

Philosophically, the semantic web produces more than a set of rules for
manipulation of formulae. It defines documents on the Web has having a
socially significant meaning. Therefore it is not simply sufficient to
demonstrate that one can constrain the semantic web so as to make it
isomorphic to a particular algebra of a given system, but one must ensure that
a particular mapping is defined so that the web representation of that
particular system conveys is semantics in a way that it can meaningfully be
combined with the rest of the semantic web. Electronic commerce needs a solid
foundation in this way, and the development of the semantic web is (in 1999)
essential to provide a rigid framework in which to define electronic commerce
terms, before electronic commerce expands as a mass of vaguely defined
semantics and ad hoc syntax which leaves no room for automatic treatment, and
in which the court of law rather than a logical derivation settles arguments.

Practically, the meaning of semantic web data is grounded in non-semantic-web
applications which are interfaced to the semantic web. For example, currency
transfer or ecommerce applications, which accept semantic web input, define
for practical purposes what the terms in the currency transfer instrument
mean.

##  Axiomatic Basis

_@@I [DanC] think this section is outdated by recent thoughts [2002] on_
_paradox and the excluded middle_

To the level of first order logic, we don't really need to pick one set of
axioms in that there are equivalent choices which lead to demonstrably the
same results.

(A cute one at the propositional logic level seems [Burris, p126] to be
Nicod's set in which nand (in XML toolbox &lt;not&gt;..&lt;/not&gt; and below
[xy]) is the Sheffer (sole) connective and the only rules of inference are
substitution and the _modus ponens_ equivelent that from F and [F[G H]] one
can deduce H, and the single axiom [[P[QR]][[S[SS]][[UQ][[PU][PU]]]].)

Let us assume the properties of first order logic here.

If we add anything else we have to be careful that it should either be
definable in terms of the first order set or that the resulting language is a
subset of a well proven logical system -- or else we have a lot of work to do
in establishing a new system!

##  Intractability and Undecidability

These are two goals to which we explicitly do not aspire in the Semantic Web
in order to get in return expressive power. (We still require consistency!).
The world is full of undecidable statements, and intractable problems. The
semantic web has to give the power to express such things.

Crawford and Kuipers The same explain in the introduction their Negation in
ALL paper,

> "Experience with formally specified knowledge representation systems has
revealed a trade-off between the expressive power of knowledge representation
systems and their computational complexity. If, for example, a knowledge
representation system is as expressive as first order predicate calculus, then
the problem of deciding what an agent could logically deduce from its
knowledge base is unsolvable"

Do we need in practice to decide what an agent could deduce from its logic
base? No, not in general. The agent may have various kinds of reasoning
engine, and in practice also various amounts of connectivity, storage space,
access to indexes, and processing power which will determine what it will
actually deduce. Knowing that a certain algorithm may be nondeterministic
polynomial in the size of the entire Web may not be at all helpful, as even
linear time would be quite impractical. Practical computability may be assured
by topological properties of the web, or the existence of know shortcuts such
as precompiled indexes and definitive exclusive lists.

Keeping a language less powerful than first order predicate calculus is quite
reasonable within an application, but not for the Web.

##  Decidability

A dream of logicians in the last century to find languages in which all
sentences were either true or false, and provably so. This involved trying to
restrict the language so as to avoid the possibility of (for example) self-
contradictory statements which can not be categorized as a true or not true.

On the Semantic Web, this looks like a very academic problem, when in fact one
anyway operates with a mass of untrustworthy data at any point, and restricts
what one uses to a limited subset of the web. Clearly one must not be able to
derive a self-contradictory statement, but there is no harm in the language
being powerful enough to express it. Indeed, endorsement systems must give us
the power to say "that statement is false" and so loops which if believed
prove self-contradictory will arise by accident or design. A typical response
of a system which finds a self-contradictory statement might be similar to the
response to finding a contradiction, for example, to cease to trust
information from the same source (or public key).

###  Reflection: Quoting, Context, and/or Higher Order Logic

_@@hmm... better section heading? maybe just quoting, or contexts? one place
where we really do seem to need more than HOL is induction._

The fact that there is [Burris p___] "no good set of axioms and rules for
higher order logic" is frustrating not only in that it stumps the desire to
write common sense mathematically, but also because operations which seem
natural for electronic commerce seem at first sight to demand higher order
logic. There is also a fundamental niceness to having a system powerful enough
to describe its own rules, of course, just as one expects to be able to write
a compiler for a programming language in the same language _(@@need to study_
[ _references from Hayes_](http://lists.w3.org/Archives/Public/www-
archive/2002Apr/0057.html)_, esp "Tarski's results on meta-descriptions (a
consistent language can't be the same expressive power as its own metatheory),
Montague's paradox (showing that even quite weak languages can't consistently
describe their own semantics)"_. When Frege tried second-order logic, I
understand, Russel showed that his logic was inconsistent. But can we make a
language in which is consistent (you can't derive a contradiction from its
axioms) and yet allows enough to for example:-

  * Model human trust in a realistic way 
  * Write down the mapping from XML to RDF logic to allow a theorem to be proved from the raw XML (and similarly define the XML syntax in logic to allow a theorem to be proved from the byte stream), and using it; 

The sort of rule it is tempting to write is such as to allow the inference of
an RDF triple from a message whose semantic content one can algebraically
derive that triple.

    
    
    forall message,t, r, x, y (
      (signed(message,K)
        & derivable(t, message)
        & subject(t, x)
        & predicate(t, r)
        & object(t, y))
       -> r(x,y)
    )
    

(where K is a specific constant public key, and t is a triple)

This breaks the boundary between the premises which deal with the mechanics of
the language and the conclusion which is about the subject-matter of the
language. Do we really need to do this, or can we get by with several
independent levels of machinery, letting one machine prepare a "believable"
message stream and parse it into a graph, and then a second machine which
shares no knowledge space with the first, do the reasoning on the result? To
me this seems hopeless, as one will in practice want to direct the front end's
search for new documents from the needs of the reasoning by the back end. But
this is all hunch.

Peregrin tries to categorize the needs for and problems with higher order
logic (HOL) in [Peregrin]. His description of Henkinian Understanding of HOL
in which predicates are are subclass of objects ("individuals") seems to
describe my current understanding of the mapping of RDF into logic, with RDF
predicates, binary relations, being subclass of RDF nodes. Certainly in RDF
the "property" type can be deduced from the use of any URI as a predicate:

forall p,x,y p(x,y) -&gt; type(p, property)

and we assume that the "assert" predicate &lt;rdf:property&gt; is equivalent
to the predicate itself.

forall p,x,y assert(p,x,y) &lt;\--&gt; p(x,y)

so we are moving between second-order formulation and first-order formulation.

(2000) The experience of the [PCA] work seems to demonstrate that higher order
logic is a very realistic way of unifying these systems.

(2001) The treatment of contexts in [CLA] seems consistent with the design
we've implemented.

##  Induction, primitive recursion, and generalizing to infinitely many cases

It seems clear that FOL is insufficient in that some sort of induction seems
necessary.

> I agree with Tait (Finitism, J. of Philosophy, 1981, 78, 524-546) that PRA
is THE NECESSARY AND SUFFICIENT logic for talking about logics and proofs

>

> [ Robert S. Boyer, 18 Apr
93](http://theory.stanford.edu/people/uribe/mail/qed.messages/22.html)

also: [pra.n3](https://www.w3.org/DesignIssues//2001/03swell/pra.n3), an N3 transcription of [Peter Suber,
Recursive Function
Theory](http://www.earlham.edu/~peters/courses/logsys/recursiv.htm)

also: ACL2: [ A Precise Description of the ACL2
Logic](http://www.cs.utexas.edu/users/moore/publications/km97a.ps.gz) Kaufmann
and [Moore](http://www.cs.utexas.edu/users/moore/) 22 Apr 1998, [ rdf
scratchpad entry
26Mar](http://rdfig.xmlhack.com/2002/03/26/2002-03-26.html#1017177958.271019)

(for another sort of induction, i.e. as opposed to deduction, see:
[Circumscription](http://www-formal.stanford.edu/jmc/circumscription.html) by
McCarthy, 1980.)

* * *

##  Yet to be addressed (1999)

I personally need to understand what the limitations are on higher order
logics...and which are hard limitations and which are unresolved areas.

Was Frege's formulation of second order logic (which should be of course a
formulation of common sense) buggy in that Russel found it could derive a
contradiction, or are we really finding it is not possible to represent a
mathematical system to follow common sense reasoning? Yes, Frege seems to have
used the classical logic in which any proposition must be true or false.

When we say that there are valid sentences which cannot be derived - what
exactly do we mean by "valid"? In predicate logic, validity can be defined by
a truth table, ie evaluation for all truth evaluations of the variables
[Burris]. In fact this method equates to a resolution by mapping algebraically
into disjoint (say) normal form, and so is not an operation "outside" the
language. In any logic with unbounded sets this is not practical. Typically we
fall back on some logic such as common sense outside the language under
discussion. In higher order logic, intuition suggests we should be able to to
construct such a proof of validity in the logic itself. Goedel's
incompleteness theorem specifically addresses the difference between validity
and derivability, so perhaps a good exposition of that [DanC recommends The
Unknownable@@]would contain the necessary distinctions.

I wonder whether the answers can be found on the web...

After a hallway chat with Peter SP-S, DMAL meeting 2001/2/14:

The paradox problem lies not simply in being able to express a paradox, but
the logic being such that merely considering a paradox leads one to be able to
deduce a falsehood. One can take issue then, with either the ability to
express the paradox, or with the "p or not p" axiom. Logics which try to get
above first order logic can be divided into two groups in this way. There are
sets of logics which use sets, but limit them in some way - for example, by
requiring sets to be "well formed", meaning they are either empty or contain
at least one element which is disjoint with the set itself. These tricks limit
the logic so that you can't in fact have the Russel paradox set (of all sets
which are not members of themselves) as you exclude such things as not well-
formed. As Peter admitted, on the web it seems silly to use this route when
people will be expressing paradoxes.

The other route alsob has many followers. Some of them are, people say,
complicated. But it seems that the path can only be in that direction.
Meanwhile, back at the ranch, I notice that most of the semantic web
applications I have been playing with involve rules and axioms which are not
at all complete. Each application has its own sets of axioms and can be
individually proved consistent (or not). So one way forward for standards
would be to instantiate that, allowing each document and message on the
semantic web to have a pointer to the vocabulary its uses, including its
varieties of logical connectives and their assocaited axioms.

@@@

[](http://www.altavista.com/)

Mapping RDB and SM models - defining URIs; nulls; etc.

##  On reasoning from contradictions and the excluded middle

_@@prose_

Pat Hayes mentioned a logic in which the law of the excluded middle does not
exist - which si important as you can always considera paradox which is
neither true nor false. See email 2000/09/01

> I think that a more suitable 'basic' logic might be generalized horn clause
logic. This is similar to the horn-clause subset of FOL which is used in logic
programming, but instead of full negation (which is computationally expensive)
or negation-by-failure (which is cheap but grubbily nonmonotonic), it uses an
elegant intermediate idea called intuitionistic (or constructive) negation
(which is like full negation but rules out proofs by contradiction: basically,
it insists on a higher standard of provability than classical negation. In
intuitionistic reasoning, Holmes' famous advice about eliminating the
impossible does not always apply.) It is computationally tractable, completely
monotonic, and has a neat, elegant semantic theory behind it. It escapes some
of the limitations of Horn logic while retaining a lot of its advantages. Its
been implemented and seems to have been applied to some neat applications. It
might be just what you need. For details see [the
papers](http://citeseer.nj.nec.com/hogan98putting.html) at
http://citeseer.nj.nec.com/hogan98putting.htmlhttp://citeseer.nj.nec.com/hogan98putting.html,
especially [the 1996 "meta-
programming...."](http://citeseer.nj.nec.com/158146.html) and the [main
citation at the top](http://citeseer.nj.nec.com/hogan98putting.html). For the
raw logic follow the McCarty 88 references.

quoted without permission. DanC recommends [Non-Contradiction and Excluded
Middle](http://www.earlham.edu/~peters/courses/logsys/pnc-pem.htm) in Peter
Suber's [Logical
Systems](http://www.earlham.edu/~peters/courses/logsys/lshome.htm) course
notes as an explanation of intuitionistic logic. TimBL noted the same bit that
I did on first reading:

> In the world of metamathematics, the intuitionists are not at all exotic,
despite the centrality of the PEDC (hence the PEM) to the ordinary sense of
consistency. Their opponents do not scorn them as irrationalists but, if
anything, pity them for the scruples that do not permit them to enjoy some
"perfectly good" mathematics.

_is socratic completeness, as in [__Crawf90__], directly relevant? hmmm@@_

solutions to paradoxes around wtr in KIF: [ complex one in
KIFv3](http://meta2.stanford.edu/kif/Hypertext/node35.html#SECTION00093000000000000000),
[simpler, more limited one in later KIF
spec](http://logic.stanford.edu/kif/dpans.html#10.3). ([KIF/RDF
stuff](https://www.w3.org/DesignIssues//2000/07/hs78/KIF.html) from Jul 2000)

* * *

##  References

[PCA] Proof-Carrying Authentication. Andrew W. Appel and Edward W. Felten, 6th
ACM Conference on Computer and Communications Security, November 1999.
([background](http://www.cs.princeton.edu/sip/projects/pca/)) [ Mar 2000
discovery](http://lists.w3.org/Archives/Public/sw99/2000JanMar/0005.html).
based on [LF]

[Burris] Stanley N. Burris, Logic for Mathematics and Computer Science,
Prentice Hall 1998.

[BurrisSup][Supplementary text to the
above](http://thoralf2.uwaterloo.ca/htdocs/stext.html).

[Cheng] The ERM model paper, available in [Laplante]

[ConnollySoLREK] [Dan Connolly's home page for this sort of stuff. "A Study of
Linguistics: Representation and Exchange of
Knowledge"](https://www.w3.org/DesignIssues//Collaboration/knowledge).

[Crawf90]

> [ ALL: Formalizing Access Limited
Reasoning](https://www.w3.org/DesignIssues/ftp://ftp.cs.utexas.edu/pub/qsim/papers/Crawford+Kuipers-
sowa-91.ps.Z)  
>  J. M. Crawford jc@cs.utexas.edu  
>  Benjamin Kuipers kuipers@cs.utexas.edu  
>  Department of Computer Sciences  
>  The University of Texas At Austin  
>  Austin, Texas 78712  
>  25 May 1990

>

> Abstract

>

> Access-Limited Logic (ALL) is a language for knowledge representation which
formalizes the access limitations inherent in a network-structured knowledge
base. Where a classical deductive method or logic programming language would
retrieve all assertions that satisfy a given pattern, an access-limited logic
retrieves all assertions reachable by following an available access path. The
complexity of inference is thus independent of the size of the knowledge-base
and depends only on its local connectivity. Access-Limited Logic, though
incomplete, still has a well defined semantics and a weakened form of
completeness, _Socratic Completeness_, which guarantees that for any query
which is a logical consequence of the knowledge-base, there exists a series of
queries after which the original query will succeed. This chapter presents an
overview of ALL, and sketches the proofs of its Socratic Completeness and
polynomial time complexity.

[algernon papers](http://www.cs.utexas.edu/users/qr/algernon.html#references)

[Crawf91] J. M. Crawford and B.J. Kuipers, "Negation and proof by
Contradiction in Access Limited Logic", in _Proceedings of the Ninth National
Conference on Artificial Intelligence (AAA1-91)_, Cambridge MA, 1991

[Date] An Introduction to Database Systems, 6th Edn, Adison-Wesley, 1995

[Davis] Randall Davis and Howard Schrobe, "[6.871: Knowledge Based Application
Systems](http://www.ai.mit.edu/courses/6.871/)" course supporting information,
1999

[CLA] [Contexts: A Formalization and Some Applications](http://www-
formal.stanford.edu/guha/), Ramanathan V. Guha, 1991 Stanford PhD thesis. see
also: [ContextLogic.lsl](https://www.w3.org/DesignIssues//XML/9711theory/ContextLogic.lsl), May 2001
transcription into larch.

[HOLintro]M. J. C. Gordon and T. F. Melham, "Introduction to HOL A theorem
proving environment for higher order logic", Cambridge University Press, 1993
ISBN 0 521 44189 7

[Laplante] Phillip Laplante (Ed.), "Great Papers in Computer Science", West,
1996, ISBN:0-314-06365-X

[Marchiori98] M. Marchiori, Metalog paper at QL98

[Peregrin] Jaroslav Peregrin, "[What Does One Need, When She Needs "Higher-
Order Logic?](http://dec59.ruk.cuni.cz/~peregrin/HTMLTxt/hol.htm)"
_Proceedings of LOGICA'96, FILOSOFIA, Praha,_ 1997, 75-92

[VLFM] J. P. Bowen, [Formal Methods, in WWW Virtual
Library](http://www.comlab.ox.ac.uk/archive/formal-methods.html)

@@

Much of this is following in the wake of Dan Connolly's investigations, and so
many of the references were provided directly or indictly by Dan.Other
pointers from Dan Connolly

  * DC on the need for HOL - [ private communication](http://lists.w3.org/Archives/Team/w3t-tech/1998OctDec/0314.html)

[LF] Harper, Honsell, Plotkin "[A Framework for Defining
Logics](http://www.dcs.ed.ac.uk/lfcsreps/91/ECS-LFCS-91-162/)", Journal of the
ACM, January 1993 appears to be the seminal paper on ELF paper ([ACM
pdf](http://www.acm.org/pubs/articles/journals/jacm/1993-40-1/p143-harper/p143-harper.pdf))  
[connolly's (attempted) transcription into larch](https://www.w3.org/DesignIssues//XML/9711theory/ELF)

[Pat Hayes, Research Interests and Selected
Papers](http://www.coginst.uwf.edu/~phayes/research.html) contains stuff on
time modelsImpl

Reiter, R., On Closed World Data Bases, in: H. Gallaire and J Minker (eds.),
Logic and Data Bases, Plenum, 1978, pp. 55-76. Defines Cloased World
Assumption? Ref from CIL

Perlis, D., Languages with Self-Reference I: Foundations. (or: We Can Have
Everything in First-Other Logic!). Artificial Intelligence, 25:301-322, 1985.

##  Footnotes

"Second-order logic is rather difficult to study, since it lacks a decent set
of axioms and rules of inference, so we have little to say about it" --
Footnote to preface to [Burris], p.xii

@@

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

