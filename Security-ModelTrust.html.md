Tim Berners-Lee  
Date: 2015-02-15, last change: $Date: 2015/03/27 21:20:36 $  
Status: personal view only. This is not a formal W3C director view, nor view
of the TAG or the Consortium as a whole. It is a contribution to the
discussion. It consists of a number of related observations, which could have
gone into separate notes, but in the end seemed to be all fairly connected. Of
the four notes on security, this is the most philosophical.

[Up to Design Issues](https://www.w3.org/DesignIssues/./)

* * *

#  Web Security - Model Real Trust

## Mapping machine trust to human trust

We must be able to be able to transfer our trust to our machines from our
actual real world situation. In some cases, we trust (say) a bank because we
trust a large ISP to give certificates out for big thing like banks. The PKI
Certificate Authority chain deserves the business gets when it arbitrates
identity on the global scale.

Sometimes, for a bank, a lawyer, a real estate agent, or an accountant we are
using, we sit down and have a face-face conversation at least at the start of
our long-term relationship, spending a lot of time to establish that trust
relationship, signing such as signing contracts. In this case, we have plenty
of time to exchange keys securely as peers with no hierarchical
infrastructure.

Sometimes we will trust people because we know them personally, and then we
must be able to explain this fact to the computer which acts as our agent.
Sometimes we know people because they are part of a family, and we exchange
keys within a family context and trust the family web server. Sometimes we
know someone or a web site because we are part of an organization, like a
university, or we are employees of a company.

My computer (of whatever sort) must allow me to add specific certificates
because I have these relationships. It is at the moment a breakage in the
system that browser manufacturers are fighting tooth and nail to stop people
doing anything useful with an unsigned or a self-signed certificate. This is,
with all due respect, playing into the hands of the corporate trust structure,
PKI, which of course benefits from being used to convey these trust paths.
This is wholly inappropriate for several reasons. One is that actually
trusting my family server though the PKI system is an expensive way to go. One
is that actually trusting my family server though the PKI system is a
misrepresentation of why I trust the family server. The PKI system has many
weak points, and in fact is a security liability for me to use it for
something where I should be using more intimate key exchange system.

Currently, mit.edu's certificates for working with staff are distributed by
MIT to employees and are self-signed. I have a close relationship with MIT, so
it is reasonable for me to accept this certificate. I can walk into MIT
offices and hold them accountable. They already have issues me with an RFID
card and a credit card and all kinds of stuff. I don't need to trust them
because of a large set of root servers ion all kinds of countries which have
from time been hacked.

Unfortunately current rhetoric from browser manufacturers suggests that the
user getting the browser to accept an self-signed cert is a horrible
violation, and should be stopped. No, it should be enabled, and a great user
interface provided for me, the user, to control and review the process.

* * *

This is the 3rd of 4 related notes:

  1. ["HTTPS Everywhere" considered harmful](https://www.w3.org/DesignIssues/Security-NotTheS.html)
  2. [The Same Origin Policy - Origin Granularity](https://www.w3.org/DesignIssues/Security-Origin.html)
  3. [Model Real Trust](https://www.w3.org/DesignIssues/Security-ModelTrust.html)
  4. [Client-Side Certificates](https://www.w3.org/DesignIssues/Security-ClientCerts.html)

## References

[Up to Design Issues](https://www.w3.org/DesignIssues/Overview.html)

[Tim BL](https://www.w3.org/People/Berners-Lee)

