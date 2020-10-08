---
layout: post
title:  "Introduction to Enterprise Scale"
date:   2020-10-09 11:55:17 -0400
categories: azure enterprise-scale
---
I'd like to summarize the recently released Enterprise Scale architecture for Azure
The [main documentation is here](https://github.com/Azure/Enterprise-Scale)
and the [course here](https://docs.microsoft.com/en-us/learn/paths/enterprise-scale-architecture/)

Here's how I explain it:

Corporations have central IT teams that handle all the digital resources the business needs. There are developers, sysadmins, operations, helpdesk, managers, procurement, financial controllers, etc. When they decide to use the cloud, all these roles must adapt. Without central guidance, **shadow IT** and resource sprawl happens. Anyone with an expense account can consume the cloud. That wasn't possible when all IT hosted its assets within the four walls of a datacenter.

Instead of allowing chaotic consumption, Microsoft provides guidance and best practices on how to use the Azure cloud. This is called the [Cloud Adoption Framework, or CAF](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/) and it starts with the business strategy and organizational alignment (in terms of people and responsabilities). For more technical architectural guidance (ignoring the people/process part), Microsoft also has a [Well Architected Framework](https://docs.microsoft.com/en-us/azure/architecture/framework/) and it also [a training course](https://docs.microsoft.com/en-us/learn/paths/azure-well-architected-framework/)

CAF suggest a program-based approach to Cloud. The steps are **Strategy, Plan, Ready, Adopt, and in parallel, Govern and Manage**. It's like an iterative process, similar to [Total Quality Management](https://en.wikipedia.org/wiki/Total_quality_management).
Within CAF, in the Ready phase, there's **the idea of a Landing Zone, as an analogy to a modern airport**, with protocols, facilities and resources to safely and quickly receive and dispatch mission-critical workloads. CAF doesn't tell you exactly how to do to a LZ, but it's exhaustive on the what it should accomplish, in 8 [design areas](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-areas) that cover the Ready, Manage and Govern topics :
* Enterprise Enrollment
* Identity
* Network topology
* Resource Organization
* Governance Disciplines
* Operations baseline
* Business continuity and DR
* Deployment options

Here's where the Enterprise Scale comes into play. We give you up to **three (3!) starter kits to create your Landing Zones**. You should consider if you are starting from scratch (no cloud workloads) or if you have to onboard already existing resources and put them under central control. There are 3 different technologies involved as well: Azure Blueprints, Terraform, Azure ARM Templates. And some are modular and offer different networking implementation. This page has a great summary of the [Implementation Options for Landing Zones](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/implementation-options)

You should also evaluate the maturity of your IT organization, its size and level of decentralization. Here's [good guidance to compare operating models of all sizes](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/operating-model/compare)

We'll analyze the one based on ARM templates: [Enterprise Scale Landing Zone, or ESLZ](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/). Take it as reference and implement your own, as it's modular, has 3 networking options, and it can be extend it using Infrastructure-as-code. ![Enteprise Landing Zones](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/_images/operating-model/enterprise-operations.png)

Let's see why do we like the ESLZ for corporations: it has an opinionated answer to the previous 8 design areas, here are the links for a detailed explanation
* [Enterprise Agreement (EA) enrollment and Azure Active Directory tenants](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/enterprise-enrollment-and-azure-ad-tenants) enforcing MFA, PIM and break-glass accounts
* [Identity and access management](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/identity-and-access-management) with default custom roles (NetOps, SecOps), enforcing security center, etc
* [Management group and subscription organization](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/management-group-and-subscription-organization) with suggested names for management groups, how to manage subscription quotas, budgets, etc
* [Network topology and connectivity](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/network-topology-and-connectivity) recommending vWAN, but also offering alternative examples for hub-and-spoke and no-hybrid-connectivity. Check the [ESLZ github repo](https://github.com/Azure/Enterprise-Scale#deploying-enterprise-scale-architecture-in-your-own-environment) for the 3 reference implementations (so far)
* [Management and monitoring](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring) enforcing Diagnostic settings via Azure Monitor, using network watcher, audit logs, etc
* [Business continuity and disaster recovery](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/business-continuity-and-disaster-recovery) enforcing Azure Backup and Site Recovery for all production VMs
* [Security, governance, and compliance](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/security-governance-and-compliance) with default Keyvault, Azure Policy and ASC Benchmarks
* [Platform automation and DevOps](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/platform-automation-and-devops) by keeping ARM templates, dashboards, policies in a Git repository, and providing Github Actions called AzOps 

By using the ESLZ Arm Template, you can have all these resources created with a single click, and you can enable/disable certain components too.

In the next blog post I'll review the user experience when launching the ESLZ in an empty subscription on my demo Azure tenant. 


