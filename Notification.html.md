[![](https://www.w3.org/Icons/WWW/arch1990)](https://www.w3.org/DesignIssues/OldDocs.html)TimBL

* * *

#  Notification of new material

Does one need to bring it to a reader's attention when new unread material is
added?

  * Asynchronously (e.g. by mail) when the update is made? 
  * Synchronously when he browses or starts the application? 
  * Under the control of the modifying author? (i.e. can I say whether my change is a notifiable change? - Yes) 

How do you express interest - in a domain, in a node, in things near a node,
in anything you have read already, etc? A [separate web](https://www.w3.org/DesignIssues/Multiuser.html#3)
which is stored locally, and logically overlay the public web?

There are two ways to make the connection between the modified material, and
an interested person. One is, at the time of modification, to trace the
interested parties. The other is, at some later time, for a daemon program (or
a browser) to make a search for new things of interest to a given reader.

This is an essential feature. I suspect that a mixture of the two techniques
might be necessary. Efficient dating of nodes, and date-based searches
provided by the server, could make it easier for the browser to find
interesting things which are new. It should also be possible to create a
mailing list of people interested in a given topic, and use it to mail
announcements of change.

This requirement is addressed by the
["Interested"](https://www.w3.org/MarkUp/Relationships.html#z12) relationship of HTML, along
with the [POST](https://www.w3.org/Protocols/HTTP/Methods/Post.html) method of
[HTTP](https://www.w3.org/Protocols/HTTP/HTTP2.html) for a generic notification semantics.

