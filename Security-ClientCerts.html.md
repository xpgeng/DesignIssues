Tim Berners-Lee  
Date: 2015-02-15, last change: $Date: 2015/03/27 21:20:31 $  
Status: personal view only. This is not a formal W3C director view, nor view
of the TAG or the Consortium as a whole. It is a contribution to the
discussion. It consists of a number of related observations, which could have
gone into separate notes, but in the end seemed to be all fairly connected.
Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Web Security - Client side certs

## Authenticating both sides is important

When you are browsing the news and interacting with incoming information, you
may be happy not to be identified or even keen to be anonymous. There are
times, though, when you want to be well identified yourself, whether moving
money around at the bank or chatting with friends. Normally, we do this with
passwords.

Public key cryptography is a really wonderful gift from mathematics. We should
be making better use of it. Above I have sketched a few areas in which we can
improve the way we use it to authenticate the server in this client-server
system. We use it occasionally to authenticate the client. We should I think
do that much more often.

When I ask people about "client-side certs" (Public Key certificates used by
the browser to authenticate the user), a typical response if they are going
out of fashion, that they are difficult to use, and that browsers aren't
really supporting them properly. But then if you ask people about passwords,
then scream that they hate passwords. In fact, key pairs are just so much
better than passwords in many ways.

For passwords, you should think of a massively big one which is therefore
[impossible to remember](http://xkcd.com/936/) so you end up relying on your
computer to remember it, and it should of course be a different one for each
of the things you do business with, and the other party has store a copy of
this, and your code has to send it across the net risking it being ensnared
within your system or their system, and then they have to store it, which can
be pretty insecure, to judge from history. Whereas with public keys, you
generate a private key which is stupendously long and unguessable, use it for
many different other parties, and you never have to send it to them, and they
never see it or store it. That has got to be better. Yes, you can't scribble
your secret key on a Post-It™; note but that is actually an advantage.

So here is an agenda of things the browsers can do right now to make client
certs easier.

  1. Remember my certificate choices for different web sites, (and allow me to edit the list in the preferences if necessary if I get muddled). 
  2. Make the list of certificates much more friendly, when I have to chose one to use on a web site. Make sure the certificates are labelled in a way that makes them distinct -- not all just labelled with my name (duh!). Use more screen space. Allow me to hover or click to see more. 
  3. When I am in a session which has been authenticated using a cert (the same TLS session or using a cookie) allow me to cancel that identify (log out) and re-identify using a different user. 
  4. Provide an API for a web app to determine which cert has been used by the user to access a given resource. (At the mo 
  5. (detail) When I am creating a new private key using &lt;keygen> within a web app, fire an event which the web app can listen to so that it can continue with the workflow. 
  6. Allow me, if I sync my passwords between my machines, to chose which client side certs to sync between machines. Depending on the level of security, for many keys I will never want them to leave the one machine. 

## Just do it

Many of the things which I hear people wish for, mentioned in this article or
not, are often put out into the conversation but with a sigh and the caveat
that "It would be nice, but that's not how browsers work".

The bowsers are code, in many cases open source code. They are being changed
all the time. Unlike a decade ago, they are also being upgraded all the time,
because of the need for security-related bug fixes, and so a new idea can be
tried out in browsers really fast. When security is an issue, as it is for all
the above, browser manufacturers are in a position to make changes. So let us
not wring our hands over the fact changes we want to make are not how browsers
work today. Let's just change it.

* * *

v

## References

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

