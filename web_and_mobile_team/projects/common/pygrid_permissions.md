## Introduction

_Last modified: April 25th, 2020_

The current PyGrid system allows for tensors to be designated as public or private. It also allows those private tensors (known as `PrivateTensor` in PySyft) to be accessible by a dictionary of specified users. While this is a good rudimentary approach to the problem, as PyGrid attempts to scale into production, a more flexible system is required.

In the new permissions system, permissions may be applied to a user directly. The grid owner will specify which users have access to which private tensors. They also specify that user's privacy budget which gets updated according to each `get()` request the user makes against the gateway.

To make managing user permissions easier, the PyGrid Admin also allows you to specify "groups". Groups allow for organizing subsets of users into pre-determined permissions lists. If a user is part of a group, their permissions are determined by that of their group AND their user-specific permissions. For instance, if a group does not have access to a specific private tensor, the grid owner may decide to allow permissions for a specific user in that group to have access to the tensor, but disallow access for the other users in the group.

It's also worth nothing that there is a separate system of "roles" which strictly relate to administrative access to a PyGrid gateway. All newly created users default to the "User" role, which does not allow for any administrative access to the PyGrid Gateway or Network. The roles are described below, according to their access level from lowest to highest:

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
