Tim Berners-Lee  
Date: 2006-11-23, last change: $Date: 2007/01/22 21:05:37 $  
Status: personal view only. Editing status: draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Using labels to give semantics to tags

###  Abstract

Existing user interfaces for managing, for example, mail, photos, contacts and
songs allow searching using both user-generated 'tags' and also well-defined
properties such as the date-time of a photograph, or the values of headers in
an email message. Users have on many web sites provided many tags, but their
re-use by others has been limited due to the fact that the same tag word has
quite different meaning when used by another person or used on another site.

Other data, such 'geotagging' of places, declaration of friends and
colleagues, by contrast, have a well-defined meaning and allow query across
data from many sites. This article discusses how the user interface metaphor
of a luggage label cam used to associate metadata from well-defined ontology
with tags from a particular context.

The article discuses ways of encoding the labels in RDF.

###  Introduction

There are a mixed feelings about the passion for tagging which typifies the
Web 2.0 wave. On the one hand, there is excitement about the fact that users
are, as a large number, adding re-usable information to the information space,
allowing sites such as del.icio.us and flickr to sort, cluster and query
masses of otherwise amorphous photos and web content. On the other hand, there
is the sinking feeling that tags are headed the same way as keywords of
Information Retrieval in the 1980s: initial hope, and then being stranded
between the unbearable constraints of a controlled vocabulary and the hopeless
ambiguity of uncontrolled user-generated keywords. Tom Gruber, writer of books
on ontology who runs a Web 2.0 site himself. gave a talk at ISWC 2006 which
touched on bringing the gap, and taking the passion to organize and express,
and using it to make re-usable data.

There is currently a tension in the tagging world as to whether tags are
regarded as global in meaning, or whether there meaning really depends on the
tagger. In del.icio.us, one can query for thinks tagged with a certain word by
a certain person. (I heard of one online community which was considering
making a system to allow one formally to state when one has committed to use a
given tag in the same way as another person, or growing mesh of people. That
would be a very interesting feature, as it would allow a useful definition to
gain growing acceptance, to progressively move from being a private idea to
being a group global standard.)

Meanwhile, other sites get users to provide semantic web data with well-
defined global ontologies. The locations of people, events and photos,
relationships between people, authorship of publications, things and people an
image depicts, and so on, is done using well-defined identifiers (under the
covers) for everything involved, including the relationships and properties.
The resulting data is extremely re-usable. The problem is that it isn't as
quick as tagging with a single word off the top of one's head.

###  Example: Soccer folders

I face these problems day to day, and like many geeks, am driven by the urge
to make the boring things in life happen automatically, with the computer
helping more effectively. There are lots of things I can do with N3 rules --
but I'd like to have a nice user interface to it which hides as much
technology beneath the surface as possible. I'd like as many non-geeks as
possible to be able to use the same tools.

Let's take one example. I took a bunch of photos of a local soccer team, once
when they played Wayland, and once when they played Arlington. I loaded them
all into iPhoto. I wanted to burn a CD for the team of the best of the bunch.
I also want to be able to find them later.

On the first day, I didn't take any other photos, so the simplest thing was to
make a 'smart folder' (actually 'smart Album' in iPhoto) , which had in it by
definition the photos taken on that day. The smart folder allows you to
specify a combination (_and_ or _or_) a number of constraints such as time,
keyword, text and rating. I called this one _Soccer vs Wayland_.

On the second day, I took other photos as well, so the smart folder was going
to be more complicated. So instead, I just found all the photos, selected
them, and dumped them in a new plain folder _Soccer vs Arlington_.

These of course one would represent in RDF as classes. - but we'll get into
that later.

Ok, so here's where we get into wish-list territory.

1) At that point, I wanted to be able to make a virtual folder _Soccer_, and
make the two folders subfolders. (There used to be a photo processing tool
called _Retriever_ which would handle hierarchical classifications well, but
that I lost track of.) This would indicate that anything in either of the two
Soccer subfolders was a member of the Soccer folder -- or was tagged 'soccer'
if you like.

In fact, you can make a smart folder _Soccer_ consisting of all the things
which are either in _Soccer vs Wayland_ or _Soccer vs Arlington_. You have to
make it as a smart folder, which is not as intuitive, but woks fine. It
doesn't give me the nice hierarchical user interface.

###  Labels

Actually I now want to associate some exportable re-usable data. The folder
names are essentially my local tags. Exporting them doesn't help much.

Suppose, for example, I want to geotag the photos, so that I can find them on
a map, or people interested in sports at the given field could find them. The
current user interface allows me to select all the photos in one folder and
apply keywords and apply metadata to them, as a batch operation. It is
actually useful that the data is carefully stored in each photo, but it is sad
that the fact that the metadata (such as a comment about the game) was applied
to everything in the folder.

I'd like to be able to associate the random tag name I just made up with
properties to be applied to each of the things tagged. Suppose at the user
interface we introduce a label. A label is a set of common metadata that I
want to apply to things at once.

The user interface could really milk the _label_ metaphor, by representing a
label as a box with a hole in the end with a bit of string. It clashes perhaps
with the folder metaphor. If we use both, then I'd like to be able to drop a
label on a folder, and let all the things in the folder inherit the labeled
properties.

I'd like to see for each photo firstly what properties it has, but secondarily
which labels and hence folder the properties came from.

The essential thing about a label is that as I build it, I am prompted to use
shared ontologies. They could be group ontologies which others have exported,
they could be globally understood ontologies like time and place, and email
address of a person depicted. As I create the label from an (extendable) set
of options in menus, and using drag and drop and other user interface tricks
for noting relationships, I am creating data which will be much more useful
than the tag. The tag then I can slap on very easily.

The hope is then that by making label creation something which is low cost,
because I have to do it only once and can apply it many times, the incentive
for me @@

###  Expressing labels

In this section we leave the user interaction and discuss the way in which
labels can be exchanged in RDF under the covers. This of course is important
for interoperability. A label can be expressed in many ways. in bits on the
wire. The label describes a set of things, which in RDF is a class*.
Information about the class and the things in it -- the things labeled -- can
be given in various ways.

####  As a rule

As a rule, it could look like

    
    
       { ?x a soc:SoccerWaylandPhoto }
    => { ?x geo:approxLocation [ geo:lat 47. geo:long 78 ];
            foaf:depicts soc:ourTeam.
       }
    

####  In OWL

A label is a fairly direct use of OWL restrictions:

    
    
    SoccerWaylandPhoto rdfs:subClassOf [
        [ a owl:Restriction; owl:owl:onProperty geo:approxLocation;
          owl:hasValue  [ geo:lat 47. geo:long 78 ]],
        [ a owl:Restriction; owl:onPredicate foaf:depicts;
         owl:allValuesFrom soc:ourTeam].
    
    

(Let's not discuss the modeling of depiction here, rather elsewhere.) This is
very much the sort of thing OWL is designed for.

####  How not to

There is one trap which one must beware of. Remember that the label is a
concept. It is a class. It isn't a photo. The label may have been created by
someone, at a particular time, but that person and that time have nothing to
do with the creator and time of a photo which is so labeled. You can **not**
write

    
    
    soc:SoccerWaylandPhoto
            geo:approxLocation [ geo:lat 47. geo:long 78 ];
            foaf:depicts soc:ourTeam.
    

####  Special vocabulary

It is possible to make a special label terms which are only used only for
labels:

    
    
    soc:SoccerWaylandPhoto
            LAB:approxLocation [ geo:lat 47. geo:long 78 ];
            LAB:depicts soc:ourTeam.
    

and have some metadata like

    
    
    foaf:depicts  ex:labelPredicate LAB:depicts.
    geo:approxLocation ex:labelPredicate LAB:approxLocation.
    

and a general rule like

    
    
        { ?x a ?lab. ?lab ?p ?z. ?p ex:labelPredicate ?q }
     => { ?x ?q ?z }.
    

or

    
    
        { ?lab ?p ?z. ?p ex:labelPredicate ?q }
     => { ?lab rdfs:subClassOf [ a owl:Restriction;
           owl:onProperty ?q; owl:hasValue ?z] }.
    

These methods are more or less inter-convertible. There are various
communities which understand OWL and N3 rules, which may find those forms most
convenient.

###  Sharing tags and labels

The architecture of this system then is that tags are initially local to the
user. Anyone can use any word to to tag anything they want. Labels are used to
associate meaning with them, but the tag itself is local.

Mapped into RDF, tags are classes in a local namespace. They can of course be
shared. Tagging things with other people's tags attributes to them the
properties associated with those tags, if any. Some people may define tags
with rather loosely defined meaning, and no RDF labels, in which case others
will be less inclined to use those tags.

###  Smart Labels and one-variable rules

When one combines a selection expression of a 'smart folder' with a label,
then the result is a form of rule which is restricted to one variable. This
can be expressed in OWL as a subclass relationship between restrictions.

A lot of information can be expressed as rules, but finding an intuitive user
interface to allow lay users to express their needs with rules has been a
stumbling block. These smart folder and label metaphors, combined, could be a
route to solving this problem*.

##  Work in the area

There are many systems which use selection rules to define virtual sets of
things. There probably lots which use an abstraction equivalent to labels.

One system which effectively uses labels is (I think) described as 'semantic
folders' (@@link Lassila and Deepali), to be published

There is a language for labels being defined, as it happens, by the Web
Content Labeling (WCL) Incubator Group at W3C. The final form of expression
has not been decided.

##  Conclusion

The concept of a label as a preset set of data which is applied to things and
classes of things provides an intuitive user interface for a operation which
should be simple for untrained users.

* * *

###  See also

Newman.R., [Tag ontology
design&gt;](http://www.holygoat.co.uk/projects/tags/), 2005-03-29.

Stefano Mazzochi,[Folksologies: de-idealizing
ontologies](http://www.betaversion.org/~stefano/linotype/news/85/), 2005-05-05

Tom Gruber, _Where the Social Web Meets the Semantic Web_, Keynote, ISWC 2006.
( [video](http://seminars.ijs.si/iswc2006/video.asp?video_id=1831))

[W3C Content Label Incubator Group](http://www.w3.org/2005/Incubator/wcl/)

Dan Connolly, [Some test cases from WCL/POWDER work in
N3.](http://www.w3.org/2000/10/swap/test/powder4.n3)

##  Footnotes

*we do not here discuss the difference between rdfs:Class and owl:Class 

How could other variables be added? Other variables can be expressed as paths
from the base variable, and paths can be selected from a menu-like tree, and
so on. The tabulator has a user interface for selecting a subgraph for a
query. The smart folder selection panel could have the option for adding
another similar panel for an item connected by a search path.

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

