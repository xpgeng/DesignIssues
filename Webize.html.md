Tim Berners-Lee  
Date: 1998, last change: $Date: 2010/03/09 14:07:04 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

# Webizing existing systems

_This discusses the introduction of URIs as names in a system to scale it to
the web._

The web is extended in two ways - by adding new bits of technology to the
existing stuff, and by "webizing" existing applications and systems. Webizing
is really important, not only as a way of bootstrapping the web using large
amount of legacy information, but because the existing systems have been
researched and designed over the years and it is really important we do not
lose the knowledge accrued during that process.

The essential process in webizing is to take a system which is designed as a
closed world, and then ask what happens when it is considered as part of an
open world. Practically, this effect on a computer language is to replace the
names/tokens/identifiers for URIs. Thus, where before reference could only be
made to something in the same document/program/module one can with equal ease
make reference to something in a different one somewhere in that abstract
space which is the Web.

In a clean case, this will be done so that the URI for an object is rather
naturally related to its representation in the original language. For example,
the element with ID "foo" in bar.xml is bar.xml#foo. However, to do the same
for an attribute defined in a DTD or schema is more difficult, because of the
complex nature of the spaces and subspaces for element and attribute names in
XML. It is great when the webized language is very similar to the original
language, and ideal when it actually compiles. Dan Connolly's 2000/8
webization of KIF uses URIs for identifiers, but to be accurate because URIs
are case sensitive and KIF tokens not, lower case letter had to be marked with
escaped with backslashes in the translation which made the result less
readable. Changing the underlying language in small ways can make the
translation much less cumbersome!.

Here is a slightly flippant view on the webize() function, each row of which
probably needs an essay of explanation, but provided here without any.

x | webize(x)  
---|---  
Hypertext | WWW  
Data | [Linked data](https://www.w3.org/DesignIssues/LinkedData.html)  
Top-down structured design | Bottom-up ontology design  
Data Hiding | Data Re-use  
Goto Considered Harmful | Goto drives the economy  
unix file system | [ACL'd r/w linked data](https://www.w3.org/DesignIssues/CloiudStorage.html)  
Large-scale structure: Hierachy | [Large-scale structure Scale
free](https://www.w3.org/DesignIssues/Fractal.html)  
"Tired" | "Wired"  
  
### Example - webizing a database

Imagine that a database is to be made available on the web in RDF. Suppose the
database itself will have a URI of http://weather.org/current An SQL database
is essentially a closed world, in that the various thing in it were not
designed to be linked to from outside. An SQL statement

    
    
    SELECT temp, zip  FROM weather WHERE temp  > 30

makes reference to terms which have meaning within the database. There is no
reference in that statement to the database - that is simply part of the
context.

Now suppose we determine what the URI will be for the pieces of the database,
perhaps current/weather for a table, and current/weather.temp for a column in
a table. We could then expend the syntax (excuse my SQL - I am making this up)

    
    
    USING c FOR http://weather.org/current  
    
    
    USING u FOR http://places.org/usa  
    
    
    SELECT c:readings.temp, u:location.lat, u:location.long
      FROM JOIN c:readings, u:location
      WHERE c:readings.zip = u:location.zip
      AND c:readings.temp > 30;

This is an (incorrect I expect @@@) SQL which links out of the local database
to combine it with information from a remote one. This syntax I am sure won't
work in practice, but should illustrate the principle. Namespaces c and u are
introduced for two reasons: for brevity, as repeating them in the code would
have been too cumbersome; and for syntactic reasons as URIs tend to contain
characters which would be ambiguous with other syntax is allowed in SQL column
names.

Of course, whether actually SQL on a set of scattered databases is valuable
may be questionable - it may not optimize as well as some other query
languages. However, suddenly the things defined by the database are available
to the outside world. For example, the concept of temperature reading as used
by weather.org in its database of current conditions

`http://weather.org/current/readings.temp`

is now a concept, an RDF property in fact, which is available for all the
world to refer to. These references need not all be in SQL. Because the schema
for the database will declare it to be an RDF property or something
equivalent, many different systems can use the information and refer to the
concept.

#### Notes specifically on this example

I note, before we leave this example, that there are two concepts important to
a table. One is the type of thing described by a row. A row in the reading
table, for example, defined a weather reading, something which had a location
and temperature and humidity and place. The other concept is the set of
objects which are actually in the table. In the classic SQL example of the
employees table, there is a rdf:class employee, subclass of person, and also
the fact that someone works for the company iff they are in the table.

A second note on exporting databases. When you really put something on the
web, there is often, for flexibility and security, a layer between what you
expose and the internal storage. Just as web pages are not files though often
closely related to files, and have the same form - a string of bytes and a
MIME type. Exposed remote operations are not local procedures though closely
related to them, and have the same form -- a service URI and a method name and
parameters. Similarly one would probably export a derived view of a database
in many cases - one which would have the form of a database. This allows
different engineering decisions to be made on the external manifestation
(persistent and what the customer wants) and the internal form (efficient and
convenient for you).

## Webizing nested languages

Sometimes this is easy and sometimes it is hard. It is hard, for example, when
the language uses nested scoping to great effect. In this case there is a very
large amount of context which is completely different between the beginning
and end of such a link. The _go to_ instruction is considered harmful [ref] by
Dijkstra because it "_as it stands is just too primitive; it is too much an
invitation to make a mess of one's program_." This of course is true of the
hypertext link too, in a way. Both allow an open webbed world which typically,
if used with no restraint, remove rules which give sanity and analysability to
a language and allow optimization of the code compiled. So, just as some
languages prevent one from jumping into or out of an inner loop of a program,
so it may make no sense to allow a link to be made into something within a
nested structure, because the referenced thing just does not have any meaning
when taken out of context.

When dealing with language which have nested context, it may be necessary
either to define how something inside represented independently of context, or
to make it impossible.

Be careful, though, before jumping to this conclusion. In many cases, it is
important to webize nested objects completely. For example, in a 3d scene
language, an object may be within a scene within an object within a scene and
still have identity which is important to be able to refer to. In a hypertext
document, there is a nested context which for example affects the style, and
the reference is made to the destination anchor not as a isolated piece of
hypertext, but in the context of the whole document.

The principle that on the Web, anything must be able to say anything about
anything means that these innermost nested objects must have URIs.

It may also be the case that an attempt to webize a language reveals bad
points in the design which really need to be ironed out anyway for the cause
of good software engineering. If a name in some module has in fact quite
different meanings when used in different contexts, then it isn't suitable for
webizing as it is, and maybe two separate derived URIs should be made in the
mapping. Maybe the language should actually be cleaned up so that the concepts
are distinct.

A very simple case is in a documentation control system, when humans use the
same document name ("the pipe size draft") to refer to a particular document
and also to the set of documents from

An exercise for the reader is to contemplate and determine whether it is
webized, and if not, what it would take, and what would be the cleanest way of
going it. Try looking at XML schemas (what is the URI of an element type?).

When stuck, recourse to common sense. Ask what the construct actually
represents in a global context, if anything. This might mean clarifying the
language itself.

## Conclusion

Webizing a language involves turning from a system which assumes a closed
world to one which will operate as part of the open web. Some cases are easier
than others. Webizing one application gets one a good idea of what sorts of
design decisions force a closed world assumption and make webizing difficult,
and what by contrast makes a weblike application which immediately benefits
from the rest of everything out there.

* * *

## References

GTCH: Edsger W. Dijkstra, "[Go To Statement Considered
Harmful](http://www.acm.org/classics/oct95/)", _Communications of the ACM_,
Vol. 11, No. 3, March 1968, pp. 147-148.

Connolly, Dan, "[Knowledge Interchange Format (KIF) as an RDF
Schema](https://www.w3.org/DesignIssues//2000/07/hs78/KIF.html)", 2000/8

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

2000/8/31

