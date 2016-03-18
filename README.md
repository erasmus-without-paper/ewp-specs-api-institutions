Institutions API
================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Institutions API**. Once implemented by the host,
it allows external clients to retrieve general information on institutions
covered by this host. This information includes things like address, logo image
and key contact persons.


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.

 * Clients are advised to use POST when passing large number of parameters
   (servers MAY set a limit on their GET query string length).


Request parameters
------------------

Parameters MUST be provided either in a query string (for GET requests), or in
the `application/x-www-form-urlencoded` format (for POST requests).


### `hei_id` (repeatable, required)

A list of institution identifiers.

Clients may retrieve proper identifiers from the [Registry Service]
[registry-spec]. Servers MUST be able to accept all HEI IDs declared in their
[manifest files][discovery-api].

*Repeatable* means that the URL may contain multiple occurrences of this
parameter, e.g. `hei_id=uw.edu.pl&hei_id=uj.edu.pl`.


### `include_iro_sections`

Optional. Boolean (either `true` or `false`). Default value: `false`.

Indicates if the requester wants the server to include the IRO section in the
response. These sections can be quite big, so we will send them only when the
client wants them.


Permissions
-----------

All requests from the EWP Network MUST be allowed access to this API. Consult
the [Echo API][echo] specs for details on handling unprivileged requests.


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply. 

 * Invalid (uncovered) `hei_id` values MUST be ignored. Servers MUST return
   a valid (HTTP 200) XML response in such cases, but the response will simply
   not contain the information on the unknown `hei_id` values. (If all values
   are unknown, servers will respond with an empty envelope.)


Response
--------

Servers MUST respond with a valid XML document described by the [response.xsd]
(response.xsd) schema. See the schema annotations for further information.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
