Tim Berners-Lee  
Date: 2015-02-15, last change: $Date: 2015/03/28 20:46:47 $  
Status: personal view only. This is not a formal W3C director view, nor view
of the TAG or the Consortium as a whole. It is a contribution to the
discussion. It consists of a number of related observations, which could have
gone into separate notes, but in the end seemed to be all fairly connected.
Editing status: first draft.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

# Web Security - "HTTPS Everywhere" harmful

The web is (in 2015) a place where security is increasing essential, and
always under threat. It is also a space which needs to be consistent, logical,
and user-serving. There follow some thoughts following many recent discussions
of "HTTPS Everywhere" and points west.

## It's not the "S" in "https:"

A few years after HTTP appeared, around when W3C was founded in 1994, it was
clear that an unencrypted and unauthenticated connection was too much of a
liability for a lot of serious stuff, such as e-commerce, which everyone
wanted to do on the web. (In those days, mass Deep Packet Inspection was not
technically feasible, so the ubiquitous snooping which we have to day was not
the main driver.) There were, among the ideas, two secure versions of HTTP
proposed, one known as [S-HTTP](https://www.ietf.org/rfc/rfc2660.txt) and the
other, as HTTP-S. To cut a long story short, HTTP-S prevailed.

There was a technical decision as to whether to make HTTPS protocol an
extension of the existing HTTP protocol, used to look up URIs which started
with "http:", or to give it its own URI prefix.

When you look at that design choice, you have to remember that the URL is
being used to communicate between two people, for example, the person who
writes the link containing the href with the link, and the person who later
sees the link and clicks ion it. Lets look at some of the arguments.

To use the existing http: | Make a new https: URI prefix  
---|---  
This gives the link follower the task of ensuring that the communications
happen securely* | This gives the person making the link a way to ensure that
the communications of the link follower  
Allows a smooth upgrade of HTTP to be more secure HTTP | Creates a separate
space, a "secure web" in which only good things happen.  
Keeps the web one web | Gets information about security levels confused with
the identity of the resource.  
  
_* By "secure" I will normally mean in this article "with encryption and
authentication"._

There may have been important other reasons and arguments, so the historian is
invited to check the email archives, but looking back with 20 year hindsight
and experience, it seems that the overriding concern must have been that
someone making the link had the ability to insist that the link follower gets
a secure experience. You imagine a bank wanting to print
"https://bankofexample.com/foo" and be sure everyone who read it gets to the
right bank, without being spied on or diverted, and has a secure session with
them. The bank using the same prefix 'http:' would not give that assurance. It
turns out not that was not the most important assurance to give.

Now, an overriding concern is that the user who follows the link should be
protected from being spied on, phished, scammed, or impersonated, and it is
the browser's job to make that so, and, crucially, make the user the clearly
aware of the level of security, and why they are trusting whom.

What has changed? Well, Some people feel that in fact looking back the
decision to make the https: URI space was in fact even at that time a mistake.
Now also, you can argue that things have changed in that people are
individually more aware, and individually under attack. It is not now the link
maker's task to ensure the user is secure. It is the user's task to ensure
that their interactions are secure.

  * People now more understand that they want to have a secure communication, especially with a bank, but with most other places too. The browser must act on behalf of the bowser user, the person following the link, primarily.
  * People have been trained to look not for the 's' in the URL bar (which conveys the URL only) but for the padlock which used to demonstrate a secure connection to somebody, and nowadays mercifully, the browser user interface which gives them the name of the holder of a validated certificate provided by the server.
  * The 'http:' has in fact (2015) relatively recently been removed from the browser bar altogether for some browsers. While this infuriates those of us who are actually interested in it, it certainly puts another nail in the coffin of the idea that the 's' in the URI is important part of the architecture.
  * "The HTTPS is a safe space" has lead to the notion in bowser vendors that it should be ring-fenced. The Same Origin Policy in this spirit suggests that once a user enters the secure web by an https: link, then everything which affects the session at all must come also over authenticated TLS. This has led to a class of web apps being broken, in contrast with the usual rule of back compatibility with old content.

(The last point is related to the common design failure that trust is as
single-valued scalar thing. It has been more any more clear that we and our
systems should not just trust things or not trust them, or even to trust them
on a scale form 0 to 1. We trust different people for different things. We
trust one person for recommendations on food, and another for movies, and to
muddle these trusts could be disastrous. Similarly we allow different agents
and services and code modules do access different things for different
purposes. Our computer systems must reflect and implement that. A https:
secure oil/water boundary does not do that. A symptom if that you can never
find the perfect place to put that boundary.)

## Don't break the web

There is a currently (2014, 15) a massive move to get the web secure in the
sense of encrypted and authenticated. Of encryption and authentication, the
encryption part is the part which has garnered the most attention, both among
its promoters and those in governments [ who](http://www.theguardian.com/uk-
news/2015/jan/12/david-cameron-pledges-anti-terror-law-internet-paris-attacks-
nick-clegg) [ protest](http://arstechnica.com/tech-policy/2014/10/us-top-cop-
decries-encryption-demands-backdoors/) against it has giving too much power to
users, criminals included, compared with law enforcement. Projects such as
[LetsEncrypt](https://letsencrypt.org/) and the EFF's [HTTPS
everywhere](https://www.eff.org/Https-everywhere) for example promote a
wholesale move to the HTTPS protocol.

The concerns behind the need for security are valid. There is a lot of abuse
which it would prevent. The problem with HTTPS Everywhere drive is when the
"S" is put into the URI. The problem is of course that moving things from
http: space into https space, whether or not you keep the rest of the URI the
same, breaks any links to. Put simply, the HTTPS Everywhere campaign taken at
face value completely breaks the web. In a way it is arguably a greater threat
to the integrity for the web than anything else in its history. The underlying
speeds of connection of increased from 300bps to 300Gbps, IPv4 has being moved
to IpV6, but none of this breaks the web of links in so doing.

## TLS Everywhere

A proposal then is to do HTTPS everywhere in the sense of the protocol but
**not the URI prefix**. A browser gives the secure-looking user interface
message, such as displaying the server certificate holder name above the
document, only when the document has been fetched in an authenticated over an
encrypted channel. This can be done by upgrading the HTTP to include TLS in
real time, or in future cases by just trying encrypted version first. There
has been some discussion of this from including a
[RFC2817](https://www.ietf.org/rfc/rfc2817.txt) (2000) "HTTP Upgrade to TLS"
(Though that was motivated apparently by the need to save low-numbered ports,
an issue I omitted from the table above.).

The HTTP protocol can and by default is upgraded to use TLS without having to
use a different URI prefix. The https: prefix could even in fact be phased
out, and instead user education focussed on understanding the level of
assurance being given about the level of security, including authentication of
the other party, encryption of the communication, and the anonymity,
traceability, or strong authentication of the user to the other party.

* * *

This is the first of four related notes:

  1. ["HTTPS Everywhere" considered harmful](https://www.w3.org/DesignIssues/Security-NotTheS.html)
  2. [Model Real Trust](https://www.w3.org/DesignIssues/Security-ModelTrust.html)
  3. [The Same Origin Policy - Origin Granularity](https://www.w3.org/DesignIssues/Security-Origin.html)
  4. [Client-Side Certificates](https://www.w3.org/DesignIssues/Security-ClientCerts.html)

## References

  * Email discusssion on www-tag@w3.orgat many times including [ December](https://lists.w3.org/Archives/Public/www-tag/2014Dec/thread.html#msg128), [ January 2015](https://lists.w3.org/Archives/Public/www-tag/2015Jan/thread.html), etc.
  * Mike Specter &lt;specter@mit.edu&gt; private communication.
  * [HTTPS Everywhere](https://www.eff.org/Https-everywhere) is a Firefox, Chrome, and Opera extension that switched yor from http: addresses to equivalent htps: addresses where they are available, using a map in its configuration. EFF
  * [Lets'Encrypt](https://letsencrypt.org/) is a project to make a new Certificate Authority (CA) which will make it easy and free to get a server certificate automatically by proving you control a given domain.
  * [](https://www.w3.org/DesignIssues/)

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

