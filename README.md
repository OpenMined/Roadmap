# OpenMined 2020 Roadmap

This repository documents the current roadmap for the OpenMined community, organized by team and use case. This roadmap is in line with our community's mission:

**OpenMined's Mission Statement:** to make the world more privacy-preserving by lowering the barrier-to-entry to privacy-preserving technologies through free, open-source software and education.

In line with this mission, this year we will seek to accomplish the folowing goal.

**Primary 2020 Goal:** solve real privacy problems _in production_ and lower the barrier-to-entry for others to do so through software and education.

While it might seem a bit surprising for an un-incorporated entity to be pursuing production deployments and the development of open courseware, we feel that it is essential to pursue real-world deployments in the development of our software. Specifically, it's impossible to truly know whether we are writing the _right_ software without actively seeking to use it to solve someone's problem.

Furthermore, we feel that our ability to educate individuals on how to make the world more privacy-preserving is only legitimate if we ourselves are involved in actually deploying real-world use cases.

Thus, in 2020 we will seek to put our software into production and, leveraging our knowledge through experience, teach others to do so. Thus, we have two key activities for the year:

1. **Production Deployments:** we have several production use cases we will deploy within real-world enterprises, smartphone applications, and cloud platforms around the world. Pursuing these deployments will be the primary motivation behind the development tasks we pursue across development teams.

2. **Education:** In addition to creating blogs, tutorials, youtube videos, and documentation throughout the year, we will finish the year by creating a course (as a followup to our previous [Udacity Course](http://udacity.com/private-ai)) which will teach students how to deploy the same use cases we have deployed throughout the year. Additionally, this course will prepare students for an examination which will certify their ability to process private data.

# 2020 Production Deployments

Below are listed the production deployments the OpenMined community will seek to develop during 2020. They are divided into roughly 3 groups, with two deployments each: Enterprise, Smartphone, and Open Research platforms.

Each use case has several primary attributes:

- **Dev Teams:** These are the development teams within OpenMined who will be leading the development of features needed for this particular use case. Note that one dev team can contribute toward multiple use cases and multiple dev teams can be co-operating on the same use case. Note additionally that dev teams often include a mixture of members who are paid/volunteer.

- **Funding Partners:** This is the list of partner organizations and individuals who are funding the open-source development. These contributions can come in the form of funding for internal engineering talent (meaning an entity is paying their internal developers to work on the open-source components of the project), funding for developer grants (meaning an entity is sponsoring OpenMined dev team members to develop the project), or other sources of support such as cloud compute credits, marketing contributions, or pen-testing.

- **Use Case Partner:** This is the partner organization within which we will actually be deploying our sofware. For smartphone applications, this is the organization which has a smartphone app. For healthcare applications, this is the hospital network. In most cases it is ideal for this to also be one of the funding partners, but this is not a strict requirment.

- **Educational Deliverables:** Upon the completion of the use case, this is the list of instructional material which we will create to aid others in deploying versions of this usecase within their own organizations.

## Enterprise Platform Use Cases

If your mission is to make the world's use of data more privacy preserving, the best place to start is with the current processors of sensitive information such as financial or medical enterprises. In these use cases, we seek to strategically choose the first use cases which we feel the technology is plausibly ready for within 2020. Note that while there might be more impactful use-cases in the future, we are intentionally choosing to select use cases based on our beliefs about our stack's maturity.

Secondarily, we are intentionally choosing use-cases which have both a social and a profit-focused component for the participating organizations. We feel that this is an important strategy to maximise for both the impact and the repeatability of the use cases we implement. If we were to focus exclusively on the social impact, we can expect organizations would make a smaller investment and that fewer enterprises/startups would follow our lead in 2021. However, if we were to focus exclusively on profit-focused use cases, we would fail to accomplish our community's mission. Thus, we are seeking for a healthy amount of both.

- **Enterprise Use-Case 1:** Cross-Organization Model Evaluation

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team), [Security and Identity Team](https://github.com/OpenMined/Roadmap/tree/master/security_and_identity_team)

  - Funding Partners: TBD - Apply Here

  - Use Case Partner: TBD - Apply Here

  - Educational Deliverables:
    - Written Example Server/Client Application + Tutorial
    - End-of-year Course Module

- **Enterprise Use-Case 2:** Cross-Organization Federated Learning

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team), [Security and Identity Team](https://github.com/OpenMined/Roadmap/tree/master/security_and_identity_team), Tensorflow Team

  - Funding Partner: TBD - Apply Here

  - Use Case Partner: TBD - Apply Here

  - Educational Deliverables:
    - Written Example Server/Client Application + Tutorial,
    - End-of-year Course Module

## Smartphone Platform Use Cases

- **Smartphone Use-Case 1:** [Federated Learning with Secure Aggregation across Web & Mobile](https://github.com/OpenMined/Roadmap/blob/master/federated_learning_team/projects/model_centric_fl.md)

  - Lead Dev Team: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team)
  - Supporting Dev Teams:

    - [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team)

  - Funding Partners:

    - [PyTorch](https://pytorch.org/) (\$250K across multiple use cases)
      - [Initial Announcement](https://pytorch.org/blog/openmined-and-pytorch-launch-fellowship-funding-for-privacy-preserving-ml/)
      - [Call for Contributors](https://blog.openmined.org/announcing-the-pytorch-openmined-federated-learning-fellowships/)
      - [Announce Contributors](https://blog.openmined.org/pytorch-grant-recipients/)

  - Use Case Partner: TBD - If you would like to be the first to deploy this system within your app (and have our help to do so), please email partnerships@openmined.org.

  - Educational Deliverables:

    - Written Example FL iOS Smartphone App + Tutorial
    - Written Example FL Android Smartphone App + Tutorial
    - Written Example FL Web App + Tutorial
    - End-of-year Course Module

- **Smartphone Use-Case 2:** Consumer-Selected Third-party On-Device ML

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team)

  - Funding Partners: TBD

  - Use Case Partner: TBD

  - Educational Deliverables

    - Written Example FL iOS Smartphone App + Tutorial
    - Written Example FL Android Smartphone App + Tutorial
    - Written Example FL Web App + Tutorial
    - End-of-year Course Module

- **Smartphone Use-Case 3:** [Encrypted MLaaS (continuation of 2019 RAAIS grant)](https://blog.openmined.org/raais/)

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team)

  - Funding Partners: The RAAIS Foundation

  - Use Case Partner: United Nations Privacy Task Team

## Open Research Platform Use Cases

- **Open Research Use Case 1:** Open Model Hosting Platform

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team), Tensorflow Team, [Security and Identity Team](https://github.com/OpenMined/Roadmap/tree/master/security_and_identity_team)

  - Funding Partners: TBD

  - Use Case Partner: N/A - This will be deployed to the open internet for general use

  - Educational Deliverables

    - Tutorial/Documentation - how to host/use models on PyGrid
    - Tutorial/Documentation - How to run your own node

- **Open Research Use Case 2:** Scalable, Debuggable Compute Use Case

  - Dev Teams: [Federated Learning Team](https://github.com/OpenMined/Roadmap/tree/master/federated_learning_team), [Security and Identity Team](https://github.com/OpenMined/Roadmap/tree/master/security_and_identity_team)

  - Funding Partners: TBD

  - Use Case Partner: TBD

  - Educational Deliverables

    - Tutorial/Documentation - how to scale up compute for training ML models
    - Tutorial/Documentation - how to do remote debugging using PySyft

# Project Layout

For those interested in a visual representation of all of OpenMined's various projects and how they relate to one another, [please view the following document](https://app.lucidchart.com/invitations/accept/1158eee8-a446-4d30-906b-60abb6d993fc).
