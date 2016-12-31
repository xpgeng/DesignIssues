[![](https://www.w3.org/Icons/WWW/arch1990.gif)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

#  Document formats

The question of the format of the contents of a node is independent of the
format of all the management information (except for the format of the anchor
position within the node content). Therefore, the hypertext system can be
largely defined without specifying the node format. However, agreement must be
reached between client and server about how they exchange content information.
Many hypertext systems qualify as ªhypermediaº systems because they handle
media other than plain text. Examples are graphics, video and sound clips,
object-oriented graphics definitions, marked-up text, etc.

##  Format negotiation

Most hypermedia systems on the market today have the same application program
responsible for the hypertext navigation and for the browsing. It would be
safer to separate these features as much as possible: otherwise, in defining a
universal hypertext system, one is burdened with defining a universal
multimedia browser. This would certainly not stand the test of time. Node
content must be left free to evolve. This implies that format conversion
facilities must be available to allow simple browsers to access data which is
stored in a sophisticated format. Such conversion facilities tend to exist in
many applications, though not, in general, in hypertext applications.

The format of the content of a node should be as flexible as possible. Having
more than one format is not useful from the user's point of view -- only from
the point of view of an evolving system. I suggest the following rules:

##  1\. Basic formats

There is a set of formats which every client must be able to handle. These
include 80-column text and basic hypertext ( [HTML](https://www.w3.org/MarkUp/MarkUp.html) ).

##  2\. Conversion

A server providing a format which is not in the basic set of formats required
for a client must have the possibility of generating some sort of conversion
of the text (even if necessary an apology for non-conversion in the case of
graphics to text) for a client which cannot handle it. This ensures universal
readability world over.

##  3\. Negotiation

For every format, there must be a set of other possible formats which the
server can convert it into, and the most desirable format is selected by
negotiation between the two parties. The negotiation must take into account:

  * the expected translation time, including current load factors 
  * the expected data degradation 
  * the expected transmission time (?!!) 

The times one could assume will be roughly proportional to the length of the
document, or at least linear in it.

Application-specific node formats (e.g. physics event) would allow specialized
browsers to perform local processing. This is a natural extension of the
hierarchy of node formats. I would suggest one stick to the rule that a server
providing such a type of data must provide some default conversion to a
standardized view.

An index or a keyword could be a specific node format which would be
manageable by a browser.

##  Examples

Examples of rich text formats which exist already at CERN are as follows,
with, in brackets after each, other formats into which it might be
convertible:

  * [SGML](https://www.w3.org/MarkUp/SGML.html) ( [Tex](../../DataSources/QWERTZ/README.txt) , Postscript, plain text) 
  * Bookmaster (Postscript, I3812, plain text) 
  * TeX (DVI, plain text) 
  * DVI (IBM 3812, Postscript, etc) 
  * Microsoft RTF (postscript, plain text, Next ªWriteNowº) - [See Specs](../../DataSources/RichTextFormat/RTF.txt)
  * Postscript, [Editable Postscript](../../Standards/PostScript/IPF.html) (IBM 3812 bitmap) 
  * plain text 

When a server (or browser) is obliged to perform a conversion from one format
to another, one imagines that the result would be cached so that, if the same
conversion were needed later, it would be available more rapidly. Format
conversion, like notification of new material, is something which can be
triggered either by the writer or by the browser. In many cases, a conversion
from, say, SGML into Postscript or plain text would be made immediately on
entry of the new material, and kept until the source has been updated (See
[caching](https://www.w3.org/DesignIssues/Caching.html) , [up to design issues](https://www.w3.org/DesignIssues/Overview.html) ).

* * *

&amp;copyTimBL 1991

