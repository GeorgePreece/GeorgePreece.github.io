---
layout: "article"

title: "Architecture Decision Records"
description: "Learn how to document architecturally-significant decisions and why it is crucial for development teams"
author: "George Preece"
category: article
tags: architecture
---
# Architecture Decision Records
Coined by Michael Nygard, an Architecture Decision Record (ADR) is a lightweight artefact capturing the motivation behind an architecturally-significant decision. The reasoning behind decisions is not always apparent, and this often leads developers into a rabbit hole of exploration and questions. Better clarity into these decisions helps align development teams toward the desired architecture.

ADRs have proven to be valuable artefacts in the world of agile. They are concise documents with a focussed audience and intent. Generally, an ADR will describe the context, the decision itself, other solutions explored and the consequences (positive or negative) after applying the decision.

## Architecturally-Significant Requirements
ADRs address architecturally-significant requirements (ASRs). The project team should define what they consider architecturally significant, however, a good rule of thumb is: if the decision is costly/expensive to unwind, it is significant. Nygard summarised these requirements as those that affect either:
- **the structure**; such as choosing a distributed architecture style over a monolithic one
- **non-functional characteristics**; such as usability, reliability, performance or supportability (software quality attributes)
- **dependencies**; such as choosing which web server framework to use
- **interfaces**; such as public REST/SOAP APIs
- or **construction techniques**; such as the language of choice for building the software

## Getting Started

As a form of agile documentation, it is essential to consider the following core value defined in the [agile manifesto](https://agilemanifesto.org/) when assessing if you should create an ADR.

> Working software over comprehensive documentation

This value is not an excuse to produce minimal or lacking documentation but rather a reminder to consider what documentation is valuable. We could create ADRs for every decision made, but documenting all of them is not always beneficial or practical.

All teams should use a template for ADRs. Templates help guide the author, informing them of the content required to formalise the decision (almost like a definition of done). They also assist with normalisation, making them more predictable and easier to digest for the team. There are many openly-available templates, and it would be wise to start with an existing one rather than creating your own. The team can adapt the template as their ADR usage begins to mature. [Nygard's original template](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions) is a solid choice as it provides a loose and straightforward format.

ADRs should live close to the source code and be easily accessible to their primary audience (developers/architects). Two popular choices are on a project wiki or directly with the source code (in the repository). Both options work well. Just ensure you stay consistent, as this collection will serve as the decision log. A good practice for naming the artefact is to include the date (or sequence identifier) and use a concise noun phrase such as "Use Jetty web server".

Since we are documenting an architectural decision, it is crucial to provide as much clarity as possible. We should follow technical writing best practices, such as using an active voice and avoiding ambiguity. If you are unfamiliar with technical writing, I highly recommend Google's [Technical Writing One](https://developers.google.com/tech-writing/one) course. The course can be completed within a couple of hours and provides a solid foundation for producing technical documentation.