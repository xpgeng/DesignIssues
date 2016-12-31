Tim Berners-Lee  
Date: 2004/12/17, last change: $Date: 2005/02/17 15:39:27 $  
Status: personal view only. Editing status: first draft. An understanding of
[Notation 3](https://www.w3.org/DesignIssues/Notation3.html) is assumed for this article.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Reifying RDF (properly), and N3

Reification in this context means the expression of something in a language
using the language, so that it becomes treatable by the language. RDF graphs
consist of RDF statements. If one wants to look objectively at an RDF graph
and reason about it is using RDF tools, then it is useful, at least in theory,
to have an ontology for describe RDF statements. This note described one
suitable ontology.

When RDF extended to N3, then one way of discussing the semantics is to
describe N3 documents in RDF. This document does both.

The namespace used is `<http://www.w3.org/2004/06/rei#>` , for which here we
use the `rei:` prefix. Also, we use the ex_:_ prefix for the namespace
`<http://example.com/ex#>`.

##  RDF Terms

RDF terms are nodes in the RDF Graph. In RDF, these can be of three types:
named nodes, blank nodes, and literals. We will also call named nodes
_symbols_.

###  Symbols

Named nodes are named by URI strings, so a named node can be defined simply by
its URI string. The symbol which in N3 is written as
&lt;http://example.com/&gt; would be described as the RDF node:

    
    
    [ a rei:Symbol;  rei:uri "http://example.com/ex#joe" ]
    

###  Blank nodes

Blank nodes (or Bnodes for short) are nodes do not have URIs. When describing
a graph, we can say that a node is blank by saying that it is in the class
rei:BNode.

    
    
    [ a rei:Bnode ]
    

This blank node in the description is a description of a blank node in the
original graph. They are node the same blank node. We could in fact name the
blank node for the purposes of description:

    
    
    ex:bnode1 a rei:BNode.
    

###  Literals

Literals in an RDF graph are defined only by their value, just as symbols are
defined by their URIs. When using RDF to describe RDF, RDF literals can
clearly be used to give the value:

    
    
    [ a rei:Literal, rei:value "The quick brown fox"]
    

In fact, the domain of rei:value is rei:Literal, so it is not necessary to
explicitly state that something is a literal, one can just write:

    
    
    [rei:value "The quick brown fox"]
    

##  RDF Statements

A RDF statement is defined by its three parts, known as subject, predicate and
object, each of which is a term. In RDF, neither the subject nor the predicate
may be a Literal. The statement which in N3 is `ex:joe ex:name "James Doe".`
would be described as

    
    
    [ a rei:Statement;
      rei:subject [rei:uri "http://example.com/ex#joe"];
      rei:predicate [rei:uri "http://example.com/ex#name"];
      rei:object [rei:value "James Doe"]
    ] 
    

In fact, the fact that it is a rei:Statement would have been clear as the
domains of rei:subject, rei:predicate and rei:object are all rei:Statement.

##  RDF Graphs

An RDF graph is a set of statements. RDF itself doesn't have the concept of a
set, it only has the concept of an ordered list (RDF collection). However, the
OWL relation owl:oneOf related a class to a list of its members, and so we can
form a set the set containing 3 4 and 5 as `[ owl:oneOf (3 4 5)]` . using this
convention, we can describe an RDF Graph as the set of statements. For
example, the graph whose contents which would be written, in N3 as

    
    
    ex:joe ex:name "James Doe".
    ex:jane ex:name "Jane Doe".
    

would be described in this ontology as:

    
    
    {  a rei:RDFGraph;
       statements [ owl:oneof (
          [ a rei:Statement;
      rei:subject [rei:uri "http://example.com/ex#joe"];
      rei:predicate [rei:uri "http://example.com/ex#name"];
      rei:object [rei:value "James Doe"]
          ]
          [ a rei:Statement;
      rei:subject [rei:uri "http://example.com/ex#jane"];
      rei:predicate [rei:uri "http://example.com/ex#name"];
      rei:object [rei:value "Jane Doe"]
          ] ) 
    

Using the set may be ungainly, but it ensures that two RDFGraphs which contain
the same statements are demonstrably the same in their reified form. (We
envisage that further developments systems may have explicit processing for
sets, and N3 syntax could even be extended to include set literal syntax,
which would of course make this easier.)

##  The quoting of URIs

The use of an explicit string as the URI for the subject above is also
ungainly, compared with the use in the original N3 where a prefixed symbol can
be used. Why is the string given explicitly, instead of writing it as symbol?

Let's suppose for a moment that we just use the symbol, not the string for the
URI:

    
    
    #Wrong:
    [ a rei:Statement;
      rei:subject ex:joe;
      rei:predicate ex:name;
      rei:object [rei:value "James Doe"]
    ] 
    

This should be a description of an RDF statement. It must preserve the
original graph, including the URIs it used. The statements which would be
described as

    
    
    [ rei:subject ex:joe;                        # Wrong
      rei:predicate ex:name;
      rei:object [rei:value "James Doe"]] 
    

and

    
    
    [ rei:subject ex:jd1;                         # Wrong
      rei:predicate ex:name;
      rei:object [rei:value "James Doe"]] 
    

are different graphs, even if "http://example.com/ex#joe" and
"http://example.com/ex#jd1" are two URIs for the same person. However, if the
system knows that &lt;ex:jd1&gt; and &lt;ex:joe&gt; are in fact thhe same
person, then the second statement can be derived from the first. It is
important (in our application) to be able to know which name a graph used for
something. The form of reification which is provided by the original RDF
specification is not suitable, because it loses that information.

##  N3 Formulae

N3 extends RDF to allow graphs themselves to be another form of literal node.
A graph can be quoted inside another graph, as one of the terms of a
statement:

    
    
    ex:jane  ex:knows   { ex:joe ex:name  "James Doe" }.
    

Jane knows "joe's name is '_James Doe_'". As above, the quotation effect is
important. Jane's knowledge is in these terms. Even though ex:jd1 and ex:joe
may be the same person, Jane might not know that, and so may not know that
ex:jd1's name is _James Doe_.

An N3 formula also introduces quantification. Variables are introduced by
allowing a given set of symbols to be universally quantified over the formula,
and another set to be universally quantified.

A formula is described by three sets: the set of statements (the graph), the
set of universals and the set of existentials. The semantics of an N3 formula
are that the universal quantification is applied to the result of applying the
existential quantification to the conjunction of the statements. (a la _forall
x: exists c such that ..._). The N3 formula

    
    
      @keywords a.
      [] a car. { ?x a car } => { ?x a vehicle }.
    

(roughly, _There is a car. Anything which is a car is a vehicle_) is shorthand
for

    
    
    @keywords a.
    @forAll :x.
      @forSome :c.
        :c a car.
        {x a car } => {x a vehicle}.
    

would be described as a formula whose universals were just x, whose
existentials were just c, and whose statements was the implication - a
statement whose subject and object were themselves formulae. This follows in
the code below, obtained by passing the code above through `cwm --reify.` The
output is:

    
    
    @prefix : <http://www.w3.org/2004/06/rei#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @keywords a.
        
    [ a <http://www.w3.org/2000/10/swap/log#Truth>;
      universals[owl:oneOf(
                    "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#x"  ) ];
      existentials [owl:oneOf(
                    "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#c"  ) ];
      statement [ owl:oneOf([
         object [uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#car" ];
         predicate [uri "http://www.w3.org/1999/02/22-rdf-syntax-ns#type" ];
         subject [uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#c" ]
                   ]  [
         object [
             universals [ owl:oneOf () ] ];
             existentials [ owl:oneOf () ];
             statements [ owl:oneOf (
               [ object  [uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#vehicle" ];
                 predicate [uri "http://www.w3.org/1999/02/22-rdf-syntax-ns#type" ];
                 subject[ uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#x" ] ] ) ];
         predicate [uri "http://www.w3.org/2000/10/swap/log#implies" ];
         subject  [
             universals  [owl:oneOf ()];
             existentials [owl:oneOf () ];
             statements  [owl:oneOf  (
               [ object [uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#car" ];
                 predicate [uri "http://www.w3.org/1999/02/22-rdf-syntax-ns#type" ];
                 subject [uri "http://www.w3.org/2000/10/swap/test/reify/ex1.n3#x" ] ] ) ]] ] ) ] ].
        
    

##  Asserting truth

Note that in this mode, the formula is not only described, but it is also
stated to be a Truth. To simply describe a formula as existing doesn't say
anything. Formulae are abstract things, to say one exists doesn't add
anything. Some would say, all formulae exist, just as all lists exist.
However, to assert that one is true asserts its contents. The RDF file output
above has, by definition of the terms in the reification namespace, the same
meaning as the full N3 formula from which it is produced. It does to any agent
which understands the meaning of the reification namespace.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

