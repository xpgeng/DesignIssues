[![W3C](https://www.w3.org/DesignIssues/w3c_home.gif)](https://www.w3.org/Overview.html)

Tim Berners-Lee

Date: April 1998, updated 9/97

Status: personal view. Editing status: Italic text is rough. Requires complete
edit and possibly massaging, but content is basically there.

Audience: Those people who asked what I meant by a consistent user interface
and then said, "Don't just say it, write it down!". For software developers in
the hope that some of this will come true.  This has worked before. I'm a bit
embarassed, as everyone has pet ideas about how the UI is frustrating, and
listening to them can be tedious, I know! Perhaps this is why I haven't
written this down before.

Contributions: Examples from Dan Connolly of what needs to be easy.

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Web Architecture: 6

See also [ComNet 97 talk](https://www.w3.org/Talks/9702ComNet/slide1.htm).

* * *

#  Cleaning up the User Interface 2: Hypertext editing

Tim BL 3 April 1998

If you think surfing hypertext is cool, that's because you haven't tried
writing it. If you have found your bookmarks/favorites have become a more and
more important part of your life, that's because you have learned to put up
with the simplest form of hypertext editing there is as a compromise. If you
are using a really intuitive hypertext editor, then tell me about it.

##  Hypertext editing

The Web is universal and so should be able to encompass everything across the
range from the very rough scribbled idea on the back of a virtual envelope to
a beautifully polished work of art.

Somewhere near the "draft" end of the scale is its use a hypertext communal or
personal notebook which is very close to a major original use of the Web in
1990. In this mode I can browse over notes made by people in my group, and
rapidly contribute new ideas.

I'm editing this now on a pretty intuitive editor. AOLPress is may not be a
top of the line pape layout tool but it can do some of the things which my
original "WorldWideWeb" program could do. I wouldn't say that either of these
programs was the ideal interface, but if you look also at things like KMS and
Doug Engelbart's interface, you see that for all the fancy HTML we have
nowadays, there is some immediacy we have lost.

Here are some things I would like to be able to do very rapidly. Dan Connolly
suggested a click count as a way of measuring the effort, with 10 clicks
penalty when you have to think of a filename or anchor ID.

##  Imagine there's no mode, imagine there's no location

A first assumption, by the way, is that you have modeless interface in which
browsing and editing are not separate functions. If to edit a page, you have
to switch from browsing mode to editing mode, then you have lost already. If
you have had to switch to edit mode, and think of a local filename in which to
save the file, then you have lost doubly, If you have had to answer lots of
difficult questions about where to save absolute or relative links, you have
lost yet again and probably messed up the file already! You should not have to
think about "where" things are.

##  Make a link

In WorldWideWeb, you had to

  * Select the target phrase 
  * Hit "command/M" to mark where you were, (Which generated an anchor with a made up name, and remembered it); 
  * Switch to the document to contain the link if different; 
  * select the text to be linked; 
  * Hit "Command/L" to make the link 

In AOLPress, I can do the same thing except the "Mark" function consists of
three steps: Press the "anchor" button, hit return to accept the program's
suggested anchor name, and then hit the "copy URL" button.

In a drag-and drop world, every window should have an icon for the document it
holds which can be dragged to make a link. (Later versions of NeXTStep had
this with alt/click on the titlebar).

##  Make a new linked node - Annotate

In WorldWide Web, this was deliberately easy:

  * Select a phrase 
  * Hit "Command/N". (A new node is created) 
  * Think of a filename in response to the "SaveAs" dialog box :-( 

The new node would be created from a template which could set up to have your
signature at the bottom, etc. The original phrase was automatically linked to
the new node. The cursor was left ready for you to type in what you'd just
thought of.

In a world with PICS servers, then a neat operation is to annotate a page you
don't have access to:

  * Create a new node somewhere where you have write access 
  * Create a PICS label with a pointer to it 
  * Store the PICS label on the label server as a label about the annotated node. 

The XML LINK work will allow, we hope, a link to be made into the middle of an
existing unwritable document with some hope of reliability.

Here are a few other operations which would be very useful when you really use
hypertext as a thinking tool.

##  Excerpt

Dan is always asking for this and doing it by hand. I have never seen an
editor which will do it automatically (though Dan has found some [javascript
hacks](https://www.w3.org/2000/08/eb58) that work pretty well).

  * Copy to the clipboard a BLOCKQUOTE with inside it a copy of the selected text, linked back to the original document from which it came. Make the link to an existing anchor in the document if one is there, or else a new one if one can be made, or else the document as a whole failing that. 

##  Insert an image

It's always nice to be able to grab a screen shot or a video frame and insert
it into the minutes you are taking of a meeting -- but how many keystrokes
does it take?

* * *

[Back to User Interface 1](https://www.w3.org/DesignIssues/UI.html); [Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

TimBL, Apr 1998  
$Id: Editor.html,v 1.12 2009/08/27 21:38:06 timbl Exp $

