## Introduction

_Last modified: April 24th, 2020_

Dynamic federated learning is one of the primary use-cases of the OpenMined ecosystem. By allowing data scientists to search for and ETL remote tensors, so they can train models on data they literally "cannot see".

In this concept, a data owner may allow a data scientist (internal to their organization, or external) to submit their model for training, all while tracking and permissioning their usage at a granular level. Doing such training does not permit the data scientist to steal the private, and often sensitive, information of the data owner. It is noteworthy that in this setting, we assume that the data owner is a trusted organization and that future extensions of this project will enable the use of encrypted computation for joint protection of the model and tensors during training.

For this process to work correctly, the data owner will place their private data inside of a PyGrid "gateway" that acts as both a data store and a load balancer, distributing work to one or many PyGrid "nodes" which act as workers on that data. Each node has dedicated compute resources with which to train models on behalf of the data scientist. There is also an optional layer on top of a PyGrid gateway called a PyGrid "network" that allows a user to search for available tensors across multiple gateways under the same network. Regardless of presence of a network, a data owner may deploy their PyGrid gateway either to their own privately managed servers, or to a major cloud provider like AWS, GCP, Azure, Heroku, or DigitalOcean.

The data owner can create users on their gateway with a variety of preset and custom permissions, as well as designate each user's "privacy budget" (tracked via an "epsilon value") which is used to track how many `get()` requests that particular user has made. This ensures that no one user has complete access to the private tensors of the PyGrid gateway, nor can they make unlimited model training requests. Permissions can be created and assigned at both the user-level and the tensor-level, allowing for smart defaults to be set, and overrides to be assigned on a case-by-case basis. Tensors can be listed as "public" or "private":

- **Public** means they're visible in a gateway or network search and available for training request by any user.
- **Private** means they're visible in a gateway or network search and may be used to train a model, but the results of the training are disclosed only if the user has appropriate permissions to observe them. If the user does not have permissions, they may submit a request for a modification of their permissions to the data compliance officer.

Of course, it would be difficult to manage multiple users, permissions, and model training requests through a command line or Python notebook. This creates the need for a small user interface to be developed to aide in the management of a private PyGrid gateway. We call this user interface the "PyGrid Admin" and it will serve as the secondary component of this project's roadmap. An administrator will be able to manage their entire gateway through this white-labeled user interface, which will be hosted as a standalone single-page application separate from the PyGrid API itself. Developing the PyGrid Admin as a standalone front-end application allows for the PyGrid gateway infrastructure to be scaled separate from the needs of running a user interface. Thus, the PyGrid Admin may be hosted on a variety of cloud-based file server platforms like AWS's S3, GCP's Cloud Storage, Microsoft's Azure Blob Storage, Netlify, or other such static asset hosting solutions.

One important administrative role of the PyGrid Admin is approving and denying data requests - we call this role the "data compliance officer". This individual is responsible for ensuring that the results of model training, which will be sent back to the data scientist, do not contain private information. The application will be responsible for empowering the data compliance officer with all of the information they need to make this decision, including: advanced analytics, differential privacy budgeting (tracked via an epsilon value), user request history, model and plan inspection, data request inspection, and other sources of information. Enforcement of these decisions will be performed by this individual within the PyGrid Admin, ensuring total control over their private data.

**Patrick Cason<br />**
_Web and Mobile Team Lead_

## Associated Roadmaps

This roadmap describes a project that is comprised of multiple other smaller projects. Each of these smaller projects has been described in their own "mini-roadmap", listed below:

- [Reorganization of PyGrid](common/pygrid_reorganization.md)
- [Automatic privacy budgeting](common/privacy_budgeting.md)
- [PyGrid Admin UI](common/pygrid_admin.md)
- [Adding permissions to PyGrid](common/pygrid_permissions.md)
- [Adding cloud deployment to PyGrid](cloud_deployment.md)

## Terminology

Let’s start off by defining a few terms that will be regularly used throughout this document:

- **Model** - a standard machine learning model
- **Plan** - a serialized list of operations that can be executed by a PyGrid Node
- **Gateway** - a data store and load balancer that serves as the primary public endpoint for a PyGrid network
- **Node** - a single server acting as a worker for a PyGrid gateway, where model training takes place
- **Privacy budget** - the amount of data per user that a data compliance officer can justify leaving their system
- **Epsilon value** - the name of the value for measuring a user's privacy budget

We will also use this section for defining each of the components of the OpenMined dynamic federated learning system:

- **PyGrid** - a library consisting of multiple services that allows for "nodes" to be deployed and managed through a single "gateway". This is the main project where model training requests will be sent to and private data will be hosted.
- **PySyft** - a framework for privacy-preserving machine learning that is the primary library called internally by PyGrid
- **PyGrid Admin** - a user interface (UI) for managing a PyGrid network, allowing an administrator to manage user and tensor permissions and model trainin requests by those users

## Overview

### 1. Host

To start, an individual or organization must deploy their own PyGrid network comprised of a single PyGrid gateway which is responsible for hosting private data, and one or many PyGrid nodes which are responsible for performing model training. Commands may be issued to the gateway, which it then delegates to the appropriate node. This allows for the simple management of complex networks with hundreds or thousands of nodes.

```python
# 1. Create a basic PyGrid network with a gateway and multiple nodes
# 2. Deploy this PyGrid network to a cloud provider or private cloud network
```

At this point, there is a fully-hosted PyGrid network [running in the cloud](cloud_deployment.md). It's time to host data within that network and create helpful tags so that a data scientist requesting model training can appropriately request only relevant tensors.

```python
# 1. Connect to this deployed PyGrid network as an administrator
# 2. Host a diabetes patient tensor
# 3. Host a cancer patient tensor
# 4. Tag each tensor appropriately
```

### 2. Permission

At this point, we've created our network and are ready to begin creating users and permissions. To make this process quicker, we suggest that creating users and assigning permissions is done through the PyGrid Admin UI. For a full overview of user roles and permission, [please visit that sub-roadmap here](common/pygrid_permissions.md). The premise is as such:

- Users are created inside of the PyGrid Gateway and given a base-level of permissions for querying tensors in the database.
- Data scientists will not be given any UI access in the PyGrid Admin UI, and will be required to interface with the Gateway or Network via a command line or Python Notebook.
- Tensors may have individual permissions set to them, such as a "public" or "private" status.
- Data scientists are given access to all public tensors and whatever private tensors an administrator permits. They will have the ability to search all tensors, regardless of their status.
- Groups may be created to make assigning permissions in batch easier.
- There are multiple other roles for various Gateway and Network administrators.

Generally speaking, permissions are highly flexible and can be assigned to users, groups, and tensors. Overrides are made possible in the exact same order of priortity (highest to lowest).

### 3. Search

Once PyGrid has been hosted, tensors have been uploaded, users have been created, and permissions have been set, data scientists may begin making requests to the gateway. This process begins with a simple search of what tensors the data scientist may be interested in. Once they've searched the gateway and have found a tensor they would like to work with, they may begin provisioning compute resources and start working.

```python
# 1. Log into the PyGrid gateway
# 2. Do a search of the gateway
# 3. Provision compute resources
# 4. Select a tensor from the list and start working
```

If additional permissions are needed to select a tensor for training, the data scientist may request permission right in their Jupyter Notebook before continuing on.

```python
# 1. Log into the PyGrid gateway
# 2. Do a search of the gateway
# 3. Request permissions to select a tensor from the list
# 4. Carry on...
```

### 4. Train

Once the tensor has been selected for training, the data scientist may perform their work as normal.

```python
# 1. Do work
```

Once they are satisfied with the result, they may call `get()` to make a request for the trained model to be sent back to their machine. This then sends a notification to the data compliance officer to perform an audit of the trained model,

### 5. Enforce

It's important for a data compliance officer to have control over what data leaves their system. This person's primary job is to read through a model trained on the system, look at the effect that training the model had on their system's privacy leakage, and then determine whether or not the release of this trained model should be allowed. It's also worth nothing that a data scientist who makes a `get()` request for a tensor that exceeds their alotted privacy budget will be automatically denied.

If the the data compliance officer agrees that the privacy leakage is appropriate, they can choose to fulfill the `get()` request and release the trained model back to the data scientist. This is done through the PyGrid Admin UI. Optionally, they may choose to deny this request and the data scientist will be notified of the decision. Currently, the way this decision is communicated between the data compliance officer and the data scientist is arbitrary and determined by the individual relationship of those two individuals. It's outside the scope of this roadmap to prescribe a communication gateway for these individuals. Privacy budgeting is discussed at [much greater detail here](common/privacy_budgeting.md).

## Projects

### PyGrid

- [INSERT ISSUES HERE](https://google.com)

### PySyft

- [INSERT ISSUES HERE](https://google.com)

### PyGrid Admin UI

- [INSERT ISSUES HERE](https://google.com)
