## Introduction

_Last modified: April 24th, 2020_

Allowing PyGrid to be deployed to various cloud providers is one of the key ingredients of the success of OpenMined. This means that anyone will be able to deploy private ML solutions to the cloud without having to worry about managing deployment infrastructure or configuring Docker images. Granted, we will still include the ability to deploy PyGrid to a Docker, or Docker-like, containerized environment. We will also still continue to support deployment to local area networks ("Intranet") and private cloud infrastructure primarily serving our enterprise customers. However, we hope to see the vast majority of PyGrid deployments be done to the public cloud. This will primarily involve developing PyGrid to run and scale appropriately on the following targeted cloud providers:

- Amazon Web Services
- Google Cloud Platform
- Microsoft Azure
- Heroku
- DigitalOcean

Some additional providers we'd like to support at a later point, include:

- IBM Cloud
- Alibaba Cloud
- Rackspace

These are currently ordered in terms of the perceived priority based on the requests of users and customers. Ideally, depending on the provider's support, we'd like to offer "one-click deployment" as an option from the PyGrid Github repository. This allows a person looking to try out PyGrid to easily deploy an instance to a cloud provider without any configuration. We would like for these easy deployment options to utilize a cloud provider's "free-tier" if they offer one - this crucially lowers the barrier to entry for someone just looking to get started without any initial investment.

Another requirement of cloud deployment will be the ability to provision, scale, and monitor resources. This would include the following base functionality:

- **Horizontal scaling:** The ability to add or remove PyGrid Nodes from a PyGrid Gateway
- **Vertical scaling:** The ability to increase or decrease compute resources for one or more PyGrid Nodes
- **Workload monitoring:** The ability to visually inspect which PyGrid Nodes are being utilized, their current task, and their resource utilization
- **Update software:** The ability to upgrade a given PyGrid instance to the latest release, ensuring that new features are automatically added and vulnerabilities are regularly patched

These functionalities will be possible via a rich integration into the [PyGrid Admin UI](common/pygrid_admin.md). While it will also be possible to perform these same functions in a command line interface, it's generally easier to do them visually and within context of the current resource workload.
