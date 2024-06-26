---
layout: page
title: Project Administration
nav_order: 5
has_children: false
permalink: /projects/home/
---

# Project Administration

In this section, we'll show you what kind of admin opperations are available when it comes to your **Fusion hubs** and **projects**.\
Previously we only used the **query** operation, which is for **read-only** access. This time we want to modify things and that requires a **mutation**, which is used when you want to **create**, **modify** or **delete** something. 

## Add users to hub

First let's add someone to our **hub**

```js
mutation AddUsersToHub($input: AddUsersToHubInput!) {
  addUsersToHub(input: $input) {
    hub {
      name
      users {
        results {
          firstName
          userName
          email
        }
      }
      projects {
        results {
          name
          id
        }
      }
    }
  }
}
```
```js
{
  "input":{
    "hubId": "YOUR HUB ID HERE!",
    "userEmailAddresses":[
      "YOUR USER'S EMAIL ADDRESS HERE!"
    ]
  }
}
```

## Create new project

Now create a new **project** in the same **hub**

```js
mutation CreateProject($hubId: ID!, $name: String!, $type: ProjectTypesEnum!) {
  createProject(input: {hubId: $hubId, name: $name, type: $type}) {
    project {
      id
      name
    }
  }
}
```
```js
{
  "hubId": "YOUR HUB ID HERE!",
  "name": "Test Project",
  "type" : "OPEN"
}
```

## Add users to project

Then add a user to this newly created **project** as well.

```js
mutation AddUsersToProject($input: AddUsersToProjectInput!) {
  addUsersToProject(input: $input) {
    project {
      name
      users {
        results {
          firstName
          lastName
          email
        }
      }
    }
  }
}
```
```js
{ 
  "input": {
    "projectId": "YOUR PROJECT ID HERE!",
    "userEmailAddresses": [
      "YOUR USER'S EMAIL ADDRESS HERE!"
    ]
  }
}
```


[Next Step - Custom Properties](../../properties/home/){: .btn}