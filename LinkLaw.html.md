Tim Berners-Lee

Date: April 1997

Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

###  Commentary on Web Architecture

* * *

#  Links and Law

###  _Preface_

This personal note I have put into the set of web architectural notes as it
expresses fundamental understandings upon which the practical use and power of
the web rest.

The questions addressed are about the relationship of the hypertext forms of
_linked_ and _embedded_ material to the social concepts involved such as
attribution, endorsement, and ownership of information.

Links in hypertext are new in that they can be followed automatically, but the
concepts of reference and inclusion of material predate paper. There should
not therefore be much confusion about what links imply, but as there have been
some strange suggestions recently which would seriously damage the web, I
write this note.

###  Abstract

Normal hypertext links do not of themselves imply that the document linked to
is part of, is endorsed by, or endorses, or has related ownership or
distribution terms as the document linked from. However, embedding material by
reference (sometimes called an embedding form of hypertext link) causes the
embedded material to become a part of the embedding document.

##  Two sorts of link

Basic HTML has three ways of linking to other material on the web: the
hypertext link from an anchor (HTML "A" element), the general link with no
specific source anchor within the document (HTML "LINK" element) and embedded
objects and images (IMG and OBJECT). Let's call A and LINK "**normal**" links
as they are visible to the user as a traversal between two documents. We'll
call the thing between a document and an embedded image or object or
subdocument "**embedding**" links.

This distinction is an old one in hypertext. Some systems such Peter Brown's
original "Guide" worked only by expanding links inline, and some (such as HTML
before the IMG tag was introduced) worked only with normal links.

##  Normal Links

**The intention in the design of the web was that normal links should simply be references, with no implied meaning.**  
---  
  
A normal hypertext link does NOT necessarily imply that

  * One document endorses the other; or that 
  * One document is created by the same person as the other, or that 
  * One document is to be considered part of another. 

Typically when the user of a graphical window-oriented Web browser follows a
normal link, a new window is created and the linked document is displayed in
it, or the old document is deleted from its window and the linked document
displayed in its place. The window system has a user interface metaphor that
things in different windows are different objects.

###  Meaning in content

So the existence of the link itself does not carry meaning. Of course the
contents of the linking document can carry meaning, and often does. So, if one
writes "See Fred's web pages (link) which are way cool" that is clearly some
kind of endorsement. If one writes "We go into this in more detail on our
sales brochure (link)" there is an implication of common authorship. If one
writes "Fred's message (link) was written out of malice and is a downright
lie" one is denigrating (possibly libellously) the linked document. So the
content of hypertext documents carry meaning often about the linked document,
and one should be responsible about this. In fact, clarifying the relative
status of the linked document is often helpful to the reader.

##  Embedded Material

The relationship between a document and an image embedded in that document is
quite different from normal link. (In some designs it is still refered to as a
sort of link).

**Images, embedded objects, and background sounds and images are by default to be considered part of the document.**  
---  
  
If I say, "To understand this you only have to read this article", or "This is
the agreement between us", I am talking about a particular document. It is
important that we have a clear picture of what is part of that document and
what isn't. Embedded images clearly are part of the embedding document. The
author of a document has responsibility for the content, even if the images he
or she includes are from another web site.

(There are issues of expectations to be set about availability and security
from corruption of remote material, but I do not address these here. Here I
just emphasize is that embedded images should be considered part of a
document, but documents connected by a normal link should be regarded as
separate documents.)

We compose documents out of parts, and the finished work comprises
contributions from the parts and also from the arrangement. It is very
important that we can include remote parts by reference without having to make
a separate local copy. When an embedded image (or sound) is included by
reference to its original address (URI) this allows an inquirer to know that
address, and hence know the current version of the image. It allows the owner
of the image to to a certain extent to know and possibly to control who has
access to that image. Also I expect in that in the future it will allow one to
find out the owner and licence terms for distribution of that image, which is
important for intellectual property rights to be respected on the Web.

####  Explict distinction

Advertising provides an exception to this rule: a case in which the embedded
image is **not** part of the document.  At risk of making ittoo easy for users
to turn  off advertizing, it would be ideal if the distinction were make in
the markup between embeeded information which is or is not part of the
document.  This would allow, for example, a border to be places around an
advertizement to allow the user to realize that it does not come from the same
source as the text.  I personally feel that this would be an important step
forward in the integrity  of the web. A flag like

    
    
    <IMG src="banner-ad.gif" foreign>
     
    

would be fine.

##  User Interface

When Web documents are presented to people, most current browsers (1997) make
a clear distinction between embedded images, which are presented in the same
window as the embedding document at the same time, and linked documents which
never are. The window system's concept of a "Window" is used to convey when
things are part of the same document. It is important for many reasons, some
of which were mentioned above, that user interfaces continue to make this
distinction.

####  Frames

The "frames" of HTML unfortunately provide an interface which is less clear.
The parts of the document do appear with the same window, but because within a
single frame (subsection of a window) one can follow hypertext links replacing
content with a separate document, it is easy to create the impression that the
owner of the surrounding frames is in fact responsible for the defining
document. It is possible that work by the HTML community can produce explict
markup (such as the "foreign" flag above) for conveying, when frames are used,
which parts of the screen are considered to be the same document. In the mean
time, it is appropriate for content providers so make efforts to ensure by the
design of (and/or statements on) their web pages that users are not left with
the illusion that information within an embedded frame is part of their
document when it is really not.

_Next: Some dangerous [**Myths** about Links](https://www.w3.org/DesignIssues/LinkMyths.html)_

* * *

_A reminder that this is personal opinion, not related to W3C or MIT policy. I
reserve the right to rephrase this if misunderstandings occur, as its always
difficult to express this sort of thing to a mixed and varied audience._

* * *

[Next:  Metadata architecture](https://www.w3.org/DesignIssues/Metadata.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

