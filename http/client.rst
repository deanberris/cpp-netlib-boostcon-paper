
HTTP client
===========

The cpp-netlib HTTP client is composed of three template classes:

::

    namespace http {
        template <class Tag> basic_request;
        typedef basic_request<default_> request;
        template <class Tag> basic_response;
        typedef basic_response<default_> response;
        template <class Tag> basic_client;
        typedef basic_client<default_> client;
    }

``request`` and ``response`` each model the message concept.

TODO: message, specialized request & responses.
TODO: client, embeddable, light-weight and extensible (using tags)

