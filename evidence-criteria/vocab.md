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

<a name="badge-evidence" />
### Badge Evidence Object

The value of the Badge Evidence extension in the 'earn' statement. This object is a map of the criteria ids to arrays
of Statement Reference objects referencing the statements that contributed to earning the badge. 

For example:

```
{
    "http://example.com/criteria/1": [
        {
            "objectType": "StatementRef",
            "id": "dbeef3b3-ab1a-4420-8423-0db631b4f467"
        },
        {
            "objectType": "StatementRef",
            "id": "d160c5ed-4833-489e-ad78-fd0afe5d4f65"
        }
    ],
    "http://example.com/criteria/2": [
        {
            "objectType": "StatementRef",
            "id": "f7de98b1-aa65-40d1-9602-58fce7cf86a5"
        }
    ]
}
```

This object asserts that statements ```dbeef3b3-ab1a-4420-8423-0db631b4f467``` and 
```d160c5ed-4833-489e-ad78-fd0afe5d4f65``` led to the achievement of criterion 
```http://example.com/criteria/1```; statement ```f7de98b1-aa65-40d1-9602-58fce7cf86a5```
led to the achievement of criterion ```http://example.com/criteria/2```. 

<a name="templates-metadata" />
### Criteria Templates and Metadata
Criteria Activity Definitions include two extensions that combined define the requirements of each
criterion:

* ```http://specification.openbadges.org/xapi/extensions/criteria-templates```
* ```http://specification.openbadges.org/xapi/extensions/criteria-metadata```

The templates extension contains a Criteria Templates object which defines one or more template xAPI
statements that can be compared to xAPI statements representing the learner's experience. The metadata
extension contains a Criteria Metadata object with defines exactly how these templates are compared
to activity statements. These objects are outlined below.

#### Templates
The Criteria Templates object is a map of statement templates by template id. The template id is 
a UUID. A statement template is the same as an xAPI statement object, but limited to certain properties
and all properties are optional. 

Furthermore, the value of any boolean or numeric property in the statement can be replaced by a "#" string wildcard
known as a 'capture' the function of these captures is outlined below. 

The template may contain all and any of the following properties:

* Statement: verb, object, result, context, authority
* Verb: id
* Result: score, success, completion, response, duration (ms), extensions
* Score: scaled, raw, min, max
* Context: registration, instructor, team, contextActivities, revision, platform, language, statement, extensions
* Activity: id
* StatementReference: id

Actor is not included as the Actor will be matched to the learner earning the badge. 

For example, the template statement below has an id of ```e4f05a1a-fd15-4847-a565-2c55ee9bda59``` and
contains just one property, Verb Id. 

```
"e4f05a1a-fd15-4847-a565-2c55ee9bda59": {
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/experienced"
    }
}
```

#### Metadata
The Criteria Metadata object defines how these templates are intepreted and compared. The 
table below outlines its properties. 'With type' in the Required column indicates that the
property is required for the types of criteria it is relevant for. See the 
[types section below](#criteria-metadata-types). 

Property | Type | Description | Required 
--- | --- | --- | --- 
type | string | "match" or "capture" or "subset" or "group". 
The type of criteria [See below](#criteria-metadata-types). | Required
templateId | UUID | Id of the template to be compared with learner activity | With type
captureIndex | number | The index of the "#" wildcard within the template statement used for this criterion. | With type
aggregate | string | "max", "min", "avg" or "sum". The aggregation to perform on captured values. 
[See below](#criteria-metadata-capture) | Optional
predicate | string | ">=" or "=" or "<=" | The assertion being made about the value. | With type
value | number | A numeric value being compared against capture values, match counts, subset sizes, or aggregation results. | Optional
duration | ISO 8601 duration | A duration value being compared against match counts, subset sizes, or aggregation results. | Optional
grouping | string | "statement" or "registration". Indicates the statement property that all subcriteria must have in common. | With type
subCriteria | Array of Criteria Metadata objects | cannot itself contain subCriteria | With type

Note that any aggregation is performance at the point in time the badge is awarded; badges are not revoked 
in the event the aggregation no longer meets the requirements. 

<a name="criteria-metadata-types"/>
##### Types
Some of the properties above are only used in conjunction with certain types. The table below describes
each type and lists the properties that are valid with each. 

 Type | Description | Valid properties 
--- | --- | --- 
match | The statement about the learner's activity matches all the fields provided in the template. 
| templateId, value
capture | --- 
| templateId, captureIndex, aggregate, predicate, value
subset | --- | value, subCriteria
group | --- | grouping, subCriteria


<a name="criteria-metadata-match"/>
##### Match process
For 'match' type criteria, in order for data from statement to statisfy a criterion, that statement must
match one of the defined templates, but capture values (values marked with a "#") are ignored.

A statement matches a template when both the following
conditions are true:
1. All of the template's literal property values must be present in the statement and contain the same value.
2. All of the template's captured values must be present in the statement, but may contain anyvalue.

<a name="criteria-metadata-capture"/>
##### Capture process
For 'capture' type criteria, in order for data from statement to statisfy a criterion, in order for data 
from statement to statisfy a criterion, that statement must
match one of the defined templates with capture values (values marked with a "#")compared to the values 
in the statement. 

A statement matches a template when both the following conditions are true:

1. All of the template's literal property values must be present in the statement and contain the same value.
2. All of the template's captured values must be present in the statement and the value must meet the requirements
of the value, predicate and (if it is included) aggregate fields. 

Where a single template contains multiple captured values, both of these values must be matched in the same statement.
Multiple templates should be used if the intention is for the learner to be allowed to match these captured values
across multiple statements. 

##### Examples
This section provides example 2 example template and metadata of each type. 

###### template 1
```
"e4f05a1a-fd15-4847-a565-2c55ee9bda59": {
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/experienced"
    }
}
```

###### template 2
```
"9966b865-99e2-45d0-8e70-6e77ccfff145": {
    "result": {
        "score": {
            "raw" : "#"
        }
    }
}
```

###### 'match' criterion
One statement with the 'experienced' verb is required to meet the criterion.
```
{
    "type": "match",
    "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59"
}
```

###### 'match' criterion with predicate
Three or more statements with the 'experienced' verb is required to meet the criterion.
```
{
    "type": "match",
    "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59",
    "predicate": ">=",
    "value": 3
}
```

###### 'capture' criterion (without aggregate)
Score euqal to or more than 576 points. 

```
{
    "criteria": [
        {
            "templateId": "9966b865-99e2-45d0-8e70-6e77ccfff145",
            "type": "capture",
            "captureIndex": 1,
            "predicate": ">=",
            "value": 576
        } 
    ]
}
```

###### 'group' criterion
Two of the criteria from examples above must be met within one registration. 
```
"criteria": 
[
    {
        "type": "group",
        "grouping": "registration",
        "subCriteria": [
            {
                "type": "match",
                "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59"
            },
            {
                "templateId": "9966b865-99e2-45d0-8e70-6e77ccfff145",
                "type": "capture",
                "captureIndex": 1,
                "predicate": ">=",
                "value": 576
            } 
        ]
    } 
]
```

###### 'subset' criterion
One of two of the criteria from examples above must be met. 
```
"criteria": 
[
    {
        "type": "subset",
        "value": 1,
        "subCriteria": [
            {
                "type": "match",
                "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59"
            },
            {
                "templateId": "9966b865-99e2-45d0-8e70-6e77ccfff145",
                "type": "capture",
                "captureIndex": 1,
                "predicate": ">=",
                "value": 576
            } 
        ]
    } 
] 

## Open Badges Extension Details
This section outlines two extensions to Open Badges for includsion of xAPI criteria and evidence 
data within a Badge Class and Badge Assertion. 

### xAPI Criteria
'xapi-criteria' is an extension of the OB Badge Class. This property is equivelent to the 'xapi-criteria'
property included in the Badge Class extension [described above](#badge-class); the contents of both
properties (within the badge and within the statement) are the same. 

### xAPI Evidence
'xapi-evidence' is an extension of the OB Badge Assertion. Contains a [Badge Evidence object](#badge-evidence).

## Badge Class Localization
As Open Badges are defined as activities within statements, their names and descriptions are language maps, 
enabling them to be localized. Open Badges badge class objects also contain name and description properties
but these are not localized. To work around this this, systems hosting badge class definitions can return
the name and description using the most appropriate language available in the Activity Definition based on
the Accept-Language requested. 

## Retrieving Statements
'canonical' format SHOULD be used when retrieving statements for use in this recipe, except when transfering statements between LRS, when 'exact' MUST be used.

