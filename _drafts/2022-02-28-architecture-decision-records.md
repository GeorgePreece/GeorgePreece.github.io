---
layout: "article"

title: "Architecture Decision Records"
description: "Learn how to document architecturally-significant decisions and why it is crucial for development teams"
author: "George Preece"
category: article
tags: architecture
---
# Architecture Decision Records
[Coined by Michael Nygard](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions), an Architecture Decision Record (ADR) is a lightweight artefact capturing the motivation behind an architecturally-significant decision. The reasoning behind decisions is not always apparent, and this often leads developers into a rabbit hole of exploration and questions. Better clarity into these decisions helps align development teams toward the desired architecture.

ADRs address architecturally-significant requirements. The project team should define what they consider architecturally significant, however, a good rule of thumb is: if the decision is costly/expensive to unwind, it is significant. Nygard summarised these requirements as those that affect either:
- **the structure**; such as choosing a distributed architecture style over a monolithic one
- **non-functional characteristics**; such as usability, reliability, performance or supportability (software quality attributes)
- **dependencies**; such as choosing which web server framework to use
- **interfaces**; such as public REST/SOAP APIs
- or **construction techniques**; such as the language of choice for building the software

It is essential to understand that ADRs are a form of agile documentation, and the [agile manifesto](https://agilemanifesto.org/) defines the following core value.

> Working software over comprehensive documentation

This value is not an excuse to produce minimal documentation but rather a reminder to consider what documentation is valuable. We can create ADRs for numerous decisions, but documenting all of them is not always beneficial or practical. Again, it is for the team to decide what they consider significant.

## Creating an ADR
All teams should use a template for ADRs. Templates help guide the author, informing them of the content required to formalise the decision (almost like a definition of done). They also assist with normalisation, making them more predictable and easier to digest for the team. 

There are many openly-available templates out there. I would highly recommend starting with an existing template rather than creating your own. The team can adapt the template as their ADR usage begins to mature. 

Another decision the team should align on is where these records are stored. ADRs should live close to the source code and easily accessible to anyone who needs access. Two popular choices are on a project wiki or directly with the source code (in the repository). Both options work well. Just ensure you stay consistent as this collection will serve as the decision log.