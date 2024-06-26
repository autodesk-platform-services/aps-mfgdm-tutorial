---
layout: page
title: Prerequisites and GraphQL
nav_order: 2
has_children: false
permalink: /prerequisites/home/
---

# Prerequisites

Before jumping into action, you need to fulfill a few (but essential) prerequisites to follow these tutorials. **The steps need to be fulfilled in sequence for you to be able to follow this tutorial (only move to the next step after completing the previous one)**:

1. Firstly, you will need a **Fusion Team** account. The **MFG Data Model API** only works for models in a **Team Hub**, so make sure you have that and not just a **Personal Hub**
![Team Hub](/mfgdm-api-tutorial/assets/images/teamhub.png)

2. If you don't have any good **Fusion** designs to test things with, you can open and save the [sample models](https://www.autodesk.com/support/technical/article/caas/sfdcarticles/sfdcarticles/How-to-access-samples-files-for-Fusion-360-tutorials.html) in your project using **File** -> **Save As** inside **Fusion**.

![Fusion sample models](/mfgdm-api-tutorial/assets/images/samples.jpeg)

Now let's continue with a quick introduction into **GraphQL**.

# GraphQL

The way the **MFG Data Model** is structured makes it a perfect match for **GraphQL**.

For those unfamiliar with **GraphQL**, it is a query language for APIs.
It provides a complete and understandable description of the data in your API, and gives you the power to ask for exactly what you need and get back exactly that and nothing more.

**GraphQL** is much easier to use than **REST**, but it requires a better understanding of data structures​.

With a single endpoint, data fetching is easier because you don't need to make requests to multiple endpoints to get a set of data.

The request specifies precisely the data that’s going to be returned.

Let's see how you could retrieve the properties of a component and see what other components it's using. 

With the **MFG Data Model GraphQL** endpoint, such a query would look like this:
```js
query {
  componentVersion(componentVersionId: "Y29tcH5jby5uckdoR0ZIb1FXU3NQdFlhU0V2YThnfkd4YWpYb3NuUHdCenU5Y0huVmd4bUNfYWdhfm5jM2lianhOaHJLRU9XYjZBUVdhSGE") {
    id
    name
    partNumber
    partDescription
    occurrences {
      results {
        componentVersion {
          partNumber
        }
      }
    }
  }
}
```
And the response for this query will look like this:
```js
{
  "data": {
    "componentVersion": {
      "id": "Y29tcH5jby5uckdoR0ZIb1FXU3NQdFlhU0V2YThnfkd4YWpYb3NuUHdCenU5Y0huVmd4bUNfYWdhfm5jM2lianhOaHJLRU9XYjZBUVdhSGE",
      "name": "Steering Wheel Assembly -- FoFD test",
      "partNumber": "Steering Wheel Assembly - Original",
      "partDescription": "Steering Wheel",
      "occurrences": {
        "results": [
          {
            "componentVersion": {
              "partNumber": "bolt-1"
            }
          },
          {
            "componentVersion": {
              "partNumber": "bolt-2"
            }
          },
          {
            "componentVersion": {
              "partNumber": "Base-modified"
            }
          },
          {
            "componentVersion": {
              "partNumber": "Steering wheel form v1"
            }
          },
          {
            "componentVersion": {
              "partNumber": "Center-bracket-modified"
            }
          }
        ]
      }
    }
  }
}
```

Note that in this case we specified that we wanted to obtain a **component version** from a **Fusion** design with **component version id** `Y29..SGE`.
From this component, we specified we wanted to get the list of occurrences of other components, and what exact properties of those we want: **partNumber**.

With a **REST** API we would need additional requests, and wouldn't be possible to specify with this precision the data in the response.

To summarize, with **GraphQL** we have the benefits below:

- Single **REST** API endpoint – You only need to send your query to this endpoint when coding it in your applications
- No fixed Structure for the exchange of data – as compared to the **Model Derivative REST** API, where you will get a large JSON dataset, that you need to understand and be able to find the data you are looking for
- No over-fetching – as compared to the Model Derivative REST API, where you may need to call various APIs several times to get the data you are looking for.
- Efficiently using resources – Because the **GraphQL** implementation is on the Autodesk server side, it handles the requests to get the data you are asking for. This minimizes the traffic and allows us to optimize without disruption to the **GraphQL** aspects.

Before moving to the next step, let's run our very first query.

For that, you just need to go to the **Explorer** app at [https://mfgdatamodel-explorer.autodesk.io/](https://mfgdatamodel-explorer.autodesk.io/), log in, and run the query from the very first panel called **GetHubs**, just like in the image below:

![First Query](/mfgdm-api-tutorial/assets/images/firstquery.png)

> _We'll get back to GraphQL syntax throughout the queries in the next section. As it's not like the usual **REST** requests, we'll cover the differences and possibilities in parallel, while also learning the supported **MFG Data Model API** queries._

[Next Step - Explorer and First Queries](../../explorer/home/){: .btn}
