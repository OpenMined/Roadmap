## Introduction

_Last modified: February 26th, 2020_

Secure model evaluation is one of the primary use-cases of the OpenMined ecosystem. By allowing developers to query a remote dataset, they can evaluate the effectiveness of their models on data they literally "cannot see".

In this concept, a data supplier may allow a data scientist (internal to their organization, or external) to submit their model for private validation, all while tracking and permissioning their usage at a granular level. Doing such validation does not permit the data scientist to steal the private, and often sensitive, information of the data owner. It is noteworthy that in this setting, we assume that the data owner is a trusted organization and that future extensions of this project will enable the use of encrypted computation for joint protection of the model and dataset during evaluation.

For this process to work correctly, the data owner will place their private data inside of a PyGrid "gateway" that acts as both a data store and a load balancer, distributing work to one or many PyGrid "nodes" which act as workers on that data. Each node has dedicated compute resources with which to validate models on behalf of the data scientist. If there are no active nodes available to take a validation job at the moment, the job request will be put into a job queue where it will eventually get assigned to a worker and executed. There is also an optional layer on top of a PyGrid gateway called a PyGrid "network" that allows a user to search for available datasets across multiple gateways under the same network. Regardless of presence of a network, a data owner may deploy their PyGrid gateway either to their own privately managed servers, or to a major cloud provider like AWS, GCP, Azure, Heroku, or DigitalOcean.

The data owner can create users on their gateway with a variety of preset and custom permissions, as well as designate each user's "privacy budget" (tracked via an "epsilon value") which is used to track how many `get()` requests that particular user has made. This ensures that no one user has complete access to the private dataset of the PyGrid gateway, nor can they make unlimited model validation requests. Permissions can be created and assigned at both the user-level and the tensor-level, allowing for smart defaults to be set, and overrides to be assigned on a case-by-case basis. Tensors can be listed as "public" or "private":

- **Public** means they're available in a gateway or network search and available for evaluation request by any user.
- **Private** means they are visible in a gateway or network search and may be used to evaluate a model, but the results of the evaluation are disclosed only if the user has appropriate permissions to do so. If the user does not have permissions, they may submit a request for a modification of their permissions.

Of course, it would be difficult to manage multiple users, permissions, and model validation requests through a command line or Python notebook. This creates the need for a small user interface to be developed to aide in the management of a private PyGrid gateway. We call this user interface the "PyGrid Admin" and it will serve as the secondary component of this project's roadmap. An administrator will be able to manage their entire gateway through this white-labeled user interface, which will be hosted as a standalone single-page application separate from the PyGrid API itself. Developing the PyGrid Admin as a standalone front-end application allows for the PyGrid gateway infrastructure to be scaled separate from the needs of running a user interface. Thus, the PyGrid Admin may be hosted on a variety of cloud-based file server platforms like AWS's S3, GCP's Cloud Storage, Microsoft's Azure Blob Storage, Netlify, or other such static asset hosting solutions.

One important administrative role of the PyGrid Admin is approving and denying data requests - we call this role the "data compliance officer". This individual is responsible for ensuring that the results of a model evaluation, which will be sent back to the data scientist, do not contain private information. The application will be responsible for empowering the data compliance officer with all of the information they need to make this decision, including: advanced analytics, differential privacy budgeting (tracked via an epsilon value), user request history, model and plan inspection, data request inspection, and other sources of information. Enforcement of these decisions will be performed by this individual within the PyGrid Admin, ensuring total control over their private data.

**Patrick Cason<br />**
_Web and Mobile Team Lead_

## Terminology

Let’s start off by defining a few terms that will be regularly used throughout this document:

- **Model** - a standard machine learning model
- **Plan** - a serialized list of operations that can be executed by a PyGrid Node
- **Model evaluation/validation** - the ability to supply test data (in this case, from a private dataset) to a pre-trained model for the purposes of testing and evaluating that model's prediction accuracy
- **Gateway** - a data store and load balancer that serves as the primary public endpoint for a PyGrid network
- **Node** - a single server acting as a worker for a PyGrid gateway, where model evaluation takes place
- **Privacy budget** - the amount of validation requests a user can make on a given dataset
- **Epsilon value** - the name of the value for measuring a user's privacy budget

We will also use this section for defining each of the components of the OpenMined secure model evaluation system:

- **PyGrid** - a library consisting of multiple services that allows for "nodes" to be deployed and managed through a single "gateway". This is the main project where validation requests will be sent to and private data will be hosted.
- **PySyft** - a framework for privacy-preserving machine learning that is the primary library called internally by PyGrid
- **PyGrid Admin** - a user interface (UI) for managing a PyGrid network, allowing an administrator to manage user and tensor permissions and model validation requests by those users

## Overview

### 1. Host

To start, an individual or organization must deploy their own PyGrid network comprised of a single PyGrid gateway and one or many PyGrid nodes, which will be responsible for hosting private data and performing model evaluation. The PyGrid gateway will facilitate this work, allowing developers working with this network to not need to issue commands directly to a single node. Instead, commands may be issued to the gateway, which it then delegates to the appropriate node. This allows for the simple management of complex networks with hundreds or thousands of nodes.

```python
# IONESIO - Please replace this code block with PyGrid code that does the following:
# 1. Create a basic PyGrid network with a gateway and multiple nodes
# 2. Deploy this PyGrid network to a cloud provider or private cloud network
```

At this point, there is a fully-hosted PyGrid network running in the cloud. It's time to host data within that network and create helpful tags so that a data scientist requesting model evaluation can appropriately request only relevant datasets.

```python
# IONESIO - Please replace this code block with PyGrid code that does the following:
# 1. Connect to this deployed PyGrid network as an administrator
# 2. Host a diabetes patient dataset (can be arbitrarily defined as "MY_DIABETES_PATIENT_DATASET")
# 3. Host a cancer patient dataset (can be arbitrarily defined as "MY_CANCER_PATIENT_DATASET")
# 4. Tag each dataset appropriately
```

### 2. Permission

TODO: Need to permission tensors, users, and the user to tensor relationship(s)
TODO: Redo this entire section

At this point, we've created our network and are ready to begin creating users and permissions. At a high level, the permissioning system will have concept of users and roles: users can have a "privacy budget" and a list of associated roles, while roles will have lists of permissions ("things" that a user may or may not do). While it's possible to create custom roles, there are some defaults that apply to any PyGrid network:

1. **User**<br />
   Sample role

### 3 - X. FIGURE ME OUT

TODO: Do the data scientist workflow here
TODO: Allow for model eval to happen in two ways: I can send a model for validation OR the model is already on the machine, and instead I send the evaluation script

### 5. Enforce

TODO: Enforce access requests as an administrator

## Projects

### PyGrid

- TODO: Add a project to change the names of gateway, node, and add network
- TODO: Add a project to rearrange the flow of data hosting, authentication, etc.
- [Hello world](https://google.com)

### PySyft

- [Hello world](https://google.com)

### PyGrid Admin

- [Hello world](https://google.com)
