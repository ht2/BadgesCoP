# Vocabulary
This document defines the identifiers and extensions used for OB Earning. Examples can be found in the [readme](readme.md) of this directory.

## Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Earned](http://specification.openbadges.org/xapi/verbs/earned.json) | States the `actor` earned the `object`. | Yes
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/base/0) | States the `statement` uses the OB recipe. | Yes
attachments.usageType | [OB Attachment](http://specification.openbadges.org/xapi/attachment/badge.json) | States that the `attachment` is an OB image. | Yes
object.definition.type | [OB Object](http://activitystrea.ms/schema/1.0/badge) | States that the `object` is an OB. | Yes

## Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
result.extensions | [OB Assertion](http://specification.openbadges.org/xapi/extensions/badgeassertion.json) | Contains an xAPI OB Assertion Object. | Yes
object.definition.extensions | [OB Class](http://specification.openbadges.org/xapi/extensions/badgeclass.json) | Contains an xAPI OB Class Object. | Yes

### [OB Assertion](http://specification.openbadges.org/xapi/extensions/badgeassertion.json) Properties

Property | Type | Description | Required
--- | --- | --- | ---
@id | IRI | Link to the OB assertion. | Yes


### [OB Class](http://specification.openbadges.org/xapi/extensions/badgeclass.json) Properties

Property | Type | Description | Required
--- | --- | --- | ---
@id | IRI | Link to the OB class. | Yes
image | IRI | Link to the OB image. | Yes
criteria | IRI | Link to the OB criteria | Yes
issuer | IRI | Link to the OB issuer | Yes
