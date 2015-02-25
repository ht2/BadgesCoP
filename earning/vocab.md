# Vocabulary
This document defines the identifiers and extensions used for OB Earning.

## Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Earned](http://specification.openbadges.org/xapi/verbs/earned.json) | States the `actor` earned the `object`. | Yes
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/base/0) | States the `statement` uses the OBs recipe. | Yes
attachments.usageType | [OB Attachment](http://specification.openbadges.org/xapi/attachment/badge.json) | Contains an xAPI OB Assertion Object. | Yes
object.definition.type | [OB Object](http://activitystrea.ms/schema/1.0/badge) | Contains an xAPI OB Class Object. | Yes

## Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
result.extensions | [OB Assertion](http://specification.openbadges.org/xapi/extensions/badgeassertion.json) | Defines the OB assertion. | Yes
object.definition.extensions | [OB Class](http://specification.openbadges.org/xapi/extensions/badgeclass.json) | Defines the OB class. | Yes
