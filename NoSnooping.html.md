Tim Berners-Lee  
Date: 2009-03-09, last change: $Date: 2009/03/11 15:48:30 $  
Status: personal view only. Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  No Snooping

Most of these notes are about architecture at the web layer. However, a
healthy web for society places requirements also on the Internet layer.

In 2008, this was threatened in the UK by the company
[Phorm](http://en.wikipedia.org/wiki/Phorm) proposing to use data from deep
packet inspection (DPI). The system would use special apparatus at the
Internet Service Provider (ISP) to monitor traffic, peek inside the IP
packet's payload, and determine every URL looked in a household's browsing on
the web. This profile would be used to provide taregetted advertizing. They
also planned to automatically "protect" users by redirecting any access to
blacklisted (phishing, etc) sites.

A discussion was held at the House of Lords by Baroness Miller on 2009-02-11.
These are some notes I made for the event, which I attended.

  1. The Internet in general has and deserves the same protection as paper mail and telephone. 
  2. If fact you could argue that it needs it more, as it carries more or our lives and is more revealing than our phone calls or our mail. 
  3. The access by an ISP of information within an internet packet, other than that information used for routing, is equivalent to wirtetapping a phone or opening sealed postal mail. 
  4. The URLs which people use reveal a huge amount about their lives, loves, hates, and fears. This is extremely sensitive material. People use the web in crisis, when wondering whether they have STDs, or cancer, when wondering whether they are homosexual and whether to talk about it, to discuss political views which may to some may be abhorrent, and so on. 
  5. We use the internet to inform ourselves as voters in a democracy. We use the internet to decide what is true and what is not. We use the internet for healthcare and social interaction and so on. These things will all have a completely different light cast on then if the users know that the click will be monitored and the data will be shared with third parties. 
  6. The URLs produced when using forms contain the information typed into those forms. Personal data, private data. 
  7. If people really want privacy, then many users and sites may switch to using SSL encryption: to doing theior actual web surfing thorugh an encrypted tunnel. This takes a lot of server CPU cycles, making server farms more expensive. It would slow the user's computer. It would effectively slow down the whole net. It also prevents the use of HTTP proxies, which currently help the efficiency of web access. 
  8. There are considerable risks if the information is abused. Imagine: 
    * To be able to buy a profile of a person you are interested in; 
    * To discriminate based on profiles of people when deciding whether suitable to employ them; 
    * To discriminate in giving life insurance, and so on, against those the have lookup up (say) cardiac symptoms on the web; 
    * Criminal attacks on government officials at home; 
    * Foreign attacks on the country made by targeting and analyzing key individuals; 
    * Predators choosing, stalking, and targeting victims;... 

to name a few.

  9. The information could be deliberately abused by an inside worker, or could be acquired by an attack on the system's machines. 
  10. The power of this information is so great that the commercial incentive for companies or individuals misuse it will be huge, so it is essential to have absolute clarity that it is illegal. 
  11. To put his in perspective, it is like the company having a video camera inside your house, except that it gives them actually much more information about you. 

The act of reading, like the act of writing, is a pure, fundamendal, human
act. It must be available without interference or spying.

###  Acknowledgements

Thanks to colleagues who reviewed these notes and provided useful feedback,
including Hal Abelson, Karen Myers, Thomas Rossler, Amy van der Hiel, and
Danny Weitzner

###  References

Phorm in Wikipedia http://en.wikipedia.org/wiki/Phorm

The author on BBC news disapproving of the spying on people's URLs:
http://news.bbc.co.uk/2/hi/technology/7299875.stm

* * *

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

