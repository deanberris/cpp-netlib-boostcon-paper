
One of the core components in the library is the concept and the implementation
of a common message type. In most (not all) network protocols, the concept of a
message is central to the definition of the protocol. In HTTP, SMTP, XMPP, and
even other protocols like SNMP and ICMP, there is a common notion of a "packet"
or a message. In cpp-netlib we chose to implement the concept of a message that
has the following common parts:

  * **Source** - every message has a source identifier which varies from
    protocol to protocol.

  * **Destination** - every message has a destination identifier which varies
    from protocol to protocol.

  * **Headers** - each message is assumed to contain headers, which may be empty
    in cases where the protocol does not support it, but is nonetheless
    supported by cpp-netlib messages.

  * **Body** - the content area of a message which varies from protocol to
    protocol (also sometimes referred to as payload).

This division is purely logical -- in the underlying implementation, the message
type can choose to have different means of storing the data, dependinn on the
type used to tag the message. This section covers the `Message Concept`_ as well
as the `Basic Message`_ implementation.


Message Concept
```````````````

.. include:: messages/concept.rst

Basic Message
`````````````

.. include:: messages/basic.rst


