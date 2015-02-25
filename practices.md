# Best Practices

## Contents
1. [Recording Earns](#recording-earns)
2. [Retrieving Earns](#retrieving-earns)

## Recording Earns
### Endpoint
[POST http://www.example.com/xapi/statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#stmtapipost)

### Request Body
```json
{
  "verb": {
    "id": "http://specification.openbadges.org/xapi/verbs/earned.json",
    "display": {
      "en-US": "earned"
    }
  },
  "result": {
    "extensions": {
      "http://specification.openbadges.org/xapi/extensions/badgeassertion.json": {
        "@id": "http://www.example.com/assertion/1"
      }
    }
  },
  "context": {
    "extensions": {
      "http://id.tincanapi.com/extension/jws-certificate-location": "http://www.example.com/cert.pem"
    },
    "contextActivities": {
      "category": [{
        "id": "http://specification.openbadges.org/xapi/recipe/base/0",
        "definition": {
          "type": "http://id.tincanapi.com/activitytype/recipe"
        },
        "objectType": "Activity"
      }]
    }
  },
  "attachments": [{
    "usageType": "http://specification.openbadges.org/xapi/attachment/badge.json",
    "display": {
      "en-US": "Name of the badge"
    },
    "contentType": "image/png",
    "length": 48826,
    "sha2": "42a33cb2af34603730577c2e5ddd78858feb34860c4e5bf0f473fa7456d3994a"
  }],
  "object": {
    "id": "www.example.com/badge/1",
    "definition": {
      "extensions": {
        "http://specification.openbadges.org/xapi/extensions/badgeclass.json": {
          "@id": "www.example.com/badgeclass/1",
          "image": "www.example.com/badgeimage/1",
          "criteria": "www.example.com/criteria/1",
          "issuer": "www.example.com/issuer/1"
        }
      },
      "name": {
        "en-US": "Name of the badge"
      },
      "description": {
        "en-US": "Description of the badge."
      },
      "type": "http://activitystrea.ms/schema/1.0/badge"
    },
    "objectType": "Activity"
  }
}

### Notes
`context.extensions.http://id.tincanapi.com/extension/jws-certificate-location` should only be used when the Badge has been signed using JWS.
```

## Retrieving Earns
### Endpoint
[GET http://www.example.com/xapi/statements](https://github.com/adlnet/xAPI-Spec/blob/master/xAPI.md#stmtapiget)

### URL Parameters
Name | Value
--- | ---
verb | http://standard.openbadges.org/xapi/verbs/earned.json
agent | *Your own agent (earner) filter*
