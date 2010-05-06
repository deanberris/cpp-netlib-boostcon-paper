
The Message Concept specifies what the valid operations on a message are as well
as what messages look like semantically. The following table summarize the
operations and syntactic as well as semantic properties of messages.

**Legend**

:M: The message type.
:m,n: An instance of **M**.
:S: A string type.
:s,k,v: An instance of **S**.

+------------------------+---------------------+-------------------------------------+
| Construct              | Result              | Description                         |
+========================+=====================+=====================================+
| M()                    | Instance of M       | Default constructible.              |
+------------------------+---------------------+-------------------------------------+
| M(m)                   | Instance of M       | Copy constructible.                 |
+------------------------+---------------------+-------------------------------------+
| m = n;                 | Reference to m      | Assignable.                         |
+------------------------+---------------------+-------------------------------------+
| swap(m, n);            | ``void``            | Swappable.                          |
+------------------------+---------------------+-------------------------------------+
| source(m);             | unspecified         | Retrieve the source of m.           |
+------------------------+---------------------+-------------------------------------+
| destination(m);        | unspecified         | Retrieve the destination of m.      |
+------------------------+---------------------+-------------------------------------+
| headers(m);            | ``Range<Pair<S,S>`` | Get the range of headers of m.      |
+------------------------+---------------------+-------------------------------------+
| body(m);               | unspecified         | Retrieve the body of m.             |
+------------------------+---------------------+-------------------------------------+
| m << source(s);        | ``M &``             | Set the source of m.                |
+------------------------+---------------------+-------------------------------------+
| m << destination(s);   | ``M &``             | Set the destination of m.           |
+------------------------+---------------------+-------------------------------------+
| m << header(k, v);     | ``M &``             | Add a header to m.                  |
+------------------------+---------------------+-------------------------------------+
| m << remove_header(k); | ``M &``             | Remove a header from m.             |
+------------------------+---------------------+-------------------------------------+
| m << body(s);          | ``M &``             | Set the body of m.                  |
+------------------------+---------------------+-------------------------------------+

Types that model the Message Concept are meant to encapsulate data that has a
source, a destination, one or more named headers, and a body/payload. Because
the accessors and the directives are not required to be part of the message type
that models the Message Concept, a message can be implemented as a POD type and
have all manipulations performed in the directive implementations, as well as
value transformations done in the accessors.

