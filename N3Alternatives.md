Tim Berners-Lee  
Date: 2002/03/14, last change: $Id: Notation3.html,v 1.49 2001/11/27 23:59:33
timbl Exp $  
Status: personal view only. Editing status: draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Ideas about Web Architecture

_This is simply a footnote historical record about some rather arbitrary
choices, to save me going over the reasons again and again. It is not part of
the main thread._

* * *

#  Alternative design choices in [Notation3](https://www.w3.org/DesignIssues/Notation3.html)

In this article:

  1. Syntax for Graph traversal ("paths") 
  2. Infix operators
  3. Syntax for sets
  4. Other issues

##  Syntax for graph traversal

There is a strong need for a neat syntax for converting an expression for x
into an expression for something removed one step along the graph from x by an
arc of type (rdf:Property) p. For example, if x is a person then we want an
expression for x's email address. _(I am dropping the prefixes in this
discussion to reduce clutter)_

"Neat"? Compact, powerful, simple, naturally understandable because of
metaphors with existing use of similar syntax.

Strictly, we are talking about _some y, such that p(x,y)_, or in n3, [is p of
x]. There is no implication in this syntax at the moment (but could be later)
that there is only one such y. The information that there can be only one such
y, when it is so, is conventionally in stored by noting that p is a
daml:uniqueProperty property. This can be stated in any document, though
current colloquial use puts it into the schema for p.

I will call moving from x to [ is p of x] forward traversal, and moving from x
to [p x] backward traversal. My instinct is that forward traversal, which is
the only thing you can do naturally in many systems of linked objects, is more
common need in the language than backward traversal.

Backward traversal can also be expressed as forward traversal through the
inverse of a property, so a compact expression for the inverse of a property
would be an alternative, so long it was clear when this was syntactic device
for making a backward link, and when(if ever) it was actually used to make

We need both to chose punctuation and also the grammar, as to the precedence
of the operator if any. To be able to write "the person whose wife's uncle is
driving my bother's car" . Mostly here I am looking at traversal expressions
going left to right with no precedence, but "of" as used in english is an
exception in that it is right to left.

###  Use case examples

Forward traversal: The phone number of the home of the chair of the conference
x,

Example scenarios  |  English  |  Existing Notation3 (2002/02)  
---|---|---  
  
Forward traversal

|  The phone number of the home of the boss of x. X's boss' home's phone
number.  |  [ is :phone of [is :home of [is :boss of :x]]]  
Mixed traversal  |  The phone number of the home of someone whose boss is the
uncle of x.  |  [is :phone of [is home of [ boss [is uncle of :x]]]]  
Units  |  100 dollars.  |  [dollars "100"]  
Units  |  the price in dollars  |  [ is dollars of price]  
Language  |  The french phrase "chat"  |  [ lang:fr "chat"]  
Language  |  The title in french  |  [ is lang:fr of :label]  
Mixed  |  The author of the book whose title in english is "The Little Prince"
|  [is author of [ has title [lang:en "The Little Prince"]]]  
Unary function  |  The sine of x.  |  [is sine of x]  
Nary function  |  The maximum of 12, 23 and 20  |  [is math:max of ("12" "23"
"20")]  
Nary function (named args) **Not** a traversal case  |  The the result of
spellchecking foo.html with dictionary eng.dict.  |  [we:spellcheck
&lt;foo.html&gt;; we:dictionary &lt;eng.dict&gt;.]  
Labeled traversal  |  an sculture whith a price of x dollars and creator y
domiciled in italy.  |  [a Sculpture; cost [ dollars x]; creator [=y; domicile
cc:it]] _This use of "=" is not real N3 syntax_  
  
The last case, labelled traversal, is in fact much more than graph traversal -
by embedding variables into the graph in search template (rule antecedent),
one make a reference which can be used in a rule conclusion. One can also, by
reusing a variable more than once, make multiply connected (right phrase?)
graph in place of a tree.

###  Dot

This problem has strong analogy with moving from an object to a slot in an
object. Python, c++, etc: x.email, so that metaphor is a natural one to pick
up.

Pro: For programmers, this is a natural.

Con: Dot as the end of an n3 sentence would have to be protected by following
space or punctuation. The language is made more complex in that either some
tricky tokenizing with some form of look-ahead becomes necessary.

There is no equivalent convention as far as I know for backward traversal, so
let's pick something random and inverse to "." -- say "^". (Metaphor: back up
rather than down forwards?). Think of "^" as a combination of "." and an
operator to generate the inverse property. (Or maybe "^" should be that
property, which would make foo.^bar a back-traversal except that it would
actually be represented using an extra triple.)

###  Bang

There is a form of path familiar to those who knew email and net news in the
days of source routing: when one had to specify a series of machine names
through which the mail had to be forwarded, as in
`mcvax!cernvax!online!timbl`. Though few current users will remember it, it
has the advantage over dot of being unused elsewhere in teh N3 syntax. This
leaves the N3 language simpler.

Example scenarios  |  English  |  Using dot and caret, left to right  |  Right
to left parsing with $ and %  |  Keywords, right to left  
---|---|---|---|---  
Forward traversal  |  The phone number of the home of the boss of x. X's boss'
home's phone number.  |  x.boss.home.email  |  |  email of home of boss of x  
Mixed traversal  |  The phone number of the home of someone whose boss is the
uncle of x.  |  x.uncle^boss.home.email  |  |  email of home of thatwhich boss
uncle of x  
|  The formula from parsing a document whose URI is the first command line
argument  |  "1".os:argv^log:uri.log:semantics  |
log:semeantics%log:uri$os:argv%"1"  |  log:semantics of [] which has uri []
which is od:argv of "1"  
Units (b)  |  100 dollars.  |  "100"^dollars  |  dollars$"100"  |  thatwhich
dollars 100  
Units (f)  |  the price in dollars  |  price.dollars  |  dollars%price  |
dollars of price  
Language (b)  |  The french phrase "chat"  |  "chat"^lang:fr  |  langfr$"chat"
|  thatwhich lang:fr "chat"  
Language (f)  |  The title in french  |  title.lang:fr  |  lan:fr%title  |
lang:fr of title  
Mixed  |  The author of (the book) whose title is the french "Le Petit Prince
|  "Le Petit Prince"^lang:fr^doc:title.author  |  author % doc:title $ lang:fr
$"Le Petit Prince"  |  author of thatwhich _has_ title thatwhich _has_ lang:fr
"Le Petit Prince"  
Unary function  |  The sine of x. sin(x)  |  x.sin  |  sin%x  |  sin of x

x's sin  
  
(its inverse)  |  arcsin(x)  |  y^sin  |  sin$y  |  thatwhich sin y  
N-ary function  |  The maximum of 12, 23 and 20  |  ("12" "23" "20").max  |
max$("12" "23" "20")  |  max of ("12" "23" "20")  
Labeled traversal  |  A sculpture with a price of x dollars and creator y
domiciled in italy.  |  [a Sculpture; cost :x^dollars; creator [is y; domicile
cc:it]]

_This use is not real N3 syntax unless we change "is'_

|  domicile$  |  [] a Sculpture; cost [] dollars 100; creator :y which
:domicile cc:it. _Note that a consistent grammar is not obvious_  
  
###  Multiply, Divide

Metaphor: Units of measure

A snappy syntax is useful in the leaves of an expression tree,. Examples come
up frequently when the logical way to express data types, units of measure,
and so on is with a graph traversal. With units of measure, people use use
multiplication and division, and these actually make sense mathematically.

Cost = 100*dollars or even Cost/dollars = 100 and Cost/day=100*dollars.

Pro: / and * are indeed inverse, when you have unique and unambiguous
functions: x/y*y =x.

Con: This is not always the case! Also, "*" and "/" in math, and in units of
measure, have properties like commutativity which you expect of "*" and it
doesn't have in this context/. Also, I had expected that it would be pragmatic
to add in operators directly to the syntax for convenience, and so was
reserving _\+ - * /_.

###  Keywords \- which, of, 's, the

The english language suggests some keywords.

"which" I have considered using in a sentence to turn the current object into
the new subject. There are two forms I had thought of, I'll call them "which"
and "thatwhich" for now. "Which", as in english, applies to a started object
and allows labelled traversal. "thatWhich" is used for backward traversal,
though the grammar is different.

`:joe :son :johnny which has :girlfriend :jane.`

`:joe :son thatWhich :girlfriend :jane.`

`thatwhich has :home thatwhich has :email thatwhich has`

Pro: _which_ reads very well (unless you insist on _whose_!), especially with
N3's optional _has_ before the property.

Con: _thatwhich_ is unbeliveably ugly. Even _which_, while reading well, is
not a very concise form.

A possibility is to just use _which_, with [] for the _that_ or _something_
which precedes it in english grammar. In fact, if someone wants _something_ as
a synonym of [] I wouldn't violently object.

`:joe :son [] which :girlfriend :jane.`

A synonym for "which" could be the more mathematical "suchthat", which
suggests a vertical bar.

`:joe :son [] | :girlfriend :jane.`

This makes an effective traversal operator []| which is an eyeful, but the
pipe is nice as a connector.

`joe son :johnny | girlfriend jane | mother [] | email <audey@example.com>.`

"Of" is interesting, though could be confusing that it parses right to left

`email of home of boss of x` means `email of (home of (boss of x))`

I just noticed that when I write on the blackboard, % and _of_ look pretty
similar, so % to be read as _of_ would a possibility for forward traversal
prefix operator.

The astute will have noticed that "of" is already used as a keyword in N3.
However, all is not lost, in fact much could be gained. Could one not split
"of" and "is" into separate features of the language, `p of y` being simply
short for what is currently `[ is p of y]`, and `is` being an operator which
at the syntactic level indicates that two things are the same node.

(This is not the same as N3's =, which is daml:equivalentTo, which has axioms
about properties of similar things being the same, but is not involved at this
level. N3 and RDF treat different URI-identified nodes separately, whether or
not a daml:equivalentTo arc joins them))

This allows things like

`joe brother [ is fred; wife margy; kids jane, john]`.

Contrast "of" with with the english 's, German -es

`x's boss's home's email` meaning (`(x's boss)'s home)'s email`

which reminds one of Ada's

`x'boss'home'email`

of whose etymology I am unaware.

Con: I was kinda thinking of keeping all the quotes I can in hand for use in
various forms of quotation! So many languages needs many forms of quotation
and run out of options all to fast. (XML an Python both use " and ' to mean
the same - a waste if you ask me!)

One could go the other way and just use a keyword "s"

`x s boss s home s email.`

or use a "$" with a closeness to "'s" and expectation of being read aloud as
such:

x$boss$home$email

"The" in english signifies the uniqueness of something, and so could be used
to indicate that something is indeed a function.

the email of the home of the boss of x

###  Arrows

Access limited logic, and the original N3 design, one of the conceptual graph
serializations, and other languages derived from a transcription of whiteboard
circles-and-arrows diagrams, use "-&gt;" or "&gt;" as a traversal operator.
Multics used (I understand) "&gt;" for descent of a directory tree and "&lt;"
for ascent, so ../../foo/test would be &lt;&lt;foo&gt;test which is neat even
though it frightens the xml-minded side of one.

N3 uses &lt;&gt; to surround URIs, which i suppose could be changed, but it
interferes strongly with this.

###  Slashes

Same idea as arrows, but using slash.

Pro: The metaphor with directory traversal is useful (even though the graph
being traversed is not always a tree).

Pro: A nice simplicity.

`x.uncle^boss.home.email`

becomes

`x/uncle\boss/home/email`

Con: Unix types could find it strange when finding their universal escaping
character used as anything else. And it rules our using it for that form.

Con: The confusion which Microsoft introduce by using backslashes for
directories has done lasting harm to the community, leaving many people still
unsure which is which. This sort of

###  Parens

The application of a monadic function is a special case of the traversal of a
graph arc, so syntactic metaphors from functions would seem appropriate. The
most obvious case is when a function takes a list, to just abut the function
identifier to the list, looking like a regular function call in more languages
than I could name:

`x = math:max(y z w)` for `x = [ is math:max of (y z w)]`

Pro: Looks great.

Con: Doesn't work when the function doesn't take a list. Also, if you get a
space in between, it means something completely different. Hopefully it will
in some cases at least be a syntax error, but not within in a list.

Maybe a separator of some sort as punctuation would work a left/right reversed
from of "."

`x = math:max$(y z w)`

###  Summarizing

Categorizing  |  Forward traversal  |  Backward traversal  
---|---|---  
suffix  |  x.email

x's email

|  y^email  
prefix  |  email of x

email(x)

|  [] which email y

[] | email y  
  
One thing that becomes evident: it can be really difficult to read the
backward traversal in english. Like many systems, (including WWW) , english is
optimized for forward traversal

###  Swan

Sandro's swan language used a name immediately followed by "(" as a function
opener as in sum(2 3).

He also used "." for path traversal.

##  Infix operators

I had reserved * / + - for infix operators for arithmetic. The | operator for
or and &amp; for and (or union and intersection of sets) are also reasonable
to use in this way.

If N3 is to have a to have a path toward becoming a language in which
arithmetic and set operations are easy to write, it is hard to improve on
infix notation. This would, however, change the form of the language
significantly. It isn't clear that it would still be predictively parsable.

##  Sets

The following considers design alternatives in extending N3 to include a
notation for set literals. 2005/1/1

###  Background on containers

In the area of containers, RDF started with some "Sequences" and "Bags" which
were in my opinion and with the benefit of hindsight, sub-optimal (The
infinite rdf:_1 series of predicates was downright weird, and taking it into
consideration made code much mroe complicated. Futher, for all the arbitrary
complexity of the rdf:_nnn predictaes, they didn't tell you that essential bit
of information as to when the container was finished: what **wasn't** in the
container) .

RDF does however have a **collection** which is an ordered list, and is very
useful. N3 has a shorthand syntax ( 1 2 3 ) for the list of the numbers 1, 2
and 3, and the RDF/XML syntax has parseType="collection" shorthand. There is
also defined a way of expressing lists in triples using blank nodes, using
`rdf:first` and `rdf:rest`, and `rdf:nil`. The list 1 2 3 would be expressed
as

    
    
    [ rdf:first 1; rdf:rest [  
         rdf:first 2; rdf:rest [  
            rdf:first 3; rdf:rest rdf:nil]]]
    

This is, if you like, a reification of a list. It described it totally. Some
RDF systems actually store lists in this way. The RDF and OWL specs together
are not (as far as I was aware) very clear about the axioms of lists. One
would expect clear axioms that all lists exist, that any two lists with the
same first and rest are owl:equivalent, and so on.

###  Introducing sets

It turns out that in many cases in applications we have seen, containers are
in fact logically unordered sets, not ordered lists. Whether it is mail
addresses on a mailing list, or rows in a database, or statements in an N3
formula, the order is immaterial, and something can occur in the set once or
not at all.

In these circumstances to use a list to represent the data is suboptimal in
may ways. For example,

  * It is not clear when two different lists actually have the same members in a different order that they represent the same set; 
  * The information about what is in fact a set end up being communicated out of band, or just assuemd by those who know the application; 
  * Underlying implementations cannot use code library support which is optimized for sets. 

For these reasons it is useful to have sets in the language in the same way as
lists: to have a reification - a way of expressing them in triples so as to be
able to pass them though general RDF applications whcih may be unaware of
them, and a shorthand syntax to allow them to be written effeciently.

###  Reification

It turns out that OWL provides is with owl:oneOf, a relationship between a
class and a list, such that the class is the class of things which are members
of the list. Unless for some reason one wants to make sets different from
classes, it seems appropriate to use classes for sets, and furthermore to use
owl:oneOf as the constructor which allows us to specify a specific set in
terms of an arbotrary ordering of its contents. The set of numbers 1,2 and 3
would then be written as

    
    
    [ owl:oneOf (1 2 3)] 
    

or, to elaborate it down to triples:

    
    
    [ owl:oneOf   
      [ rdf:first 1; rdf:rest [  
         rdf:first 2; rdf:rest [  
            rdf:first 3; rdf:rest rdf:nil]]]]
    

Of course, any reification of a set whish lists the same members in a
different order describes the same set.

###  Syntax

This is the more difficult choice! Here is a table of suggested syntax
extensions to N3 for sets.

Syntax extensions suggested for sets in N3  Syntax  |  Advantages  |
Disadvantages  
---|---|---  
(1, 2, 3)  |  Miniumal encroachment on to new punctuation.  
Comma becomes a marker for lack or ordering. This is consistent with an object
list.  |  Parser has to look ahead a whole expression to know which it is
dealing with: major change.  
($ 1 2 3 $)  |  "S" stands for "set". Otherwise just like lists.  |  
{$ 1 2 3 $}  |  "S" stands for "set". Curly braces are conventional for sets.
Curly braces are used for formulae, which are also unordered.  |  Curly is
used for formulae, which are not normal collections  
{$ 1, 2, 3 $}  |  "S" stands for "set". Curly braces are conventional for
sets. Curly braces are used for formulae, which are also unordered.  
Comma becomes a marker for lack or ordering. This is consistent with an object
list.  |  Curly is used for formulae, which are not normal collections.  
{* 1, 2, 3 *}  |  "S" stands for "set". Curly braces are conventional for
sets. Curly braces are used for formulae, which are also unordered.  
Comma becomes a marker for lack or ordering. This is consistent with an object
list.  |  Curly is used for formulae, which are not normal collections.
Asterisk could be used as infix operator, though not with .  
{, 1, 2, 3 }  |  Curly braces are conventional for sets. Curly braces are used
for formulae, which are also unordered.  |  Curly is used for formulae, which
are not normal collections. Weird and unconventional to start with a comma  
@Set{1, 2, 3}  |  Just a new keyword, no extra syntax.  |  d.  
  
The current choice is {$ 1, 2, 3 $} which is conventional mathematical set
notiation, plus dollar signs to distinguish a set from a formula.

An interetsing possibility pointed out by Sandro Hawke is to actually make
sets and formulas examples of the same thing. A formula is just a set: a set
of statements. This makes statements first class objects. This is inherently
appealing in its symmetry. However, as there is no statment opener syntax,
only the closer (".", and effectively ";" and ","), there is no way for the
parser to know in advance whether a statment or set is being parsed. This
would not be the end of the world, but makes life more difficult. Futher, the
current syntax alows an empty property list, so [ a :Deciduous, :Pine ]. is
valid N3. This means that { :x } is a valid statment (with no triples), which
would overlap with set syntax.

###  Disjoint sets?

There is an issue as to whether {$ :a , :b, :c $} imlies that a, b and c are
distinct. There was a [
discussion](http://rdfig.xmlhack.com/2005/01/26/2005-01-26.html#1106763446.326655)
of this in the SWIG.

If sets are disjoint:

  * You can say how many members are in a set. 
  * You cannot form the union or intersection of two sets unless all the members involved are known to be disjoint, (or one knows whcih ones are equivalent), for example if one knows that they each are members of a larger set. 
  * In applications where the assumption is that a set is disjoint, the system can check and trap an errro if two members turn out to be the same. 
  * Cwm in smush mode, --mode=e, when it takes into account equality, would probably remove dupliactes from sets but there would be no signifince. 

If sets are not disjoint:

  * You don't know how many members they have, in general. 
  * You can do set union, but not intersection. 
  * You can validly handle sets where you don't actually know how mny distinct (people say) there are. 
  * Cwm in smush mode, --mode=e, when it takes into account equality, would on loading a new equality, in some cases reduce the number of members of a set mentioned in the knowledge base. 

One possibility is to build into the processor that in a mode in whcih it is
aware of equality it also tracks disjointness, for example using inverse
functional properties and functional properties with numeric ranges.

Of course, where all the members of a set are vlues of a datatype which
provides a binary equality operator, such as integers, this is not a problem.

##  Considered design alternatives in other areas

(older)

  1. Using : for &gt;\- and -&gt; so that the propertylist looks like a list of attributes. Advantages: really human readable. Disadvantage: keep "=" as an operator. Also, I don't like "=" being used for something which is not equality. It is ingrained as a binary reflexive operator and it would be confusing to use it in attribute attribution. Alternative alternative: use ":" for both "-&gt;" and "-&lt;". 
  2. Use/allow keyword "has" for &gt;\- and "is" for &lt;-. Maybe, if still unambiguous, allow "of" for both "-&gt;" and "-&lt;". And/or use colon instead of "of". These assume that the english words people pick as properties are noun clauses. I actually preferred the use of verb clauses for what is in fact a verb. I used to prefer "wrttenBy" to "author". Now I have found the role-noun form much better. 
  3. Making the subject of the propertylist, be another property. (Say, "ref"). This is like Henrik's SOAP-RDF mapping. Every statement has to become an anonymous node syntax example: [ &gt;\- core:ref -&gt; [ &gt;\- x:firstname -&gt; "Ora" ] ; &gt;\- dc:wrote -&gt; [ &gt;\- dc:title -&gt; "Moby Dick" ]]. The thing becomes a binary rather than ternary syntax so we should use binary syntax. Using -&lt; and -&gt; only (omitting the &gt;\- and &lt;\- ) example would be 

[ core:ref : [ x:firstname : "Ora" ] ;

dc:wrote : [ dc:title : "Moby Dick" ]

]

or equally well

[ x:firstname : "Ora" ;

dc:wrote : [ dc:title : "Moby Dick" ]

]

We need better examples, requiring explicit reference to the subject by URI.

  4. Allowing well-formed XML element as object. reserve &lt;alpha for this? What does XML infoset look like expressed in RDF in notation3? decide: don't do it. Burdens notation3 compiler with XML parser weight. 
  5. Use &lt;&gt; for URIs instead of ' - DanC. Hmmmm I wanted to keep &lt;&gt; for other things maybe like string delimiters. Actually it is cool to use inverse &lt;. for stings &gt;this is a string&lt; because then you end up being able to make pages which look like markup and which are functions in notation3. 
  6. Bind vs @prefix. Bind was a directive which declared a namespace with an implicit "#" between the namespace and the local name. This has many advantages: it meant that by looking at a URIref one could separate it unambiguously into namespace URI and fragment ID. This in turn meant one could dereference the namespace URI to get a schema or other information describing the namespace. However, this is not standard RDF. Nevertheless, the use of namespaces ending in "#" is recommended, as then the items in the name space can be easily described by a single document associated with the namespace identifier. 
  7. Whitespace:  what about unicode NL? This was included as one  of teh few changes which happened in XML as it changed fro 1.0 to 1.1 . NL is a C1 control character which was introduced to allow the EBCDIC newline character to eb encoded.  Why should one have a separate NL from the LF which CCITT defined all those years ago as the code to be used when newline (CR LF together) was required? 

##  Fodder

Connolly points out: "This grammar starts to look a lot like the formalized
english/conceptual grammar stuff. &gt;
http://meganesia.int.gu.edu.au/~phmartin/WebKB/doc/grammars/ &gt;
http://www8.org/w8-papers/3b-web-doc/embedding/embedding.html

Philippe Martin says, "Given the similarities of your Notation 3 with the
(currently) more readable and expressive Frame-CG notation (FCG) that I
designed 2 years ago and that is one of the notations used in my large-scale
knowledge server [WebKB-2](http://www.webkb.org/) , you might want to have a
look at some executable [example
files](http://www.webkb.org/doc/webkb2OntologicalExamples.html) (e.g. ) and at
the [grammar](http://www.webkb.org/doc/F_languages.html#FCG). The wide range
of "quantifiers" is especially useful. You are welcome to copy any part of the
FCG grammar into your Notation 3. (email 2001/09/17)

##  Footnote

###  Thought process behind implicit definition

How does one label a node in notation 3 for incomming reference? (The
quivalent of "rdf:id=")? How about a property "Thought process behind implicit
definition How does one label a node in notation 3 for incomming reference?
(The quivalent of "rdf:id=")? How about a property "is hereby defined to be"
with a suitable shorthand? One can then refer to such as thing internally as
'#foo' which is a bit messy but not bad. You can't have keywords and
identifiers both using that precious status of pure alphanumerics unless you
reserve keywords. [ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname -&gt; "Ora"
] . [ '#ora' &gt;\- dc:wrote-&gt; [ &gt;\- dc:title -&gt; "Moby Dick" ] ] . [
&gt;\- x:firstname -&gt; "Laura" ] &lt;\- x:hasChild-&lt; '#ora' . or equally
well [ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname -&gt; "Ora" ] . [ '#ora'
&gt;\- dc:wrote-&gt; [ &gt;\- dc:title -&gt; "Moby Dick" ] ] . [ &gt;\-
x:firstname -&gt; "Laura" ] &lt;\- x:hasChild-&lt; '#ora' . Ah. Now consider
what is the difference betwen reference and definition? I conclude there is
none, as both are the assertion that the resource in question is identified by
a URI. In the statements: [ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname
-&gt; "Ora" ] . [ '#ora' &gt;\- x:lastname -&gt; "Lassila" ] . is there any
significance that the node '#ora' is defined to be one which has firstname
"ora" and lastname "Lassila" whichever way one looks at it. I would therefore
propose that the use of a new local symbol :foo or '#foo' is taken as
introducing it, but the definition of it by the document is really the whole
web of statements which involve it. In fact, it maybe rather difficult to talk
about the definition of it as distinct from the document, as as it is always
best to avoid extra concepts, I won't. The above examples should just be,
therefore, [ '#ora' &gt;\- x:firstname -&gt; "Ora" ] . [ '#ora' &gt;\-
x:lastname -&gt; "Lassila" ] isn't that simpler?.is hereby defined to be" with
a suitable shorthand?

One can then refer to such as thing internally as '#foo' which is a bit messy
but not bad. You can't have keywords and identifiers both using that precious
status of pure alphanumerics unless you reserve keywords.

[ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname -&gt; "Ora" ] .

[ '#ora' &gt;\- dc:wrote-&gt; [ &gt;\- dc:title -&gt; "Moby Dick" ] ] .

[ &gt;\- x:firstname -&gt; "Laura" ] &lt;\- x:hasChild-&lt; '#ora' .

or equally well

[ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname -&gt; "Ora" ] .

[ '#ora' &gt;\- dc:wrote-&gt; [ &gt;\- dc:title -&gt; "Moby Dick" ] ] .

[ &gt;\- x:firstname -&gt; "Laura" ] &lt;\- x:hasChild-&lt; '#ora' .

Ah. Now consider what is the difference betwen reference and definition? I
conclude there is none, as both are the assertion that the resource in
question is identified by a URI. In the statements:

[ &gt;\- n:def -&gt; '#ora' ; &gt;\- x:firstname -&gt; "Ora" ] .

[ '#ora' &gt;\- x:lastname -&gt; "Lassila" ] .

is there any significance that the node '#ora' is defined to be one which has
firstname "ora" and lastname "Lassila" whichever way one looks at it. I would
therefore propose that the use of a new local symbol :foo or '#foo' is taken
as introducing it, but the definition of it by the document is really the
whole web of statements which involve it. In fact, it maybe rather difficult
to talk about the definition of it as distinct from the document, as as it is
always best to avoid extra concepts, I won't.

The above examples should just be, therefore,

[ '#ora' &gt;\- x:firstname -&gt; "Ora" ] .

[ '#ora' &gt;\- x:lastname -&gt; "Lassila" ]

isn't that simpler?.

* * *

##  References

