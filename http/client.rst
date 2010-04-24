
HTTP client
===========

The cpp-netlib HTTP client is composed of three template classes:

::

    namespace http {
        template <class Tag> basic_request;
        template <class Tag> basic_response;
        template <class Tag> basic_client;
        typedef basic_request<default_> request;
        typedef basic_response<default_> response;
        typedef basic_client<default_> client;
    }


Each of these use again the tag-based static polymorphism that was described in
previous sections.  A default, human-readable typedef is provided for each one
of the ``basic_request``,  ``basic_response`` and  ``basic_client``.
``basic_request`` and ``basic_response`` each model the message concept. They
make use of directives to set and get HTTP headers, body etc. The code snippet
below shows how to set the HTTP header field "Connection" with the option
"close" using the DSEL described in the directives section:

::

    using namespace boost::network;
    http::request request("http://www.boost.org/");
    request << header("Connection", "close");

The ``basic_client`` implements all HTTP methods as member functions (HEAD,
GET, POST, PUT, DELETE).  Therefore, the code to make an HTTP request looks
trivially simple:

::

    using namespace boost::network;
    http::client client;
    http::request request("http://www.boost.org/");
    http::response response = client.get(request);

Accessing data from ``http::response`` is also done using directives.  To
get the response headers, we use the ``headers`` directive which returns,
in the default case, a map of strings to strings:

::

    using namespace boost::network;
    typedef headers_range<http_client::response>::type response_headers;
    boost::range_iterator<response_headers>::type iterator;

    response_headers headers_ = headers(response);
    for (iterator it = headers_.begin(); it != headers_.end(); ++it) {
        std::cout << it->first << ": " << it->second << std::endl;
    }    
    std::cout << std::endl;
