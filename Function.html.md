[![](https://www.w3.org/Icons/WWW/arch1990.gift)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

#  Function

##  Home document

When WWW starts up, it presents the user with a home document. [to be
elaborated how this is selected].

##  Presentation

Documents are presented in one of three ways:

  * as formatted SGML-source text, by WWW itself, with anchor display and selection possible, 
  * as text or PostScript, by WWW itself, with anchor display and selection possible, 
  * as any other format of document by a foreign program which understands the format, but with no anchor display (and hence no selection possible). 

##  Navigation by link

Only tail anchors are visible. Choosing the tail anchor of a link (by double-
clicking or typing a number etc.) WWW [traverses the
link](https://www.w3.org/DesignIssues/FunctionTraverse.html) and displays the target document, with the head
anchor highlighted (if this is not the entire document)

##  Navigation by Search

A document which is an index will have an associated search panel (or prompt)
where the user has to type search keywords. Confirmation of the keyword set
(by typing return to the search panel) will lead to the search being done and
the resulting list of data being displayed as a new document.

