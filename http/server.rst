
HTTP server
===========

As with the HTTP client, the HTTP server that is provided with cpp-netlib is
extensible through the tag mechanism and is embeddable.  The template class
declaration of ``basic_server`` is given below:

::

    namespace http {
        template <class Tag, class RequestHandler> basic_server;
    }

The second template argument is used to specify the request handler type. The
request handler type is a functor type which should overload the function call
operator (``RequestHandler::operator()`` should be overloaded) that takes two
parameters: the first one being a reference to a ``const basic_request<Tag>``
and the second being a reference to a ``basic_response<Tag>`` instance.

All the logic for parsing the HTTP request and building the ``const
basic_request<Tag>`` object resides internally in the ``basic_server`` template.
Processing the request is delegated to the ``RequestHandler`` type, and the
assumption of which would be that the response is formed inside the
``RequestHandler`` function call operator overload.

The ``basic_server`` template however is only an underlying implementation while
the user-visible implementation is the ``http::server`` template. This simply
specializes the ``basic_server`` template to use the ``default_`` tag and
forwards the ``RequestHandler`` parameter:

::

    namespace http {
        template <class RequestHandler> server
        : public basic_server<default_, RequestHandler>
        {};
    }

To use the forwarding server type you just supply the request handler
implementation as the parameter. For example, an "echo" server example might 
look something like this:

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


Here, all we're doing is returning the original request body with an HTTP OK
response (200).
