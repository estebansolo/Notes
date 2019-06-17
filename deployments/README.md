# Deployments

## Table of Contents

- [Introduction](#introduction)
  - [CDN](#cdn)
  - [API](#api)
  - [Monolithic Applications](#monolithic-applications)
  - [Microservices](#microservices)
- [Deployment Options](#deployment-options)
  - [Amazon Web Services](#amazon-web-services)
  - [Microsoft Azure](#microsoft-azure)
  - [Google Cloud Plaform](#google-cloud-plaform)
  - [Digital Ocean](#digital-ocean)
  - [Zeit](#zeit)
  - [Heroku](#heroku)
  - [GitHub Pages](#gitHub-pages)
  - [Surge](#surge)

## Introduction

### CDN

Content Delivery Network. Many servers distributed around the world provide these common files and they are not dynamically generated to our users and they can quickly access them.

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### API

Aplication Programming Interface. It represents the communication capacity between software components.

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Monolithic Applications

#### Advantages

- Good for small applications.
- Easy to develop.
- Easy to deploy.
- Easy to work individually or in small teams.

#### Disadvantages

- Difficult to maintain in the long term.
- Costly to climb.
- In case of an error the whole application can be dropped.
- More difficult to test.
- More difficult to debug.

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Microservices

What is a micro-service?
The code divided into several applications.

#### Advantages

- Easy to deploy.
- Easy to scale.
- Easy to test.
- Easy to debug.
- In case of error only one service falls.
- Different technologies can be used.

#### Disadvantages

- Hard to orchestrate.
- Communication between services may be slow.
- Difficult to know how to divide our application.
- It is more expensive to maintain.

Important:

Orchestration and Choreography of Services = Both concepts are based on how to communicate our services and that everything works as if it were a single application.

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

## Deployment Options

### Amazon Web Services

With infrastructure control, is the largest of all options to deploy.

See more: [Amazon Web Services]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Microsoft Azure

With infrastructure control, Perfect for applications in C# and .Net

See more: [Microsoft Azure]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Google Cloud Plaform

With infrastructure control, One advantage is that it has several of Google's own APIs that can be integrated into the application.

See more: [Google Cloud Plaform]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Digital Ocean

With infrastructure control, it allows you to have a private server and start finding everything you want there.

See more: [Digital Ocean]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Zeit

Without infrastructure control, deploy of any kind, even Docker containers. Can only be used with Web servers. Some advantages when deploying:

#### Deployment types:

- Applications Node.js
- Static Sites
- Docker Containers

#### Characteristics:

- It's easy.
- Scales automatically.
- Deploy immutable, each deploy returns a URL that can be accessed.
- Deploy without drop.
- Deploy Unlimited
- HTTP2 Automatically
- Free SSL Certificate
- Logs for each Deploy
- DNS (zeit.world)
- Buy Domains by CLI

See more: [Zeit] / [Notes](zeit/)

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Heroku

Without infrastructure control, it allows you to deploy without having to think about how the app will work underneath or the infrastructure of it.

See more: [Heroku]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### GitHub Pages

Static sites, Allows to deploy static files. It is completely free but the code is open source.

The project must be public, also is used mainly to document libraries. The steps to make a page available are the following.

- Go to Settings
- In the **_github pages_** section, select the branch master
- Click on Save to finish

See more: [GitHub Pages]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

### Surge

Static sites, Allows you to make static deploys very easily by means of a CLI.

```
npm i -g surge
```

Go to folder

```
surge
```

Use login data

See more: [Surge]

<div align="right">
  <small><a href="#table-of-contents">:arrow_up: Up</a></small>
</div>

[amazon web services]: https://aws.amazon.com/
[microsoft azure]: https://azure.microsoft.com/en-us/
[google cloud plaform]: https://cloud.google.com/
[digital ocean]: https://www.digitalocean.com/
[zeit]: https://zeit.co/
[heroku]: https://www.heroku.com/
[github pages]: https://pages.github.com/
[gitlab pages]: https://about.gitlab.com/product/pages/
[surge]: https://surge.sh/
