Tim Berners-Lee  
Date: 2011, last change: $Date: 2015/04/04 15:55:45 $  
Status: personal view only. Editing status: first draft. An note follows a
discussion on the Jena bug tracker as to whether my plea for the support of
relative URIs was a bug or a wish. I found that using Jena libraries, which
does not provide the option of relative URIs, many things broke my working day
to day. It seems strange so long after the introduction of URIs to br writing
something so basic about how they should be used, but it seems these are
points which have passed some people by.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Using Relative URIs

URIs are so ubiquitous that they are now used in many different sorts of
system. There is a whole class of issues which arise when bits of the web
architecture are designed by those who are not aware of the ways in which
others use them, an end up coding or speccing so as to break others' preferred
design patterns. One of these patterns is the use of relative URIs.

## Recap: Local IDs

Localidentifiers as an important case of URIs. Elsewhere in the these notes
there are more complete descriptions of the way the URI system works, and
specifically as to how the # character is used to take what was locally only a
local identifier and by prepending the URI of the document in which that local
identifier is used, turning it into a global identifier. Hence, hypertext
turns into the WWW, and data files turn into the Web of Data, and so on. We
call it [webizing](https://www.w3.org/DesignIssues/Webize.html) a system. Here is web architecture in one
line:

    
    
     
                <global id of document>  #  <local id of whatever>
     

So when a file on the web refers to something internal it can just use the
local ID. It would be very cumbersome to include the whole URI of the document
itself in each of these references.

    
    
     
                #  <local id of whatever>
     

  * This file can be copied and put up on any web server
  * The file can therefore be used as a template for other new systems
  * The fie is shorter and much easier to read than one in which all the URIS are spelled out in full.

As an illustration of the last point, consider a program written in a
programming language. Imagine writing a program, say, like:

    
    
         pi = 3.14159265359;
         print (2 * pi);
    

an it being saved in circles.py as

    
    
        <file:///users/foo/programs/play/circles.py#pi> = 3.14159265359;
        print (2 * <file:///users/andys/programs/play/circles.py#pi>);
    

Not practical, not the sort of thing you can copy and move around. The fact is
that throughout computer systems, local identifiers and relative filenames are
very common. We loose a lot if we drop this relative feature when we move to
the web.

## Relative URIs

In fact, when a number of files all refer to each other such as a bunch of
HTML, CSS, SVG and JS files as part of w web application, or a set of Turtle
files as part of a Linked Data dataset, then also save a lot of space and
fragility by using relative URIs, using the unix-like conventions

There are, though, relatively few systems which in fact can be implemented by
a single file. There are a huge number in which the system is implemented in
one directory of a file system, or in that and its descendants in the tree.
For example, an HTML file may have local CSS files and images. The system may
be edited in unix file space, where any URLs will be file:/// URLs, and it may
at the same time by seen through a web server, where the various resources are
referred to by relative URLs:

    
    
        <a href="intro.html">
         <img src="../images/foo.png"/>
        </a>
     

It isn't just coincidence that the syntax of URLs matches that of unix-like
file systems. It is designed to let systems be looked at either with file://
glasses or with http:// glasses and still work. This is very useful. This
means that you can directly export onto the web a system which has been built
up as a local filesystem, and it means that when you have a file-mapped web
server, like Apache, you can use all kinds of unix tools to build or analyze
your stuff. For anyone who has been working this way for more a decade to two
this may be blindingly obvious, but if you work in a content-management system
which is not a file-system-mapped one, or you work with a file system which
does not use the *ix conventions, then this may not be second nature.

What the Relative URI Pattern gives you then, is the ability for you system to
work with different base addresses without being modified.

  * You might want to view a directory both locally as a file and also remotely through a web server.
  * You might want to develop the system on a test system, with testing of the internal relationships, then move it to a production system.
  * You might want a system to be visible as part of many web sites, for example a common login system or help system shared my many related websites
  * You might provide parts of a web site by proxying another. Maybe when it comes to editing files your main web server proxies though to a specialist server.
  * You may want a build a system which you can hand to others to copy elsewhere.

and so on.

Many systems, including most of the ones I have built and use day to day, have
many internal relative links but really are better built without a knowledge
of their own base URI, in that stored URIs are always relative. Even if the
software absolutizes them in processing them, as there are no absolute URIs
for the local identifiers. This is not to say all systems are like this, but
some are and they are an important class.

Note other reasons for relative URIs include readability, and storage space
and transmission length.

### Best Practice

Because an application developer is very likely to find it valuable to use
relative URIs, any software libraries which serialize web file formats such as
HTML and Turtle must provide the option (or the default) to serialize using
relative URIs.

When data is stored in files, for example on a web server, it is good practice
to store it using relative URIs.

When data is sent across the net, also, such as in HTTP, relative URIs should
be used.

Yes, there are cases when people want to design systems without this
properties, so absolute URIs should be an option.

### Failure example

The XML space when it defines how namespaces are declared in the top of the
document, officially forbids relative URLs. The authors envisages a narrow set
of use cases in which the terms defined in the namespaces were all absolutely
references and stable and global in nature, and the data in the document could
be local and unstable. Unfortunately they did not understand the general need
to generate relative URIs in arbitrary situations. The cwm command line and
the cwm serializer have an option to override this constraint and generate
relative URIs. A solution of course for RDF users is instead of RDF/XML to use
the Turtle (nor N3) serialization, which is normally preferable anyway for
many reasons.

The Jena RDF system does not (currently 2015) include code to generate
relative URIs, and when it serializes data into RDF/XML or turtle, it only
generates absolute URIs. This prevents it being used for a wide range of
systems which require the use of relative URIs.

There is a classic failure mode for RDF systems in which developers bring up a
system on test.acme.com and then move it to production.acme.com and all the
links break. I know there are cases for absolute URIs but the relative URIs
are very important best practices.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

