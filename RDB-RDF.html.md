Tim Berners-Lee Created

Date: September 1998.

$Id: RDB-RDF.html,v 1.25 2009/08/27 21:38:09 timbl Exp $

Status: . Editing status: Comments please. An parenthetical discussion to the
[Web Architecture at 50,000 feet](https://www.w3.org/DesignIssues/Architecture.html). and the [Semantic Web
roadmap](https://www.w3.org/DesignIssues/Semantic.html).

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

* * *

#  Relational Databases on the Semantic Web

There are many other data models which RDF's Directed Labelled Graph (DLG)
model compares closely with, and maps onto. See a summary in

  * [What the Semantic Web can represent](https://www.w3.org/DesignIssues/RDFnot.html)

One is the Relational Database (RDB) model.

##  The Semantic Web and Entity-Relationship models

Is the RDF model an entity-relationship mode? Yes and no. It is great as a
basis for ER-modelling, but because RDF is used for other things as well, RDF
is more general. RDF is a model of entities (nodes) and relationships. If you
are used to the "ER" modelling system for data, then the RDF model is
basically an openning of the ER model to work on the Web. In typical ER model
involved entity types, and for each entity type there are a set of
relationships (slots in the typical ER diagram). The RDF model is the same,
except that relationships are first class objects: they are identified by a
URI, and so anyone can make one. Furthurmore, the set of slots of an object is
not defined when the class of an object is defined. The Web works though
anyone being (technically) allowed to say anything about anything. This means
that a relationship between two objects may be stored apart from any other
information about the two objects. This is different from object-oriented
systems often used to implement ER models, which generally assume that
information about an object is stored in an object: the definition of the
class of an object defines the storage implied for its properties.

For example, one person may define a vehicle as having a number of wheels and
a weight and a length, but not foresee a color. This will not stop another
person making the assertion that a given car is red, using the color vocabular
from elsewhere.

Apart from this simple but significant change, many concepts involved in the
ER modelling take across directly onto the Semantic Web model.

##  The Semantic Web and Relational Databases

The semantic web data model is very directly connected with the model of
relational databases. A relational database consists of tables, which consists
of rows, or records. Each record consists of a set of fields. The record is
nothing but the content of its fields, just as an RDF node is nothing but the
connections: the property values. The mapping is very direct

  * a record is an RDF node; 
  * the field (column) name is RDF propertyType; and 
  * the record field (table cell) is a value. 

Indeed, one of the main driving forces for the Semantic web, has always been
the expression, on the Web, of the vast amount of relational database
information in a way that can be processsed by machines.

RDF's serialization format -- its syntax in XML -- is a very suitable format
for expressing relational database information.

###  Special aspects of the RDB model

Relational database systems manage RDF data, but in a specialized way. In a
table, there are many records with the same set of properties. An individual
cell (which corresponds to an RDF property) is not often thought of on its
own. SQL queries can join tables and extract data from tables, and the result
is generally a table. So, the practical use for which RDB software is used
typically optimized for doing operations with a small number of tables some of
which may have a large number of elements.

A fundamental aspect of a database table is that often the data in a table can
be definitive. Neither RDF nor RDB models have simple ways of expressing this.
For example, not only does a row in a table indicate that there is a red car
whose Massachusetts plate is "123XYZ", but the table may also carry the
unwritten semantics that if any car has a Massachusetts plate then it must be
in the table. (If any RDF node has "Massachusetts plate number" property then
than node is a member of the table) The scope of the uniquenes of a value is
in fact a very interest property.

The original RDB model defined by E.F. Codd included datatyping with
inheritance, which he had intended would be implememnted in the RDB products
to a greater extent that it has. For example, typically a person's home
address house number may be typed as an an integer, and their shoe size may
also be also be typed as an integer. One can as a result join to tables
through those fields, or list people whose shoe size equals their house
number. Practical RDB systems leave it to the application builder to only make
operations which make sense. Once a database is expreted onto the Web, it
becomes possible to do all kinds of strange combinations, so a stronger typing
becomes very useful: it becomes a set of inference rules.

In a pure RDB model, every table has a primary key: a column whose value can
be used to uniquely identify every row. Some products do not enforce this,
leading to an ambiguity in the significance of duplicate rows. A curious
feature is that the primary key can be changed without changing the identity
of a row. (A person can change their name for example). SQL allows tables to
be set up so that such changes can cascade through the local system to preseve
referential integrity. This clearly won't work on the Web. One solution is to
use a row ID -- which many systems do in fact use although SQL doesn't expose
it in a standard way. Another is for the application to coinstrain the primary
key not to change. Another is to put up with links breaking.

RDB systems have datatypes at the atomic (unstructured) level, as RDF and XML
will/do. Combination rules tend in RDBs to be loosely enforced, in that a
query can join tables by any columns which match by datatype -- without any
check on the semantics. You could for example create a list of houses that
have the same number as rooms as an employee's shoe size, for every employee,
even though the sense of that would be questionable.

The new SQL99 standard is going to include new object-oriented features, such
as inherited typing and structured contents of cells - arrays and structs.
This RDB model with things from the OO world. I don't deal with that here in
that the RDF model works as a lowest commoin denominator being able to express
either and both.

###  Schemas and Schemas

A difference between XML/RDF schemas (and SGML) on the one hand and database
schemas on the other is the expectation that there will be a relatively small
number of XML/RDF schemas. Many web sites will export documents whose
structure is defined by the same schema, and this is in fact what provides the
interoperability.

A database schema is, as fasr as I know, created independently for each
database. Even if a million companies clone the same form of employee
database, there will be a million schemas, one for each database.

It may be that RDF will fill a simple role in simply expressing the
equivalence of the terms in each database schema.

###  Exposing a database on the Web

In order to be able to access a table, and make extra statements about it
which will enable its use in more and more ways, the essential objects of the
table must be exported as first class objects on the Web.

When mapping any system onto the Web, the mapping into URI space is critical.
Here we are doing this common operation generically for all relational
databases. It is obviously usefuil for this to be done in a consistent ways
between multiple vendors would be useful - an area for possible
standardization.

Here is a random example I may have gotten wrong, basd on whatI understand of
the naming within databases. The database itself is defined within a schema
which is listed in a catalog.

Mapping an RDB into the Web - strawman  Catalog  |  http://www.acme.com/mycat
|  
---|---|---  
Schema  |  http://www.acme.com/mycat/schema1  |  
Database  |  http://www.acme.com/mycat/schema1/empdb/  |  Relative:  
Table  |  /mycat/schema1/empdb/emps  |  emps  
Column name  |  /mycat/schema1/empdb/emps/shoe  |  emps/shoe  
View  |  /mycat/schema1/empdb/emps2  |  emps2  
Row  |  /mycat/schema1/empdb/emps/rowid=123  |  emps/rowid=123  
Cell  |  /mycat/schema1/empdb/emps/rowid=123;col=shoe  |
emps/rowid=123;col=shoe  
Arbitrary query  |  /mycat/schema1/empdb/?select+empno+from_[...]_ |
?select_[...]_  
  
2002 version, see [real code](http://www.w3.org/2000/10/swap/dbork/dbview.py)
implemented by Dan Connolly:

What |  Uriref relative to http://www.acme.com/wherever/  |  rdf:type  
---|---|---  
  
Database description of database "personnel"

|  personnel

(say - whatever)

|  soc:Work, rdfdocument, db:DatabaseDescription  
The conceptual database(a table of tables??)  |  personnel#_database

(Arbitrary, must not clash, linked by `**db:describes**` from personnel)

|  
A document giving all the data in the database. May support PUT?  |
personnel/_data

(Arbitrary, must not clash with table names, linked by **`db:allData`** from
personnel)

|  soc:Work, rdfdocument  
The concept of the table "employees": The class of exactly those things which
are in the table.  |

personnel/employees#.table

(was: personnel#employees, but changed to allow it to be deref'd to giev
useful data)

(defined in personnel)

|  rdfs:Class, db:Table  
A description of the table. Optimization: includes the current size of the
table. Identifies primary key if any.  |  personnel/employees

(**Convention**. The bit of the classname before the #)

|  soc:Work, rdfdocument, db:TableDescription  
A description of all the tables. Just an (optional) optimization.  |
personnel/_all

(Arbitrary, must not clash, linked by `**db:tableSchemas**` from
personnel/employees)

|  soc:Work, rdfdocument, db:TableDescription  
The concept of a column in the table, the Property something has iff that is
recorded in the table.  |  personnel/employees#email

(Defined in personnel/employees)

|  rdf:Property, db:Column  
A document giving all the data in the table. May support PUT  |
personnel/employees/_data

(Arbitrary, must not clash, linked by **`db:tableData`** from
personnel/employees)

|  soc:Work, rdfdocument,  
A document giving the data in the row for which the primary key is 1234. (Iff
primary key exists). May support PUT  |  personnel/employees/1234

(**Convention.** Note the primary key value must be encoded suitably!)

|  soc:Work, rdfdocument  
The concept of the thing describd by that row.  |

personnel/employees/1234#item

(**Convention**)

(when primary key exists, then employees#_data etc use this URIref for the
item 1234 intead of making anonymous nodes)

(employees/_data#1234?@@)

|  personnel/employees#_Class  
A document giving the information in just one cell  |
personnel/employees/1234/email

(**Convention**)

|  [ is rdf:domain of personnel/employees#email ]  
Arbitrary query  |  personnel/_sql?select+empno+from_[...]_

(arbitrary, linked by `**db:sqlService**` from personnel if supported.)

|  soc:Work, rdfdocument  
Arbirary HTML form field match (select * from employees where email like
"*fred*") [@details]  |  personnel/_fquery?email=*fred*;name=Joe

(arbitrary, linked by `**db:formService**` from personnel if supported)

|  soc:Work, rdfdocument  
POST point for RDF data, either new data, or assertions that some (n3) Formula
is a log:Falsehood.  |

personnel/_postme

(arbitrary, linked by `**db:deltaService**` from personnel if supported. Could
be same URI `personnel` in fact, as we are dealing iwth a different method)

|  db:postable  
  
@@@ How to use typing to indicate that the URI in the table is a (relative?)
URI to another object, not a string?

@@@ This works fine when implemented live on a database. However, it is a
little tricky to emulate in a typical file-based web server because of the use
of "personnel" in this case both as directory and as

One of the things which makes life easier is to make the mapping so that the
relative URI syntax can be used to advantage. For example, here, everything
within the database (the scope of an SQL statement) can be writted as a short
URI.

There is a question as to how much of the SQL query syntax should be turned
into identifier. For example, is a query on a primary key really an
identifier? Is the extraction of a single cell really an identifier? It would
be useful to be able to treat them as such. However, it would be wiser to use
the "?" convention to indicate a generalized SQL idempotent query. (A URL
should [of course](https://www.w3.org/DesignIssues/Axioms.html#get) _never_ be used to refer to the results of
a table-changing operation such as UPDATE or DELETE. In this case, if HTTP
were used, an SQL query should IMHO be POST ed to the database URI. Of course,
you can use your favorite networked database access protocol)

In the above the column name of the table could be refered to using the table
as a namespace, a row for example being

    
    
    <foo  
      xmlns:t="http://www.example.com/mycat/personnel/employees">  
      <t:email>joe@example.com</t:email>  
      <t:age>45</t:age>  
    </foo>
    

and one row of the the result of joining this table (of people) and another
table (about people) by their primary keys would use namespaces from both
tables:

    
    
    <foo  
      xmlns:t="http://www.example.com/mycat/personnel/employees"  
      xmlns:u="http://www.acme.com/mycat/schema1/empdb/likes">  
        <t:email>joe@example.com</t:email>  
      <t:age>45</t:age>  
      <u:music>blues</u:music>  
    </foo>
    

* * *

##  Later related work:

[R2O, an Extensible and Semantically Based Database-to-Ontology Mapping
Language.](http://www.cs.man.ac.uk/~ocorcho/documents/SWDB2004_BarrasaEtAl.pdf)
Barrasa J, Corcho O, GÃ³mez-PÃ(C)rez A. Second Workshop on Semantic Web and
Databases (SWDB2004). Toronto, Canada. August 2004\.

* * *

_This has been elaborated with help of an RDB tutorial and discussion from
Andrew Eisenberg/Sybase_.

* * *

See also: [Why RDF is more than XML](https://www.w3.org/DesignIssues/RDF-XML.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html); back to [Architecture from
50,000ft](https://www.w3.org/DesignIssues/Architecture.html)

timbl

