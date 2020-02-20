CHANGE THE ENTIRE ROADMAP TO REMOVE MODEL ENCRYPTION

## Introduction

_Last modified: February 17th, 2020_

Encrypted Machine Learning as a Service (EMLaaS) is one of the primary use-cases of the OpenMined ecosystem. By allowing developers to query a remote, encrypted dataset, they can evaluate the effectiveness of their models on data they literally "cannot see".

In this concept, a data supplier may allow a data scientist (internal to their organization, or external) to submit their model for encrypted validation, all while tracking and permissioning their usage at a granular level. Doing such validation does not permit the data scientist to steal the private, and often sensitive, information of the data owner - nor does it allow the organization or individual that owns this data from intercepting the intellectual property of the data scientist. Using PyGrid from OpenMined, it's possible for model validation to be performed without either side compromising on privacy, security, or intellectual property.

For this process to work correctly, the data owner will place their private data inside of a PyGrid "gateway", which acts as the primary endpoint for a network of PyGrid "nodes". Each node has dedicated compute resources with which to validate models on behalf of the data scientist. The data owner can create users with a variety of preset and custom roles, as well as designate each user's "epsilon budget" which is used to track how many `get()` requests that particular user has made. This ensures that no one user has complete access to the encrypted dataset of the PyGrid gateway, nor can they make unlimited model validation requests (unless allowed by an administrator).

Of course, it would be difficult to manage an entire network of user permissions, roles, and model validation requests through a command line or Python notebook. This creates the need for a small user interface to be developed to aide in the management of a private PyGrid network. We call this UI the "PyGrid Admin" and it will serve as the secondary component of this project's roadmap. An administrator will be able to manage their entire network through this user interface, which will be hosted as a standalone single-page application separate from the PyGrid API itself. Developing the UI as a standalone front-end application, allows for the PyGrid network infrastructure to be scaled separate from the needs of running a user interface. Thus, the PyGrid Admin UI may be hosted on a variety of cloud-based file server platforms like AWS's S3, GCP's Cloud Storage, Microsoft's Azure Blob Storage, Netlify, or other such static asset hosting solutions.

**Patrick Cason<br />**
_Web and Mobile Team Lead_

## Terminology

Let’s start off by defining a few terms that will be regularly used throughout this document:

- **Model** - a standard machine learning model
- **Plan** - a serialized list of operations that can be executed by a PyGrid Node
- **Model validation** - the ability to supply test data (in this case, from an encrypted dataset) to a pre-trained model for the purposes of testing and evaluating that model's prediction accuracy
- **Gateway** - the primary public endpoint for a PyGrid network
- **Node** - a single server running within a PyGrid network, accessible via the PyGrid Gateway
- **Privacy budget** - the amount of validation requests a user can make on a given encrypted PyGrid dataset
- **Epsilon value** - the name of the value for measuring a user's privacy budget
- **Encrypted Machine Learning as a Service (EMLaaS)** - the ability to for a model to train or predict (but for purposes of this roadmap: prediction only) against private data in the cloud

We will also use this section for defining each of the components of the OpenMined EMLaaS system:

- **PyGrid** - a library consisting of multiple services that allows for "nodes" to be deployed and managed through a single "gateway". This is the main project where validation requests will be sent to and encrypted data will be hosted.
- **PySyft** - a framework for privacy-preserving machine learning that is the primary library called internally by PyGrid
- **PyGrid Admin** - a user interface (UI) for managing a PyGrid network, allowing an administrator to manage user roles and permissions and model validation requests by those users

## Overview

XXX

## Projects

XXX
