Tim Berners-Lee  
Date: 1998, last change: $Date: 2009/08/27 21:38:06 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Conversations and state

See also: [Paper Trail](https://www.w3.org/DesignIssues/PaperTrail) \- presented as a a student project

The basic model of the web is a world of information. Theoretically, a mapping
between URIs and representations of the resources they identify, and
experientially fro a person a space one can navigate.

Interestingingly, trends at the leading edge of user interface development,
and at the semantic web development both point to a world which uses a
different model. Human interfaces are moving from screens to conversational
mode. The semantic web, while very exciting when viewed as a

Human user interfaces use more and more devices such as speech, gestures and
so on, which are not screens. What is special about a screen? A screen with a
window system presents a large amount of informatoin at the same time to a
person. In practice, more or less everything which a person is concentrting on
at one time can be presented in its current state. When the number of pixels
on a screen broke through a certain threshold (roughly the 640x320 VGA limit)
this led to the development of direct manipulation interface metaphors:
folders one could open, and drag and drop. The essential things about this is
that the computer is at every instant presenting the current state, whether it
or the human is manipulating it. The communication betwen personand machine is
in terms of the mutual manipulation of a shared state. The web was intended to
extend that form of communication by mutual manipulation of a shared state to
remote human-human interaction. While the tools and protocols have their
limitations (see UI) much of its effectiveness derived from this model.
Because fundamental thing is a shared space of information, one can talk about
navigation around within the space, and use all the primaval facilities that
the human memory has for navigation.

This is all very well, but it was not always so. When computer terminals had
only 24 rows of 80 characters, even when they were addressable, there was a
tendency for most jobs to use command line interafaces, for example when
manipulating files and directories. The interface was conversational, in that
the exchanges were small commands and responses. There was a shared abstract
state, but it was imagined in the abstract by the person, and held in some
unvisualized form by the computer. This too has itas advantages, in that the
imagination of a person can well exceed (on a good day) the capacity of a
screen in its ability to hold complex interrelated structures. The interesting
thing is that now there is a tednedncy to use many devices which do not have
the large screen. The screens on cellphones are currently so small that, while
one can scale a web page down and adapt it to a small screen, this might be
chosing simply the wrong interface metaphor. When the audio phone only is
used, then the shared state becomes zero and the interface is completely
conversational again.

The characteristic of a conversation is the state is the set of utterances, or
messages, which have been conveyed. This is differenet from a shared
expression of a commonly agreed state. The [Paper Trail
concept](https://www.w3.org/DesignIssues/PaperTrail.html) links these two modesl in the Semantic Wee Semantic
Web, by formally defining the overal agreed state as a function of messages to
date. A service which allows a phone user to browse the web converts the other
way: it conveys part of the the space of information by means of a
conversation. It is is important for a number of reasons.

  * It allows us to formalize the models of human-machine interface which are in fact conversational for many non-screen devices; 
  * It allows us to formalize social, for example commercial, transactions for which the paper trail is in fact th emost accurate model anyway; 
  * It provides us with tools we can use for formally analysing the infrastructure protocols such as HTTP which with which the information world is actually implemented in practice. 
  * The standardization of XML protocols has, with XML (and RDF), a richness in terms of marshalling data formats to build on, and, with xml-schemas xforms and rdfs, a richness to draw on in terms of languages for defining valid documents, but has no basis yet for defining with equivalent power the validity (and semantics) of a sequence of interrlated messages which are a protocol. 

It is not as though the web today itself perfectly matches the stateless model
at all. The moment it was created as a basically stateles system, many web
site designers took it as their challenge to get around this model in order to
create a conversational interface -- and many still do Our concerns about
privacy stem largel;y from the knowledge that our "reading" of documents is in
fact done by a series of protocols which leave a trace. The P3P project
involves quantifying the information transfer which actually takes place. Our
handling of HTML forms is getting more complex, and a form itself, becomes, on
many sites, the definition os a protocol - a set of valid sequences of
information actions..

This was written as a note to accompany a talk to the W3C Advisory Committee
of November 2000. At such times, we discuss the status of existing work and
look ahead to feel the direction in which we will need to move in the future.
Often, we notice that Web technology is now entering a field new to the Web
but old of itself. In these cases, we can view the process we need to go
through either has extending web technology into this field, or of _Webizing_
the field. This has happened, more or less, to hypertext to SGML, and is
heppending to knowledge representation. Now an interesting field is teh formal
specification of protocols. There is much out there to build on, but is has
not been applied yet to the exchange of XML documents conveying RDF graphs.
However, it seems to be a relevant direction in which to look when predicting
where the leading edge, and therefore the Consortium, should be in a few
year's time.

@@ - already web privacy concerns come from in fact it being a conversation --
there is implict state. A

@@ Reasons for formalizaing protcols a la Paper Trail.: uses concepts of
validation and will be able to resuse tools - extends semnatics of documnets
to semnatics of conversaions. \- Creates a formal basis for defining
conversaionsal systems of all kinds, including indirctly human language
oriented systems.

@@ Machine-machines and human-human convergence

Originally written 2000/11

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

