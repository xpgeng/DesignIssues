[![](https://www.w3.org/Icons/WWW/arch1990.gif)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

#  Proof that HTTP 1.0 is compatible with 0.9

###  Assume:

version 1.0 has the version number at the end of the GET for the browser and
inside an HTML tag for the server. Then:

    
    
     Browser Server
     old     old      OK.
     new     old      new browser can handle 0.9 anyway.
     new     new      OK.
     old     new      old browser never sends anything
                      but GET string with no version number,
                      so then it must be 0.9.
    

