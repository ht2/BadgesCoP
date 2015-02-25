# Vocabulary
When combining the xAPI with Open Badges (OBs), `actors` earn OBs, where a badge is an online representation of a skill. This document defines the identifiers and extensions used in the best practices define by this CoP.

## Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description
--- | --- | ---
verb.id | [Earned](http://specification.openbadges.org/xapi/verbs/earned.json) | States the `actor` earned the `object`.
context.contextActivities.category.N.id | [Open Badges Recipe](http://specification.openbadges.org/xapi/recipe/base/0) | States the `statement` uses the Open Badges recipe.
attachments.usageType | [Badge Attachment](http://specification.openbadges.org/xapi/attachment/badge.json) | Contains an xAPI Badge Assertion Object.
object.definition.type | [Badge Object](http://activitystrea.ms/schema/1.0/badge) | Contains an xAPI Badge Class Object.

## Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description
--- | --- | ---
result.extensions | [Badge Assertion](http://specification.openbadges.org/xapi/extensions/badgeassertion.json) | Defines the badge assertion.
object.definition.extensions | [Badge Class](http://specification.openbadges.org/xapi/extensions/badgeclass.json) | Defines the badge class.
