Tim Berners-Lee  
Date: 2009-06, last change: $Date: 2009/06/30 15:49:50 $  
Status: personal view only. Editing status: Good enough for folk. Notes after
talking with various people in UK and US governments who would like to put
data on the web and want to know the next steps.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Putting Government Data online

####  Abstract

Government data is being put online to increase accountability, contribute
valuable information about the world, and to enable government, the country,
and the world to function more efficiently. All of these purposes are served
by putting the information on the Web as Linked Data. Start with the "low-
hanging fruit". Whatever else, the raw data should be made available as soon
as possible. Preferably, it should be put up as Linked Data. As a third
priority, it should be linked to other sources. As a lower priority, nice user
interfaces should be made to it -- if interested communities outside
government have not already done it. The Linked Data technology, unlike any
other technology, allows any data communication to be composed of many mixed
vocabularies. Each vocabulary is from a community, be it international,
national, state or local; or specific to an industry sector. This optimizes
the usual trade-off between the expense and difficulty of getting wide
agreement, and the practicality of working in a smaller community. Effort
toward interoperability can be spent where most needed, making the evolution
with time smoother and more productive.

##  Introduction

This, 2009, is the year for putting government data online. Both [
US](http://www.whitehouse.gov/the_press_office/Transparency_and_Open_Government/)
and [
UK](http://www.cabinetoffice.gov.uk/newsroom/news_releases/2009/090610_web.aspx)
governments made public commitments toward open data. The [ TED talk on Linked
Data](http://www.ted.com/index.php/talks/tim_berners_lee_on_the_next_web.html)
was in February. Groups from the
[Guardian](http://www.guardian.co.uk/technology/free-our-data) to the
[Sunlight Foundation](http://www.sunlightfoundation.com/) had already been
pushing for it for a long time. People like Watchdog.net, mysociety.org, and
govtrack.us had been pushing by publishing government data themselves in
various formats, including Linked Data.

So if you want to do this, what should you do? This article addresses this
question very briefly, and makes a set of points which will probably be
outdated by later developments, but answer a set of relevant question, asked
or not.

##  Using Linked Data as the interconnection bus

Government data is put online typically for 3 reasons:

  1. Increasing citizen awareness of government functions to enable greater accountability; 
  2. Contributing valuable information about the world; and 
  3. Enabling the government, the country, and the world to function more efficiently. 

Each of these purposes is best served by using Linked Data techniques.

In general Linked Data is:

**Open**: Linked Data is accessible through an unlimited variety of applications and applications because it is expressed in open, non-proprietary formats. 

**Modular**: Linked Data can be combined (mashed-up) with any other piece of Linked Data. For example, government data on health care expenditures for a given geographical area can be combined with other data about the characteristics of the population of that region in order to assess effectiveness of the government programs. No advance planning is required to integrate these data sources as long as they both use Linked Data standards. 

**Scalable**: It's easy to add more Linked Data to what's already there, even when the terms and definitions that are used change over time. 

The essential message is that whatever data format people want the data in,
and whatever format they give it to you in, you use the RDF model as the
interconnection bus. That's because RDF connects better than any other model.

  * It uses URIs and so allows linking of things and concepts 
  * It allows separate systems designed independently to be later joined at the edges 
  * It allows interoperability to be added where cost-effective 
  * It allows any data to be expressed in a mixture of vocabularies. 

That's enough about why it is useful. That is elaborated elsewhere, but it can
be difficult for those familiar with other technologies to understand the
difference. Sometimes it is better just to do it.

##  Just do it

The chances are quite high that the data your department/agency runs off will
be largely in relational databases, often with a large amount in spreadsheets.

There are two philosophies to putting data on the web. The top-down one is to
make a corporate or national plan, by getting committees together of all the
interested parties, and make a consistent set of terms (_ontology_) into which
everything fits. This in fact takes so long it is often never finished, and
anyway does not in fact get corporate or national consensus in the end. The
other method experience recommends is to do it bottom up. A top-level mandate
is extremely valuable, but grass-roots action is essential. Put the data up
where it is: join it together later.

A wise and cautious step is to make a thorough inventory of all the data you
have, and figure out which dataset is going to be most cost-effective to put
up as linked data. However, the survey may take longer than just doing it. So,
take some data.

A really important rule when considering which data could be put on the web is
not to threaten or disturb the systems and the people who currently are
responsible for that data. It often takes years of negotiation to put together
a given set of data. The people involved may be very invested in it. There are
social as well as technical systems which have been set up. So you leave the
existing system undisturbed, and find a way of extracting the data from it
using existing export or conversion facilities. You add, a thin shim to adapt
the existing system to the standard.

Ok, so you have some data. What form is it in?

###  Relational databases

There are (2009) a number of open source tools for putting relational
databases up as Linked Data, _D2RServer_ and _Triplify_ being two.

These each use a mapping file, in some language, to explain how the database
structure actually represents things and the relationships. 1

You probably don't want to to run a publicly available server on your existing
database unless it is generally set up for high volume use. You might want to
take a copy of the whole database, and run a live semantic web server from it,
or you can generate the RDF once and make a copy of that to serve.

####  Using other people's terms

It is wise and friendly and interoperable, when you public RDF data, to use
terms other people are already sharing. Like foaf:name for the name of a
person, or dc:title for the title of something, and so one. Like geo:lat and
geo:long for latitude and longitude[2](https://www.w3.org/DesignIssues/). There are a number of these, growing
of course. The [Semantic Web Interest
Group](http://www.w3.org/2001/sw/interest/) is a community which can help you
find them: there are also online tools such as
[Swoogle](http://swoogle.umbc.edu/), Sindice, etc. [](https://www.w3.org/DesignIssues/)

###  Spreadsheets

In many organizations a surprising amount of information, sometimes critical
information, is emailed around in spreadsheets. Much of the early recovery.gov
data was published in spreadsheet form. Some of these are raw tables, with a
header in the top row. These are close to raw data. You can export them as a
comma-separated (or tab-separated) file, CSV. Others are spreadsheets with a
lot of substructure, and little headings and notes all over them for the human
user. These are less easy to convert.

There are a number of [tools](http://esw.w3.org/topic/ConverterToRdf) for
converting the format of a spreadsheet, typically in CSV form, into RDF.

###  XML

If you have existing data in XML, first, put that XML up on the web while you
think. Then, figure out what the XML is about, what things and what
relationships. Then, commission or write a program, possibly a simple script,
maybe written in XSLT, or your favorite scripting language, to convert each
XML file into RDF. You might need to add a file which points to all the things
you have data about, if they are not already linked.

###  Random application formats

Ok, so your data is not in any of the above forms. It is in a proprietary
format, or managed by a proprietary program. But there is some way you can get
at it. So someone will have to write a program somewhere, to get it out, and
convert it to one of the Linked Data standard forms.

(It is actually fairly simple. First, you think of what things the data is
about. You make up URIs for those things. Suppose for example your data is
about books and shelves. You decide the URI for the books will be
http://id.example.com/id/isbn/123457890 and the URIs for shelves will be like
http://id.example.com/id/shelf/746 . Then you write a (CGI) script, which,
when given that a URI like that extracts the data about the book (including
which shelf it is on) and outputs it, or similarly for the shelf (including a
list of the books on the shelf). It outputs it in RDF/XML or N3. That script
is your web server of virtual linked data.)

###  Existing Web Site

If you have an existing web site with, maybe, a page about each thing, there
is an easy way of putting the data in those pages into Linked Data. You can
change the scripts which generate the site so that the data which is behind
each page is in fact put into the page so that it can be re-extracted by
others as data. The technology to do this is called [RDFa](http://rdfa.info/)
3. An alternative is for the each web page to have a parallel page which has
the data in RDF/XML. 4

##  Giving access to data

Ok, so you have your data in RDF as Linked Data. Now what?

###  Index it

The semantic web toolkit includes the SPARQL query language which allows a
client anywhere on the net to query a SPARQL service. Some methods of
publishing data, like D2RServer, provide a built-in SPARQL service. If you
have generated a bunch of linked data, then there are various products, free
or commercial, which will scoop it up into a "triple store" and provide a
SPARQL service.

A SPARQL service is a generally useful tool for technically aware users. Many
clients and analytical tools just use a SPARQL server. A SPARQL server looks
for patterns in the data and for each match, or outputs what it found in one
of a number of formats, including constructed RDF, XML and, in some cases,
JSON, and maybe even CSV.

###  Generating XML with SPARQL

SPARQL, then, can be used as an RDF to XML converter. You amass a heap of
linked data. Then you think of a combination of data, involving connections
across different data. There is a SPARQL query for that data with the results
expressed in XML. That SPARQL query can be encoded into a long URI, a URI for
a virtual XML document for that particular view.

###  Generating CSV files and JSON

Some SPARQL servers also support JSON as an output format. This is easy to use
in Web Applications.

###  Generating nice web pages

The priority first is to get raw data onto the net, and preferably converted
into Linked Data form. This is partly because there may be other sites,
commercial or not, who pick it up and make great interfaces to that data. Of
course there are times when the government site must provide a easy human
interface for ordinary users to access the data.

There are many routes to pretty HTML for real users. Tools like Exhibit
provide facetted browser views, given a configuration set up by the web
master, for example.

Webmasters can can run script in languages (not standardized yet) like XSPARQL
or N3 rules, or write custom code in their favorite programming language such
as PHP, Python, Ruby, or server-side Javascript.

Note, though, there are two ways though that a department or agency web site
can never be expected to compete with external sites. One is because there are
as yet no user interface techniques which allow a normal user to create their
own query, (though tools like Tabulator are getting close).

The second is that an external site will add value to the data by joining it
to other data from different sites for a particular purpose. If the Department
of Transport publishes road accident data, a cycling site selects the cycle
accident subset, and can publish it as a map adding cycle routes and hills,
and cycle shops. An agency publishes data about the amount of money given to
different towns, another maps it against the per capital income levels in
those towns. And so on in uncountable permutation.

An informal random sample of some public feedback suggests that there are
users who would prefer each of these formats above, so a system which
generates them automatically is clearly called for.

##  Metadata

When you write or generate a small RDF file for each dataset exported, the
results can be harvested as more useful linked data to form a catalog. Like
the data, this can be distributed form as linked data, and also sucked into a
repository to be indexed and SPARQLed. Remember that, as with the data, RDF
allows you to mix vocabularies, so you can record everything you or others may
feel is important about the datasets. This provenance information is very
valuable. It clearly is one of the many areas this note touches on which much
more could be said.

Neither does it really address licensing issues. In the US, government data is
generally in the Public Domain. It is good to put the fact that a given
resource has a given license in a machine-readable way. The creative commons
cc:license term is appropriate. Creative commons also have produced a "CC0"
waiver which disclaims all rights appropriately (and where possible) for each
country.

##  Privacy

A very common and important concern is the privacy of data which contains
personally identifiable nformation. This article does not suggest that all
data should be made public, nor does it discuss issues with anonymisation of
data. Systems where PIP is an issue will probably not be an early choice when
selecting those to put on the web. However, in cases in which these issues
have already been resolved and the data is already public but not in the
standard form, converting it to Linked Data is an excellent idea. In general,
new government systems should be built to be aware of the provenance of the
data they use, and of the appropriate use to which it may be put. But the
design of these [ accountable systems](http://dig.csail.mit.edu/2008/06/info-
accountability-cacm-weitzner.pdf) is another topic we do not have space for
here.

##  Conclusion

This brief note is too short to go into great detail, and has ignored many
important topics. It has stressed the practical technical steps. Deeper
information, about techniques and also about the social issues and challenges,
are being produced frequently elsewhere. Many cities have Semantic Web
gatherings or [meetup groups](http://semweb.meetup.com/), which can be a
source of mutual support for those involved in or interested in the
technology. The W3C eGov Interest Group is an international group of people
sharing challenges and solutions.

* * *

####  Footnote: Do's and Don'ts

  * Do pick URIs which are likely to be [persistent](https://www.w3.org/Provider/Style/URI)
  * Do put RDF metadata giving the license. 
  * Do use the RDF and SPARQL standards 
  * Make sure your human readable pages are [accessible](http://www.w3.org/WAI). 

  * Do NOT hide data files inside zip files unless they are also available directly. 
  * Do NOT put data up in proprietary formats. 
  * Do NOT wait until you have a complete schema or ontology to publish data. 
  * Do NOT seek to replace existing data systems. 

[1] D2RServer will generate a default mapping file, which will not make a very
good RDF graph. Browsing the resulting RDF with am RDF browser (such as
Tabulator) will however often show up the deficiencies and suggest
improvements

[2] WGS84 latitude and longitude, like you get from a normal GPS unit.
([more](http://www.w3.org/2003/01/geo/))

[3] RDFa is used, for example, in the UK [Civil Service
Jobs](http://www.civilservice.gov.uk/jobs/index.aspx) web site.
([example](http://www.civilservice.gov.uk/jobs/careers-
detail.aspx?JobId=4730))

[4] Separate RDF/XML web pages are used, for example, in the [BBC
programmes](http://www.bbc.co.uk/programmes) data. Here content negotiation
gives RDF/XML to data clients, and HTML to document browsers.
([example](http://www.bbc.co.uk/programmes/genres/comedy#genre))

##  References and Resources

  * [ Linked Open Data](http://www.thenationaldialogue.org/ideas/linked-open-data), in "The National Dialogue" about US recovery transparency. 
  * [ShowUsABetterWay.com](http://ShowUsABetterWay.com/) (UK) 
  * [Example UK Data available for reuse](http://www.showusabetterway.co.uk/call/data.html)
  * [TheNationalDialog](http://TheNationalDialog.org/).org (US) 
  * [Open Government Initiative](http://www.whitehouse.gov/open/) (US) 
  * [ The Power of Information Taskforce Report](http://www.cabinetoffice.gov.uk/reports/power_of_information.aspx) (UK Gov) one of whose recommendations is linked government data 
  * [eGovernment at W3C](http://www.w3.org/2007/eGov/)
  * [W3C eGovernment Interest Group](http://www.w3.org/2007/eGov/IG/)
  * [Improving Access to Government through Better Use of the Web](http://www.w3.org/TR/egov-improving/), W3C eGov IG 
  * [ Transparency and Open Government](http://www.whitehouse.gov/the_press_office/Transparency_and_Open_Government/), Memorandum for the Heads of Executive Departments and Agencies, Barack Obama, 2009-01-21 
  * [Paper on the lessons from the UK AKTivePSI project](http://eprints.ecs.soton.ac.uk/14429/)
  * [Semantic Web Development Tools](http://esw.w3.org/topic/SemanticWebTools), eSW Wiki. 
  * [Tools to convert data into RDF](http://esw.w3.org/topic/ConverterToRdf), in eSW Wiki. Don't just look in the wiki for things -- add things you have found! 
  * [RDFA.info](http://rdfa.info/) a resource about RDFa. Ben Adida. 

####  Acknowledgements

Thanks for input to this article from Nigel Shadbolt and Danny Weitzner.
Thanks also to the chairs (John Sheridan and Kevin Novak) and members of the
W3C eGov interest group, and all those in UK and US governments with whom we
have discussed these issues at these early stages.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

