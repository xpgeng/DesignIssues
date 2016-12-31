Tim Berners-Lee  
Date: 2005-06-09, last change: $Date: 2006/10/29 17:19:39 $  
Status: personal view only. Editing status: first draft. This was written when
the W3C Technical Architecture group responded TAG issue HTTPRange-14. This
resolves the question originally addressed in a previous _[What to HTTP URIs
Identify](https://www.w3.org/DesignIssues/HTTP-URI.html)_ note.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  What HTTP URIs Identify

##  Abstract

HTTP URIs, in the web architecture, have been used to denote documents -- "web
pages" informally, or "information resources" more formally. However, with the
growth of the Semantic Web, which uses URIs to denote anything at all, the
urge to use and practice of using HTTP URIs for arbitrary things grew
steadily. The W3C Technical Architecture group eventually decided to resolve
the architectural problem that if an HTTP response code of 200 (a successful
retrieval) was given, that indicated that the URI indeed was for an
information resource, but with no such response, or with a different code, no
such assumption could be made. This compromise resolved the issue, leaving a
consistent architecture.

##  Introduction

HTTP URIs, in the web architecture, have been used to denote documents -- "web
pages" informally, or "information resources" more formally. However, with the
growth of the Semantic Web, which uses URIs to denote anything at all, the
urge to use and practice of using HTTP URIs for arbitrary things grew
steadily. The Dublin Core project, one of the first RDF vocabularies, and
later Friend of a Friend, and various others simply used HTTP URIs to identify
RDF Properties. The result was that one could no longer be sure that an HTTP
URI was intended to identify the web page one got when one used the URI in a
browser. In fact, there was a danger of confusion is one party used the URI
for an abstract concept and another used it for the web page. The author wrote
a long _Design Issues_ note about this, [What do HTTP URIs Identify?](https://www.w3.org/DesignIssues/HTTP-
URI.html). The reader is directed to read that if more detail of the arguments
is needed.

This whole issue caused, until 2005, a lot of discussion in technical circles,
and much heated debate. In June 2005, the TAG resolved the issue as a function
of the runtime protocol response. Basically, the argument is that if you have
used a URI to get a web page, then you can use the URI to identify the
Information Resource which is that web page: For example, the New York Times
home page, or this page you are reading now.

###  Resolution

The TAG resolution effectively extends the range of things one can use HTTP
URIs. However, it does not allow one to simply serve a web page at a URI which
is used for something else. Of course, it is a general principle of web
architecture that it is useful to serve information to those that look up a
URI. In the case that the URI is not intended to be used for an information
resource.

The W3C Technical Architecture group eventually decided to resolve the
architectural problem that if an HTTP response code of 200 (a successful
retrieval) was given, that indicated that the URI indeed was for an
information resource, but with no such response, or with a different code, no
such assumption could be made. This compromise resolved the issue, leaving a
consistent architecture.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

