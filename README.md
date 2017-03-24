Institutions API
================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Institutions API**. Once implemented by the host,
it allows external clients to retrieve general information on institutions
**either covered, or otherwise known**, by this host. This information
includes things like address, logo image and key contact persons.


<a name="known-heis"></a>

"Covered" vs "known"
--------------------

Initially, this API was supposed to work *only* with `hei_id`s **covered** by
the server's EWP Host. In other words, implementers were required to return
information only on "their own" HEIs. Later, however,
[it turned out](https://github.com/erasmus-without-paper/ewp-specs-api-iias/issues/6) that in
some cases, it would also be very useful if the server could provide some
(very basic) information on **other known HEIs** too.

Currently, server implementers MUST be able to provide some basic information
on all such institutions which they **refer to** (by their SCHAC IDs) in other
EWP APIs. It doesn't have to be much information though - most often, just the
name will be enough!


Request method
--------------

 * Requests MUST be made with either HTTP GET or HTTP POST method. Servers MUST
   support both these methods. Servers SHOULD reject all other request methods.

 * Clients are advised to use POST when passing large number of parameters
   (servers MAY set a limit on their GET query string length).


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.


### `hei_id` (repeatable, required)

A list of institution identifiers (no more than `<max-hei-ids>` items) - IDs of
HEIs the client wants to retrieve information on.

This parameter is *repeatable*, so the request MAY contain multiple occurrences
of it. The server is REQUIRED to process all of them.

Server implementers provide their own chosen value of `<max-hei-ids>` via their
manifest entry (see [manifest-entry.xsd](manifest-entry.xsd)). Clients SHOULD
parse this value (or assume its equal to `1`).

Clients may retrieve proper HEI identifiers from other EWP APIs (most often,
the [Registry Service][registry-spec]). Servers MUST be able to accept all HEI
IDs declared in their [manifest files][discovery-api], **and** all HEI IDs
which they refer to in other EWP APIs.


Permissions
-----------

 * All requests from the EWP Network MUST be allowed to access this API.

 * Additionally, implementers MAY allow this API to be accessed by
   **anonymous** external clients too (without the need of using any client
   certificate).


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Invalid (unknown) `hei_id` values MUST be **ignored**. Servers MUST return
   a valid (HTTP 200) XML response in such cases, but the response will simply
   not contain the information on the unknown `hei_id` values. If all values
   are unknown, servers MUST respond with an empty `<response>` element.
   This requirement is true even when `<max-hei-ids>` is equal to `1`.

 * If the length of `hei_id` list is greater than `<max-hei-ids>`, servers
   MUST respond with HTTP 400.


Response
--------

Servers MUST respond with a valid XML document described by the
[response.xsd](response.xsd) schema. See the schema annotations for further information.


Related data model entities
---------------------------

 * Inst/Org Unit
 * Coordinator
 * HEI Contact Info
 * Person


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
[registry-spec]: https://github.com/erasmus-without-paper/ewp-specs-api-registry
[discovery-api]: https://github.com/erasmus-without-paper/ewp-specs-api-discovery
[echo]: https://github.com/erasmus-without-paper/ewp-specs-api-echo
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
