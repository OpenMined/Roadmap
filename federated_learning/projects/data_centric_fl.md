## Introduction

_Last modified: July 18th, 2020_

Dynamic federated learning is one of the primary use-cases of the OpenMined ecosystem. By allowing data scientists to search for and ETL remote tensors, so they can train models on data they literally "cannot see".

In this concept, a data owner may allow a data scientist (internal to their organization, or external) to submit their model for training, all while tracking and permissioning their usage at a granular level. Doing such training does not permit the data scientist to steal the private, and often sensitive, information of the data owner. It is noteworthy that in this setting, we assume that the data owner is a trusted organization and that future extensions of this project will enable the use of encrypted computation for joint protection of the model and tensors during training.

For this process to work correctly, the data owner will place their private data inside of a PyGrid "Node" that acts as both a data store and a load balancer, distributing work to one or many PyGrid "Workers" which compute on that data. Each Worker has dedicated compute resources with which to train models on behalf of the data scientist. There is also an optional layer on top of a PyGrid Node called a PyGrid "network" that allows a user to search for available tensors across multiple Nodes under the same network. Regardless of presence of a network, a data owner may deploy their PyGrid Node either to their own privately managed servers, or to a major cloud provider like AWS, GCP, Azure, Heroku, or DigitalOcean.

The data owner can create users on their Node with a variety of preset and custom permissions, as well as designate each user's "privacy budget" (tracked via an "epsilon value") which is used to track how many `get()` requests that particular user has made. This ensures that no one user has complete access to the private tensors of the PyGrid Node, nor can they make unlimited model training requests. Permissions can be created and assigned at both the user-level and the tensor-level, allowing for smart defaults to be set, and overrides to be assigned on a case-by-case basis. Tensors can be listed as "public" or "private":

- **Public** means they're visible in a Node or Network search and available for download by any user.
- **Private** means they're visible in a Node or Network search, but are not available for download (`.get()`) by a user without additional permission. This involves filing a training or inference request.

Of course, it would be difficult to manage multiple users, permissions, and model training requests through a command line or Python notebook. This creates the need for a small user interface to be developed to aide in the management of a private PyGrid Node. We call this user interface the "PyGrid Admin" and it will serve as the secondary component of this project's roadmap. An administrator will be able to manage their entire Node through this white-labeled user interface, which will be hosted as a standalone single-page application separate from the PyGrid API itself. Developing the PyGrid Admin as a standalone front-end application allows for the PyGrid Node infrastructure to be scaled separate from the needs of running a user interface. Thus, the PyGrid Admin may be hosted on a variety of cloud-based file server platforms like AWS's S3, GCP's Cloud Storage, Microsoft's Azure Blob Storage, Netlify, or other such static asset hosting solutions.

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
- **Plan** - a serialized list of operations that can be executed by a PyGrid Worker
- **Node** - a data store and load balancer that serves as the primary public endpoint for a PyGrid network
- **Worker** - a single compute server for a PyGrid Node, where model training/inferencing takes place
- **Privacy budget** - the amount of data per user that a data compliance officer can justify leaving their system
- **Epsilon value** - the name of the value for measuring a user's privacy budget

We will also use this section for defining each of the components of the OpenMined dynamic federated learning system:

- **PyGrid** - a library consisting of multiple services that allows for "Workers" to be deployed and managed through a single "Node". This is the main project where model training requests will be sent to and private data will be hosted.
- **PySyft** - a framework for privacy-preserving machine learning that is the primary library called internally by PyGrid
- **PyGrid Admin** - a user interface (UI) for managing a PyGrid network, allowing an administrator to manage user and tensor permissions and model trainin requests by those users

## Overview

### 1. Host

To start, an individual or organization must deploy their own PyGrid network comprised of a single PyGrid Node which is responsible for hosting private data, and one or many PyGrid Workers which are responsible for performing model training. Commands may be issued to the Node, which it then delegates to the appropriate Worker. This allows for the simple management of complex networks with hundreds or thousands of Workers.

```python
# 1. Create a basic PyGrid network with a Node and multiple Workers
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

- Users are created inside of the PyGrid Node and given a base-level of permissions for querying tensors in the database.
- Data scientists will not be given any UI access in the PyGrid Admin UI, and will be required to interface with the Node or Network via a command line or Python Notebook.
- Tensors may have individual permissions set to them, such as a "public" or "private" status.
- Data scientists are given access to all public tensors and whatever private tensors an administrator permits. They will have the ability to search all tensors, regardless of their status.
- Groups may be created to make assigning permissions in batch easier.
- There are multiple other roles for various Node and Network administrators.

Generally speaking, permissions are highly flexible and can be assigned to users, groups, and tensors. Overrides are made possible in the exact same order of priortity (highest to lowest).

### 3. Search

Once PyGrid has been hosted, tensors have been uploaded, users have been created, and permissions have been set, data scientists may begin making requests to the Node. This process begins with a simple search of what tensors the data scientist may be interested in. Once they've searched the Node and have found a tensor they would like to work with, they may begin provisioning compute resources and start working.

```python
# 1. Log into the PyGrid Node
# 2. Do a search of the Node
# 3. Provision compute resources
# 4. Select a tensor from the list and start working
```

If additional permissions are needed to select a tensor for training, the data scientist may request permission right in their Jupyter Notebook before continuing on.

```python
# 1. Log into the PyGrid Node
# 2. Do a search of the Node
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

If the the data compliance officer agrees that the privacy leakage is appropriate, they can choose to fulfill the `get()` request and release the trained model back to the data scientist. This is done through the PyGrid Admin UI. Optionally, they may choose to deny this request and the data scientist will be notified of the decision. Currently, the way this decision is communicated between the data compliance officer and the data scientist is arbitrary and determined by the individual relationship of those two individuals. It's outside the scope of this roadmap to prescribe a communication protocol for these individuals. Privacy budgeting is discussed at [much greater detail here](common/privacy_budgeting.md).

## Projects

We currently have the following project "unknowns":

- How will we be implementing privacy budgeting?
- What information should a data compliance officer be able to view related to differential privacy in order to make informed decisions?
- How will search be performed given changes in our roadmap?
- How will user and tensor permissions be affected given changes in our roadmap?

### PyGrid

#### Reorganization

- [Move dynamic FL manager from PyGridNode to PyGrid](https://github.com/OpenMined/PyGrid/issues/595)
- [Allow PyGrid to manage workers on remote machines](https://github.com/OpenMined/PyGrid/issues/596)
- [Create a abstract manager class for both static and dynamic FL](https://github.com/OpenMined/PyGrid/issues/597)
- [Move database to be associated with the Node, instead of the Worker](https://github.com/OpenMined/PyGrid/issues/598)
- [Namespace all the API endpoints by their intentions](https://github.com/OpenMined/PyGrid/issues/600)
- [Combine Network, Node, and Worker to create a monorepo](https://github.com/OpenMined/PyGrid/issues/611)

#### General

- **TODO**
- Redo search logic to allow for searching across Datasets and Tensors within _(depends on database modeling and API for grid admin issues below)_

#### Database modeling

- [Node: Create a data model for Users object](https://github.com/OpenMined/PyGrid/issues/630)
- [Node: Create a data model for Roles object](https://github.com/OpenMined/PyGrid/issues/631)
- [Node: Create a data model for Groups object](https://github.com/OpenMined/PyGrid/issues/632)
- Node: Create a data model for Tags object
- Node: Create a data model for Datasets object
- Node: Create a data model for Permissions object
- Node: Create a data model for JobRequests object
- Node: Create a data model for AssociationRequests object
- Node: Create a data model for Statistics object
- [Network: Create a data model for Users object](https://github.com/OpenMined/PyGrid/issues/638)
- [Network: Create a data model for Roles object](https://github.com/OpenMined/PyGrid/issues/637)
- Network: Create a data model for AssociationRequests object

#### API for Grid Admin

- [Node: Create API endpoints for user CRUD operations](https://github.com/OpenMined/PyGrid/issues/633)
- [Node: Create API endpoints for role CRUD operations](https://github.com/OpenMined/PyGrid/issues/634)
- [Node: Create API endpoints for group CRUD operations](https://github.com/OpenMined/PyGrid/issues/635)
- Node: Create API endpoints for tag CRUD operations
- Node: Create API endpoints for datasets CRUD operations
- Node: Create API endpoints for permissions CRUD operations
- Node: Create API endpoints for job requests CRUD operations
- Node: Create API endpoints for association requests CRUD operations
- Node: Create API endpoints for statistics CRUD operations _(only readable by Grid Admin users or Networks with a valid association)_
- Node: Create API endpoints for infrastructure scaling operations
- [Network: Create API endpoints for user CRUD operations](https://github.com/OpenMined/PyGrid/issues/639)
- [Network: Create API endpoints for role CRUD operations](https://github.com/OpenMined/PyGrid/issues/640)
- Network: Create API endpoints for association requests CRUD operations
- Network: Create API endpoints for statistics CRUD operations _(only readable on Nodes with a valid association)_

#### Privacy budgeting

- **TODO**

#### Cloud deployment

- [Node: Deploy serverfull environment on AWS](https://github.com/OpenMined/PyGrid/issues/642)
- [Worker: Deploy serverfull environment on AWS](https://github.com/OpenMined/PyGrid/issues/643)
- [Node: Deploy serverless environment on AWS](https://github.com/OpenMined/PyGrid/issues/644)
- [Add, remove, and modify Workers on a Node for AWS](https://github.com/OpenMined/PyGrid/issues/657)
- [Network: Deploy serverfull environment on AWS](https://github.com/OpenMined/PyGrid/issues/645)
- [Network: Deploy serverless environment on AWS](https://github.com/OpenMined/PyGrid/issues/646)
- [Node: Deploy serverfull environment on GCP](https://github.com/OpenMined/PyGrid/issues/647)
- [Worker: Deploy serverfull environment on GCP](https://github.com/OpenMined/PyGrid/issues/648)
- [Node: Deploy serverless environment on GCP](https://github.com/OpenMined/PyGrid/issues/649)
- [Add, remove, and modify Workers on a Node for GCP](https://github.com/OpenMined/PyGrid/issues/658)
- [Network: Deploy serverfull environment on GCP](https://github.com/OpenMined/PyGrid/issues/650)
- [Network: Deploy serverless environment on GCP](https://github.com/OpenMined/PyGrid/issues/651)
- [Node: Deploy serverfull environment on Azure](https://github.com/OpenMined/PyGrid/issues/652)
- [Worker: Deploy serverfull environment on Azure](https://github.com/OpenMined/PyGrid/issues/653)
- [Node: Deploy serverless environment on Azure](https://github.com/OpenMined/PyGrid/issues/654)
- [Add, remove, and modify Workers on a Node for Azure](https://github.com/OpenMined/PyGrid/issues/659)
- [Network: Deploy serverfull environment on Azure](https://github.com/OpenMined/PyGrid/issues/655)
- [Network: Deploy serverless environment on Azure](https://github.com/OpenMined/PyGrid/issues/656)

### Grid Admin

#### Design

- Design login page
- Design dynamic FL users and groups page
- Design dynamic FL datasets page
- Design dynamic FL queue page
- Design pages for management of Node
- Design pages for management of Network
- Design a page for creating, deleting, and triaging association requests
- Design a page for viewing Node statistics
- Design static FL overview page
- Design static FL models and plans page

#### Development

- Need to scaffold out the initial web application
- Create basic PyGrid API connection class
- Add user-gating logic for authenticated screens
- Add login page
- Add main naviation
- Add dynamic FL users and groups page
- Add dynamic FL datasets page
- Add dynamic FL queue page
- Add page for management of Node
- Add page for management of Network
- Add page for creating, deleting, and triaging association requests
- Add page for viewing Node statistics
- Add static FL overview page
- Add static FL models and plans page

### PySyft

#### Reorganization

- [Move node_client (dynamic FL) to grid folder and rename as dynamic_fl_client](https://github.com/OpenMined/PySyft/pull/3818)
- [Rename grid_client (static FL) as static_fl_client](https://github.com/OpenMined/PySyft/pull/3818)
- [Move the static FL worker in PySyft out of the grid folder, put it in the workers folder, and rename it static_fl_worker](https://github.com/OpenMined/PySyft/pull/3818)

#### Privacy budgeting

- **TODO**
