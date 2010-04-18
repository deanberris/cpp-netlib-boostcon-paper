
Motivation
``````````

A major motivation for the developers of the cpp-netlib was that there appeared
to be no high quality, modern C++ networking library available.  Several
projects provide a lot of the functionality that we demanded, among which
include:

  * libcurl [#]_
  * C++ Sockets Library [#]_
  * Necko [#]_
  * Qt [#]_

But each of these has it's own disadvantages.

With the advent of Boost.Asio [#]_ it was felt possible to start a project 
leveraging it's capabilities to provide an application layer level library,
including direct support for the most common application layer protocols,
including HTTP, SMTP and XMPP, as well as providing enough extensibility to
implement other protocols.

.. [#] http://curl.haxx.se/libcurl/
.. [#] http://www.alhem.net/Sockets/
.. [#] https://developer.mozilla.org/en/Necko
.. [#] http://doc.trolltech.com/4.6/qtnetwork.html
.. [#] http://www.boost.org/doc/html/boost_asio.html
