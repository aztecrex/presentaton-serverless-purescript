# Purescript in the House

## _Functional and Serverless on AWS_

---

## Motivation

See if a pure functional language could be used for all parts of an application.

### Non-trivial application with lots of feature potential

### Transcend platforms

- Web
- Mobile
- Embedded


---

## Motivation

### Run completely in the cloud

### ... without servers

---

## Review of Serverless

### Ephemeral

Push code to a provider and it runs in response to events. Advantages
include elasticity,  ease of deployment, and integration with PaaS services.

Ephemeral deployments can offer huge cost savings when an application is
dark much of the time.

#### For Example

- AWS Lambda
- Google Cloud Functions
- IBM OpenWhisk

---

## Review of Serverless

### Browser-only

All logic is in the web page. It coordinates 3rd-party services directly

Browser-only applications offer elasticity and ease of deployment. Processing
load is offloaded to client computers.

Browser-only applications can be hard to integrate and require particular
attention to security.

---

## Review of Serverless

### Hybrid

The two approaches can be used together, playing to the strengths of each.
Parts of the application can be migrated between the two to support new
features and use patterns.

---

## Purescript

### Pure functional

### Haskell-like syntax

### Strict evaluation

### Compiles to Javascript for server or web

### Straightforward, powerful FFI

---

## The Presenter Application

The application is browser only. The application uses several
services directly from the web page.

### AWS IoT

### Google Signin

### AWS S3

### AWS Cognito

---

## AWS IoT

### Shadow devices

Coordinate the application with "desired" and "reported" states.

### Pub/sub Topics

Distribute events to all application components whether on server,
browser, or embedded.

---

## Google Signin

Familiar "login with google" workflow.

---

## AWS S3

S3 storage objects persist application state between sessions.

---

## AWS Cognito

Cognito federated identities tie 3rd-party authentication, such as Google Signin,
to AWS roles and data. Cognito supports both unauthenticated and authenticated
users.

Once an identity is established, it can be traded for temporary, time-limited
credentials with fine-grained service authorizations.

For example, a DynamoDB permission can limit access to a single table row. An
S3 permission can be limited to a specific file object.

---

## Build Pipelines

The application is continually deployed on every push to Github using
CodePipeline and CodeBuild.

---

## Repeatable Infrastructure

The runtime and build infrastructure is desribed by runnable templates that
provision all parts of the application.

---

## How it Works

### Viewer

#### Unauthentiated authorization

The viewer contacts Cognito without authentication and receives an
unauthenticated identity. The identity
can be traded for very limited credentials that only allow it to read the status
of an IoT shadow device.

#### Connect to the shadow

The viewer retrieves the desired state of the shadow device and configures itself
to match the desired state. It attempts to configure itself to match that state.

#### Subscribe to updates

The viewer continues to listen for changes in the shadow state and continually
matches that state with its real configuration.

---

## How it Works

### Authenticated control surface

#### Login with Google

A user's Google login state is determined using the Google APIs. If the user is
not currently logged in, the normal Google authentication flow is initiated.

#### Authorize with Cognito

The acquired Google token is submitted to Cognito for a federated identity. The
identity is exchanged for limited credentials that allow the control surface
to read and write the list of presentations in S3 and to modify the shadow
device state.

#### Load presentations from S3

The control surface initially loads the list of presentations from a file
in S3.

---

## How it Works

### Authenticated control surface

#### Change slide or presentation

When a slide or presentation button is pressed, the control surface
modifies the shadow
device state in Cognito with the new page number. The new state is immediately
received by all listening viewers.

#### Add a presentation

When a presentation is added, the surface writes it as a text file to
S3

---

## Lessons

### Authentication flow and authorization configuration

This was the most time-consuming part of development. The documentation
for Google Signin and Cognito abounds. But much of it is out-of-date,
not applicable to browser-only applications, missing critical details,
or just plain wrong.

Part of the problem is that the APIs change fairly rapidly and you can't
always tell if two documents are referring to the same API.

---

## Lessons

### Purescript works really well

- the FFI story is great
- The standard categorical data types are well conceived and avoid many
of the problems that Haskell has

### Purescript is still pretty young

- The package management tooling for Purescript can make it hard to
share code between projects
- There are not many integration-oriented packages so you will have to
do a lot of work in the FFI.


### Purecript language has a few ergonomic challenges

- Effect labels
- Import warnings
- Explicit qualification

---

## Next

### Stick with Puresript for now

- replace prototype code
- encapsulate the emerging patterns
- consider alternatives to Pux

### Slide Style

### Device model

- multiple shadows
- "reported" device state

### New integrations

- Slack
- Alexa
- Embedded controller
- Embedded viewer
- More identity providers

---

## Next

### New Features

- selectable and/or custom styles
- presentation metadata
- media controls
- animation?

---

## Next

### AWS Lambda

### AWS DymamoDB

### Self-service accounts

