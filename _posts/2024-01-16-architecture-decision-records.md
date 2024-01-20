---
layout: "article"

title: "Architecture Decision Records"
description: "Explore the role of Architecture Decision Records (ADRs) in Agile development, as they guide key architectural decisions"
author: "George Preece"
category: articles
tags: architecture
---

The use of Architecture Decision Records (ADRs) is a popular practice in Agile software development. ADRs are concise artefacts capturing the motivation behind key decisions that impact a system's architecture.

The concept of an ADR is attributed to Michael Nygard, who introduced it in his blog post [Documenting Architecture Decisions](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions). If you haven't already, I would strongly recommend reading it first, as my article aims to expand on Nygard's introduction with my own experience and views.

![image tooltip here](/images/4c3347e9-eaec-472c-ada8-7f03f01e8ac5.webp)

## Agile Documentation
ADRs are widely considered an Agile practice because they are **incremental and iterative** by nature. Once a decision is recorded, the ADR becomes immutable. If we want to reverse a decision, we supersede it with a new one. As you might envision, this results in a history of decisions effectively documenting a system's architectural evolution over time. Pretty cool, right?

In Agile development, we strive to favour working software over comprehensive documentation and ADRs align well with this. ADRs are designed to be **concise**, leading to a quick draft and review. Moreover, much like the dynamics of pull requests, the clearer and concise they are, the higher the likelihood of active engagement and collaboration within the team.

When we create an ADR, we capture not just the decision, but the **motivation**. I love using this word — motivation — to describe an ADR. It emphasises the "why" behind the decision. How many times have you worked on a system and found yourself wondering, "Why on earth was it designed this way?" That moment of perplexity is exactly what an ADR aims to prevent. This understanding will also support future decisions and onboarding new engineers.

### Architectural Significance
ADRs typically address Architecturally Significant Requirements (ASRs). ASRs are the critical, non-negotiable elements that influence our system's architecture. One challenge here is that "significant" can be subjective, which oftens lead to misalignment within project teams. Consequently, this may result in either the creation of too many records or too few; therefore, team alignment on this aspect is crucial. 

Nygard defined "architecturally-significant" decisions as those that affect the: 
- **structure** such as defining layers or deciding between distributed or monolithic systems. These decisions often impact the overall layout, organisation and communication within a system.
- **non-functional characteristics** such as deciding to make an operation asynchronous or using an ACID-compliant database. These decisions usually have a notable effect on software quality.
- **dependencies** such as building around a framework/library or integrating with an external service. These decisions are quite costly to reverse and sometimes impact supportability and autonomy.
- **interfaces** such as exposing or concealing a REST API. These decisions have an immediate downstream impact and typically require time for documentation and support.
- **construction techniques** such as introducing a Domain-Specific Language (DSL) or adopting containerisation. These decisions impact development and deployment workflows.

I like this definition because it encapsulates critical areas that shape the overall architecture without being too specific.

## Anatomy
Now that we've explored the need for and intention of ADRs, let's dive into their structure and the essentials for writing one.

### Title
As with any other documentation, we begin with the title. Often, the title is the only part that people will read, so it's crucial to keep it informative and concise. Nygard recommends prefixing the title with an incrementing number to define the order, followed by a short noun phrase. For example: 

> ADR 001: GraphQL for Account Services

### Status
If it wasn't clear already, ADRs are intended for submission and review. That is, they have an approval process. This section, describing the current state, was originally placed below the decision. Personally, I think it should be positioned at the top of the document, right below the title, or arguably even added to the title itself.

Either way, this section needs to capture the proposal status. While Nygard suggested four possible values, I prefer to use `draft`, `proposed`, `accepted`, `rejected` and `superseded`. I think the `draft` status is particularly useful when multiple contributors are involved in writing the ADR. `superseded` is used when an old ADR is replaced with a new one, in which a link to the new ADR should be provided for reference. The other statuses should be self-explanatory.

Another useful addition to this section is the inclusion of stakeholders. This typically includes the architect, the development team, the product owner and other teams impacted by the decision. 

### Context
In this section we describe the ASRs along with other influences such as politcal, social and technical contraints (time being a common example). Our primary goal here is to articulate the reasons prompting a shift in our architectural strategy. These motivations can originate from many sources such as new customer requirements or unexpected system usage. 

When drafting this section, a common issue I see is a clear bias towards a specific proposal. This bias undermines our goal of achieving the best outcome while highlighting an unwillingness to collaborate. Instead, stay impartial when descibring the context. Describe the overarching problem, not just the aspects that your solution addresses. Even if that particular solution is the ideal way forward, it allows us to evaluate all options objectively and reach the best possible outcome. Here's an example of an ineffective context, see if you can spot the bias:

> In our initial design, we used a REST API to expose our Account Services. However, following recent service enhancements such as transaction tracking, customers need to retrieve from multiple data sources in a single request. These round-trip requests have resulted in a 15% increase in running costs.

In the above context "customers need to retrieve from multiple data sources in a single request" introduces a strong bias towards a solution which supports folding these requests. From this context alone, a GraphQL API sounds like a clear winner, right? Now let's take a look at a context which is less biased towards a specific approach:

> In our initial design, we used a REST API to expose our Account Services. However, following recent service enhancements, we've observed a surge in running costs (15% increase). After discussing with consumers, they suggested they were trying to use the APIs to monitor Account activity.

Hopefully this example highlights the issue with bias. A pub-sub API doesn't even feel relevant in the first example, but in the second it almost seems favourable. Although a GraphQL API may still resolve the inherent issue of increased API costs.

### Decision
Next we need to document the decision itself. Nygard suggests we use full sentences and active voice. I like this approach because it removes ambiguity, telling the reader exactly what it is we are doing. We also need to capture the justification: How does this approach satisfy the requirement? Why have we chosen this particular solution over the other options we explored?

> We will adopt GraphQL as the primary data query language for our Account Services and gradually phase out RESTful endpoints. By reducing round-trip requests, GraphQL lowers running costs and offers more flexibility to consumers.  
> 
> Initially, we thought about implementing a pub-sub API, as it might be more efficient given the customer's usage. However, choosing GraphQL not only addresses the immediate problem but also sets the stage for a more modern API suite. If we need a pub-sub API later, this decision will not pose any conflicts.

Sometimes, the decision we propose is quite complex or difficult to understand. In these scenarios, a supporting diagram can speak a thousand words! Just ensure that it only depicts information or concepts related to the decision to avoid confusion.

### Consequences
As we know in architecture, every decision comes with its own set of trade-offs. This section is dedicated to exploring both the positive and negative outcomes of our choice. Personally I don't like the term "consequences" as it often carries a negative connotation, primarily suggesting adverse outcomes. To offer a more balanced perspective, a better title for this section in my opinion would be "Key Considerations". This title feels more neutral but also conveys that these aspects have been thoughtfully considered as part of our proposal.

Teams often opt to categorise these outcomes as "pros" and "cons". I dislike this approach because once again it introduces inherent biases. A "pro" to you very well might be a "con" to me. It also fosters a single dimensional thought process, where decisions are made based on the ratio of pros and cons.

> - Improved performance due to reduced API calls, with attention needed for optimising complex queries.
> - Significant backend adjustments required, with a focus on stability during transition and more complex ongoing maintenance
> - Enhanced client flexibility in data requests, necessitating a solid understanding of GraphQL from client-side developers
> - Challenges in integrating GraphQL with systems optimised for RESTful interactions, potentially requiring refactoring
> - A steep learning curve for the development team, leading to initial slowdowns but long-term benefits in adaptability
> - Need for effective management of complex queries to prevent performance bottlenecks
> - Strategic move for long-term API suite enhancement and scalability, with less immediate but important future considerations

## Conclusion
Valueless documentation has long been an issue in Agile development. ADRs align with Agile principles by iteratively documenting the key decisions and motivations leading to architectural shifts. The concise nature of ADRs also encourages better engagement and collaboration from others. However, it's important to ensure these proposals are purposeful by remaining unbiased and open-minded, allowing the team to review and agree on the best outcome.

```md
# ADR 001: GraphQL for Account Services
Status: Proposed
Stakeholders: George Preece, Jane Doe

## Context
In our initial design, we used a REST API to expose our Account Services. However, following recent service enhancements, we've observed a surge in running costs (15% increase). After discussing with consumers, they suggested they were trying to use the APIs to monitor Account activity.

## Decision
We will adopt GraphQL as the primary data query language for our Account Services and gradually phase out RESTful endpoints. By reducing round-trip requests, GraphQL lowers running costs and offers more flexibility to consumers.  

Initially, we thought about implementing a pub-sub API, as it might be more efficient given the customer's usage. However, choosing GraphQL not only addresses the immediate problem but also sets the stage for a more modern API suite. If we need a pub-sub API later, this decision will not pose any conflicts.

## Key Considerations
- Improved performance due to reduced API calls, with attention needed for optimising complex queries.
- Significant backend adjustments required, with a focus on stability during transition and more complex ongoing maintenance
- Enhanced client flexibility in data requests, necessitating a solid understanding of GraphQL from client-side developers
- Challenges in integrating GraphQL with systems optimised for RESTful interactions, potentially requiring refactoring
- A steep learning curve for the development team, leading to initial slowdowns but long-term benefits in adaptability
- Need for effective management of complex queries to prevent performance bottlenecks
- Strategic move for long-term API suite enhancement and scalability, with less immediate but important future considerations
```