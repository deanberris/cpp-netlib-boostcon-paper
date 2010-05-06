As with SMTP, the current cpp-netlib version does not support or implement an
XMPP client. The intention for releasing version 1.0 though includes an XMPP
client that supports most if not all of the core XMPP specification. Because
XMPP is an interactive XML-based protocol there are a number of issues
surrounding the implementation details that need to be tackled. Some of these
are:

  * **Concurrency** - by design an XMPP client is supposed to be able to handle
    concurrency properly, wherein while sending messages the client may very
    well be doing some background processing of presence stanzas or other iq
    stanzas, and at any given time a failure in the processing or disconnection
    should be handled gracefully by the embeddable client.

  * **Extensibility** - by specification, XMPP is extensible through the XML
    namespace and other extension interfaces (through custom iq stanzas).

  * **Asynchronous** - an XMPP client may very well act as a service which can
    be interacted with in an asynchronous manner -- this means it may stay
    connected to a server and only react accordingly when a valid stanza is
    received from the server.

Also because XMPP is a state-full protocol an XMPP client and the service or
handler attached to it must be insulated from the state of the XMPP stream. The
XMPP client should then also expose both a synchronous (blocking) API as well as
an asynchronous (non-blocking) API.

These issues boil down to a parameterized XMPP client similar to the HTTP server
implementation. In C++ the XMPP client may very well look something like this
from the API/usage perspective:

::

    handler h;
    xmpp::client<handler> client_(h);
    client_.connect("localhost", 52222);
    client_.auth("username", "password");
    xmpp::message msg;
    msg << source("me@here.com")
        << destination("you@there.com")
        << header("id", "aeef11231a02d22ea0023845201923")
        << body("The quick brown fox jumps over the lazy dog.");
    client_.send_message(msg);

In the above mock implementation, the handler type ``handler`` should know what
to do when messages are received asynchronously, when roster and presence
messages are sent/received, among other things. The assumption here and the
implication of the interface provided as well is that an instance of the
``xmpp::client<...>`` is an active object running on its own lifetime thread,
which it itself handles.

