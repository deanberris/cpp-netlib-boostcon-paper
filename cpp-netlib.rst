======================================================================
Techniques in Flexible Header-Only C++ Network Library Implementations
======================================================================
:Author: Dean Michael Berris <mikhailberis@gmail.com>, 
         Glyn Matthews <glyn.matthews@gmail.com>
:Date: April 8, 2010
:Description: A look into the techniques used in the cpp-netlib implementation.

Abstract
--------

This paper aims to describe the various techniques used in the implementation of
a header-only networking library using the C++ programming language. This
document applies to the recently released version 0.5 of the cpp-netlib [#]_
library. The paper is published and submitted as additional materials for the
talk of the same title scheduled in BoostCon 2010 [#]_. This document also
serves as a guide for developers who want to extend the library, and serves as
an extension manual for those interested. The paper dives into the particulars
of a common message type and the various protocol client/server implementations
that are already implemented in the library.

.. [#] http://github.com/cpp-netlib/cpp-netlib
.. [#] http://www.boostcon.com/

Introduction
------------

The cpp-netlib project started on May 20, 2007 when the first check-in was
recorded on the public Sourceforge subversion repository. The objectives of the 
project was to develop a C++ library that:

  * Is of high quality, portable, and easy to use.

  * Enables users to easily extend the library.
  
  * Lowers the barrier to entry for cross-platform network-aware C++
    applications.

There were already a number of libraries dedicated to providing network
libraries for C++.  Several projects provide a lot of the functionality that we
demanded, among which include:

  * libcurl [#]_
  * C++ Sockets Library [#]_
  * Mozilla Necko [#]_
  * Qt [#]_

However there were none that provided high level application
level protocol clients or servers that relied only on header files and required
no building of external libraries. Specifically, there were none that were open
source, liberally licensed, and allowed you to use them directly in your
programs without linking to external static or shared libraries.

The stated scope of the library included the requirement to implement everything
as header-only C++ components. This meant that the code would rely on template
metaprogramming and as much static polymorphism [#]_ as possible to achieve the
same level of quality that the dynamic non-header-only libraries were providing.

.. [#] Static polymorphism is a kind of polymorphism which occurs at compile
       time that allows types or users of the type to determine their form or
       function while being compiled. There are many examples of static
       polymorphism that use template metaprogramming.

Another stated goal of the library is to keep the API of the components simple
and straight forward. In the initial survey of network libraries available for
C++ most of the approaches were very much like frameworks or had APIs that made
a lot of assumptions about how certain things should be done. This was observed
especially for the HTTP client libraries for C++ or even just C.

With the advent of Boost.Asio [#]_ it was felt possible to start a project 
leveraging it's capabilities to provide an application layer level library,
including direct support for the most common application layer protocols
such as HTTP, SMTP and XMPP.  Additionally, this library should be
extensible enough to implement other protocols as the project grows.

By 2010 the library has grown to include not only a header-only embeddable HTTP
client library, but also an embeddable HTTP server template implementation. This
allows new and existing applications to embed an HTTP server that exposed the
application's function as a service over HTTP.

.. [#] http://curl.haxx.se/libcurl/
.. [#] http://www.alhem.net/Sockets/
.. [#] https://developer.mozilla.org/en/Necko
.. [#] http://doc.trolltech.com/4.6/qtnetwork.html
.. [#] http://www.boost.org/doc/html/boost_asio.html

Overview
--------

The document has 5 sections which cover different parts of the library. These
sections are:

  * Techniques_ -- covers the different general techniques applied throughout
    the library, the atomic traits system, tag-based extension and dispatch,
    static/dynamic-polymorphic solutions, among others.

  * Messages_ -- covers the common message type used throughout the various
    client and server implementations, the message concept, and how to create
    specific messages for different protocols (even those that are not inherently
    message based).

  * Transformations_ -- covers how transformations on messages work, the
    directive system, and how to implement your own message transformation
    routines.

  * Protocols_ -- covers the different protocol implementations already released
    as part of the library, as well as those still to be supported.

  * Pitfalls_ -- catalogs and describes the common pitfalls encountered when
    doing header-only library development especially for higher level network
    libraries.

Each section can be structured differently and depends greatly on the subject
area.

Techniques
----------

.. include:: techniques.rst

Messages
--------

.. include:: messages.rst

Transformations
---------------

.. include:: transformations.rst

Protocols
---------

.. include:: protocols.rst

HTTP
````

.. include:: http.rst

SMTP
````

.. include:: smtp.rst

XMPP
````

.. include:: xmpp.rst


Pitfalls
--------

.. include:: pitfalls.rst

Recommendations
---------------

.. include:: recommendations.rst

Further Readings
----------------

.. include:: related-reading.rst

Contact Information
-------------------

::

    Dean Michael Berris
    Email: dean.berris@gmail.com | mikhailberis@gmail.com
    IM: skype:mikhailberis | yahoo:mikhailberis | gtalk:mikhailberis
    Web: http://deanberris.com/ | http://cplusplus-soup.com/
