Release notes
=============

This document describes all the changes made to the *Institutions API*
document, starting from its first beta draft version.


0.4.0
-----

* Added the `<root-ounit-id>` element.
* Explained in some more detail *which* `<ounit-id>` values should be included
  in the response.


0.3.0
-----

* Moved `<contact>` element to a namespace of its own (see [Abstract Contact
  data type](https://github.com/erasmus-without-paper/ewp-specs-types-contact)).
* Renamed `<unit-id>` to `<ounit-id>` (since Organizational Units API now uses
  this new abbreviation, after being officially renamed from Departments API).


0.2.0
-----

* Moved `<embedded-mobility-factsheet>` out of the `master` branch into a
  separate feature branch, where it will be easier to discuss and
  accept/reject it.

* Moved `<role-id>` and `<iia-id>` relationships out of the `master` branch
  into a separate feature branch, for the same reasons as above.

(We are aiming for the `master` branch to not contain disputable features.)


0.1.0
-----

Initial release.
