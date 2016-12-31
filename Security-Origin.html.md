Tim Berners-Lee  
Date: 2015-02-15, last change: $Date: 2015/03/27 21:20:42 $  
Status: personal view only. This is not a formal W3C director view, nor view
of the TAG or the Consortium as a whole. It is a contribution to the
discussion. It consists of a number of related observations, which could have
gone into separate notes, but in the end seemed to be all fairly connected.
Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Web Security - The Same Origin Policy - Origin granularity

## Granularity of web sites, trust and the Same Origin Policy.

You can't discuss authentication of parties without discussing what
constitutes a party. In the current web, the domain name clearly distinguishes
parties. The current Same Origin Policy not only uses domain names as
principals, but it also assumes a hierarchy among them, in that for example
csail.mit.edu is deemed to subordinate to mit.edu. That is, to be simplistic,
when looking the rights os applications and the protection of user privacy, it
is assumed that a mit.edu app should be able to access data from scripts from
csail.mit.edu, but not the other way around.

Note that while the URI space has always had also a hierarchical form in the
path part of the URI, the slashes, that is currently **not** used. This means
that f your website had a structure like

    
    
    https://camps.org/campsunshine/families/smith/jane/stuff
    

in order to give Jane Smith a space to play with her scripting enabled, the
URL needs to be changed to something more like

    
    
    https://jane.smith.families.campsunshine.camps.org/stuff
    

What's wrong with this picture?

  * It forces the URLs all to be broken as they are changed. 
  * It removes the ability to be able to use relative URLs around related parts. Links between the family web and Jane's bit can't just be like "jane/stuff" they have to be absolute. This means the family can't zip up their files and run them on the home server another day, or develop them in file: space to seem what they look like offline, etc 
  * It invites the system to be changed multiple times 
  * It reveals to anyone looking a reader's DNS requests, not just that the reader is going to the innocuous camps.org site but to the web site of notorious activist Jane Smith. The reader's privacy is being whittled away a little more. 

In general, it is dangerous when the URI is made opaque in any way. Sometimes
it is necessary -- the best of many bad choices. An example is the 's' in
HTTPs. (The massive opaqueness is indeed the domain name, as that is the path
for the trust that the user has in trusting the session at all.)

It was a very early design decision to make the hierarchical nature of a URI
transparent, using "/". There is another lack of opaqueness in the
hierarchical nature of the path part of the URI. The problem with the same
origin policy as it is is that it is using a different, previously largely
unused that the idea of the "/" was just such a hierarchical syntax. In many
web bowsers like the classic Apache, the URL space maps directly to chunks of
the unix file system. This is deliberate as many good things come with the
unix file system. One is hierarchical delegation. The way unix file
permissions work, things are inherited down the tree. The way .htaccess files
are used within the server's file tree is completely hierarchical, in that a
.htaccess point at a given point can control things below it in th tree but
not above it. This is a very useful feature. It allows things to be embedded
within the system. It allows a [reverse] proxy within the web site to map
arbitrary branches of the tree onto internal or external services.

For example, when the camp.org board meets they can use one of the popular
meeting coordination tools proxied into the tree:

    
    
    https://camps.org/board/AcmeDiscss/stuff
    

Here it would be valuable to make sure that the AcmeDiscss outside service
can't so a cross-site attack to read all the board papers in

    
    
    https://camps.org/board/papers
    

The browsers are not currently programed to do that. Instead one has to set up
like

    
    
    https://AcmeDiscss.camps.org/
    

or

    
    
    https://AcmeDiscss.board.camps.org/
    

when in fact what is probably set up is in practice

    
    
    https://campsboard.AcmeDiscss.com/
    

where there in no reference at all to the actual trust structure, and the
camps.org board have to trust that any AcmeDiscss.com scripts can read their
data.

We should investigate ways of allowing trust to pass in the / hierarchy of the
path as well as the domain name. We should also move away from more reliance
on domain names in general in the web.

* * *

This is the 2nd of 4 related notes:

  1. ["HTTPS Everywhere" considered harmful](https://www.w3.org/DesignIssues/Security-NotTheS.html)
  2. [The Same Origin Policy - Origin Granularity](https://www.w3.org/DesignIssues/Security-Origin.html)
  3. [Model Real Trust](https://www.w3.org/DesignIssues/Security-ModelTrust.html)
  4. [Client-Side Certificates](https://www.w3.org/DesignIssues/Security-ClientCerts.html)

## References

@@ Pointers to email threads on www-tag etc  [2] Mike Specter
&lt;specter@mit.edu> private communication.

This is the 2nd of 4 related notes:

  1. ["HTTPS Everywhere" considered harmful](https://www.w3.org/DesignIssues/Security-NotTheS.html)
  2. [The Same Origin Policy - Origin Granularity](https://www.w3.org/DesignIssues/Security-Origin.html)
  3. [Model Real Trust](https://www.w3.org/DesignIssues/Security-ModelTrust.html)
  4. [Client-Side Certificates](https://www.w3.org/DesignIssues/Security-ClientCerts.html)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

