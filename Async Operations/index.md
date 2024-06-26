---
layout: page
title: Async Operations
nav_order: 4
has_children: false
permalink: /async/home/
---

# Async Operations

Certain properties will only be generated on request: thumbnail, export formats and physical properties. Once they were generated, you can access them again without any delay.
You can easily spot such fields in the API because they will have a property called `status`, which can have a value of `IN_PROGRESS`, `PENDING`, `FAILED`, `TIMEOUT` or `SUCCESS`

## Thumbnail

When using the **Model Derivative API** to get back a thumbail for a model, that can only be done at file level. In the case of **MFG DM API** we can do that for subcomponents as well. \
When running the below query for the first time you'll get a `status` with value `IN_PROGRESS`. If you run it a second time it should then say `SUCCESS` and this time the `signedUrl` property should provide a URL that you can simply paste in the browser to see the generated thumbnail. 

```js
query GetComponentVersion($componentVersionId: ID!) {
  componentVersion(componentVersionId: $componentVersionId) {
    id
    name
    partNumber
    partDescription
    designItemVersion {
      id
      name
      extensionType
    }
    thumbnail {
      status
      signedUrl
    }
    component {
      id
      name
    }
  }
}
```
```js
{
  "componentVersionId": "YOUR COMPONENT VERSION ID HERE!"
}
```

## Export Formats

Currently there are 3 export file formats supported by the API: STEP, OBJ and STL and you can access them through the `derivatives` field.  

```js
query GetDerivatives($componentVersionId: ID!, $derivativeInput: DerivativeInput!) {
  componentVersion(componentVersionId: $componentVersionId) {
    id
    name
    derivatives(derivativeInput: $derivativeInput) {
      expires
      id
      outputFormat
      signedUrl
      status
    }
  }
}
```
```js
{
  "componentVersionId": "YOUR COMPONENT VERSION ID HERE!",
  "derivativeInput": {
    "generate": true,
    "outputFormat": ["STEP"]
  }
}
```

## Physical Properties

Physical properties include area, volume, density, mass and bounding box. They are available under the `physicalProperties` field. 

```js
query GetPhysicalProperties($componentVersionId: ID!) {
  componentVersion(componentVersionId: $componentVersionId) {
    id
    name
    partNumber
    isMilestone
    materialName
    lastModifiedOn
    physicalProperties {
      status
      mass {
        displayValue
        value
        definition {
          name
          specification
          units {
            id
            name
          }
        }
      }
      volume {
        displayValue
        value
        definition {
          name
          specification
          units {
            id
            name
          }
        }
      }
      area {
        displayValue
        value
        definition {
          name
          units {
            name
          }
        }
      }
      density {
        displayValue
        value
        definition {
          name
          units {
            name
          }
        }
      }
      boundingBox {
        length {
          displayValue
          value
        }
        width {
          displayValue
          value
        }
        height {
          displayValue
          value
        }
      }
    }
  }
}
```
```js
{
  "componentVersionId": "YOUR COMPONENT VERSION ID HERE!"
}
```

[Next Step - Project Administration](../../projects/home/){: .btn}
