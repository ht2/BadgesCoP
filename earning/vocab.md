# Vocabulary
This document defines the identifiers and extensions used in the **earning** OBs.

## Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Earned](http://specification.openbadges.org/xapi/verbs/earned.json) | States the `actor` earned the `object`. | Yes
context.contextActivities.category.N.id | [Open Badges Recipe](http://specification.openbadges.org/xapi/recipe/base/0) | States the `statement` uses the Open Badges recipe. | Yes
attachments.usageType | [Badge Attachment](http://specification.openbadges.org/xapi/attachment/badge.json) | Contains an xAPI Badge Assertion Object. | Yes
object.definition.type | [Badge Object](http://activitystrea.ms/schema/1.0/badge) | Contains an xAPI Badge Class Object. | Yes

## Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
result.extensions | [Badge Assertion](http://specification.openbadges.org/xapi/extensions/badgeassertion.json) | Defines the badge assertion. | Yes
object.definition.extensions | [Badge Class](http://specification.openbadges.org/xapi/extensions/badgeclass.json) | Defines the badge class. | Yes
