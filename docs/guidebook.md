# Sercus Guidebook

## Overview

Sercus is a service registry manager (SRM).
You can think of it as a CRM where you track services instead of customers.

Incidentally this project has nothing to do with the French Commune by the same name.

## Context

Required: Yes

The context section should answer the following types of questions:

    What is this software system all about?
    What is it that’s being built?
    How does it fit into the existing environment? (e.g. systems, business processes, etc)
    Who is using it? (users, roles, actors, personas, etc)

Typically this is accomplished through the use of a context diagram with a supporting explanation.

## Functional Overview

* plugins
    * support for SSO
    * support for service discovery via github repo config file `.sercus.yml`
* a directory of all applications running in the ecosystem
    * what is the current health
    * who manages it
    * where is the documentation (guidebook, readme, runbook, etc.)
    * what version are we running
    * links to monitoring dashboards
    * links repos(s)
    * what are the relationships between the applications (plus the ability to generate dependency graphs in the eco-system)
* an audit log of every deployment in every environment
    * who deployed it
    * who wrote the change that was deployed
    * when it happened
    * git sha
    * docker image sha
    * link to the log of the actual deployment
* the ability to “reserve” an application+environment for testing
* reminders for when architectural and security reviews should be performed
* queue tickets / pr’s for manual deployment

## Quality Attributes

Required: Yes

While the functional overview section summarizes the functionality, this section describes the quality attributes/non-functional requirements. This section is about summarising the key quality attributes and should answer the following types of questions:

    Is there a clear understanding of the quality attributes that the architecture must satisfy?
    Are the quality attributes SMART (specific, measurable, achievable, relevant and timely)?
    Are they unrealistic?
    Are any explicitly marked as being out of scope?

Core

    Availability: a property of software that it is there and ready to carry out its task when you need it to be
    Interoperability: the degree to which two or more systems can usefully exchange meaningful information via interfaces in a particular context. The definition includes not only having the ability to exchange data (syntactic interoperability) but also having the ability to correctly interpret the data being exchanged (semantic interoperability)
    Modifiability: about change and our interest in it centers on the cost and risk of making changes. Consider:
        What can change?
        What is the likelihood of the change?
        What is the change made and who makes it?
        What is the cost of the change?
    Performance: it is about time and the software system’s ability to meet timing requirements. When events occur—interrupts, messages, requests from users or other systems, or clock events marking the passage of time—the system, or some element of the system, must respond to them in time
    Security: a measure of the system’s ability to protect data and information from unauthorized access while still providing access to people and systems that are authorized
    Testability: the ease with which software can be made to demonstrate its faults through (typically execution-based) testing
    Usability: how easy it is for the user to accomplish the desired task and the kind of user support the system provides

Additional

    Portability: a special form of modifiability. Portability refers to the ease with which software that was built to run on one platform can be changed to run on a different platform
    Development Distributability: the quality of designing the software to support distributed software development
    Scalability: Two kinds of scalability are horizontal scalability and vertical scalability. Horizontal scalability (scaling-out) refers to adding more resources to logical units, such as adding another server to a cluster of servers. Vertical scalability (scaling-up) refers to adding more resources to a physical unit, such as adding more memory to a single computer.
    Deployability: how an executable arrives at a host platform and how it is subsequently invoked
    Mobility: the problems of movement and affordances of a platform (e.g., size, type of display, type of input devices, availability and volume of bandwidth, and battery life)
    Monitorability: the ability of the operations staff to monitor the system while it is executing

## Constraints

Required: Yes

Software lives within the context of the real-world and the real-world has constraints. Examples of constraints to consider:

    Time, budget and resources.
    Approved technology lists and technology constraints.
    Target deployment platform.
    Existing systems and integration standards.
    Local standards (e.g. development, coding, etc).
    Public standards (e.g. HTTP, SOAP, XML, XML Schema, WSDL, etc).
    Standard protocols.
    Standard message formats.
    Size of the software development team.
    Skill profile of the software development team.
    Nature of the software being built (e.g. tactical or strategic).
    Political constraints.
    Use of internal intellectual property.
    etc

Note that this section specifically deals with constraints that are enforced upon the system, which is different than principles that guide the system.

## Principles

Required: Yes

Unlike constraints, principles consists of considerations that have been asked of the system or the team decided to adopt. Examples of principles include:

    Architectural layering strategy.
    No business logic in views.
    No database access in views.
    Use of interfaces.
    Always use an ORM.
    Dependency injection.
    High cohesion, low coupling.
    Ensure all components are stateless
    Prefer a rich domain model.
    Prefer an anemic domain model.
    Always prefer stored procedures.
    Never use stored procedures.
    Don’t reinvent the wheel.
    Common approaches for error handling, logging, etc.

We have existing standards and best practices. You should link to those documents rather than restating them in your guidebook when possible.

## Software Architecture

Required: Yes

What information should be included in this section?

The software architecture section is your “big picture” view and allows you to present the structure of the software. This section should not address implementation details such as infrastructure choices. You should answer the following questions:

    What does the “big picture” look like?
    Is it clear how the system works from the “30,000-foot view?”
    Does it show the major containers and their interactions (which protocols are being used)?
    Does it show the major components and their interactions?
    What are the key internal interfaces? (e.g. a web service between your web and business tiers)

What should this section look like?

Container and component diagrams should be the main focus of this section. These diagrams should be followed by a short description of elements that may require additional explanation.

Sometimes UML sequence or collaboration diagrams showing component interactions can be a useful way to illustrate how the software satisfies the major use cases/user stories/etc. Only do this if it adds value; resist the temptation to describe how every use case/user story works.

## Data

### .secrus.yml Specification

```yaml
schema: v1
name: shopping-api
description: |
    ...
repo: github.com/...
build: jenkins...
release_strategy: blue/green
type: api
team: "ecommerce"
on_call: http://...
environments:
	- name: prd
	  aliases: production, prod
	  host: aws-eb
environment_urls:
	- prd:
		- name: api
		  url: ...
		- name: dashboard
		  url: ...
		- name: management
		  url: ...
monitoring_dashboard_urls:
	- name: primary
	  url: ...
    - name: sentry
	  url: ...
doc:
	- name: guidebook
      url: ...
	  reviewed: 2020-08-31
	- name: runbook
	  url: ...
	  reviewed: 2020-09-30
dependencies:
    - catalog-api
    - inventory-api
    - shipping-api
```

Required: No

The purpose of the data section is to record anything that is important from a data perspective, answering the following types of questions:

    What does the data model look like?
    Where is data stored?
    Who owns the data?
    How much storage space is needed for the data? (e.g. especially if you’re dealing with “big data”)
    Are there any regulatory requirements for the long term archival of business data?
    Likewise for log files and audit trails?
    Are flat files being used for storage? If so, what format is being used?

## Infrastructure Architecture

Required: Yes

This section is used to describe the physical/virtual hardware and networks on which the software will be deployed. The purpose of this section is to answer the following types of questions:

    Is there a clear physical architecture?
    What hardware (virtual or physical) does this include across all tiers?
    Does it cater for redundancy, failover and disaster recovery if applicable?
    Is it clear how the chosen hardware components have been sized and selected?
    If multiple servers and sites are used, what are the network links between them?
    Who is responsible for the support and maintenance of the infrastructure?
    Are there central teams to look after common infrastructure (e.g. databases, message buses, application servers, networks, routers, switches, load balancers, reverse proxies, internet connections, etc)?
    Who owns the resources?
    Are there sufficient environments for development, testing, acceptance, pre-production, production, etc?

## Deployment

Required: Yes

The deployment section is simply the mapping between the software (e.g. containers) and the infrastructure. This section answers the following types of questions:

    How and where is the software installed and configured?
    Is it clear how the software will be deployed across the infrastructure elements described in the infrastructure architecture section? (e.g. one-to-one mapping, multiple containers per server, etc)
    If this is still to be decided, what are the options and have they been documented?
    Is it understood how memory and CPU will be partitioned between the processes running on a single piece of infrastructure?
    Are any containers and/or components running in an active-active, active-passive, hot-standby, cold-standby, etc formation?
    Has the deployment and rollback strategy been defined?
    What happens in the event of a software or infrastructure failure?
    Is it clear how data is replicated across sites?

## Operation and Support

Required: Yes

The operations and support section allows you to describe how people will run, monitor and manage your software. This section should address the following types of questions:

    Is it clear how the software provides the ability for operation/support teams to monitor and manage the system?
    How is this achieved across all tiers of the architecture?
    How can operational staff diagnose problems?
    Where are errors and information logged? (e.g. log files, Windows Event Log, SMNP, JMX, WMI, custom diagnostics, etc)
    Do configuration changes require a restart?
    Are there any manual housekeeping tasks that need to be performed on a regular basis?
    Does old data need to be periodically archived?

Materials in this section should be cross-linked with the relevant run books.

## Development Environment

Required: No

The purpose of this section is to provide instructions that take somebody from a fresh OS install to a fully-fledged development environment capable of maintaining the software. This information is typically found within the README for specific repositories. You usually only need to include this section in a guidebook if the software consists of multiple repositories or requires other software to be set up for it to be worked on locally. The type of things you might want to include are:

    Pre-requisite versions of software needed.
    Links to software downloads (either on the Internet or locally stored).
    Links to virtual machine images.
    Environment variables, Windows registry settings, etc.
    Hostname entries.
    IDE configuration.
    Build and test instructions.
    Database population scripts.
    Usernames, passwords, and certificates for connecting to development and test services.
    Links to the build servers.
    etc

## Decision Log

Required: No

The purpose of this section is to record the major decisions that have been made, including both the technology choices and the overall architecture. For example:

    Why did you choose technology or framework “X” over “Y” and “Z?"
    How did you do this? Product evaluation or proof of concept?
    Were you forced into making a decision about “X” based upon corporate policy or enterprise architecture strategies?
    Why did you choose the selected software architecture? What other options did you consider?
    How do you know that the solution satisfies the major non-functional requirements?
    etc

Ideally, this section consists of a history of architecture decision records.

## Risks and Technical Debt

Required: No

A list of identified technical risks or technical debts, ordered by priority

## Glossary

Required: No

The most important domain and technical terms that your stakeholders use when discussing the system.

## Further Reading

* This approach is heavily influenced by the practices described in https://leanpub.com/visualising-software-architecture
* Inspiration also comes from http://arc42.org/ which offers a somewhat similar approach
