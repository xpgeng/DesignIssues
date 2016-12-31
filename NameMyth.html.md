Tim Berners-Lee

Date: December 19, 1996

Status: personal view. Editing status: Italic text is rough. Reques complete
edit and possibly massaging, but content is basically there.

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

###  Axioms of Web Architecture: 2

* * *

#  The Myth of Names and Addresses  

The discussion above about the universality of URIs (Universal Resource
Identifiers) mentions briefly how URIs are designed to encompass both things
we think of as addresses and those we think of as names. Much of the
discussion of this issue has been clouded by attempts to distinguish names
from addresses. The term "identifier" was picked in an attempt to side-step
this issue but historically, that did not prevent a quagmire of circular
discussion which in some circles paralyzed any forward progress. Therefore, in
this section let me state the philosophy which to my mind sets this problem in
the right light and should prevent further fruitless discussion. _  
_

There is the commonly held belief that names and addresses are different and
distinct. We learn the importance of the difference between identifiers in a
programming language and addresses within a computer memory. We learn the
difference in properties between fully qualified domain names on the internet
and internet protocol addresses. This can lead us easily into imagining that
there are two types of objects: Names, which once attached to an object follow
it for its life wherever it should reside, and "addresses" which change
frequently whenever an object moves or is copied or replicated from one
"location" to another.

However, the only true location is a point in three dimensional space, and
within computer systems and especially networked computer systems there is a
very large number of complex indirection between almost anything we would call
a name _or_ an address and the actual physical location of the memory cell
which stores it. At one end of the spectrum a computer memory address often is
really an address within a virtual memory space allocated to a particular
project, and when used is translated by the hardware into a physical memory
address, or for that matter into an address, into a piece of memory which is
being moved out into somewhere and swapping the file on disk storage.
Filenames are mapped though mount tables and directory files into "inodes"
which are mapped onto track and sector locations. Internet protocol addresses
[IP Addresses] similarly are not bound absolutely to a given computer: they
can be re-allocated within the constraints that because they are used for
routing, there is information connecting parts of the IP address with routing
information and so the computer corresponding to a given IP address cannot be
moved far in the routing structure. So, we see that the constraint on how you
can re-use an address is a function of what information is in the address.
When most programs or people mention IP addresses, they simply quote four
decimal numbers, each between naught and 255 without worrying about the
internal structure. So, the information within the IP address which prevents
it being re-used in a different area is to most people not explicit: It is, if
you like, hidden within there as the reason why IP addresses can't be used.
When we want to use something to refer to a computer but still be able to move
the computer or at least the thing corresponding to that identification across
from one part of the internet to another, we use our domain name. The domain
name system, being completely independent of the routing system, allows us to
allocate any IP address at all to a computer of a given domain name.
Therefore, if we believe the naming myth the domain name is a name and the IP
address is truly an address.

##  Two anecdotes about names and addresses

Two real-life anecdotes illustrate the dangers of making this assumption. When
there were only a few web servers and I kept a registry of all those which I
knew, I was contacted by a group in Australia who were putting up a server
with some interesting botanical information. They sent me some details of the
server to be put into the list and they gave me the IP address of the machine.
My email reply explained that I always prefer to refer to servers by their
domain name rather than their IP address and asked them for the domain name of
the server. They replied that the domain name they would use would depend on
the department within the university which was responsible for maintaining the
server but due to a university re-organization, it was not at this point clear
which department that would be. However, they explained that they could
guarantee that the IP address of the server would remain unchanged for a long
time.

Several years later, the list of servers now abandoned as a single list of all
World Wide Web servers was among the now-extensive web of information
maintained on the server known as info.cern.ch, the first World Wide Web
server set up at the start of the World Wide Web project. At this time the
responsibility for the coordination of World Wide Web protocols was shifting
from CERN to MIT/LCS and the embryonic World Wide Web Consortium. For a while,
CERN continued to maintain the server, but later the master sources for that
information were maintained in America. Soon after this the authorities at
CERN requested that the name info.cern.ch should no longer be used to refer to
this information, as it was no longer under control of CERN and they could no
longer assume responsibility for it. In fact, there was a policy that names in
the cern.ch domain should never be allowed to refer to Internet addresses
which were not physically on the CERN site. Therefore all hypertext pointers
into the info.cern.ch space have had to be changed over the course of time to
point to the `w3.org` space.

These two examples show the "name" of objects having to be changed even though
the objects retained their essential identity. The reason was in each case
imbedded information in the name: the domain name on the server contains
authority information about the maintainer of the computer whose address
corresponds to the domain name. If the authority for an object changes,
whether it "moves" on not, then there may be a need to change its name under
these circumstances. It turns out that for almost any naming or addressing
system in which there is some information (other than random numbers or dates
of creation of the objects) built into the name that the name might have to be
changed when the facts corresponding to that information change. Therefore it
becomes simply a matter of choice between naming or addressing systems as to
what sort of information you wish to include implicitly or explicitly within
your "name" or "address".

##  Why Names Change  

See also:

  * In the Syyle Guide for Online Hypertext, [_Cool URLs don't change_](https://www.w3.org/Provider/Style/Overview.html)

It is worth looking at some of the reasons for names in practical use to
change or need to be changed. Some World Wide Web servers have unwisely simply
mapped the URL space onto a Unix filename space, and the results of this,
especially in the early days, were URLs which might look like this:

http://pegasus.cs.foo.edu/disk1/students/romeo/cool/latest/readthis.html

Looking at the segments of this name we can see as many reasons for the name
to need to be changed.

The "http:" will only be changed if the document is later served up using a
different protocol and, in fact, that is probably one of the least likely
pieces to change.

"Pegasus", the name of the computer, probably has a significance within the
university as a computer dedicated to some particular tasks such as supporting
personal student activities, and maybe maintained by a particular department
or may even be a name from a project for which the computer was originally put
into use before it became shared with general user space. So, "pegasus" will
be changed whenever the function of supporting this particular student's web
pages has to be shared with other functions.

"Cs" indicates the computer science department, so the document is bound to
the computer science department. It may not be something which the computer
science department has a lot of interest in, and the student may well transfer
his or her interests to other departments in the future.

The name of the university "foo.edu" will probably last for a good while,
though whether the university wants to continue to be associated with the
document for more than two or three years is questionable.

The next section of the path, "disk1", is clearly a mistake. In fact, of
course, disc1 is just a name which can be attached to any physical disk, but
by grouping together all the students on a certain disk in this arbitrary way,
one makes a binding between all the documents which they create which will
have to be broken whenever the computer is reorganized. In fact, the
relocation tables which most servers support allow much translation of names
to take place and make this sort of path quite unnecessary.

The next element identifies Romeo as a student which may change even though he
continues to study for the rest of his life, and then the next path element
"romeo" identifies the author of the document. As in the case with CERN above,
the original author of a document may later not wish to keep maintenance or
responsibility for ongoing versions. For example, the document may be
submitted to an organization which publishes it and formally takes over
responsibility for its upkeep; it may achieve a status of some kind as a
standard or an accepted thesis which causes its maintainers to change. The
original author may in fact deliberately simply pass on authorship of the
document to someone else. In any of these cases the name would have to change,
and all references to that name would break.

The student himself has not been very wise with his choice of path name. For
many people, what is "cool" changes with time and for most people what is
"latest" changes with time.

Perhaps the unlikely to change piece of information in the URL "readthis" as
it contains no information at all, just like the proverbial "click here".
Effectively, it is a random name assigned to the document and as such, is
perhaps the safest part of the path.

The last element of the path, "html" is not strictly necessary with most
servers, as at least some servers will, given a URL of  "readthis" ,  serve up
the data from a file which is called "readthis.html". Here the student is
making it difficult for himself later to change the format or formats in which
the file is available, without at least some confusion. Suppose, for example,
that he later decides that the information is worth providing in audio format
for blind readers. The CERN server can easily be configured so that clients
specifically requesting audio formats in preference to HTML can be served as
preferentially whereas more normal clients will get the HTML. So, here again
is a part of the path which may be later regretted.

You can play this game with almost any name and address in any system, and it
is interesting to ask yourself in each case: to what extent do I call this a
"name" and to what extend do I call it an "address"? So, in conclusion we see
that any information explicitly owned or implicitly included in a name is a
threat to its longevity.  We see  that the difference between a "name" and an
"address" is not so fundamental.  That is why

When a new URI scheme is defined, the specification defining ity should
describe the name-like and address-like properties of URIs in the new scheme,
so that that those using them can know what to be able to expect.  
---  
  
##  What's in a name?  

Why is information included then? Generally, the information is included
because in order to discover anything about the name, one has to "dereference"
the name. Typically this uses some official or unofficial set of indexes
distributed or otherwise to look up the name. Many names are hierarchical in
the authority which allocates them. DNS names are a good example. Road names
within towns are another good example. Therefore to find out where the new
"North Street" is located in small town one goes to the town for the
definitive answer. For information as to where the server "pegasus.cs.foo.edu"
is, one must send a message directly or indirectly to a server controlled by
the Foo University.

Is it possible to omit all such information from a name? Certainly. Message
identifiers in mail have only the need to be unique. So, whereas hierarchical
names and time stamps may be used to help make such identifiers unique, you
cannot dereference the names at all. Perhaps we should call these
"identifiers" rather than "names". Within a certain context, it is extremely
useful to be able to refer to a mail message by its mail identifier. We say
that these identifiers support the notion of equality: even though they cannot
be dereferenced, you can test two mail messages to find out whether they are
in fact the same simply by testing their identifiers. You can also within a
finite set of mail messages look up a message of a given identifier. You just
can't do this on a global scale. So this then is the essence of the naming
problem:  

The naming problem: if you put information in a name, it decreases its
longevity; if you don't you can't dereference it to a resource.  
---  
  
###  Naming: A social and contracual Issue

Many, many solutions to the naming problem have been attempted and
successfully deployed in different circumstances. At one end of the scale, it
would be in fact possible using a huge network of hash tables around the
world, to keep a hash index of all randomly generated unique names. The
problem with this idea is that there would have to be one single funding model
and one homogeneous quality of service for all names. There would be no way to
pay more for a more persistent name.

At the other end of the scale, hierarchical systems such as the domain name
system, and the x500 name system, have been implemented. Suppose one wants to
use a name which can be dereferenced and therefore must put some information
in it. That information will lead us to some authority or some root to
dereferencing the name. How can we maintain the lifetime of that name as
something which can be dereferenced? The only way is that we have a contract
with all the agencies which are involved in supporting the systems which
dereference that name that they should continue their operation giving a
certain quality of service for a certain period of time.

Suppose the Foo Alumni Association ran a URL service in which a special name
such as "http://alumni.foo.edu/1998/romeo/202-aab" would be available to any
graduating paying their dues, and maintained indefinitely (perpetual care) on
receipt of a suitable endowment.

Of course, as organizations disolve and mutate, there is nothing to stop one
organization from taking over the support of  the archives another.  Forthis
purpose, it would be very useful to have a syntax for putting a date into a
domain name.  This would allow a system to find an archive server.  Imaging
that, failing to find "info.cern.ch", one could search back and find an entry
"info.cern.ch.1994" which pointed to www.w3.org as a current server holding
archive information for info.cern.ch as it was in 1994, with, of course,
pointers to newer versions of the documents.

###  Quality of Service

Looking at an "http:" URL, while some look more sensible than others, it is
not immediately evident whether great pains are being taken to make the name
very persistent.  We have just discussed such a range of reasons why names can
change, and clearly the social and contractual arrangements can be quite
involved, so it is clearly difficult to simply define a quality of service for
naming.  However, defining some well known quality of service levels would be
a very useful task. This is the sort of task ideally suited to a group of
trechnologies, librraians or archivists.

 In any event, for identifiers in the http space and many others, it would be
useful to be able to assert what the quality of service is. This is
information about a URI and a resource.  Like the [information about generic
URIs](https://www.w3.org/DesignIssues/Generic.html#Dimensions), it is about the sort of identity between the
URI and the resource.

Metadata should be used to express the quality of service for the binding
between a URI and a resource.  
---  
  
##  _  
_

* * *

[Next: Metadata architecture](https://www.w3.org/DesignIssues/Metadata.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

