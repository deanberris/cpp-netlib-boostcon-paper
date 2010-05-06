Overall cpp-netlib is meant to show that template metaprogramming applies very
well in the domain of network library programming that allows for extensible yet
simple interfaces. The mechanisms used borrow largely from existing libraries in
a way that allows cpp-netlib to stay as a header-only library.

Moving forward cpp-netlib is set to add richer tools and extensions to existing
and yet to be implemented clients and servers. The HTTP client and server
implementations are still being improved upon taking feedback from different
venues. Other efforts are being discussed and further clarified (like the XMPP
and SMTP clients).

In implementing other header-only libraries not necessarily in the networking
domain, more patterns and techniques should be explored and further formalized
and publicized. Those pointed out in this paper are the few ones that have been
distilled from cpp-netlib, there are yet other patterns and idioms found in
other libraries that may be useful in different contexts.

