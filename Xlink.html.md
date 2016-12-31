Tim Berners-Lee  
Created Date: 2002/06, last change: $Date: 2002/07/01 18:33:45 $ Z  
Status: personal view only. Editing status: first draft.

Written in response to TAG discussion and specifically [tag issue
23](http://www.w3.org/2001/tag/ilist#xlinkScope-23)

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  When should I use XLink?

When we are designing a new XML language, and we refer to something on the web
by URI, should we use [XLink](https://www.w3.org/DesignIssues/)?

Three possible answers:

  1. No, you don't have to unless there is some functionality of xlink which you would like to lever. 
  2. You should use xlink whenever your application is one of hypertext linking, as xlink functionality such as power to control user interface behavior on link traversal is useful and should be implemented in a standard way to allow interoperability. 
  3. You should always make an XLink whenever you make a reference with a URI, as all such references are in some way a link. 

The short answer in my humble opinion, is that (2) is right.

When an application uses functionality which is within the scope of Xlink, it
should use xlink. To do otherwise breaks the principle that we are trying to
make an interoperable web.

The third extreme case, that xlink should always be used, is not tenable, as
URIs are used generally as identifiers for everything. Paul Cotton and David
Orchard pointed out on a TAG call (2002/6/17) that the scope of Xlink is
hypertext linking. A motivation for XLink was to give to languages for human
documents a much richer form of hypertext than HTML, with features which had
in fact been used in hypertext products for many years before the web.

A counter-example is the speech grammar specification, which uses a URI
parameter to refer to a piece of grammar in an external file. This logical
information is not intended to be browsed by people as a document. There is no
need for the hypertext functionality of Xlink. There is no need to clutter the
language with xlink:href syntax.

The idea that all uses of URIs are formally hypertext links does not use the
term _hypertext_ in the sense I use here, or in the sense in which hypertext
link functionality is the scope of Xlink.

The XHTML specification does not use xlink, as (I understand) the working
group felt that it was too clumsy to use a different namespace, and they
wanted it to look like HTML, which uses href=. The group is (2002/06) looking
at schema annotation ways of declaring html:href to carry the significance of
an xlink. These are known as "hlink". The pros and cons of schema annotation
in general as a means to add semantics or style to a langauge are currently
under debate in the community.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

