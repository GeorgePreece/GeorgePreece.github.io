---
layout: "article"

title: "Architecture Decision Records"
description: "Learn how to document architecturally-significant decisions and why it is crucial for development teams"
author: "George Preece"
category: article
tags: architecture
---
# Architecture Decision Record
Coined by Michael Nygard, an Architecture Decision Record (or ADR, for short) is a lightweight artefact capturing the motivation behind an architecturally-significant decision. The reasoning for decisions is not always apparent, and this often leads developers into a rabbit hole of exploration and questions. Better clarity behind these decisions helps align development teams toward the desired architecture.

ADRs address architecturally-significant requirements. The project team should define what they consider architecturally significant, however, a good rule of thumb is: if the decision is costly/expensive to unwind, it is significant. Nygard summarised architecturally-significant decisions as those that affect either:
- **the structure**; such as choosing a distributed architecture style over a monolithic one
- **non-functional characteristics**; software quality attributes such as usability, reliability, performance or supportability
- **dependencies**; such as choosing which webserver framework to use
- **interfaces**; such as public REST/SOAP APIs
- or **construction techniques**; such as the language of choice for building the software