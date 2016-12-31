[Up to Design Issues](https://www.w3.org/DesignIssues/./)

#  Delta: an ontology for the distribution of differences between RDF graphs

[Tim Berners-Lee](http://www.w3.org/People/Berners-Lee/) and [Dan
Connolly](http://www.w3.org/People/Connolly/), [MIT Computer Science and
Artificial Intelligence Laboratory (CSAIL)](http://www.csail.mit.edu/)  
This work is supported in part by funding from US Defense Advanced Research
Projects Agency (DARPA) and Air Force Research Laboratory, Air Force Materiel
Command, USAF, under agreement number F30602-00-2-0593, Semantic Web
Development.  
Created: 2001, current: $Revision: 1.114 $ of  $Date: 2015/09/25 20:31:33 $  
Status: personal view only. Editing status: rough. 2004/03: Extended to add
pointers to implementations, and details of actual language used. see also:
[comments from reviewers](http://lists.w3.org/Archives/Team/sw-
team/2004Jul/0008)

Keywords: RDF, Difference, patch, remote update, synchronization, graph
comparison.

* * *

####  Abstract

The problem of updating and synchronizing data in the Semantic Web motivates
an analog to text diffs for RDF graphs. This paper discusses the problem of
comparing two RDF graphs, generating a set of differences, and updating a
graph from a set of differences. It discusses two forms of difference
information, the context-sensitive weak patch, and the context-free strong
patch. It gives a proposed **update ontology** for patch files for RDF, and
discusses experience with proof of concept code.

##  Introduction

The use of text files to record programs, documents, and other artifacts is
supported by version control systems such as RCS[Tich85] and CVS[Ber90] that
are based on the ability to compute the difference between two text files and
represent it as diff[Mill85], i.e. a set of editing instructions. The use of
database tables to record bank accounts and records of all sorts is supported
by the relational calculus[Codd70] and its expression as SQL statements. In
both cases, the data goes thru a sequence of states; not only are the states
represented explicitly (as text files or database tables) but also the
transitions from one state to the other can be represented explicitly (either
as editing instructions or SQL insert/update statements). Difference (\Delta)
and sum (\Sigma) functions are ubiquitous in computing and, like
differentiation and integration, are inverse in the sense that:

v1 = \Sigma(v0, \Delta(v0, v1))

Since the transitions can be represented much more compactly than the pairs of
states, and the sigma function is straightforward to compute, the deltas are
useful for efficiently updating data distributed among two or more peers.

We are developing a Semantic Web Application Platform ([SWAP](https://www.w3.org/DesignIssues//2000/10/swap/))
including tools and applications to manipulate RDF graphs much like
traditional tools manipulate text files. It includes `cwm`, a command-line
tool for processing RDF in both the standard XML encoding[RDF04] and an
experimental encoding, Notation3 (n3)[Ber03].

As we build the Semantic Web, using RDF graphs[RDFC04] to represent data such
as bibliographies[DC02], syndication summaries[RSS] and medical
terminology[Gol03], we see a need for difference and sum functions for RDF
graphs. The use of RDF to represent test results[EARL],[OWLT] motivates better
ways to compare the actual results of software tests with the intended results
and isolate the differences.

###  The Synchronization Problem

One of the most stubborn problems in practical computing is that of
synchronizing calendars and address books between different devices. Various
combinations of device and program, from the same or different manufacturers,
produce very strange results on not-so-rare occasions.

The problem has three parts. There is the syntactic problem of extracting the
data from the strange device or its storage medium and turning into something
manageable, such as RDF. There is the semantic problem of understanding what
the fields mean: can one have two home phone numbers? There is the problem of
actually synchronizing changes, particularly in the general case that changes
have been made on both devices.

Because the direct syntactic conversion to RDF often leaves something which
has strained and awkward semantics, it is often necessary or tempting to mix
the semantic and syntactic conversions. (See [RDF calendaring](https://www.w3.org/DesignIssues//2002/12/cal/)
discussions.) Because the merging of changes requires more application
knowledge than the bare RDF data provides, it is tempting to mix the
conversion and sync algorithm. However, this mixing reduces the modularity and
testability of the resulting program. Perhaps if the three stages were
separated, then a more robust system, and one more extensible by the addition
of information in new ontologies, would result.

In the semantic web architecture, the application constraints on the data can
be represented in the ontology, and so can be used by a a generic
synchronization system.

On the one hand, the syntactic problems are straightforward, if tedious, and
the much harder semantic problems may explain why many existing
synchronization packages break down. But on the other hand, perhaps it is the
combination of the two that result in so many failures; perhaps software that
separates the problems, treating synchronization generically, will be more
robust. We hope this work contributes to further work on specifications such
as SyncML[Sync02].

And while in the general case, concurrent changes may be completely
irreconcilable, the diff mechanisms discussed here solve an interesting part
of the problem space.

###  Problems with the line-oriented approach

RDF graphs can be serialized and used with traditional line-oriented tools. In
the general case, with no constraints on how the graphs are serialized, line-
oriented deltas can be as large as the data itself, even between files
representing the same graph. However, when files are edited by hand, small
changes to the data naturally result in small textual diffs. But since the
difference is expressed as the difference between two text files, not the
difference between two graphs, the delta is dependent on the graph
serialization. It's not enough to have the original graph to use the delta;
one needs a copy of the particular serialization.

Pretty-printing algorithms reduce the large number of possible serializations
of an RDF graph to a few actual serializations. The difference engine[Kly04]
produces human-readable difference descriptions using an algorithm analogous
to comparing pretty-printed graphs; its descriptions are not sufficient to
reconstruct one graph from the other, however.

We find it practical to use CVS to manage both hand-edited and machine-
serialized RDF data files in many cases. A notable exception is the reference
results for tests: comparison of experimental test results versus reference
results yield many false test failures every time we change the pretty-
printing algorithm in the slightest. The cost of managing the reference
results this way is barely tolerable.

The straightforward pretty-printing algorithm works in the obvious way when
all the nodes are named (either with URIs or literals): triples are sorted by
subject, and those that share a subject are grouped together. Notation3 has
syntax for grouping triples that shared predicates. Unlabeled nodes (_blank
nodes_ or _bnodes_) that have no incoming triples are treated like named
subjects. Bnodes that have one incoming link serve as internal nodes in the
pretty-printing tree. Bnodes that have more than one incoming triple are given
arbitrary labels for the purpose of serialization and are hence treated like
named subjects. For example, the triples

    
    
    :Bob :pet _:p.
    _:p :size "small".
    :Bob :brother :Pete.
    _:p :mother _:p2.
    :Pete :pet _:p2.
    

are pretty-printed as

    
    
        :Bob     :brother :Pete;
             :pet  [
                 :mother _:g0;
                 :size "small" ] .
         
        :Pete     :pet _:g0 .
    

The ordering and the identification of bnodes are the two ways which
serializations of the same graph can arbitrarily differ. `Cwm` not only
attempts to find a serialization which minimizes the number of arbitrarily
named nodes but often happens to regenerate arbitrary names consistently
across runs. Even so, diffs of pretty-printed RDF are still unsatisfactory,
since changes as small as one triple can lead to arbitrarily large textual
diffs if that triple changes the set of bnodes that need arbitrary labels.

To completely eliminate the arbitrary choices in how to serialize an RDF
graph, we could employ a canonicalization algorithm such as the one[Car03s] in
Jena[Car03], or [cant.py](https://www.w3.org/DesignIssues//2000/10/swap/cant.py) from our own SWAP toolkit.
One problem with this approach is that the canonical form is expressed in the
N-Triples[RDFT04] representation. Deltas between N-Triples files are verbose
and tedious to read for most practical graphs. Further, the problem of large
textual diffs resulting from small changes remains: these canonicalization
algorithms work by computing a signature for each blank node based on nearby
triples and sorting the results; adding or removing one triple near a blank
node will change its signature and hence potentially the labeling of many
bnodes.

##  Goals: Economy and Robustness

SQL statements and text file diffs are attractive because they succinctly
represent the difference between two states. If the difference between two
text files were not much smaller than either of the text files, it would be of
little use. The essential feature of a difference algorithm, then, is
_economy_: small differences between input states should result in small
deltas.

Much of the popularity of CVS is due to its support of concurrent development.
It makes a patch file[Wall] representing the changes each party has made.
These changes are made, in order, to the repository file to generate new
versions. In the event that two agents take a copy of the same version v0 and
make different changes to it (v1a and v1b), the party that commits last
attempts to make v1 which incorporates both diffs:

v1 = \Sigma(\Sigma(v0, \Delta(v0, v1a)), \Delta(v0, v1b))

Note that \Delta(v0, v1b) is applied to something other than v0. The context
diff and unidiff formats are sufficiently robust that it does work in most
practical cases. When it does not work, then the user is left with the problem
of manually reconciling the conflicts. This happens when, for example, one
party moves the date of a meeting at the same time as someone else moves or
deletes the meeting. It may be that the criterion that a problem needs human
involvement is very application-dependent.

There are thee failure modes:

  1. Inconsistent changes were made. This failure mode is not automatically soluble. 
  2. The patch was incapable of finding the appropriate points in v1a at which to make the change \Delta(v0, v1b). This form of failure we can eliminate for certain RDF graph deltas. 
  3. The patch was misapplied: the context was used to determine points at which to make the change, but the wrong point was used, and erroneous data resulted. This is unacceptable. 

A _robust_ patch is one which may be applied so a file different to the one it
was originally generated from, without being misapplied and hence generating
erroneous information. In the line oriented tools, the _patch_ program was
introduced to be more robust than simply applying the patch as a series of
editor commands.

##  Delta and Sigma for RDF Graphs

An RDF graph is a set of (subject, predicate, object) triples, i.e. a set of
typed links between nodes. Each node may or may not be named (either by a URI
or a literal). As a measure of the size of the difference between two RDF
graphs G1 and G2, one can use the sum of the size of the set differences
|G1-G3| and |G2-G3| where G3 is the largest common subgraph of G1 and of G2.

###  Computing differences between RDF graphs

In the case in which all the nodes are named, computing the difference between
two graphs is simple and straightforward:

If G1 and G2 are ground RDF graphs, then the _ground graph delta_ of G1 and G2
is a pair (insertions, deletions) where insertions is the set difference G2-G1
and deletions is G1-G2.

This form of delta is reasonably economical: the storage cost is linear in the
size of the difference between the graphs. Straightforward extensions with
slightly improved economy might be more specific in expressing differences in
which only one or two parts of the triple have changed.

It is also completely robust. Each statement is independent, with no
variables: there is no cause for ambiguity. The deletion statements may be
deleted from, and the insertion statements added to, any graph.

In the case where not all of the nodes are named, finding the largest common
subgraph becomes a case of the graph isomorphism problem. The arc labels do
have names (in a very large set of practical cases, including all those which
can be serialized as RDF/XML). Graph isomorphism is in fact a class of
difficult problem that cannot be solved in polynomial time but which has not
been shown to be NP complete[Kob93]. While the general graph isomorphism
problem has readily available solutions[Ski97][Ski01], they do not seem to be
a good match for the practical cases of RDF graph diff.

There is an interesting subset of real cases in which there are a mixture of
named and unnamed nodes, but none of the unnamed nodes is very far from a
named node. In this case, the unnamed nodes can be indirectly identified by
giving a path from a named node. The difference is then expressed by giving
this local context and the related changes.

###  A patch file format for RDF deltas

By analogy to the text diff, there is a need not only for a difference-finding
algorithm, but for a patch file format. Such a format needs:

  * a way to uniquely identify what is changing 
  * a way to distinguish between the pieces added and those subtracted 

It is straightforward to pinpoint the parts of the graph that have changed
when all nodes are named, but less so in the presence of anonymous nodes.

To identify what is changing, we use Notation3 expressions for quoted RDF
graphs with schema variables, and we introduce three new terms. For example:

    
    
    @prefix diff: <http://www.w3.org/2004/delta#>.
    { ?x  bank:accountNo "1234578"; bank:balance 4000}
     diff:replacement
    { ?x  bank:accountNo "1234578"; bank:balance 3575}.
    

This one new property `replacement` can express any change. Deletions can be
written `{...} diff:replacement {}` and additions can be written `{}
diff:replacement {...}`.

The second alternative is very similar but involves two properties, one for
inserting and one for deleting:

    
    
    { ?x  bank:accountNo "1234578"}
      diff:deletion  { ?x  bank:balance 4000};
      diff:insertion { ?x  bank:balance 3575}.
    

The form using `diff:insertion` and `diff:deletion` is implemented in
[cwm](https://www.w3.org/DesignIssues//2000/10/swap/doc/cwm).

The first and second form are related by

    
    
    { ?F replacement ?G }    <=>  { ?F deletion ?F; insertion ?G }   
    

###  Weak and Strong diffs

To address robustness, we distinguish two types of RDF graph deltas: a _weak_
delta gives enough information to apply it to exactly the graph it was
computed from, but a _strong_ delta specifies the changes in a context-
independent manner. The difference is not in the patch file format, but in the
information a particular patch gives.

Returning to the bank example, if bank account numbers are globally unique,
then the replacement pattern will bind ?x to a node identifying a particular
bank account. In OWL[OWL] terms, if `bank:accountNumber` is an
`owl:InverseFunctionalProperty`, then the node must be the `owl:sameAs` any
other node with the same account number. In that case, the patch will be
strong.

If, however, many accounts can have the same number, applying that patch to
another knowledge base may inadvertently alter the wrong account. The patch
would be weak.

In normal information processing, of course, numbers such as bank account
numbers are used to avoid this confusion. Consider those graphs in which every
blank node is in fact unambiguously identified by one functional or inverse
functional property. Further, that property is invariant under any changes
represented by the deltas.

The pattern for terms goes as follows:

Given a background ontology W and a graph G, if a blank node b in G is the
object of a triple whose subject v is _functionally ground_ and whose
predicate p is an `owl:FunctionalProperty` according to W, then v.p is a
_functional term label_ for b in G with respect to W. Likewise, v\uparrow q is
a functional term label for b if q is an `owl:InverseFunctionalProperty`, b is
the subject, and v is the object. Recursively, v is functionally ground if it
is a name (URI or literal) or a bnode with a functional term label.

Then we can rewrite certain graphs:

With respect to a background ontology W, a graph G is _fully labeled_ iff
every node in G is functionally ground. A _functional RDF graph_ is a set of
triples whose terms are URIs, literals, or functional terms. A functional RDF
graph F is a _functional analog_ of an RDF graph G iff G is fully labeled and
F can be obtained from G by replacing each bnode b in G with a functional term
label for b.

The diffs of functional RDF graphs are just as simple to make as ground RDF
deltas:

Given a background ontology W, a _strong_ delta between fully labeled graphs
G1 and G2 is a pair (insertions, deletions) where insertions is the set
difference F2-F1, deletions is F1-F2, and F1 and F2 are functional analogs of
G1 and G2 respectively.

(@@need to define sigma for strong deltas?) It is actually the same as for any
delta: horn match and delete or insert.

A strong delta is like a context diff that cannot be mis-applied.

If D is a strong delta between fully labeled graphs k1 and k2, and k3 is a
subset of k1, then \Sigma(k3, D) is consistent with k2. @@TODO: proof

One advantage of a strong patch is, then, that one can take a patch from any
true knowledge base change and apply it to a subset knowledge base, and the
result will be true. For example, if changes to a knowledge base are
represented by a sequence of strong diffs, one can subscribe to the diffs from
any given point on, and acquire a subset of the final knowledge base.

As a practical matter, achieving fully labeled graphs requires care in
building and using the ontology. As a supplement to the good practice of using
URIs to distributing data, it is useful to identify things indirectly by using
terms with published ontologies that say whether they are many-many, many-1,
1-many or 1-1. The [diff.py](https://www.w3.org/DesignIssues//2000/10/swap/diff.py) program from
[SWAP](https://www.w3.org/DesignIssues//2000/10/swap/Overview.html) will generate a strong diff between two
files, provided it can find sufficient information in the Web to fully label
the input graphs.

We note in passing that the ontologies we used all involved inverse functional
datatype properties, which are OWL/Full but not OWL/DL.

##  Application to Update and Sync

Though we have made small scale tests, we are interested in pursuing strong
diffs, and suspect they will be are useful in a variety of applications.

###  Peer-peer update and sync

The algorithm for synchronizing two databases can be straightforwardly
generalized to N. In a decentralized peer-peer network such as Network News
Transfer Protocol[NNTP] (or many others), messages are timestamped and
distributed eventually to every party, though a message may be received by
different parties at different times. When the network is reliable, there may
be a well-defined maximum delivery time.

A crude algorithm is to apply the patches in order of the time-stamp. If a
message arrives with a timestamp preceding the recent ones already taken into
account, they are unwound so that the new version can be built in the proper
order. A patch which fails (as in a CVS conflict) is rejected. In the case of
RDF graphs, failure can be a pre-agreed form of consistency, such as (for
example) OWL-DL consistency. The sender of the failed patch will realize this
as they will be running the same algorithm on the same patches, and will have
to take recovery action.

A new version can be given a version id by hashing the version id of its
predecessor with the message id of the patch used to make the new from the
old. The community can refer to versions by these ids, and if they want to
refer to a commonly held document, then one only has to wait for the maximum
delivery time to know that everyone in the community will know the value of
the knowledge base for that version. Even without waiting, anyone who knows of
a version with that ID will know they have the same contents.

###  Patches as knowledge

The idea of the strong patch file format is interesting because a patch is a
little bit of knowledge. A patch for example that where my phone number was
1234 it should now be 5678, when in the context in which it is known to be a
change to a valid knowledge base between one week and the next, indicates that
my phone number has actually changed. One might conclude, say, that I moved or
changed jobs. A strong patch has meaning in itself, and distributing and
filtering these becomes an interesting way of processing knowledge. In some
areas (like houses for sale) it is the new changed information which is of
most interest, and in some areas (like currency rates) if you listen to a
stream of changes you will in fact accumulate a working knowledge of the area.

###  Patches as news

From the historical _NCSA Mosaic What's New_ page to the current syndication
of RSS streams [RSS], the interest in news on (or off) the Web demonstrates
that there is great interest in changes to the status quo. We speculate that
this will also be the case on the Semantic Web. When the state is represented
in RDF, then RDF diffs represent news. The W3C Technical Reports list is
available as RDF, and the W3C RSS feed is partly, effectively, a list of
changes to the Tech Reports list. This could be formalized by explicitly
distributing RDF diffs.

##  Future directions

The algorithm developed to date produces difference files only on graphs which
are labeled directly with URIs or indirectly with functional properties or
inverse functional properties.

It may be useful to extend the algorithm to cope with graphs which are not
completely labeled, but where the unlabeled bits are the same in each graph,
and so a strong diff can still be produced. Another avenue would be to look at
using more than one property to label a node when one is not sufficient.

Applications which do not need robustness can use weak patches. The algorithm
could be extended to do more of a canonicalization-style signature-based match
to optionally give a weak diff where a strong diff cannot be given.

In practice, while RDF fundamentally has a graph structure, the graph is often
used to encode ordered lists (RDF collections). While lists are in fact
represented by a structure of _first_ and _rest_ links within the graph, when
serialized they are normally represented directly as lists, and within
software implementations they may be stored specially. The representation of
changes to lists may merit a special syntax in the difference file, to avoid a
mess of _rdf:first_ and _rest:rest_ statements. (@@DanC: first/rest are
functional, so I don't think this case mertis anything special.)

RDF does not contain the notion of an unordered set, though one can with OWL
create a class which has an enumerated set of members. If the use of unordered
sets becomes common, which the authors suspect would be wise in the long run,
then a difference engine should be aware of such sets and be able to express
differences between them.

This application, like the rule language, demonstrates the usefulness of the
quoted formulae of n3. The authors believe that many applications will need
this ability to quote RDF graphs within graphs. As n3 becomes a language of
communication, difference files will of course have to express changes to
nested formulae. As these are graphs, this is basically a straightforward
recursive use of the difference system for single graphs. A simple though
verbose alternative is to reify the n3 before building differences.

With these extensions, the simple difference file format may lose the elegance
of its current simplicity. However, even with these extensions, most data and
ontologies shipped around the web -- the bottom layers of the semantic web
layer cake -- will be plain RDF graphs and so have simple difference files.

Clearly there are many algorithms which can be imagined for efficiently
generating deltas for RDF graphs. The ones written are not particularly
efficient, having being designed as proof of concept.

##  Conclusions

There are many uses for technology of communicating differences between graphs
or changes to a graph. While in general the generation of differences is
basically a graph isomorphism problem, in a wide set of practical cases, one
can efficiently generate a difference, or patch file. So-called strong patch
files are particularly interesting, and open up a new series of applications
based on the syndication of change information. However, to be able to
generate them, one needs either a well-labeled graph, which in turn needs an
ontological knowledge of inverse functional properties to allow nodes to be
indirectly labeled. The patch file format proposed is simple, being a new
ontology of only two (or three) new properties, and directly uses Notation3
syntax and semantics, which itself is a simple extension of RDF. This format
can be generated by all sorts of difference-finding algorithms. It can be
absorbed by any system capable of matching RDF subgraphs. The patch file
ontology is a candidate for a future standard for remote update of RDF data.

##  Followup (2015)

In the several years since this was originally written, the general concepts
of diffs and patches, delta and sigma, differentiation and integration, been
constant themes in distributed systems. Neil Fraser's 2008 [Differential
Synchronization](https://neil.fraser.name/writing/sync/) paper discussses some
architectures in which diffs and patches are routed in various ways.
Specifically it sends diffs in loops so that while one party hopes that the
other(s) will use be able to apply all their patches, in fact that party gets
back a stream of patches which include both the other's edits but also their
own apologies for not being able to apply a patch.

The discussion there is about eding texts, and assumes that the system has to
watch for a user to edit the text using other tools, and then make a diff to
see what has changed. An alternative if for the user's tools to send the diffs
explictly. The style of programming in the tablator-derived work on SoLiD is
for diffs to be sent immediately before the change is acknowledgeed in the UI,
so that they can be reverted if the patch fails. This requies good latency of
course.

The [Linked Data Platform at W3C standardizing formats for patches, and a way
to discover that an HTTP server suports incoming patches, or will send
outgoing ones.

##  References

see [Diffbib.bib](https://www.w3.org/DesignIssues/lncs04/Diffbib.bib)

[RDF04]

     Beckett, D. [ RDF/XML Syntax Specification (Revised)](http://www.w3.org/TR/2004/REC-rdf-syntax-grammar-20040210/) W3C Recommendation, 10 February 2004. 

[Latest version](http://www.w3.org/TR/rdf-syntax-grammar) available at
`http://www.w3.org/TR/rdf-syntax-grammar`

[DC02]

     Beckett, D. and Miller, E. and Brickley, D. [ Expressing Simple Dublin Core in RDF/XML](http://dublincore.org/documents/2002/07/31/dcmes-xml/) Dublin Core Metadata Initiative Recommendation 31 July 2002
[RSS]

     Beged-Dov, Gabe et. al. [RDF Site Summary (RSS) 1.0](http://web.resource.org/rss/1.0/) 6 December 2000
[Ber90]

     Berliner, Brian CVS II: Parallelizing Software Development [USENIX](http://www.usenix.org/) Conference Proceedings pp 341--352 January 22-26, 1990 Washington, D.C.

[ online copy](http://www.hpcc.ecs.soton.ac.uk/hpci/tools/cvs/html/cvs-
paper.html); [ ms source](http://cvsweb.xfree86.org/cvsweb/cvs/doc/cvs-
paper.ms)

[Ber03]

     Berners-Lee, Tim and Hawke, Sandro and Connolly, Dan [Semantic Web Tutorial Using N3](http://www.w3.org/2000/10/swap/doc/) Twelfth International World Wide Web Conference Budapest, Hungary May 2003
[Car03]

     Carroll, Jeremy J. and Dickinson, Ian and Dollin, Chris and Reynolds, Dave and Seaborne, Andy and Wilkinson, Kevin [ Jena: Implementing the Semantic Web Recommendations](http://www.hpl.hp.com/techreports/2003/HPL-2003-146.html) Hewlett-Packard HPL-2003-146 Dec 2003

[Jena](http://www.hpl.hp.com/semweb/jena.htm) includes a graph diff program
`rdfcompare` in the [command line
tools](http://jena.sourceforge.net/tools.html).

[Car03s]

     Caroll, Jeremy J. [ Signing RDF Graphs](http://www.hpl.hp.com/techreports/2003/HPL-2003-142.html) Hewlett-Packard HPL-2003-142 Jul 2003
[Codd70]

     Codd, E. F. [A Relational Model of Data for Large Shared Data Banks](http://www.acm.org/classics/nov95/), Communications of the ACM, Vol. 13, No. 6, June 1970, pp. 377--387. 
[Gol03]

     Golbeck, Jennifer and Fragoso, Gilberto and Hartel, Frank and Hendler, James and Parsia, Bijan and Oberthaler, Jim [The national cancer institute's thesaurus and ontology](http://www.mindswap.org/papers/WebSemantics-NCI.pdf). Journal of Web Semantics, 1(1), Dec 2003. 
[RDFT04]

     Grant, J. and Beckett, D. [RDF Test Cases](http://www.w3.org/TR/2004/REC-rdf-testcases-20040210/), W3C Recommendation, 10 February 2004. 

[Latest version](http://www.w3.org/TR/rdf-testcases) available at
`http://www.w3.org/TR/rdf-testcases`

[RDFC04]

     Klyne, G. and Carroll, J. J. [Resource Description Framework (RDF): Concepts and Abstract Syntax](http://www.w3.org/TR/2004/REC-rdf-concepts-20040210/), W3C Recommendation, 10 February 2004. 

[Latest version](http://www.w3.org/TR/rdf-concepts/) available at
`http://www.w3.org/TR/rdf-concepts/`

[NNTP]

     Kantor, Brian and Lapsley, Phil [Network News Transfer Protocol](http://www.ietf.org/rfc/rfc977) IETF RFC977 February 1986
[Kly04]

     Klyne, Graham [Semantic Web Inference Scripting in Haskell](http://www.ninebynine.org/RDFNotes/Swish/Intro.html) Feb 2004

see esp. section [ Comparing
graphs](http://www.ninebynine.org/RDFNotes/Swish/Intro.html#GraphDiff)

[Kob93]

     Johannes Kobler and Uwe Schoning and Jacobo Toran [The Graph Isomorphism Problem: Its Structural Complexity](http://www.birkhauser.com/cgi-win/ISBN/0-8176-3680-3) Progress in Theoretical Computer Science. Birkhauser, Boston, MA, (1993). 

[ preface, TOC, etc.](http://www.informatik.hu-
berlin.de/Institut/struktur/algorithmenII/Buecher/GI/). cited in [
KaibelSchwartz2002.references.bib](http://www.math.tu-
berlin.de/~schwartz/papers/KaibelSchwartz2002.references.bib)

[Mill85]

     Miller, Webb and Myers, Eugene W. A File Comparison Program Software---Practice and Experience, 15(11), pp. 1025--1040, November 1985. 

[ bib](http://liinwww.ira.uka.de/cgi-
bin/bibshow?e=TF0tqf/fyqboefe%7d789658&r=bibtex&mode=intra)

[Ski97]

     Skiena, Steve The Algorithm Design Manual [Telos Pr](http://www.telospub.com/) New York 1997
[Ski01]

     [Skiena, Steve](http://www.cs.sunysb.edu/~skiena/) 1.5.9 [ Graph Isomorphism](http://www.cs.sunysb.edu/~algorith/files/graph-isomorphism.shtml) in the [Stony Brook Algorithm Repository](http://www.cs.sunysb.edu/~algorith/index.html) Stony Brook University 2001

with reference to [ GMT - Graph Matching
Toolkit](http://www.cs.sunysb.edu/~algorith/implement/gmt/implement.shtml)

[Tich85]

     Tichy, W. [ RCS--a system for version control](http://portal.acm.org/citation.cfm?id=4202&dl=ACM&coll=GUIDE) Software Practice &amp; Experience Volume 15 , Issue 7 (July 1985) Pages: 637--654
[Sync02]

     [ SyncML Specifications, Version 1.1](http://www.openmobilealliance.org/tech/affiliates/syncml/syncmlindex.html) Feb 2002 [Open Mobile Alliance (OMA)](http://www.openmobilealliance.org/)
[Wall]

     Wall, Larry et. al. [patch](http://www.gnu.org/software/patch/patch.html) Free Software Foundation 27 Jun 2000
[EARL]

     Chisholm, W. and Palmer, S. B. Editors: [Evaluation and Report Language (EARL) 1.0](http://www.w3.org/TR/2002/WD-EARL10-20021206/) W3C Working Draft (work in progress), 6 December 2002

[Latest version](http://www.w3.org/TR/EARL10/) available at
http://www.w3.org/TR/EARL10/

[OWLT]

     Carroll, J. J. and De Roo, J. Editors: [OWL Web Ontology Language Test Cases](http://www.w3.org/TR/2004/REC-owl-test-20040210/) W3C Recommendation , 10 February 2004. 

[Latest version](http://www.w3.org/TR/owl-test/) available at
http://www.w3.org/TR/owl-test/

[OWL]

     Schreiber, G. and Dean, M. Editors: [OWL Web Ontology Language Reference](http://www.w3.org/TR/2004/REC-owl-ref-20040210/) W3C Recommendation , 10 February 2004. 

[Latest version](http://www.w3.org/TR/owl-ref/) available at
http://www.w3.org/TR/owl-ref/

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

