# Purescript in the House

## _Functional and Serverless on AWS_

---

# Purescript in the House

### Why do this?

### Purescript

### Serverless

### Application and How it works

### Discussion and code review

---

## Why do this?

See if a strongly-typed pure functional language could be used for
all parts of an application.

### I just wanted a quick way to write and show a presentation

- Preferrably using Markdown syntax
- write it in Haskell?  Not a great browser story (yet)


### Could it be networked?

- Web
- Mobile
- Embedded


---

## Why do this?

### Could it be run without servers?

---

## Purescript

### Strongly typed pure functional

Pure functional means the code doesn't hide its effects.

### Compiles to Javascript

Suitable to run in browser, Node, Lambda, and others.

### Haskell-like syntax

### Strict evaluation

No need for a runtime component.

### Straightforward, powerful FFI

No runtime means all imported functions are just simple javascript
functions. You can break effect encapulation here, though.

---

## Quick Review of Serverless Architecture

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

## Quick Review of Serverless Architecture

### Browser-only

- All logic is in the web page. It coordinates 3rd-party services directly
from the brower.
- Elasticity and ease of deployment. Processing
is offloaded to client computers.
- Browser-only applications can be hard to integrate and require particular
attention to security.

---

## Quick Review of Serverless Architecture

### Hybrid

The two approaches can be used together and parts can be migrated
between the two to support new features and use patterns.


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

The runtime and build infrastructure are desribed by runnable templates that
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
to match the desired state.

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

# Purescript in the House

## Discussion and Code

---

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

---

## Next

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

