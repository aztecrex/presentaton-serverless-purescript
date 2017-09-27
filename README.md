# Purescript in the House

_Functional and Serverless on AWS_

---

# Motivation

## Non-trivial application with lots of feature potential

## Transcend platforms
- Web
- Mobile
- Embedded

# Prefer to develop in Haskell but...

integrating in browser not a great story (yet).

---

# Motivation

## Run completely in the cloud

## ... without servers

---

# Review of Serverless

## Ephemeral

Push code to a provider and it runs in response to events. Advantages
include elasticity,  ease of deployment, and integration with PaaS services.

Ephemeral deployments can offer huge cost savings when an application is
dark much of the time.

### For Example

- AWS Lambda
- Google Cloud Functions
- IBM OpenWhisk

---

# Review of Serverless

## Browser-only

All logic is in the web page. It coordinates 3rd-party services directly

Browser-only applications offer elasticity and ease of deployment. Processing
load is offloaded to client computers.

Browser-only applications can be hard to integrate and require particular
attention to security.

## Hybrid

The two approaches can be used together, playing to the strengths of each.
Parts of the application can be migrated between the two to support new
features and use patterns.

---

# Purescript

## Pure functional

## Haskell-like syntax

## Strict evaluation

## Compiles to Javascript for server or web

## Straightforward, powerful FFI

---

# The Presenter Application

