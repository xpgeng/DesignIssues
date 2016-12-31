[![](https://www.w3.org/Icons/WWW/arch1990.gif)](https://www.w3.org/DesignIssues/OldDocs.html)

* * *

#  Document caching

Three operations in the retrieval of a document may take significant time:

  * [Format conversion](https://www.w3.org/DesignIssues/Formats.html#4) by the server, including [version regeneration](https://www.w3.org/DesignIssues/Versioning.html#3)
  * Data transmission across the network 
  * Format conversion by the browser 

At each stage, the server (in the first case) or browser (in the other cases)
may decide to keep a temporary copy of the result. This copy should ideally be
common to many browsers.

Automatic caching relieves the user of having to explicitly save things which
may be referred to again. It also relieves the system of keeping multiple
copies (one for each user who has read the document). It allows local disk
space to used optimally. Cache management takes into account such factors as

  * expiry date
  * file size 
  * time taken to get the file 
  * frequency of access 
  * time since access 

##  Expiry date

As a guide to help a cache program optimise the data it caches, it is useful
if a document is transmitted with an estimate by the server of the lengt of
time the data may be kept for. This allows fast changing documents to be
flushed from the system, preventing readers from being mislead. (I would not
propose any notification of document changes to be distributed to cache
managers automatically). For example, an RFC may be cached for years, while
the state of the alarm system may be marked as valid for only one minute.

Window-oriented browsers effectively cache documents when they keep several at
a time in memory, in different windows. In this case, for very volatile data,
it may be useful to have the browser automatically refresh the window when its
data expires.

( [design issues](https://www.w3.org/DesignIssues/Overview.html) )_________________________________

[Tim BL](../../../WWW/disclaimer.html)

