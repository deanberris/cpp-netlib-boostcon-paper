The default implementation of a simple type that models the Message Concept is
available in cpp-netlib. This default implementation is named ``basic_message``
which supports a ``Tag`` template parameter. The definition of ``basic_message`` 
looks like this:

::

    template <class Tag>
    struct basic_message;

The ``basic_message`` template requires that the following tag-dispatched
metafunctions are defined for the type ``Tag``:

::

    template <class Tag>
    struct string;

    template <class Tag>
    struct headers_container;


All the operations defined by the message concept are implemented by this basic
message type. Other message implementations can either use this common message
type or specialize it according to whether they want to use different containers
or whether it's going to be just a POD type.

