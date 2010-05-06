
The current version of the library doesn't support (E)SMTP yet but the
intention is to implement an (E)SMTP client much like how an HTTP client is
already implemented. Because of the message-based nature of the cpp-netlib
implementation, the (E)SMTP client is a natural fit for the library.

The envisioned API for an SMTP client is presented below in C++ code:

::

    smtp::client mua;
    mua.connect("localhost", 25);
    smtp::message msg;
    msg << source("me@localhost.com")
        << destination("someone@somewhere.com")
        << header("cc", "somone.else@somewhere-else.com")
        << header("mime-type", "text/plain")
        << body("The quick brown fox jumps over the lazy dog.");
    mua.send(msg);

This is intended for sending messages. At this time there is no plan or
intention to implement an embeddable (E)SMTP server, although it could well be
supported to allow for creating (E)SMTP-based services. If ever there is an
effort to implement an embeddable server, it will most probably follow the HTTP
server model.


