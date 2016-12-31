# README


![W3c](https://www.w3.org/Icons/WWW/w3c_home.gif)

* * *

#  Design Issues

##  Architectural and philosophical points

These statements of architectural principle explain the thinking behind the
specifications. These are personal notes by Tim Berners-Lee: they are not
endorsed by W3C. They are aimed at the technical community, to explain
reasons, provide a framework to provide consistency for for future
developments, and avoid repetition of discussions once resolved.

  * [ Preface ](Preface.html.md) (1998-10-01) 
  * [ The Stack of Specifications ](Stack.html.md) (2002-07-29) 
  * [ Levels of Abstraction: Net, Web, Graph  ](Abstractions.html.md) (2007-10-23) 
  * [ **Web Architecture from 50,000 feet**** ](Architecture.html.md) (1998-09-04) 
    * [ Principles of Design](Principles.html.md) (1998-9) 
    * [ The Web Model: Information hiding and URI syntax ](Model.html.md) (19998-01-29) 
  * [ Axioms of Web architecture: URIs ](Axioms.html.md) (1996-12-19) 

    * [Fragment identifiers](Fragment.html.md)
    * [_Using Relative URIs_](Relative) (2011) 
    * [_Webizing an existing application_](Webize.html.md) (2000/09) 
    * [What do HTTP URIs identify?](HTTP-URI.html.md) (2002/09) 
    * [What HTTP URIs identify](HTTP-URI2.html.md) (2005/6) 
    * [_A Short History of the term "Resource"_](TermResource.html.md) (2009/8) 
  * [_Links and laws_](LinkLaw.html.md) \- what does a hypertext link imply? (April 1997) 
    * [_Myths about Links_](LinkMyths.html.md) (April 97) 
    * [_Persistent Domains_](PersistentDomains)\- an idea for persistence of URIs(2000/10) 
  * [The Myth of Names and Addresses](NameMyth.html.md)
  * [Generic resources 3-96](Generic.html.md)
  * [Metadata Architecture](Metadata.html.md) (6 Jan 1997) 
    * _[Dictionaries in the Library?](NamespacesAreResources.html.md)_ On the two-level system design error (2000) 
  * [The meaning of a document](Meaning.html.md) \- grounding in a global namespace (1999 - in progress) 
    * [The Interpretation of an XML document](XML) (2002)
  * [Mandatory extensions: A fundamental design need](Mandatory.html.md)(1999? in progress) 
  * [Extensible languages and web evolution](Extensible.html.md)(Feb 1998) 
  * [Evolvability (April 1998)](Evolution.html.md)
    * [Mandtory extensions](Mandatory.html.md) (2000/1) 
  * Web Security: new 2015
    1. ["HTTPS Everywhere" considered harmful](Security-NotTheS.html.md)
    2. [Model Real Trust](Security-ModelTrust.html.md)
    3. [The Same Origin Policy - Origin Granularity](Security-Origin.html.md)
    4. [Client-Side Certificates](Security-ClientCerts.html.md)
  * [A roadmap to the Semantic Web (Sept 98)](Semantic.html.md)
    * [What the semantic Web isn't but can represent](RDFnot.html.md) (1998) 
    * [ **Linked Data** ](LinkedData.html.md) (2006-07-27) 

      * [ Read-Write Linked Data ](ReadWriteLinkedData.html.md) (2009-10-11) 
      * [ Socially Aware Cloud Storage ](CloudStorage.html.md) (2009-08-17) 
    * [Putting Government Data on the Web](GovData.html.md) (2009/6) 
    * [RDF and Relational databases](RDB-RDF.html.md) (1998) (link added 2001) 
    * [Conceptual Graphs and the semantic Web](CG.html.md) (2001) 
    * [Why RDF model is not exactly the XML model](RDF-XML.html.md) (1999) 
    * [Identity: how to identify what in RDF](Identity.html.md) (2000/02) 
    * [Using labels to give semantics to tags.](TagLabel.html.md) (2006/11) 
    * [Interpretation expressed as RDF property](InterpretationProperties.html.md) (language, etc)(2000/03) 
    * [Semantic Web Toolbox: Logic and trust in XML-RDF?](Toolbox.html.md)(1999) 
    * [Semantics and Interpretation](Interpretation.html.md) (and dig.sig.) (1999/12/1) Philosophical bits 
    * [Logic and the semantic web](Logic.html.md) (1999) 
    * [The RDF-diff problem](Diff) \- transmitting changes to graphs (2001, 2004) 
    * [Rules and facts: Inference engines and the Semantic Web (2000/1)](Rules.html.md)
    * [Limiting the damage of an inconsistency](Inconsistent.html.md) (2000/1) 
    * [Notation3](Notation3.html.md): Logic and Rules on RDF - showing it is possible (2000/10) 
      * _[Design alternatives considered in Notation3](N3Alternatives)_ (2002/03) 

      * [Reification of RDF and N3](Reify.html.md) (2004/12)

    * [The Semantic Clipboard](SemanticClipboard) (2004/1) 
  * [Roadmap for Web Services](WebServices.html.md) (see WS arch WG) 
    * [Paper Trail](PaperTrail.html.md)\- read/write state derived from r/o documents in real life: which came first, the journal or the database? 
    * [Conversations and State](Conversations) \- linking the two models (2000/11) 
  * [_Filtering and censorship_](Filtering.html.md) \- more philosophical than technical: is metadata a good thing? (December 1997) 
  * [ **No Snooping** on the Internet ](NoSnooping.html.md) (2009-03-09) 
  * [_Fractal web, fractal society_](Fractal.html.md) (1999) 
  * [_User Interface in a consistent world_](UI.html.md)(6 Feb 97) 
    * [_User agent watch points_](UserAgent.html.md) -interpreting HTTP(1999/12) 
    * [_Intuitive hypertext editing_](Editor.html.md)
    * Editing and Browsing Data with RDF and SVG @@ 
  * [_Persistent Domains_](PersistentDomains.html.md) _\- a social problem, social solution_(2000) 
  * [How to write a specification (1999)](../1999/09/specification.html.md)

  
---  
  
* * *

##  Informal notes not in this series

  * [Mappings and identity in URIs and IRIs](http://www.w3.org/2003/04/iri.html.md)

##  Obsolete notes

  * [Assumed syntax](Syntax.html.md) \- a simpler RDF syntax used in the following. (1999). This proposed altervative to RDF/XMl was never adopted, RDF/XML prevailing as a standard and in practice also Notation3. 
  * [When to use XLink](Xlink.html.md) (2002/06) 

##  Original design issues

[![1990 archives](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html) _These documents date
from the original design of the web, dating from 1990 when the first HTML
editor was available to write them. When reading them please bear this in
mind. Some have been updated later. Although the design is for a global
general hypertext system, the justification for the initial project was the
CERN environment and this may be evident in some places._

This lists decisions to be made in the design or selection of a
[hypermedia](https://www.w3.org/WhatIs.html) information system. It assumes familiarity with
the concept of hypertext. A summary of the uses of hypertext systems is
followed by a list of features which may or may not be available. Some of the
points appear in the Comms ACM July 88 articles on various hypertext systems.
Some points were discussed also at [ECHT90](https://www.w3.org/Conferences/ECHT90/Points.html) .
Tentative answers to some design decisions from the CERN perspective are
included.

Here are the criteria and features to be considered:

  * [Intended uses of the system.](Uses.html.md)
  * [Availability on which platforms?](Availability.html.md)
  * [Navigational techniques and tools: browsing, indexing, maps, resource discovery, etc](Navigation.html.md)
  * [Keeping track of previous versions of nodes and their relationships](Versioning.html.md)
  * [Multiuser access: protection, editing and locking, annotation.](Multiuser.html.md)
  * [Notifying readers of new material available](Notification.html.md)
  * [The topology of the web of links](Topology.html.md)
  * [The types of links which can express different relationships between nodes](LinkTypes.html.md)

These are the three important issues which require agreement between systems
which can work together

  * [Naming and Addressing](Naming.html.md) of documents 
  * [Protocols](../Protocols/RelevantProtocols.html.md)
  * [The format in which node content is stored and transferred](Formats.html.md)
  * Implementation and optimization - [Caching](Caching.html.md) , smart browsers, knowbots etc., [format conversion, gateways.](Formats.html#4)

Other historical notes which are not otherwise referenced in this overview:

  * [Annotation](https://www.w3.org/DesignIssues/Annotation)
  * [Building Back Links](https://www.w3.org/DesignIssues/BuildingBackLinks)
  * [Proof that HTTP 1.0 is compatible with 0.9](https://www.w3.org/DesignIssues/CompatibleProof)
  * [Function](Function.html.md)
  * [From version to version of HTTP](ProtocolVersions.html.md)
  * [Summary of HTTP 0.9](HTTP0.9Summary.html.md)

  
---  
  
Other historical notes

  * [A pre-XML (pre W3C!) note about reforming SGML](https://www.w3.org/MarkUp/SGML/TimComments.html) (1993/3) 

* * *

![W3c](https://www.w3.org/Icons/WWW/w3c_home.gif)

---




