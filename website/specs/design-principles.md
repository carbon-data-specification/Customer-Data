---
layout: base
title: Design Principles
meta_description: These are the various design principles we want to keep in mind when writing our specifications
---
[Home]({{ "/" | relative_url }}) / [Specifications]({{ "/specs" | relative_url }}) / Design Principles

# CDSC-WG1 Design Principles

As we write, discuss, and publish our [specifications]({{ '/specs' | relative_url }})
for how to provide streamlined customer data access to address our target
[Use Cases]({{ '/use-cases' | relative_url }}), we will follow several design
principles that help guide our choices as a working group.

#### Table of Contents

* [Principle 1: Be Accessible](#be-accessible)
  * [Make specifications free and easily referenced](#freely-accessible)
  * [Make ample complementary documentation and materials](#ample-documentation)
  * [Make APIs and data structures easily understood by humans](#human-readable)
* [Principle 2: Be Useful](#be-useful)
  * [Focus on end users](#focus-on-end-users)
  * [Include sanity checks](#sanity-checks)
  * [Write open source test suites](#test-suites)
* [Principle 3: Be Realistic](#be-realistic)
  * [Don't assume a motivated implementer](#dont-assume-motivated-implementer)
  * [Create materials and guidance for regulators](#regulatory-guidance)
* [Principle 4: Be Adaptable](#be-adaptable)
  * [Build in flexibility](#build-in-flexibility)
  * [Encourage feedback and contributions](#encourage-feedback)
  * [Regularly review and update](#regularly-review-and-update)

---

## Principle 1: Be Accessible <a id="be-accessible" href="#be-accessible" class="permalink">🔗</a>

The carbon and energy transition sectors have and will, for the foreseeable
future, experience massive growth. This means those working on our target
[Use Cases]({{ '/use-cases' | relative_url }}) will generally always have
more new people than experienced people.

Given this bias towards new users, we must design our materials with a focus
on making it easy for new users to learn our specifications. This principle is
prioritized over following established precedents when those prior precedents
are not accessible to new users.

Below are some specific guidelines of how this principle manifests in our
working group:

### Make specifications free and easily referenced <a id="freely-accessible" href="#freely-accessible" class="permalink">🔗</a>

Our [specifications]({{ '/specs' | relative_url }}) will be published online for
free and can be viewed by anyone without registration or payment.

Additionally, each section of specifications and documentation will have permalinks,
so that users can directly link to the specific part that they want to reference.

### Make ample complementary documentation and materials <a id="ample-documentation" href="#ample-documentation" class="permalink">🔗</a>

By definition, our specifications must be comprehensive and, well, _specific_.
This unfortunately means that the specifications themselves are complex and are
probably not the most immediately readable thing for a new user.

So, in addition to publishing our official specifications, we must make an effort
to complement them with additional documentation and other materials that help
introduce new users to the specifications, answer common questions, and provide
examples and tutorials.

### Make APIs and data structures easily understood by humans <a id="human-readable" href="#human-readable" class="permalink">🔗</a>

Before a new user writes any client integration, they will typically first
explore the documentation, examples, and tutorials to try to get familiar
with how the various APIs, data models, and behaviors are structured. We want
this initial exploring experience to be intuitive and require minimal time to
get a basic understanding of how things work.

To aid in that effort, we will be preferring simple, easy-to-understand, and
human-readable field names and enumerations in our data models and API endpoints.
This strategy prevents new users during their initial exploration from constantly
having to go back and look up what various values mean. A new user should not
have to write a line of code or install a mapping/lookup tool to achieve a basic
familiarity with our specifications.

Examples of preferred naming conventions:
* `"id": "123456"` is preferred over `"objectEntryId": "123456"` (this is an unnecessarily complex field name)
* `"bill_total_cost": 100.25` is preferred over `"BILL_FIELD_004": 100.25` (where `"BILL_FIELD_004"` is mapped to bill total cost in a reference table)
* `"unit": "kwh"` is preferred over `"unit": 14` (where `14` is mapped to kilowatt hours in an enum table)
* `"updated": "2023-01-01T00:00:00Z"` is preferred over `"updated": 1672531200` (ISO times are more readable than unix timestamps)

---

## Principle 2: Be Useful <a id="be-useful" href="#be-useful" class="permalink">🔗</a>

Our goal is to have our specifications be adopted and used widely to address
our target [Use Cases]({{ "/use-cases" | relative_url }}). This means we must
write our specifications in such a way that when implmented will actually be
useful to the target organizations, communities, regulators, and stakeholders.

Below are some strategies we will be using to ensure our specifications are useful:

### Focus on end users <a id="focus-on-end-users" href="#focus-on-end-users" class="permalink">🔗</a>

Our specifications will define how a server must operate so that a client user
can integrate with it to access customer data, as well as how customers will
interact with the server to review and approve data access requests from client
users.

In this situation, a common risk is to start losing track of the needs and
preferences of the end users and trend towards biasing design decisions towards
the preferences and conveniences of the server implementers and operators,
even when those decisions reduce the usefulness or user-friendliness to end
users (both third parties and utility customers).

To mitigate this risk we must structure our discussion and decision making
process with end user preferences as having priority over server implementer
preferences. As with many things, decisions will be a balancing act of
interests, but we must always evaluate our decisions with a preference to
accomodating the end users' needs wherever possible.

### Include sanity checks <a id="sanity-checks" href="#sanity-checks" class="permalink">🔗</a>

Another common risk when writing specifications is losing track of the needs
and preferences of the majority of end users because much of the time in
writing specifications is thinking about how to handle edge cases. If we are
not careful, we could end up with specifications the overly focus on edge
cases and not the primary user stories.

To mitigate this risk, we must include in our discussions and processes
"sanity checks" where we take a step back and re-evaluate our current drafts
and decisions against the common use cases and user stories we are trying
to address. These sanity checks can help us recognize when we are starting
to lose track of our main target users' experiences.

Sanity checks can include the following exercises:
* Writing down a specific user story that is a target use case and evaluating it against our specifications
* "Play testing" where we discuss, simulate, or act out a situation that represents a common use case scenario
* Testing out demo or even real-world server implementations for ease of use for end users

### Write open source test suites <a id="test-suites" href="#test-suites" class="permalink">🔗</a>

In the same spirit of performing sanity checks for our specifications,
we must also remember that our specifications will be implemented in the
real world and used by real users.

To ensure that server implementations in the real world match our
specifications, we must additionally develop a suite of both automated
and manual tests that can be performed against demo and production
server implementations to evaluate how closely they follow our
specifications and how useful they are for end users.

These test suites must be freely available, including access to any source
code for automated test suites, under open source licenses. By being
transparent with our testing procedures, both end users and server
implementers can inspect and suggest improvements to the various test
suites that we will maintain.

---

## Principle 3: Be Realistic <a id="be-realistic" href="#be-realistic" class="permalink">🔗</a>

The carbon accounting and energy industries are huge, complicated, and
have a large diversity of regulatory constructs and business models.
Sometimes, major groups and incentives in these industries will not
necessarily align with our goals and [Use Cases]({{ '/use-cases' | relative_url }}).

There could very well be significant resistance to implementations
of our specifications, because some organizations, utilities, and
potentially even entire sectors are incentivized in ways that are at odds
with our goals and use cases.

Therefore, we must be realistic about the policy environment and real
world incentives when designing our specifications, so that they will still
be widely adopted and useful to our use cases. Below are some specific
actions we must take to successfully navigate the energy landscape.

### Don't assume a motivated implementer <a id="dont-assume-motivated-implementer" href="#dont-assume-motivated-implementer" class="permalink">🔗</a>

In some jurisdictions, it is possible that a utility may be ordered
to implement our specifications by their regulator, despite the
utility's objections and resistance.

In these situations, the server operator (e.g. the utility) will be
tasked with creating an implementation of our specifications even
though they are not strongly incentivized to make it highly useful.

We must design our specifications with the realistic point of view
that it may need to be implemented by organizations that are not
strongly motivated to create a highly useful implementation, or are
even "acting in bad faith" when implementing our specifications in
an attempt to, indirectly or actively, prevent the implementation
from gaining adoption or reaching its full potential.

### Create materials and guidance for regulators <a id="regulatory-guidance" href="#regulatory-guidance" class="permalink">🔗</a>

The energy utility sector is typically regulated by local, state,
and federal governments, which means that many server implementers
will be utilities or other central authorities who need to get
approval from their regulators before implementing our specifications.

To assist in educating, facilitating, and streamlining these
regulatory requests for implementing our specifications, we must
create regulatory informational and guidance materials the focus
on regulatory and governance bodies as the target audience.

This category is similar the first design principle's guideline
of [creating ample complementary documentation](#ample-documentation),
only for the purpose of increasing accessibility for regulators and
policy makers.

---

## Principle 4: Be Adaptable <a id="be-adaptable" href="#be-adaptable" class="permalink">🔗</a>

The energy and carbon accounting sectors are constantly evolving,
with new technologies, methods, and requirements emerging frequently.
To ensure the longevity and relevance of our specifications, we must
design them to be adaptable and responsive to changes in these sectors.

### Build in flexibility <a id="build-in-flexibility" href="#build-in-flexibility" class="permalink">🔗</a>

We must design our specifications to be flexible and extensible, allowing
for the addition of new features and functionality over time without
requiring significant changes to existing implementations (i.e. try
to be backwards compatible). This includes using modular designs and
providing clear guidance on how extensions can be integrated into
the core specifications.

### Encourage feedback and contributions <a id="encourage-feedback" href="#encourage-feedback" class="permalink">🔗</a>

We must promote an open and inclusive community that encourages
feedback and contributions from a wide range of stakeholders. By
actively soliciting input and engaging with different perspectives,
we can ensure that our specifications remain relevant and useful in
a changing landscape.

### Regularly review and update <a id="regularly-review-and-update" href="#regularly-review-and-update" class="permalink">🔗</a>

We must establish a process for regular review and updates to the
specifications to ensure they remain aligned with the latest
developments in the energy and carbon accounting sectors. This
includes monitoring changes in related standards and best practices,
as well as incorporating feedback from the user community.
