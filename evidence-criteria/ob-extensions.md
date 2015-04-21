# Open Badges Extension Details
This section outlines two extensions to Open Badges for inclusion of xAPI criteria and evidence 
data within a Badge Class and Badge Assertion. Note that these Open Badges extensions are only required
for badges defined within the Evidence and Criteria recipe and not earned badges described by the Earning recipe. 

<a name="xapi-criteria">
## xAPI Criteria
xAPI Criteria links to a JSON document containing a machine readable xAPI Badge Criteria object 
[as defined here](https://github.com/ht2/BadgesCoP/blob/master/evidence-criteria/xapi-extensions.md#badge-class).

Property     | Type        | Value Description
-------------|-------------|---------
**@context** | context IRI | http://specification.openbadges.org/extensions/xapiCriteria/context.json
**type**    | type IRI array |`['Extension', 'extensions:xapiCriteria']`
**url** | string,uri | Valid url beginning with http:// or https://

**Extendable Badge Objects:** BadgeClass

**Example implementation:**
```
{
    "extension:xapiCriteria": {
        "@context":"http://specification.openbadges.org/extensions/xapiCriteria/context.json",
        "@type": ["extension", "extension:xapiCriteria"],
        "url": "http://example.com/resources/xapi-badge-criteria.php?activity-id=http%3A%2F%2Flocalhost%3A8888%2FTinBadgesPHP%2Fresources%2Fbadge-definition.php%3Fbadge-id%3D2"
    }
    "issuer": "http://example.com/resources/issuer.php?activity-id=http%3A%2F%2Ftincanapi.com"
}
```

<a name="xapi-evidence">
## xAPI Evidence
xAPI Evidence points to a JSON document
containing a [Badge Evidence object](https://github.com/ht2/BadgesCoP/blob/master/evidence-criteria/xapi-extensions.md#badge-evidence).

Property     | Type        | Value Description
-------------|-------------|---------
**@context** | context IRI | http://specification.openbadges.org/extensions/xapiEvidence/context.json
**type**    | type IRI array |`['Extension', 'extensions:xapiEvidence']`
**url** | string,uri | Valid url beginning with http:// or https://

**Extendable Badge Objects:** BadgeAssertion

**Example implementation:**

```
{
    "extension:xapiEvidence": {
        "@context":"http://specification.openbadges.org/extensions/xapiEvidence/context.json",
        "@type": ["extension", "extension:xapiEvidence"],
        "url": "http://example.com/resources/xapi-evidence.php?statement=bc13098d-bdb6-40ae-9978-c5e72b92ba68"
    }
}
```