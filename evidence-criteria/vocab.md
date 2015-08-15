# Vocabulary
This document defines the identifiers and extensions used for OB evidence and criteria. 
Examples can be found in the [readme](readme.md) of this directory.

<a name="recipie-id" />
## Recipe Id
All statements include the Recipe ID in the 'category' context activity list.

This Vocabulary builds on the vocabulary defined for [OB Earning](../earning/). The 'earn'
statement should therefore include recipe ids for both this recipe and [OB Earning](../earning/)
version 0.0.2 (or whichever version you are using if you are using a later version; note that
later versions of the Earning recipe may or may not be compatible). 

<a name="retrieving-statements" />
## Retrieving Statements
'canonical' format SHOULD be used when retrieving statements for use in this recipe, except when transfering statements between LRS, when 'exact' MUST be used.

<a name="badge-class-localization" />
## Badge Class Localization
As Open Badges are defined as activities within statements, their names and descriptions are language maps, 
enabling them to be localized. Open Badges badge class objects also contain name and description properties
but these are not localized. To work around this this, systems hosting badge class definitions can return
the name and description using the most appropriate language available in the Activity Definition based on
the Accept-Language requested. 

##Events
This recipe includes a number of events which are defined below:

* [Define issuer](events.md#define-issuer)
* [Define Criterion](events.md#define-criterion)
* [Define Badge](events.md#define-badge)
* [Archive Badge](events.md#archive-badge)
* [Update Badge](events.md#update-badge)
* [Met Criteria](events.md#met-criteria)
* [Earned Badge](events.md#earned-badge)

## xAPI Extension Details

This section outlines the details of the various xAPI extensions used in the statements listed above. 

* [Badge Class Object](xapi-extensions.md#badge-class)
* [Badge Criteria List Object](xapi-extensions.md#criteria-list)
* [Badge Evidence Object](xapi-extensions.md#badge-evidence)
* [Criteria Templates and Metadata](xapi-extensions.md#criteria-metadata)
  * [Templates](xapi-extensions.md#criteria-metadata-templates)
  * [Metadata](xapi-extensions.md#criteria-metadata-metadata)
  * [Badge award process](xapi-extensions.md#criteria-metadata-process)
  * [Examples](xapi-extensions.md#criteria-metadata-examples)

## Open Badges Extension Details
This section outlines two extensions to Open Badges for inclusion of xAPI criteria and evidence 
data within a Badge Class and Badge Assertion. 

* [xAPI Criteria](ob-extensions.md#xapi-criteria)
* [xAPI Evidence](ob-extensions.md#xapi-evidence)
