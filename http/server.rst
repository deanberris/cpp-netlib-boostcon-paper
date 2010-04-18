
HTTP server
===========

As with the HTTP client, the HTTP server that is provided with cpp-netlib is
extensible through it's tag mechanism and embeddable.  The template class
declaration of ``basic_server`` is given below:

::

    namespace http {
        template <class Tag, class RequestHandler> basic_server;
    }

The second template argument is used to specify the request handler type.  It's
here that the logic for parsing the request and building the response belongs.
For example, an "echo" server example might be implemented something like this:

::

    using namespace boost::network;
    struct echo;
    typedef http::server<echo> echo_server;

    struct echo {
        void operator () (const echo_server::request &request,
                          echo_server::response &response) const {
            response = echo_server::response::stock_reply(
                echo_server::response::ok,
		body(request));
        }
    };



