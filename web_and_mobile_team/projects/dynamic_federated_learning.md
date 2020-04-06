## Introduction

_Last modified: April 6th, 2020_

Dynamic federated learning is one of the primary use-cases of the OpenMined ecosystem. By allowing data scientists to search for and ETL remote datasets, so they can train models on data they literally "cannot see".

In this concept, a data owner may allow a data scientist (internal to their organization, or external) to submit their model for training, all while tracking and permissioning their usage at a granular level. Doing such training does not permit the data scientist to steal the private, and often sensitive, information of the data owner. It is noteworthy that in this setting, we assume that the data owner is a trusted organization and that future extensions of this project will enable the use of encrypted computation for joint protection of the model and dataset during training.

For this process to work correctly, the data owner will place their private data inside of a PyGrid "gateway" that acts as both a data store and a load balancer, distributing work to one or many PyGrid "nodes" which act as workers on that data. Each node has dedicated compute resources with which to train models on behalf of the data scientist. There is also an optional layer on top of a PyGrid gateway called a PyGrid "network" that allows a user to search for available datasets across multiple gateways under the same network. Regardless of presence of a network, a data owner may deploy their PyGrid gateway either to their own privately managed servers, or to a major cloud provider like AWS, GCP, Azure, Heroku, or DigitalOcean.

The data owner can create users on their gateway with a variety of preset and custom permissions, as well as designate each user's "privacy budget" (tracked via an "epsilon value") which is used to track how many `get()` requests that particular user has made. This ensures that no one user has complete access to the private dataset of the PyGrid gateway, nor can they make unlimited model training requests. Permissions can be created and assigned at both the user-level and the tensor-level, allowing for smart defaults to be set, and overrides to be assigned on a case-by-case basis. Tensors can be listed as "public" or "private":

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
- **Privacy budget** - the amount of model training requests a user can make on a given dataset
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

At this point, there is a fully-hosted PyGrid network running in the cloud. It's time to host data within that network and create helpful tags so that a data scientist requesting model training can appropriately request only relevant datasets.

```python
# 1. Connect to this deployed PyGrid network as an administrator
# 2. Host a diabetes patient dataset
# 3. Host a cancer patient dataset
# 4. Tag each dataset appropriately
```

### 2. Permission

At this point, we've created our network and are ready to begin creating users and permissions. This may be done only through the PyGrid Admin UI. Since the user interface is simply a series of static files, hosting may be done by cloning the Github project to any file server. If the network administrator prefers, they may also use any of the various one-click deploy buttons in the Github project. Since the UI is separate from the PyGrid application entirely, the scaling concerns are separated. This project is defined in [much more detail here](common/pygrid_admin.md).

Permission may be applied to a user directly. The grid owner will specify which users have access to which private tensors. They also specify that user's privacy budget which gets updated according to each `get()` request the user makes against the gateway. To make managing user permissions easier, the PyGrid Admin also allows you to specify "groups". Groups allow for organizing subsets of users into pre-determined permissions lists. If a user is part of a group, their permissions are determined by that of their group AND their user-specific permissions. For instance, if a group does not have access to a specific private tensor, the grid owner may decide to allow permissions for a specific user in that group to have access to the tensor, but disallow access for the other users in the group.

It's also worth nothing that there is a separate system of "roles" which strictly relate to administrative access to a PyGrid gateway. All newly created users default to the "User" role, which does not allow for any administrative access to the PyGrid network. The roles are described below, according to their access level from lowest to highest:

#### User

This is the default user role and is reserved for a user that is non-administrative. This is the role which all external data scientists will be assigned to. This role does not grant access to the PyGrid Admin UI.

#### Compliance Officer

The compliance officer role is strictly for users that are allowed to approve and deny tensor requests. They are only allowed to triage requests made to the system. They cannot change settings within the PyGrid gateway, nor can they create new users.

#### Admininstrator

The administrator role has permission to do mostly anything on the PyGrid gateway, including triage tensor `get()` requests, create new users, and change settings. However, they do not have the ability to provision compute resources by horizontally or vertically scaling nodes.

#### Gateway Owner

The gateway owner role has permission to do anything an administrator can do, but they can also add, remove, or modify compute resources by horizontally or vertically scaling nodes.

#### Network Administrator

The network administrator role isn't tied to access control of one specific gateway. Instead, this role allows for a user to add or remove PyGrid gateways from a PyGrid network, if a network has been configured. This user does not have permissions to modify or inspect any of the individual gateways in any way. They only have permission to manage the overall network of gateways.

---

It's worth noting that there is no "Network Owner" role. This is to allow for a natural delegation of responsibility, without giving any one user too much control. The "Gateway Owner" is the master of their gateway. The "Network Administrator" is the master of the network, but does not have access to any of the gateways themselves.

Such an organizational example might be that various hospitals host their own gateways, but a data scientist may choose to query multiple different hospitals that are part of the same network. It's important here that the person who runs the network, doesn't run all the hospitals within the network.

### 3. Search

Once PyGrid has been hosted, tensors have been uploaded, users have been created, and permissions have been set, data scientists may begin making requests to the gateway. This process begins with a simple search of what datasets the data scientist may be interested in. Once they've searched the gateway and have found a tensor they would like to work with, they may begin provisioning compute resources and start working.

TODO: @iamtrask Clear up the differences in this document between datasets and tensors

```python
# 1. Log into the PyGrid gateway
# 2. Do a search of the gateway
# 3. Provision compute resources
# 4. Select a tensor from the list and start working
```

If additional permissions are needed to select a dataset for training, the data scientist may request permission right in their Jupyter Notebook before continuing on.

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

It's important for a data compliance officer to have control over what data leaves their system. This person's primary job is to read through a model trained on the system, look at the effect that training the model had on their system's privacy leakage, and then determine whether or not the release of this trained model should be allowed. It's also worth nothing that a data scientist who makes a `get()` request for a dataset that exceeds their alotted privacy budget will be automatically denied.

TODO: We need to flesh out this section further

## Projects

### PyGrid

- [Hello world](https://google.com)

### PySyft

- [Hello world](https://google.com)

### PyGrid Admin UI

- [Hello world](https://google.com)
