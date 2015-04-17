#Events
This section outlines the details of the various xAPI extensions used in statements. 

<a name="badge-class" />
## Badge Class Object

The Badge Class Object is the same as defined within the [OB Earning](../earning/) recipe, but with an additional 
required property 'xapi-criteria'. Like the 'criteria' property, this contains an IRI pointing to a resource 
outlining the criteria for the badge. 

Unlike the 'criteria' property, which points to a human-readbale HTML document,
the 'xapi-criteria' property points to a machine readable JSON document. This JSON Document contains an array
of xAPI Activity Definitions for all of the criteria required by the badge. These Activity Definitions MUST
include a name and description in at least one language and the [Activity Definition Extensions for
criteria outlined above](#define-criterion). 

<a name="criteria-list" />
## Badge Criteria List Object

Used within the Activity Definition when defining or updating a Badge Class. Contains an array of xAPI Activity
Objects. The 'definition' property SHOULD NOT be used; the 'objectType' property MUST be used. 

<a name="badge-evidence" />
## Badge Evidence Object

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

<a name="criteria-metadata"/>
## Criteria Templates and Metadata
Criteria Activity Definitions include two extensions that combined define the requirements of each
criterion:

* ```http://specification.openbadges.org/xapi/extensions/criteria-templates```
* ```http://specification.openbadges.org/xapi/extensions/criteria-metadata```

The templates extension contains a Criteria Templates object which defines one or more template xAPI
statements that can be compared to xAPI statements representing the learner's experience. The metadata
extension contains a Criteria Metadata object with defines exactly how these templates are compared
to activity statements. These objects are outlined below.

<a name="criteria-metadata-templates"/>
### Templates
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
<a name="criteria-metadata-metadata"/>
### Metadata
The Criteria Metadata object defines how these templates are intepreted and compared. The 
table below outlines its properties. 'With type' in the Required column indicates that the
property is required for the types of criteria it is relevant for. See the 
[types section below](#criteria-metadata-types). 

Property | Type | Description | Required 
--- | --- | --- | --- 
type | string | "match" or "capture" or "subset" or "group". The type of criteria [See below](#criteria-metadata-types). | Required
templateId | UUID | Id of the template to be compared with learner activity | With type captureIndex | number | The index of the "#" wildcard within the template statement used for this criterion. | With type
aggregate | string | "max", "min", "avg" or "sum". The aggregation to perform on captured values. [See below](#criteria-metadata-capture) | Optional
predicate | string | ">=" or "=" or "<=" | The assertion being made about the value. | With type 
value | number | A numeric value being compared against capture values, match counts, subset sizes, or aggregation results. | Optional
duration | ISO 8601 duration | A duration value being compared against match counts, subset sizes, or aggregation results. | Optional
grouping | string | "statement" or "registration". Indicates the statement property that all subcriteria must have in common. | With type
subCriteria | Array of Criteria Metadata objects | cannot itself contain subCriteria | With type

Note that any aggregation is performance at the point in time the badge is awarded; badges are not revoked 
in the event the aggregation no longer meets the requirements. 

<a name="criteria-metadata-types"/>
#### Types
Some of the properties above are only used in conjunction with certain types. The table below describes
each type and lists the properties that are valid with each. 

 Type | Description | Valid properties 
--- | --- | --- 
match | The statement about the learner's activity matches all the fields provided in the template. | templateId, value
capture | --- | templateId, captureIndex, aggregate, predicate, value
subset | --- | value, subCriteria
group | --- | grouping, subCriteria

<a name="criteria-metadata-process"/>
### Badge award process

<a name="criteria-metadata-match"/>
#### Match process
For 'match' type criteria, in order for data from statement to statisfy a criterion, that statement must
match one of the defined templates, but capture values (values marked with a "#") are ignored.

A statement matches a template when both the following
conditions are true:
1. All of the template's literal property values must be present in the statement and contain the same value.
2. All of the template's captured values must be present in the statement, but may contain anyvalue.

<a name="criteria-metadata-capture"/>
#### Capture process
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

<a name="criteria-metadata-examples"/>
### Examples
This section provides example 2 example template and metadata of each type. 

##### template 1
```
"e4f05a1a-fd15-4847-a565-2c55ee9bda59": {
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/experienced"
    }
}
```

##### template 2
```
"9966b865-99e2-45d0-8e70-6e77ccfff145": {
    "result": {
        "score": {
            "raw" : "#"
        }
    }
}
```

##### 'match' criterion
One statement with the 'experienced' verb is required to meet the criterion.
```
{
    "type": "match",
    "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59"
}
```

##### 'match' criterion with predicate
Three or more statements with the 'experienced' verb is required to meet the criterion.
```
{
    "type": "match",
    "templateId": "e4f05a1a-fd15-4847-a565-2c55ee9bda59",
    "predicate": ">=",
    "value": 3
}
```

##### 'capture' criterion (without aggregate)
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

##### 'group' criterion
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

##### 'subset' criterion
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