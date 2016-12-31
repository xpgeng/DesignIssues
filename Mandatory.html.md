Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:07 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Axioms of Web Architecture: n

* * *

#  Mandatory extensions

There is a common requirement for the design of a language on the web that it
should allow for extensions, but it must allow a clear declaration as to
whether understanding of an extension is a requirement to understanding of the
document or whether it may be ignored. (See [Evolvability](https://www.w3.org/DesignIssues/Evolution.html))

Historically the lack of such a "mandatory field" has led to a complete
inabaility to get any particular guaranteed behaviour be clients on the web.

This is essential for partial understanding and the smooth evolution of the
web.

A simple requirement on a language is that it not only provide for its own
extension, but provides for a way to explain whether a given extension is
optional or not. This is a fundamental key to smooth evolution from the
language to a new version.

There are manyways in which it can be done. It can be done term by term, or in
bulk about a whole new language. It can be specified in the new document, in
the schema for the new language.

XML provides in Namespaces a standard way of extending languages. It should
also, in my opinion, provide a standard way to specify mandatopry or optional
extensions.

I propose two things:

###  Sublanguages

The simple assertion that language A is a sublanguage of language B means that
the writer's intent is preserved if a dpcument in language A is converted into
a document in language B just by relabelling every term as being from langauge
B. For XML, this means that a receiver of namespace A can simply process it as
though the namespace had been delcared as B.

This assertion has got to be simple enough to put into a document for cases
where the functionality is needed without the receiver having to dereference a
schema.

###  Optional/Ignoreable/Mandatory flags for elements

In XML there are three simple thiong you can do with an element you don't
understand.

  1. Stop, and conclude you do not understand the document, or the clause in the document; Example : logical NOT 
  2. Ignore the elementand all its contents (including child elements) Example; &lt;Comment&gt;
  3. Replace the element with its contents (including children). Example: &lt;bold&gt;

The schema langauge needs to be able to specify these very simply, and indeed
it would be neatto be able to do it in a document for a given elemnt, or in
one fell swoop for all the elements in a given namespace.

Languages which donot use XML should attend to these needs in their own way!

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

