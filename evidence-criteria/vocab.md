TO BE COMPLETED. DO NOT IMPLEMENT!

# Vocabulary
This document defines the identifiers and extensions used for OB evidence and criteria. 
Examples can be found in the [readme](readme.md) of this directory.

This Vocabulary builds on the vocabulary defined for [OB Earning](../earning/). The 'earn'
statement should therefore include recipe ids for both this recipe and [OB Earning](../earning/)
version 0.0.2 (or whichever version you are using if you are using a later version; note that
later versions of the Earning recipe may or may not be compatible). 

## Define issuer
All OBs are issued by an issuer. This statement defines an issue who can later be assigend when
an OB is defined or updated.

This Statement MUST include an Activity Definition with a name in at least one language. 

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Defined Open Badge issuer](http://specification.openbadges.org/xapi/verbs/defined-issuer) |
States that the actor defined the specified badge issuer. | Required
object.definition.type | [OB Issuer](http://specification.openbadges.org/xapi/activitytype/issuer) | 
States that the `object` is an OB issuer. | Required
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required

### Extensions
None

### [Example](examples/define-issuer.json)

<a name="define-criterion"/>
## Define Criterion
Defines a criterion which can be assigned to an OB. Each criterion can belong to zero, one or more badges. 

This Statement MUST include an Activity Definition with a name and description in at least one language. 

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Defined Open Badge criterion](http://specification.openbadges.org/xapi/verbs/defined-badge-criterion) |
States that the actor defined the specified criterion. | Required
object.definition.type | [OB Criterion](http://specification.openbadges.org/xapi/activitytype/criterion) | 
States that the `object` is an OB criterion. | Required
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required

### Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
object.definition.extensions | [Criteria Metadata](http://specification.openbadges.org/xapi/extensions/criteria-metadata) | 
[See below](#templates-metadata) | Required
object.definition.extensions | [Criteria Templates](http://specification.openbadges.org/xapi/extensions/criteria-templates) | 
[See below](#templates-metadata) | Required

### [Example](examples/define-criterion.json)

## Define Badge
Defines an OB that can be awarded. This includes a list of criteria ids so that a system receiving this
statement can award a badge based on achievement of those criteria. 

This Statement MUST include an Activity Definition with a name and description in at least one language. 

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Created Open Badge](http://specification.openbadges.org/xapi/verbs/created-badge-class) |
States that the actor created a new Open Badge to be awarded. | Required
object.definition.type | [OB Object](http://activitystrea.ms/schema/1.0/badge) | 
States that the `object` is an OB. | Required
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required


### Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
object.definition.extensions | [Badge Class](http://specification.openbadges.org/xapi/extensions/badgeclass) | 
[See below](#badge-class) | Required
object.definition.extensions | [Criteria List](http://specification.openbadges.org/xapi/extensions/criteria) | 
[See below](#criteria-list) | Required

### [Example](examples/define-badge.json)

## Archive Badge
Asserts that from the specified timestamp, the Badge should no longer be awarded. The specified timestamp
MUST be the current time. Systems receiving this statement are requested to stop awarding the badge immediately,
even for activities that occured prior to this statement being issued. Systems should not revoke badges
on the basis of this statement. Systems issuing this statement should allow a reasonable tollerance for
this statement to take effect. 

The target of this statement should be an Open Badge Class that has previously been created. As the Activity 
Definition was included when the Badge Class was created, it does not need to be included in this statement.

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Archived Open Badge](http://specification.openbadges.org/xapi/verbs/archive-badge-class) |
States that the actor created a new Open Badge to be awarded. | Required
object.definition.type | [OB Object](http://activitystrea.ms/schema/1.0/badge) | 
States that the `object` is an OB. | Not Recommended
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required

### Extensions
The same Activity Definition Extensions as for creating a badge MAY be used, however including the
Activity Definition with this statement is not recommended. 

### [Example](examples/archive-badge.json)

## Update Badge
This statement is used to make changes to a Badge, for example changing the criteria required. 
This is used when designing a badge that has not yet been used.

Badge Creators MUST NOT Update a badge that has been published or even awarded;
consider archiving the badge and creating a new one in its place. 

The structure and identifiers used for this statement are the same as for creating a badge except
the verb id. The object of the statement MUST be a previously created Open Badge Class. 

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Updated Open Badge](http://specification.openbadges.org/xapi/verbs/update-badge-class) |
States that the actor created a new Open Badge to be awarded. | Required


### [Example](examples/update-badge.json)

## Met Criteria
Asserts that a statement matching the requirements of a criterion and the specified agent has been found. 
Badge awarding systems MUST evaluate and issue statements for all criteria relating to badges they 
award. They MAY additionally evaluate criteria attached to other badges or not attached to 
any badges at all. 

It is posible that a learner might meet badge criteria more than once, for example if a criterion of
a badge is to complete a course, the learner might complete the course multiple times. It is up
to the criteria tracking system whether or not to record each occasion criteria are met. 

The statement includes a result extension listing statements contributing to the meeting of the
criteria on this occasion. This list MAY include more statements than the minimum required to meet
the criterion and MAY include statements that contributed to meeting the criterion previously. The 
requirements of the criterion MUST be fully met by the statements included in the list. 

The Activity Definition is optional for this statement as the criterion has already been defined.

### Identifiers
*Use the IRIs hyperlinked to the text in the identifiers column, rather than the words themselves.*

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
verb.id | [Met criteria](http://specification.openbadges.org/xapi/verbs/met-criteria) |
States that the actor met the specified criterion. | Required
object.definition.type | [OB Criterion](http://specification.openbadges.org/xapi/activitytype/criterion) | 
States that the `object` is an OB criterion. | Optional
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required


### Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
object.definition.extensions | [Criteria Metadata](http://specification.openbadges.org/xapi/extensions/criteria-metadata) | 
[See below](#templates-metadata) | Optional
object.definition.extensions | [Criteria Templates](http://specification.openbadges.org/xapi/extensions/criteria-templates) | 
[See below](#templates-metadata) | Optional
results.extensions | [Criteria Evidence](http://specification.openbadges.org/xapi/extensions/criteria-evidence) | 
Array of [Statement Reference Objects](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#statement-references) | Required

### [Example](examples/met-criteria.json)

## Earned Badge
This statement is already covered by the [OB Earning](../earning/) recipe. The same steructure is used here, 
with the additional identifiers and extensions listed below. Both recipes MUST be included in as 
'category' Context Activties. 

Note that the Badge Class extension is defined within the [OB Earning](../earning/) recipe; the content
of that extension has been added to in this recipe. 

Systems supporting the [OB Earning](../earning/) recipe but not this recipe SHOULD ignore the
additional extensions and extension properties added by this recipe, but MAY use them where provided. 

Note that the Activity Definition **is** required in this statement despite being already provided by 
the 'created badge' statement. This is to facilitate interoperbility with systems supporting only the 
[OB Earning](../earning/) recipe, which does not include the 'created badge' statement.

xAPI Property | Identifier | Description | Required
--- | --- | --- | ---
context.contextActivities.category.N.id | [OB Recipe](http://specification.openbadges.org/xapi/recipe/evidence-criteria/0_0_1) | 
States the `statement` uses the OB evidence and criteria recipe. | Required

### Extensions
*Use the IRIs hyperlinked to the text in the extension column, rather than the words themselves.*

xAPI Property | Extension | Description | Required
--- | --- | --- | ---
object.definition.extensions | [Badge Class](http://specification.openbadges.org/xapi/extensions/badgeclass) | 
[See below](#badge-class) | Required
object.definition.extensions | [Criteria List](http://specification.openbadges.org/xapi/extensions/criteria) | 
[See below](#criteria-list) | Required
result.extensions | [Badge Evidence](http://specification.openbadges.org/xapi/extensions/evidence) | 
[See below](#badge-evidence) | Required

### [Example](examples/earned-badge.json))

## xAPI Extension Details

This section outlines the details of the various xAPI extensions used in the statements listed above. 

<a name="badge-class" />
### Badge Class Object

The Badge Class Object is the same as defined within the [OB Earning](../earning/) recipe, but with an additional 
required property 'xapi-criteria'. Like the 'criteria' property, this contains an IRI pointing to a resource 
outlining the criteria for the badge. 

Unlike the 'criteria' property, which points to a human-readbale HTML document,
the 'xapi-criteria' property points to a machine readable JSON document. This JSON Document contains an array
of xAPI Activity Definitions for all of the criteria required by the badge. These Activity Definitions MUST
include a name and description in at least one language and the [Activity Definition Extensions for
criteria outlined above](#define-criterion). 

<a name="criteria-list" />
### Badge Criteria List Object

Used within the Activity Definition when defining or updating a Badge Class. Contains an array of xAPI Activity
Objects. The 'definition' property SHOULD NOT be used; the 'objectType' property MUST be used. 

// (array of)used when defining badges - currently a list of activity IRIs, should be activity objects. 

<a name="badge-evidence" />
### Badge Evidence Object

<a name="templates-metadata" />
### Criteria Templates and Metadata

## Open Badges Extension Details

### xAPI Criteria

### xAPI Evidence

## Badge Class Localization

## Retrieving Statements
'canonical' format MUST be used when retrieving statements for use in this recipe, except when transfering statements betwen LRS, when 'exact' MUST be used.

