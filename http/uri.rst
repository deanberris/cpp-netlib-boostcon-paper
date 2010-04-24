
HTTP URI
========

Firstly, cpp-netlib provides a specialization and ``typedef`` for an HTTP URI:

::

    namespace http {
        template <class T> class basic_uri;
        typedef basic_uri<default_> uri;
    }
    
``basic_uri`` provides a parser which breaks down a URI string passed to it's
constructor into different parts.

::

    using namespace boost::network::uri;
    http::uri uri_("http://www.boost.org/");
    assert(valid(uri_));
    assert(scheme(uri_) == "http");
    assert(host(uri_) == "www.boost.org")
    assert(port(uri_) == 80)
    assert(path(uri_) == "/");

The syntax of the HTTP URI are defined in RFC 1738 section 3.3 [#]_ and the
default URI provided with cpp-netlib conforms to this.  In such a way,
specializations that conform to any URI scheme can be provided.

.. [#] http://tools.ietf.org/html/rfc1738
