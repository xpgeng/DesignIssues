Tim Berners-Lee  
Date: 2004/01, last change: $Date: 2004/01/15 19:47:08 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Semantic Clipboard

One way of looking at the Semantic Web is a breaking down of barriers between
applications. An example I have often quoted is that I would like to be able
to drag a photo album onto a calenar application and see the photos on my
calendar.

What would this actually take?

The intersting case that the calendar application and the phto album
application were written indepedently, without this case in mind. Suppose they
were, though written to be semantic-web aware. So they will have ontologies
for the things they deal with (photos, events resepctively in this case.) They
will store their data, or at least a copy of it, in RDF.

The clipboard, which stores things which we copy and paste, is a complex
thing. It doesn't always hold the value of something clipped, it sometimes
just remembers where it was clipped from. There is a form of negotiation
between the source and destination about the format for the data to be
transferred. This is why you can copy from text from a web page (which is
structured hypertext) into a plain text message. There is a negotiation, and
the source and destinatio can both use a plain text clipboad type.

In this example, we can imagine there being a Semantic Web clipboard type. The
data is basically transferred as an RDF graph. But that isn't the end of it.
Different applications understand different vocabularies (ontologies). So a
semantic web clipboard (or the application) does more than just transfer data.
It arranges to convert it into a useful form.

When you drag something onto the calendar application, it may be expecting
events. It may be able to use anything which has at least a start datetime and
and a description. the typical vocabulary here is iCalendar-like, such as
@@@@. The photo has a date of creation and may have a form of description. It
will typically have technical details of the exposure. The typical vocabulary
here is EXIF-like, such as @@@@.

RDF Interest group people have looked at conversion tools. At MIT we've had
fun converting things like this deliberately. How can it happen in this
example?

Somehow, the user must authorize conversion rules to be available to the
semantic web clipboard, so that the convertion can be done. The clipboard
indexes the rules, knows what form of information is needed by the application
through some kind of registration, and knows what sort of information is
available on the clipboard.

Typically, these things are customized. I might like the description of the
event of a phtograph being taken to have a list of the people in the shot, if
it is known; others might just want the brief "Pic!".

##  Sources and organization of rules

An advanced user who uses some kind of tool to generate a rule, as users do
today for email filtering. The user is a third party. Third party rule sources
may include system administrators.

The source could be the creator of one or other program: calendar or photo
album. One might exect the program which is released second to come with rules
for connection to other things already released. In this case, there is some
order in that the rules link applictions in a directed way. If in
laterreleases both applications offer rules to convert the same way, then a
choice has to be made, just as one sometiems has to chose whether to trust the
provider of the printer or the provider of the operating system when
installing a printer driver.

Users will have to track the trust worthiness of many different sources of
data, but these rules will give a lot back for something quite small.

There is a form of entropy which increases as these rules are used. Some rules
may be reversable, but typically they are not. You can't turn every event back
into a picture, and you can't event turn a picture taking event back into the
picture as you have lost some data. An event is in this example a more generic
thing than a picture. One might assume that the system will in general try to
reduce this information loss. This will involve trading at the highest level,
or usingthe fewest rules. The sense of specificity might therefore form an
organizing technique. This is similar to a form of pecking order between a
rich text clipboard and a plain text clipboard: is applications can use the
more sophisticated, less information is lost.

##  Conclusion

The Semantic Web clipboard might be a nifty hack in the short term, might be a
mainstay of desktop interoperability in the future. From the reseacrh point of
view, the rule management involved is a miniature version of the Semantic Web
rule indexing search engine.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

