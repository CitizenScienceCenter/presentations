<!-- $theme: gaia -->

 ### Citizen Science Center
 ### Zurich
 
 ##### Dr. Christopher Gwilliams
 ##### Technical Architect
 
 christopher.gwilliams@uzh.ch
 
---
 
 ## What?
 
 A collaboration between UZH and ETH to promote, support and grow citizen science in Zurich, Switzerland and beyond.
 
---
 
 ## How?
 
 Through a combined centre and academy for participatory research, these are designed to be a central hub for those that want to develop their own citizen science project or require assistance with a current project.
 
 
---
 
 ## Yeah, but how?
 
 * Community Management
 * Technical Resources
 * Network Connections
 * Shared Knowledge

---

## Technical Resources

Today, we focus on the framework we are developing to allow researchers to design, create, deploy and analyse citizen science projects on a number of different platforms.

This can then be accessed by citizen scientists to discover, participate and share their data

---

## Functional Requirements

* Create projects that can be used on both mobile and desktop platforms
* Support data collection in (almost) any format. I.e. allow unstructured data
* In-depth technical knowledge must not be a requirement for users
* Collected data should have the ability to be fully open and, in some cases, required
* GDPR compliance

---

## System Architecture

* Database - PostgreSQL
* Backend - OpenAPI/RAML and Python/Go
* Mobile - Flutter with OpenAPI
* Web - VueJS (TypeScript and JavaScript)

 ---

Deployment: Hosted on **ScienceCloud**, deployed through **Docker** and **Travis**

---

## Schema

[schema](img/db_er.png)


---

## Database

Two Scenarios:
1. A researcher has created some projects and wants to make it public and collect data
2. A Citizen Scientist wants to take part in a project (or projects)

---

## Researcher Scenario

A **researcher** creates (or is part of) an **organisation** that contains **projects**. **Projects** are made  up of **tasks** that can contain text and/or **media**.


---

## Citizen Scientist Scenario

A **user** takes part in a **project** and is presented with **tasks**, they create a **submission** for each task.

Pretty standard stuff, right?

---

## Why PostgreSQL? Or, Why Not NoSQL?

* Mature, stable database with support for sharding and distribution
* Excellent extensions available
* Power of relational data with the addition of unstructured data support with JSONB
* Incredibly powerful indexing

---

## So?

Each **model** is inheriting from a **base model** that has:

* ID
* Creation Date
* Modification Date
* Info

Info is a JSONB that allows users to extend their model to suit their needs without needing to extend it or modify any of the code

---

## How Do They Access It?

**OpenAPI**

An open specification that allows the description and documentation of an API and the underlying models

TL;DR - reduces `monkey` coding by a significant factor and makes complex descriptions human readable

---

## OpenAPI

```
host: api.citizenscience.ch
basePath: /api/v1
schemes:
  - https
paths:
  /users:
    get:
      tags: [Users]
      description: Retrieve all users matching a filter
      security:
        - oauth2: []
      x-swagger-router-controller: api.user
      operationId: get_users
      parameters:
        - name: search_term
          in: query
          type: string

 ```

---

## So?

OpenAPI does not just make your API documentation readable, frameworks can scaffold a server using this spec...

* [zalando/connexion](github.com/zalando/connexion) -A Python web server that loads routes and handles security based on your OpenAPI spec. The only code required is the `logic`
* [encima/openape](github.com/encima/openape) -A Go based web server that implements routing and basic `logic` (GET, PUT, POST, DELETE). The only code required is `custom routes`

---

## Wait, there's more...

Giving your specification a web frontend not only allows users to browse the documentation but to also try out the API and test responses:

[Citizen Science API](https://api.citizenscience.ch)

---

## Wow, I'm Sold. Is That All?

# NO!

## How complicated is an SDK?
## How much would you pay for one?

---

## SDK Generation

In (almost) all languages:
* Python, Go, Dart, Java, C++
* JavaScript, Rust, Haskell etc

WITH:
* built in security handling
* validation
* handling of headers and authentication


---

## Uh-huh, What Does This Mean For Me?

The hottest frontend web frameworks change more often than Amazon avoids taxes

The number of programming languages and tools required to develop mobile apps is more than the number of Starbucks in Silicon Valley

---

# So?

Talent is hard to find (and sometimes hard to train). A flexible and open development stack is **vital** to support adoption.

I.e. Any frontend developer using this stack needs to know nothing about OpenAPI, Python, Go or Docker. They just need to know the location of the Spec and an SDK is created for them.

---

# Frontend


**TODO: Image of frontend**

---

Developed using **VueJS** 2.0.

### Why?

* Solid community
* Small packed size
* Easy to learn and clean structure
* Components can be shared between pages

---

* **Not made by Google and/or Facebook**
* Well supported packages for extensibility:
    * Routing
    * Client side databases
    * Mobile webviews

---

## VueJS

VueJS has a package that can dynamically create an SDK from a Swagger Specification.

So...no need to redeploy your frontend everytime the API changes and no need to generate an SDK with every minor change. 

There is the downside that a change in the spec can break your client applications but this is resolved with the correct environments.

---

## Environments

* Local - used for development
* Docker and Test - used for local development and testing
* Staging - hosted on sciencecloud with no public access
* Production - hosted on sciencecloud with public access

`api.citizenscience.ch`

---

## Deployment

* `Gitflow` development followed
* `Deployed` to Github
* Tested using TravisCI
* Released to staging through githooks
* Manual production release on a biweekly schedule

---

### Don't like our apps? Want to make your own?

Do it, use our API to integrate with your existing project or even as a backup.

Make your own mobile client to add features we do not yet support.

---

# Mobile

To be honest, the best way to make a mobile app is [native](https://medium.com/airbnb-engineering/react-native-at-airbnb-the-technology-dafd0b43838)

This does not mean that other options do not exist:

Java, Swift, Kotlin, Objective-C, React Native, Nativescript, Cordova, PhoneGap, Ionic...

---

# Current Status

* Backend in early alpha
* Frontend in development (implemented without design)
* Mobile platform is being discussed currently
* Feedback and requirements being gathered from researchers
* 1 active project [Wenker](wenker.citizenscience.ch)

---

### Want to help?

What are you forking waiting for?

https://github.com/citizensciencecenter

Review the code, documentation, help with translations or report some bugs. We need it all!

---

# Questions?


![huh](https://media.giphy.com/media/cAEm5rSuuBEGY/giphy.gif)

christopher.gwilliams@uzh.ch

---

![excellent](https://media.giphy.com/media/dXICCcws9oxxK/giphy.gif)


	
