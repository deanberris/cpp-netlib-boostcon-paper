
The cpp-netlib provides full support for a configurable, embedded HTTP client 
nd server.

The design of the libraries require that the URI and protocol specific code
belong in their own namespace  and in the relevant sub-directories (i.e.
``http`` defined in ``protocol/http/`` and ``uri::http`` defined in
``uri/http/``).


.. include:: http/uri.rst
.. include:: http/client.rst
.. include:: http/server.rst
