[![W3C](https://www.w3.org/DesignIssues/w3c_home.gif)](https://www.w3.org/Overview.html)

Tim Berners-Lee

Date: February 6, 1997, updated 9/97

Status: personal view. Editing status: Italic text is rough. Requires complete
edit and possibly massaging, but content is basically there.

Audience: Those people who asked what I meant by a consistent user interface
and then said, "Don't just say it, write it down!". For software developers in
the hope that some of this will come true.  This has worked before. I'm a bit
embarassed, as everyone has pet ideas about how the UI is frustrating, and
listening to them can be tedious, I know! Perhaps this is why I haven't
written this down before.

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Web Architecture: 5

See also [ComNet 97 talk](https://www.w3.org/Talks/9702ComNet/slide1.htm).

* * *

#  Cleaning up the User Interface

Tim BL 6 Feb 97

We can talk in the abstract about the sorts of things we'd like to do, but it
is a wise thought experiment, to imagine how the user interface to a more
powerful Web would be. So here is a an attempt to do that thought experiment.
There are no screen mockups -- as I said, you have to use your imagination.  

###  Consistency

First of, all, the interface to a universal space should have a certain
universal consistency. Currently, the user interface yu see on your PC or Mac
has a few unfortunate inconsistencies which make it more difficult to use, and
less powerful. One is that the "desktop" interface to the file system is
different from the "browser". (See talk at Boston Web Conference WWW4, Dec
1995). It is crazy, if you think about it, that the whole screen is use to
represent the information which happens to be on your local file system, using
the metaphors of folders, while one window is used to represent the
information in the rest of the world, using the metaphor of hypertext. What's
the difference between hypertext and a desktop anyway? You can double click on
things you find in either. Why can't I put folders into my hypertext
documents? Why can't I write on the desk? Folders should be just another sort
of document. My home page could be one, or it could be a hypertext document.
The concepts of "folder" and "document" could be extended until they were the
same, but I don't think that that would be necessarily a good idea. It's OK to
have differet forms of object for distinctly different uses.

###  Location fixation

The only fundamental difference between a hypertext document and a folder is
that there is a special relationship between any document and the folder where
is "is". Unix allows a file to be in more than one directory (with hard links)
provided they are on the same disk. DOS requires a file to be in just one
directory, which again must be on the same disk. Users should not have to
worry about what disks files are on. Suppose the system just files everything
under its creator an d its creation date, and the rest of the system is just
pointers (soft links, hypertext links, shortcuts), Then a folder becomes a
useful sort of document for helping us organize things, but not a container
with implications on physical storage. The relationship between a folder and a
file in it becomes just a hypertext link. Ah, consistency!

###  Protocol - Smotocol

Another inconsistency is the current strange division between mail, browser,
and news reader tools. Each have editors. The editors are in some cases plain
text, and in some cases fancier things such as HTML. On the Internet, a mail
agent allows you to use the Simple Mail Transfer Protocol, a news agent allows
you to use the Network News Transfer Protocol, and a web editor allows you to
use the Hypertext Transfer Protocol. This is of course totally meaningless to
a user. From the user's point of view, the mail program allows you to move
data between mailboxes (folders by any other name) and also allows you to link
it into someone else's "In" box. I say "link" as it creates the relationship
"this message (file by any other name) is in this mailbox (folder)", which we
said above should be a link.

A news editor allows you to link a news document to a widely visible group
(box, folder by any other name) which is visible to people all over the world.
Functionally, it is very like mailing something to a list of people, as it
creates links to the document from groups in each of their news readers.

A web editor allows you to upload a document into a web server, though the way
in which you do that varies. (The original meaning of the HTTP "put" operation
was to have been a very equivalent "make new document and make link from this"
operation.)

Now suppose you want to create a bit of information and you want to link it
from a few individual's "in" boxes, a few news groups and a few hypertext
documents. You also want it to show up in various folders. Which application
should you use?

Clearly, this is a choice which the user should not have to make.
Conceptually, a number of links are being made. In practice, various protocols
will be used by the system. In the future, combined protocols may exist which
efficiently perform all these functions as appropriate. Let's not bother the
user with this. When I create an object, I want to pick the type of object I
am creating. I also think it is reasonable, if anyone else is going to have
access to the object, for me to specify the access list and the distribution
terms: I am controlling my new intellectual property. It is also useful for me
to specify what sort of quality of storage I want for the document. Do I want
it archived reliably for posterity? Do I want it instantly available very
rapidly and reliably? The answers to these questions will determine where the
system will store my data. The last thing I want to be asked is the filename.

The "save as" filename dialog box is one of the things currently holding up
our civilization. It doesn't ask the right information from the user. It asks
it not when you are creating the document (and thinking about it at that high
level) but when you have finished and are about to do (and thinking about)
something else. [See [ Cooper on
this](http://www.cooper.com/articles/vbpj_secondary_storage_dilemma.html)]. As
you move information from your head into a computer, everything can be
intuitive until this step asks you to think of the disks and the operating
system.

Creators of documents should be able to specify

  * Access lists and distribution terms 
  * Quality of storage 

  
---  
  
Of course, I won't want to be negotiating each of these parameters every time
I create a new object, so probably I will have a set of templates, standard
genres of document, for which these things have been set. In the case of HTML
files, I will probably want to associate a default content and a default style
sheet with each template. This will make it easier for me and for my readers
to get an intuitive feel for the access and archival status of documents at a
glance.

I will get back a URI from this operation. The quality of storage is part of
the agreement between me, as a creator of an object, and the service I use to
create and support that URI.

Sure, people like to pick URIs so that they can be mnemonic. I don't mind
that. The problem is when the URIs are picked so that it is difficult to
support them in the future. (See the section on naming, and HTTP PUT).

Let's assume that this inconsistency will be dealt with in future.

###  Signing: From Documents to Deeds

So the consistent user interface we have so far is one in which we are at home
with documents and links, and we communicate by massaging the documents and
the links.  The whole thing is "quasi-static" -- at any one time you can
believe you understand a part of it.  It has state. When you change its state
you can see what you are doing.

That's not enough.  It's not enough because in this model everything is
malleable: every document is a "living" document. Everything can change.  This
is great for an encyclopaedia but its no good for a check book.  It contains
description, but because action is represented only in the limited constrained
form to those actions which can be viewed as changes of state, there are
things we just can't do. We can do idempotent actions -- those which are just
as good if you do them twice as if you do them once.  This doesn't work for
paying bills.

We can introduce actions which count (or if you like, "actions which you can
count") in two ways which boil down to the same thing.  One way is for us to
enrich the concept of operations on the net from "GET", "PUT" and "LINK" to a
whole plethora of different functions.  We would probably divide were sources
by their object "class", which would define what set of operations are
available for each resource. This is the familiar world of distributed object
oriented programming.

The second way is that we would allow, in the user interface, documents to be
signed.  A signature on paper is a special thing (in principle).  It is a
countable operation.  You make a signature on the document and it becomes
something different.  No longer duplicatable at will, you act of signing is
caught -- and you can be held to it.  The document becomes something which has
been done: a **deed**. This is the familiar world of legal process.  On the
web, it happens when you press a "submit" button and your order is submitted
to the mail order company. When you make a document into a deed, it freezes.
You can't change deeds.  You can revoke them or cancel them out with other
deeds, but you can't change one. Deeds are not living documents.  In fact,
lots of documents are in practice frozen in that they aren't going to change
much.  But they may not be deeds: noone has explicitly made an action on them.  

The two forms are equivalent, as when you make a deed, you can in the document
write the name and parameters of any function you want executed, and submit it
to a remote operation agent. Similarly, whenever a remote non-idempotent
operation is made using some Remote Procedure Call protocol, in practice the
protocol involves making some message up containing the parameters, and
directly or indirectly putting on it some sequence number or identifier to
prevent it from being accidentally operated on twice.  Both are abstract
representations of a commitment, and action which counts.

As we're talking about user interface here, I'd like to see a clean interface
for making a deed, which makes it quite clear to me that I am committing
something, and not just doing another search.  I suppose I have a set of
"rubber stamp" icons which leave a name/date stamp on a document.  Different
stamps can be made with different levels of security.  They may represent
actions by different people, different roles, with different levels of
authority.  I guess I'd have one for stamping W3C Recommendations which have
been though the process, and a totally different one for ordering medium sized
purchases on my credit card.

Deeds don't have to be signed digitally (but it helps).  Every time you press
"send" in your email you are making a deed. The document freezes.  You may
even be digitally signing it. You lose control -- you can't take it back.  

Socially, we will have to accept electreonic deeds. Also, we will have to
define the limits of commitment which someone can imply by changing living
documents without explicitly making a deed.

@@@@

###  The "Oh yeah?" button

See also WWW4 Boston talk.

Deeds are ways we tell the computer, the system, other people,  the Web, to
trust something. How does the Web tell us?

It can happen in lots of ways but again it needs a clear user interface.  It's
no good for one's computer to be aware of the lack of security about a
document if the user can ignore it. But then, most of the time as user I want
to concentrate on the content not on the metadata: so I don't want the
security to be too intrusive. The machine can check back the reasons why it
might trust a document automatically or when asked. Here is just one way I
could accept it.

At the toolbar (menu, whatever) associated with a document there is a button
marked "Oh, yeah?".  You press it when you loses that feeling of trust.  It
says to the Web, "so how do I know I can trust this information?". The
software then goes directly or indirectly back to metainformation about the
document, which suggests a number of reasons. These are like incomplete
logiocal proofs. One might say,

> "This offer for sale is signed with a key mentioned in a list of keys
(_linked_) which asserts that tthe Internet Consumers Association endoses it
as reputable for consumer trade in 1997 for transactions up to up to $5000.
The list is signed with key (_value_) which you may trust as an authority for
such statements."

Your computer fetches the list and verifies the signature because it has found
in a personal statement that you trust the given key as being valid for such
statements. That is, you have said, or whoever your trusted to set up your
profile said,

> "Key (value) is good for verification of any statement of the form `the
Internet Consumers Association endoses page(p) as reputable for consumer trade
in 1997 for transactions up to up to $5000. '"

and you have also said that

> "I trust for purchases up to $3000 any page(p) for which `the Internet
Consumers Association endoses page(p) as reputable for consumer trade in 1997
for transactions up to up to $5000."

The result of pressing on the "Oh, yeah?" button is either a list of
assumptions on whcih the trust is based, or of course an error message
indicating either that a signature has failed, or that the system couldn't
find a path of trust from you to the page.

Notice that to do this, we do not need a system which can derive a proof or
disproof of any arbitrary logical assertion. The client will be helped by the
server, in that the server will have an incentive to send a suggested proof or
set opf possible proof paths.  Therefore it won't be necessry for the client
to search all over the web for the path.

The "Oh, yeah?" button is in fact the realively easy bit of human interface.
Allowing the user to make statements above and understand them is much more
difficult. About as difficult as programming a VCR clock: too difficult. So I
imagine that the subset of the logic language which is offered to most users
will be simple: certainly not Turing complete!

###  Programming the space: Macros by example.

@@@ TBD

##  Specific notes on Windows UI and Typical Web browsers

(1997)

The gist of it is the need for greater consistency in the UI and the
underlying system.

###  Consistency

Some basic principles:

1\. Anything of any value and persistence must have a URI so that it can be
referenced (yes, I know Microsoft have a Moniker scheme but now it has to be
URIs to go global).

2\. Any place I can use a URI I can use any URI.

3\. Links are an evident as a primary user interface metaphor, with a
consistent drag/drop or control/drag/drop for link creation, and consistent
ways of viewing by link type.

4\. The system should generate persistent URIs wherever possible. These can be
just URLs in file or http space but they should not change. This is a longer
term thing.

5\. Things like start menus, bookmarks, favorites, recent document lists,
toolbars, should be viewable as discreet objects in familiar ways. A Good
Thing is the ability to easily see and manipulate the start menu in Explorer
(right click Start). A Bad Thing is a modeful "organize favorites" dialog box
is the most inconsistent outdated constraining way of moving things around I
have seen in a while.  A modeless "Goto bookmarks" is better, but

I propose that any set or hierarchical structure should have a consistent
windows explorer interface. You clearly feel that anything which is a set can
also have an HTML view. In that case, I want HTML views of everything. Look at
al the containers we have:

  * Deskto 
  * Folder 
  * Start menu 
  * Toolbars 
  * Web pages 
  * Mailboxes 
  * Bookmarks 
  * Favorites 

These must have consistent interfaces.

Some of these we can do without. Favorites, most of the Start Menu, and
mailboxes are all ways of classifying things. They should all basically have
the same interface and frankly I don't see the need for them being different.
I want to put my inbox in my start menu. I want to be able to chose whether
something I put in a menu is terminal or expanded. In general. (I could always
put a link to the Favorites folder into the start menu but it wouldn't be
expanded as a menu. I'd like general control over menus.

(Examples of things I want to do: Bookmark mail messages of interest, indeed
any object.  Save a web page in a mailbox (which would freeze it in the cache
and keep a pointer to it)

...

)

Dialog boxes are as we really know bad UI. The "Save As" and "Open" dialog
boxes are a pain (I always want to be able to delete and rename files in them)
because the are constraining and inconsistent, and they block until you get
out. I'd be happy for an open box to simply launch an explorer window or
select a current one, while providing a receptacle for icons which are to be
opened. I'd like that receptacle (which is just the application icon) to be a
URI I can save in any of the containers above.

The history list should of course be a something which works across all
applications. A time-based view is a neat history lis, but it should apply
across everything I have done in any applicationt. Make it generic so it works
on any object. Make the index of everything I have done (maybe my whole click
stream) be available as such an object, to be viewed just like a mailbox. I
should even be able to make a link into it.

###  Maito: addresses

A mailto address is a misnomer (my fault I feel as I didn't think when we
created it) as it is not supposed to be a verb "start a mail message to this
person", it is supposed to be a reference to a web object, a mailbox. So
clicking on a link to it should bring up a representation of the mailbox. This
for example might include (subject to my preferences) an address book entry
and a list of the messages sent to/from [Cc] the person recently to my
knowledge. Then I could mail something to someone by linking (dragging) the
mailbox icon to or from the document icon.

###  Modularity: MIME types and Operations

The OS as a concept  is currently having trouble with modularity -- the module
used to be an application which provided its own communication and document
types. Now the MIME types are orthogonal. I see new applications as either
producing new mime type support or new link functionality (or both) but
separably.

I should be able to mail anything. Suppose I am editing a photo. The tool bars
are photo editing toolbars. WhenI want to mail it, I find the person I want to
mail it to (any way: not from an adders book forcibly -- I can put my friends
in my start menu or anywhere or of course find them on the web). I drag the
document onto the person icon. Now that relationship gives me a choice (To,
Cc, etc), and I will now get an extra toolbar for controlling the mail
options. If I drag it to a newsgroup, the functionality will be exactly the
same though the options may be different. I can then the links from the
message by type (To, Cc, newsgroup, embedded hypertext link, version info, etc
etc) in a consistent way. I regard dragging the icon of the document to a
folder as being making a link too. The system should stop regarding folders as
where things are stored. That has got to be decoupled, to separate the logical
thing (I classify this as important travel) from the physical thing (I put
this on drive C:). That is going to be a steady change, but early simple steps
are

  * allow the user to specify the algorithm for defining the filenames for new objects of each type, when defining templates, with a macro  like  
http://my.co.com/BY/&lt;user&gt;/&lt;yymm&gt;/NOTE/&lt;seq&gt;.txt

  * give a good default set of macros which will result in filenames which don't have to change later 
  * ask when defining the template or creating a file without a template for a storage quality which will determine in the short term the filename  and in the long term a way in which the system will duplicate, backup and distribute the document 
  * ask at the same time for a default Acess Control List for the template. 

When I hit "Send" or "Commit", then the document is frozen, and the  mail
engines and NNTP software [and version control software]  starts to actual
implement the links, and the web server allows appropriate access. All this is
under the hood, which you can lift to see how its getting on if you like.

###  Archival and Access levels

This storage quality is a common parameter which I want to be able to change
for anything. For example, I may decide that a web page or a newsgroup article
I want to have on a "personal archive" availability. S I just change it with a
menu item. No "Save As". No filenames. It has a URI already. And then I  know
it will always be available to me on my desktop and laptop. Just like that.

The two toolbars of persistence level (think of name for that) and  access
level are so important they deserve space maybe in that space to the R of the
menu bar, or in window title banner. At least in icon form. I don't expect to
have many combinations of them once I have customized the combinations I need
with the archive and access wizard.

The archive status includes important flags for disconnected working -- is
this object to be replicated and if so how often, etc.

###  Disconnected operation

The system has got toknow what its connectivity is at any time. Without a
reboot! I would like this to be a switch available across the board, switching
IPs and diconnected operation.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html); On to [Editing interfaces](https://www.w3.org/DesignIssues/Editor.html)

$Id: UI.html,v 1.5 2009/08/27 21:38:09 timbl Exp $

