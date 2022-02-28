---
layout: base
nav: use_cases
title: Use Cases
meta_description: What are the use cases that the Customer Data specifications this working group is trying to address?
---
# Use Cases

These are the use cases that this working group is writing specifications to address.


## Use Case 1: Carbon Accounting <a id="use-case-carbon-accounting" href="#use-case-carbon-accounting" class="permalink">🔗</a>

Many companies, organizations, and governments around the world are working to
measure and track their carbon emissions. This is called
[carbon accounting](https://en.wikipedia.org/wiki/Carbon_accounting).

While carbon accounting analyses vary widely, most of these procedures
for calculating carbon emissions involve obtaining customer utility data,
such as electric and natural gas usage, meter locations, rate plans, etc.

#### Needs:

* **Standardized Data Formats and Access Procedures:**
This data often needs to be gathered both as historical data
(e.g. getting the past year of usage data for a historical analysis)
and ongoing data (e.g. getting the past day's usage for real-time tracking
of emissions). To address this need, the specifications from this working
group will establish standardized data formats and access procedures so that
data can be easily obtained, analyzed, and combined from multiple sources
(e.g. companies with buildings in multiple utility territories).

* **Privacy, Consent, and Security:**
Since carbon accounting is typically for specific entities,
the actual utility data of that specific entity is required to perform
carbon accounting calculations (e.g. the actual kwh usage, meter locations,
and rate plans for the customer for the past 12 months). This data is
typcially considered private information, so specifications to address this
use case must consider privacy, consent, and security requirements as part
of the scope of work.

* **Streamlined User Experience:**
Many organizations do not have dedicated staff or sufficient resources
to spend large amounts of time and effort gathering utility data needed
for carbon accounting calculations. This effectively creates a
"barrier to entry" that limits carbon accounting to only the most well-resourced
organizations and prevents widespread adoption of decarbonization goals.
Thus, in order to address this use case adequately, the specifications
for this working group must consider user experience and performance
to allow for easy, streamlined customer utility data access.

#### Examples of users in this use case:

* Platforms that asses carbon emissions for enterprises (
[WattCarbon](https://www.wattcarbon.com/),
[FlexiDAO](https://www.flexidao.com/),
[Microsoft Cloud for Sustainability](https://www.microsoft.com/en-us/sustainability),
etc.)

* Organizations looking to adopt the [24/7 Carbon-free Energy Compact](https://gocarbonfree247.com/)
and other [ESG](https://en.wikipedia.org/wiki/Environmental%2C_social_and_corporate_governance) pledges

* Organizations that have pledged to be carbon free (
[Google](https://www.google.com/about/datacenters/cleanenergy/),
[Apple](https://www.apple.com/newsroom/2020/07/apple-commits-to-be-100-percent-carbon-neutral-for-its-supply-chain-and-products-by-2030/),
[Microsoft](https://www.microsoft.com/en-us/corporate-responsibility/sustainability/operations),
etc.)

* Consultants and advisors helping organizations that have climate and decarbonization targets


## Use Case 2: Decarbonization Projects <a id="use-case-decarbonization-projects" href="#use-case-decarbonization-projects" class="permalink">🔗</a>

Often, organizations with decarbonization targets (see [Use Case 1: Carbon Accounting](#use-case-carbon-accounting) above),
will evaluate projects that may positively impact their carbon emissions. These projects
can range from physical locally (e.g. installing solar or EV charging) and remote (e.g.
building renewable generation projects via wholesale power purchase agreements), to virtual
direct (e.g. avoiding marginal emissions by managing building usage dynamically) or financial
(e.g. switching rate plans to carbon free sources or community solar).

#### Needs:

* **Use Case 1 Needs:**
Like carbon accounting, the calculations for assessing decarbonization
projects typcially require the specific utility data for a specific entity.
So, all of the needs for carbon accounting often are needed for assessing
decarbonization projects, both for the initial feasibility analysis and
ongoing project measurement and verification ([M&V](https://en.wikipedia.org/wiki/Measurement_and_Verification)).

* **Utility Bill and Cost Breakdowns:**
Decarbonization projects are frequently analyzed based on financial
payback or savings calculations (e.g. converting a fleet of company
vehicles to EVs would remove gasoline costs while incurring more
electricity costs). Thus, to address this use case the specifications
must consider how to obtain customer utility bill and cost breakdown
information so that these complex financial analyses can be performed,
both for initial financial analysis and ongoing cost monitoring.

#### Examples of users in this use case:

* Property owners looking to install decarbonization projects on their properties (EV charging,
distributed solar, etc.)

* Contractors, vendors, consultants, and advisors who work with property owners with decarbonization projects
(EV charging vendors, solar installers, ESCOs, etc.)

* Building control and energy management systems that dynamically modify the behavior of equipment based
on carbon impact or customer savings (demand charge reduction via batteries, dynamic EV charging, HVAC controls, etc.)

* Platforms and firms that analyze customer rate plan options to maximize carbon impact (community solar,
direct power purchase agreements, etc.)


## Use Case 3: Distributed Grid Flexibility <a id="use-case-distributed-flexibility" href="#use-case-distributed-flexibility" class="permalink">🔗</a>

*"In the past, we would forecast load and deploy generation. In the future, we will forecast generation and deploy load." -overheard at utility conference*

While the first two use cases focus on individual entities' carbon impact,
as more and more non-dispatchable renewables get deployed, the grid will
increasingly need sources of dynamic load flexibility to partially address
the intermittency of solar and wind generation. Technologies to allow for
higher and higher penetration of renewables on the grid can often be installed
"behind the meter" as distributed energy resources (DERs).

While these technologies do not directly decarbonize the grid, they allow for
higher penetration of cheap, zero carbon renewables. Thus, this working group
considers grid flexibility and load management technologies a key use case
for bolstering decarbonization efforts.

#### Needs:

* **Use Case 1 Needs:**
Like carbon accounting, the calculations for assessing the eligibility of
deploying or using a distributed grid flexibility or load management technology
typically requires the specific utility data for a specific entity.
So, all of the needs for carbon accounting often are needed for assessing
distributed grid flexibility technologies, both for the initial feasibility
analysis and ongoing measurement and verification ([M&V](https://en.wikipedia.org/wiki/Measurement_and_Verification)).

* **Program Eligibility and Participation Information:**
Because distributed grid flexibility and load management technologies are active
participants in managing load on the electrical grid, they often are registered
as part of a utility or central operator program (e.g. demand response programs).
Thus, the specifications to address this use case must consider how to include
program eligibility and participation details as part of the standardized customer
dataset.

#### Examples of users in this use case:

* Apps and devices that participate in demand response programs (
[CEC Load Management Rulemaking](https://www.energy.ca.gov/proceedings/energy-commission-proceedings/load-management-rulemaking),
[NYISO Demand Response](https://www.nyserda.ny.gov/All-Programs/Energy-Storage/Energy-Storage-for-Your-Business/Demand-Response-Programs),
etc.)

* Apps and devices that monitor grid conditions and control DERs and IoT prevent additional
carbon-intensive generation from coming online (e.g. marginal emissions).

## What use cases are not in scope <a id="not-in-scope" href="#not-in-scope" class="permalink">🔗</a>

* TODO: discuss at working group meeting
