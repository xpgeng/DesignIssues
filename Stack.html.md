Tim Berners-Lee Date: 2002/05, last change: $Date: 2003/01/06 19:40:09 $  
Status: personal view only. Editing status: rough..

_Abstract: This is backgrounder explaining where the web specifications fit
into the internet technology as a whole. It explains the philosophy of
electronic communications having well-defined meaning grounded in a stack of
interconnected specifications. This is all normally -- and quite justifiably
-- taken for granted by Web engineers. But it is needs to be emphasised when
the Internet is abused , for example by spammers who forge email headers, or
companies who cheat protocol timeouts in order to claim greater performance,
and in doing so, break the system. This article debunks the idea that "its Ok
to interpret things this way as more and more people are doing it"._

_It was originally the subject of a keynote address at the International World
Wide Web Conference in Hawai'i, April 2002._

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  The Stack of Specifications

Bits mean something.

When you connect a cat-5 ethernet cable to your computer, you effectively
commit to taking part, with your computer, in a very special system. It is a
system in which the meaning of messages is determined, in advance, by
specifications. This is a principle which is so basic to network computer
systems that it is rarely stated. But as the stack of specifications gets
higher and higher, and as electronic commerce, legally enforceable agreements,
and socially sensitive issues such as privacy and fraud become matters of
public concern, it is worth reiterating for the record.

The Internet works because of interoperability between different computers,
despite different hardware, operating systems, local language context, and
software supplier. Users of the web sign on to the use of these languages when
they use the Internet.

There is this little philosophy joining many specifications, without which the
Web falls apart.

Lets take an example.

###  You have an ethernet cable

You walk into a meeting room, and you are offered a thin cat-5 cable with a
10-base T connector. This is an Ethernet connector which only takes Ethernet
packets. The only way to use it to communicate is for your computer to send
packets which are formatted to the Ethernet specification. The Ethernet
specification is a large document (Similar to **IEEE standard 802.3**) put
together by a bunch of engineers, and once they were done Ethernet existed as
a standard, and computers which know nothing about each other could exchange
packets over local area networks..

The Ethernet defines the format of an Ethernet packet, which has a little
header information, but mostly carries information on behalf you the user. The
spec also, importantly, defines some rules of behaviour. For example, the
ethernet doesn't work if more than one computer tries to transmit at once.
There is a rule that if you find that happens, everyone involved backs off and
comes back at a random interval. Each computer is supposed to wait on average
the same amount of time before trying again. Of course, you could cheat by
actually pretending that your random number happened to be really small every
time, and on average your computer would end up getting though more and
blocking everyone else out, just like people who always seem to be the one
talking in a meeting. But that would be cheating, and contrary to the Ethernet
specification. By connecting to an ethernet cable, there is an understanding
that your computer will stick to the rules

An ethernet packet can be sent to anyone on the same wired or wireless local
area network. How does a computer know what to do with a packet when it gets
it? How does it know how to interpret that packet? Well, there is a field in
the packet which tells it, in a coded way, what the use of the packet is, and
therefore how to interpret it.

Of course, there are lots of uses of the Ethernet, but a very common use of an
Ethernet packet is to use it to carry an Internet packet. Ethernet packets can
only cross the local area network, while Internet packets are forwarded
anywhere in the world. So, there is a particular code - a particular value for
the field in the Ethernet packet - which tells any receiving computer that the
data is actually an Internet Packet. This means that to understand anything
more about the packet means, you have to read another spec: the **Internet
Protocol (IP, RFC791).**

@@@ The complete graph of interdependencies between specifications.

###  You send an Internet packet

So suppose you send an Internet packet. You put the ethernet address of the
local "router" computer into the ethernet address field, but within the "data"
part of the ethernet packet is the IP packet and inside that is an internet
address field, which takes the IP address (the thing like 18.96.237.175) which
identifies the computer Although the ethernet packet you send it in only gets
as far as some computer a "router" on the local net, that computer passes the
IP contents on, from computer to computer across interconnected networks until
it arrives on the right local network for its actual destination.

So how does that computer know what to do with it? Well, there is a field in
the IP packet which carries a coded value to tell the computer receiving it
what to do with it. .

    
    
    From Internet Protocol (RFC791):
    A summary of the contents of the internet header follows:
    
          0                   1                   2                   3
          0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |Version|  IHL  |Type of Service|          Total Length         |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |         Identification        |Flags|      Fragment Offset    |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |  Time to Live |    **Protocol**   |         Header Checksum       |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |                       Source Address                          |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |                    Destination Address                        |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
         |                    Options                    |    Padding    |
         +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
                          Example Internet Datagram Header
    
                                     Figure 4.
    

And there are a lot of things you can do with an IP packet, but a very common
one is to use that IP packet to set up, or to be a part of, a reliable stream
of communication using the **Transmission Control Protocol (TCP) (RFC 793).**

###  You send a TCP packet

When you send, or your computer sends, a packet in the TCP protocol, there is
an understanding that that packet conforms to the protocol. That means a
couple of things. It means that you agree that the packet's contents it to be
interpreted according to the TCP protocol specification. It also means that
you agree to abide by the rules of the specification, which determine, rather
like with the Ethernet protocol, how long your computer will wait before re-
sending a packet which didn't seem to get there. If your computer re-sends too
early, then it hogs the Internet and slows down everyone else. If your
computer send a packet to start a new connection when it doesn't really want
to, then the destination computer will prepare a lot of memory to receive all
the data you are going to send, and wait. If you keep doing it, then that
computer can just run out of memory and stop working. So you can cheat and you
can do real damage by breaking protocols.

###  Introducing IANA: The Port number registry

So you computer must stick to the TCP specification. When it does that, the
TCP protocol assures that the two computers have a reliable connection without
any missing bits. What they use it for is no concern of TCP, apart from the
fact that the TCP protocol specifies, within the TCP packet (which is inside
the IP packet (inside the ethernet packet)) a special field whose coded value,
or **port number**. There is a convention, which is written into the TCP
specification, (@@check and quote wording) that the meaning of the port number
is determined by a table which is changed from time to time, but kept by the
**Internet Assigned Numbers Authority** (IANA). Without going into the
politics of the changes and control around IANA, it is just worth noting that
this is, architecturally, a "flexibility point", where the community can
introduce a new protocol to run on top of TCP/IP without having to write it
into a new version of the TCP/IP specification itself.

The port number registry is on the web (@@ link) but also, on a unix computer,
there is a list of the well-known ports in the file /etc/services.

When you send a TCP/IP packet there is therefore an understanding that if you
send to one of the well-defined port numbers, then you are going to use it in
a way defined by the specification defined in the IANA registry. For example,
port number 25 indicates that you are going to use it to transfer some email,
and that you undertake to communicate according to the Simple Mail Transport
Protocol specification.

###  You send an email message

You get the picture. One specification, once you commit to it, depending on
the values of certain fields, invokes further specifications. By committing
originally to using an ethernet cable, you commit to your computer using, on
your behalf, the various other specifications. In the case in which your
computer sends email, it may for example open a TCP/IP connection to to port
25, and then use the Simple Mail Transfer Protocol (SMTP, RFC821). This
specification indicates that the body of the SMTP communication is formatted
according to the email message specification, RFC822. RFC 822 specifies the
headers on email messages. It specifies, for example that a given "From" field
indicates the email address sender of the message.

It is possible, of course, to cheat. with the SMTP protocol. It is possible to
lie about who is sending the message - to send a message which appears to be
from one person to a friend. This breaks to protocol. It breaks it, here, in a
way which is very clear to people: it sneaks past their personal email
filtering, and also any automated filtering, tricking them into reading a
message. This is a security violation. It can use up a person's time, energy,
bandwidth and disk space for the commercial gain (indirectly through
advertising and sales) of the perpetrator.

The Internet specifications, to which any Internet user implicitly agrees in
using the Internet at all, define what the fields in an email message mean. To
put incorrect information in these fields is to make a misrepresentation, just
as it would have been in any other medium. It should be subject to the same
penalties as lying or fraud in any other medium.

When the Internet was young and used by research institutions, its misuse
would inconvenience other users and lead to reprobation and the disdain of
one's peers. Now that the Internet is such as large force in society, it is
possible to make a lot of money and create a lot of damage by protocol abuse.
You can compare a lie in an internet message, depending on how it is done, to
forging a check, connecting to the electricity supply the other side of the
meter, or to poisoning the water supply. Society must therefore be careful to
be absolutely clear about the illegality of such misuse.

###  You publish a Web page

When you publish a web page, just as when you send an email message, the web
page or the message generally carries a meaning. Well,it can be a picture or a
poem which is more artistic than linguistic, but in a large number of cases
the meaning is a well-defined part of a communication between parties. It may
be a human-readable document, like the page describing a pair of pants your
are about to buy from a store, or it may be machine-processable, like the
Online Financial Exchange (OFX) format bank statement your financial software
downloads from your bank.

Of course, you would find it hard work to make sense of the OFX file if you
just read it without the help of the financial agent, and your financial agent
wouldn't make much sense of the catalog page. Something must allow us to
distinguish how web pages and emails should be interpreted, just as a computer
has to figure out how to make sense of an Ethernet packet. And just the same
sort of thing indeed happens.

When you publish a web page, you give it a HTTP URI. You pick a URI from the
space of URIs which are yours to define. Some people have space on their own
domain, some people have the right to pick URIs in part of someone else's
domain. But the URI is one which you own or over which you have authority. You
are not allowed to pick one in someone else's space.

Whoever owns the domain has the authority to define which computer serves
information in it. They have the authority then to have a computer -- a web
server - which is configured to act on their behalf. It is then assumed that
the computer acts on the their behalf. The server is the agent of the
publisher. What it does is tell any asking browser what you have said is a
representation of the document for a given URI.

When someone follows a link to your web page, their browser opens a TCP/IP
connection to TCP port 80 on the machine which is registered as serving the
(www.whatever.com, etc) in question. Their agent, their browser, asks your
agent, the server, to give it some representation of the web page for that
URI.

Why? Because the URI specification says that what you can tell about a URI
depends on the first bit, in this case `http:`. It indicates that an **IANA
URI scheme registry** is used to tell you what specification applies.

The IANA registry indicates that the `http:` scheme calls out the **HTTP 1./1
specification**, RFC@@@.

HTTP 1.1 says that (unless otherwise specified) the client contacts the server
on TCP port 80. The IANA registry of port numbers, just as it allocates port
25 to mail transfer, allocates 80 to HTTP. The HTTP spec is therefore mutually
assumed by both parties. This spec describes what a request means, and that
when the request is successful, what the response message sent back to the
browser means.

According to HTTP 1.1, in that response, there is a field (**Content-type**)
which indicates how the body of the response should be interpreted. For each
valid value of that field, there is an **IANA content-type registry** value
which explains which specification applies to the body of the message. This is
just the same system as for email.

When the value if the field is `text/html`, it indicates that the message is a
hypertext document ("web page") which is to be presented to the human being
and interpreted then by the human being in the usual human way. If the field
indicates it is an OFX file, then that means that the OFX specification
determines what it means, and you need a program or something which
understands what the fields of the OFX documents mean. In neither case can you
argue that you didn't know. So long as the writers of the specification do a
good job (and goodness knows they work hard enough at it) then there can be no
argument as to what the actual fields in your bank statement mean.

###  You publish an XML document

When you publish a document in XML, then there is another layer involved. Many
different languages -- or even mixture of languages -- can be sent structured
as XML. The mime type of the document can just be "application/xml", which
doesn't tell the reader how to interpret it. For that, you have to look at the
outermost element of the XML document. The namespace declaration gives a URI
indicating the namespace.

Note the difference between the use of a URI and a central registry. Because
the namespace is identified by a URI, the web becomes the registry. Anyone can
make a new XML namespace. Also, one can use a URI, such as a HTTP URI, which
can be dereferenced. This allows the information which would have been in the
registry to be put into a web document. (The W3C TAG is currently debating the
issue of the best format to use for this meta information, but HTML, RDDL and
RDF have been used in various combinations. But broadly there are two types of
information. There may be a specification (or a reference to one) to tell a
human reader what the language is and how to interpret it. there may also be
data - a schema which describes the grammar of the language, or even the start
of a logical definition of what the language means.

But whatever information may or may not be available automatically, in an XML
world, a system has to look into the document, at the namespace of the
outermost element, to know how to interpret it. This generally means what
application to launch - not to mention what icon to use to represent the
document to a person.

An example of a machine-readable document with important semantics is an
online P3P web site privacy policy. This is an XML document which gives, for
each category of personal information, the sort of thing the web site promises
to do or not do with it. It can be scanned by a a browser more easily than a
person can read a privacy policy. It is a useful feature, as it saves
everyone's time and increases public confidence in responsible web sites. It
clearly depends on the meaning of the terms being well defined by the
specification.

_(Problem: this doesn't always happen: MathML and XHTML as XML in practice.@@
links)_

###  You publish an RDF document

Now let's talk semantics. Harder semantics - for logical systems. Some XML
documents are RDF documents. RDF/XML is an XML-based language for data. It is
very simple: each document is just a set of "triples". A triple gives the
value of some property of some object - or some relationship between some
object and some other object. The triples are independent, so interpreting the
document is just, the RDF spec explains, a question of interpreting each
triple.

How do you figure out what a triple means? Well, the property (or
relationship) is identified by a URI. And whoever made up the URI gets to say
what the property means, that is, what any triple using that property means.

So if make a property http://www.w3.org/2002/05/example#color and define that
the color property is a name out of the Pantone(tm) list of colors and you
send someone an order in RDF for a hat which has
_http://www.w3.org/2002/05/example#color_ of _blue256_ then you are specifying
blue256 on the pantone scale. No one can argue that you meant some other scale
of blue. Normally the argument is made much easier by my actually writing a
document http://www.w3.org/2002/05/example in which I explain what #color
means. No one can argue, in their catalog, that "By suit, we mean something
which is black, whatever _http://www.w3.org/2002/05/example#color_ someone
might say it is". The meaning of the triple is determined by the property, not
by the subject or the object of the triple.

A section through the stack  Specification  |  Field  |  Where to look up
values  |  example value  |  Example value calls out  
---|---|---|---|---  
Ethernet (cf. IEEE 802.3)

and either DIX(RFC894) or 802.2,3
[RFC1042](http://www.ietf.org/rfc/rfc1042.txt)

|  Ethernet type (or protocol identification field for LLC) 16-bit Ethertype
|  IEEE registry

Assignment by RAC process @@link

|  0x800  |  [Internet Protocol
(RFC791)](http://www.faqs.org/rfcs/rfc791.html)  
[Internet Protocol (RFC791)](http://www.faqs.org/rfcs/rfc791.html) |  Protocol
|  IANA protocol-numbers  |  [6](http://www.iana.org/assignments/protocol-
numbers) |  Transmission Control protocol (RFC793)  
[Transmission Control protocol (RFC793)](http://www.ietf.org/rfc/rfc0793.txt)
|  port  |  IANA registry

port-numbers

|  [80](http://www.iana.org/assignments/port-numbers) |  HTTP 1.1  
[HTTP 1.1](https://www.w3.org/DesignIssues//Protocols/rfc2616/rfc2616.html) |  content-type  |  IANA registry

mime types

|  application/xml  |  XML1.0+NS  
[XML](https://www.w3.org/DesignIssues//TR/REC-xml) 1.0+[NS](https://www.w3.org/DesignIssues//TR/REC-xml-names) |  xmlns  |  The Web  |
...@@..rdf  |  RDF M&amp;S 1.0  
[RDF MS 1.0](https://www.w3.org/DesignIssues//TR/REC-rdf-syntax) |  property  |  The Web  |  rdf:type  |  RDF
MS 1.0 section 4.1  
[RDF MS 1.0 definition of rdf:type](https://www.w3.org/DesignIssues//TR/REC-rdf-syntax/#type) |  object  |
The Web  |  cyc:Person  |  cyc ontology  
  
Looking at the table which summarizes the steps we have been through, you will
see the specs are connected by some field which points to the next spec
through some list or registry. For the more recent layers, the registry has
been replaced by the Web.

##  The hooks - identifiers

That's an interesting trend. If you like, we can see the technology move
through three stages of civilization, in terms of the identifiers which are
used for concepts.

  1. Using numbers or strings 
  2. Using URIs - identify the same thing in all contexts 
  3. Using dereferencable URIs 

The early protocols used numbers and strings which requires a central
registry. that worked, because the only common concepts were those in the
standard protocols, and those had to be common across the net for
interoperability. In these areas still there is a strong argument for central
control.

As we move on to later protocols, the protocols themselves become more
diverse. This is partly because they are at a higher application level. The
centralized model starts to break down, as witness some of the social
difficulties of getting an IANA allocation for a MIME type an embryonic W3C
specification. So new protocols allow new applications to be defined using
URIs, allowing anyone who has access to a bit of domain space to allocate
them.

The third stage of civilization is the one at which the identifiers can be
looked up on the web. This is quite useful for engineers who encounter new
languages. It doesn't really justify its existence, though, until one has
technology -- Semantic Web technology -- in which an automated agent can pick
up metadata about the languages on the fly, and use that metadata to enhance
its processing of data in that language.

(What if I don't have a web site? This is becoming less and less of a problem.
There are all kinds of existing ways of allocating an identifier. But the
persistence of such information is, and always will be, like the cleanliness
of water and air, an important social issue.)

##  When the chain does NOT connect

We have seen how any user of the Internet is bound to a series of
specifications which define the meanings of terms, and hence allow his or her
equipment and agents to interoperable with others. This stack prevents one
from sending a nasty email to someone and then protesting that the message
didn't mean anything. So if the stack is so strict, how _does_ one send a
nasty email message when one _doesn't_ mean it? There are plenty of times you
want to include an attachment to which you want to refer, but for which you
don't claim authorship or responsibility. Understanding the exceptions is as
important as understanding the general rule. Many protocols have ways of
breaking the chain, of including information which is not part of the meaning
of the message.

In email it is an **attachment**. There is always in email a cover note, the
basic message, which conveys the actual message. You normally only use any
attachment according to the main message. It might be "Hey, Joe, what do you
think of this paper?", or "Look at this stupid program - but whatever you do
don't run it!"

Currently (2002) XML doesn't have a common standard for what has been called
in that context "**packages**". This is a pity. It is on the agenda for XML
Protocol working group, as seen as essential for SOAP operations. One must be
able to include documents stapled to a SOAP request or response, which are not
to be just acted on.

At the Semantic Web level, those who have played with the
[Notation3](https://www.w3.org/DesignIssues/Notation3.html) language will recognize the curly brackets as the
packaging, or **quoting**. Whereas a document

    
    
    my:car  srgb:color "000044".
    

asserts that the car in question is blue, the document

    
    
    my;form67  :says {my:car  srgb:color "000044"}.
    

does not. It merely says something about the statement that the car is blue.

So being able to refer to something without asserting it, whether you call it
attachment, packaging, or quoting, is an important feature of a language. The
fact that you can do this removes the last excuse for anyone claiming not to
have meant whatever they did say in the main message!

##  Conclusion

Internet messages and Web documents are represented in computer languages with
well-defined specifications. Use of the Internet and the Web implies an
acceptance of the specifications as authoritative.

The specifications are linked together by identifiers which in earlier specs
were numbers, but in later specs are URIs, ideally URIs which can be looked up
on the Web. The ability to make these linked specifications requires the
specifications to be designed very independently. This is simply the software
engineering practice of information hiding between layers.

The trend for the higher layers is toward more and more machine-processable
metadata about such languages, which can be retrieved automatically and will
aid in processing. Some of these will relate the semantics of terms in one
vocabulary to terms in another, on a web-like way.

The fact that as we move into the applications we see more and more diverse
uses of the Web and the Net does not diminish our reliance on a sound
standards in the supporting infrastructure.

* * *

##  Related

  * The Meaning of a document 
  * The meaning of an XML document 

##  References

The table above contains hypertext links to some specifications used as
examples.

See also:

  * The RDF concepts document. @@ 

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

