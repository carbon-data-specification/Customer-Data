---
layout: base
nav: use_cases
title: Use Cases
meta_description: What are the use cases that the Customer Data specifications this working group is trying to address?
---
[Home](/) / Use Cases

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

* **Standardized Customer Datasets:**
In order to perform the needed calculations for carbon accounting and
other Use Cases, a comprehensive dataset with the appropriate data fields
must be provided. Which data fields, granularity, and time periods are
needed are highly use-case dependent, but without requirements to follow,
utilities may not provide access to adequate datasets to satisfy an intended
use case's needs. Thus, specifications to address this use case must consider
what specific datasets are required for common use cases in addition to how
the data should be formatted and accessed.

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

* Platforms that assess carbon emissions for enterprises (
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
direct (e.g. avoided emissions by managing building usage dynamically) or financial
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

* Negative emissions projects (e.g. direct air capture) that need to monitor and measure their customer's
net emissions related to the project.


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
[FERC Order 2222](https://ferc.gov/media/ferc-order-no-2222-fact-sheet),
[CEC Load Management Rulemaking](https://www.energy.ca.gov/proceedings/energy-commission-proceedings/load-management-rulemaking),
[NYISO Demand Response](https://www.nyserda.ny.gov/All-Programs/Energy-Storage/Energy-Storage-for-Your-Business/Demand-Response-Programs),
etc.)

* DER aggregators that manage collections of distributed resources and participate in grid events and markets (
[OhmConnect](https://www.ohmconnect.com/),
[Enel X](https://www.enelx.com/n-a/en),
etc.)

* Apps and devices that monitor grid conditions and control DERs and IoT prevent additional
carbon-intensive generation from coming online (e.g. avoided emissions).

* Utilities needing to standardize customer data access and sharing across multiple divisions
within the utility itself, between internal vendors, or with utility program implementers
(energy efficiency rebate programs, building electrification initiatives, etc.).


## Use Case 4: Building Benchmarking <a id="use-case-benchmarking" href="#use-case-benchmarking" class="permalink">🔗</a>

Municipalities and governments are increasingly requiring that building owners submit
whole-building energy usage information in order to do carbon accounting and measure
building energy efficiency for their jurisdiction.

#### Needs:

* **Standardized Whole-Building Data Formats:**
Whole-building usage data needed to perform building benchmarking calculations
is similar to Use Case 1: Carbon Accounting, only usage can be aggregated over
multiple usage points and be provided as a single combined reading. Thus,
the specifications to address benchmarkings must consider how to appropriately
define how data is being aggregated, and where necessary provide meta data
on the underlying individual components that were used to create the whole-building
aggregate usage values.

* **Streamlined Data Request and Access Procedures:**
Unlike individual customer data requests, which are typically sent to and
approved by individual customers, benchmarking data requests are typically
sent to and approved by the utility directly. This means the dynamics and requirements
of a "data request" changes for this Use Case. Thus, specifications that address
this use case must consider how to best structure user data requests submissions
directly to utilities rather than individual customers. Additionally,
specifications must consider that when a data request is approved, what
data access procedures will be used, and will they be different from data
access procedures from the other Use Cases.

* **Privacy and Consent Requirements:**
While individual customer data access frequently requires first obtaining
consent from the customer. Jurisdictions requiring whole-building data access
often specify thresholds over which individual customer consent is not
required to obtain whole-building usage data (e.g. if any individual
customer's usage is no more than 15% of the whole-building usage). If
whole-building usage is under these thresholds, however, individual customer
consent will still be required for each building tenant. Thus, specifications
addressing this use case must consider how to incorporate customer consent
thresholds for whole-building access, and like the other use cases, the
process by which users may request and obtain customer consent when required.

#### Examples of users in this use case:

* Cities and regions with building benchmarking mandates (
[Fort Collins Building Energy and Water Scoring](https://www.fcgov.com/bews/),
[Atlanta Building Efficiency](https://atlantabuildingefficiency.com/),
[California Building Energy Benchmarking Program](https://www.energy.ca.gov/programs-and-topics/programs/building-energy-benchmarking-program),
etc.)

* Property owners wanting to benchmark their buildings achieve green and efficiency ratings (
[Energy Star](https://www.energystar.gov/buildings),
[LEED](https://www.usgbc.org/leed),
etc.)


## Use cases NOT in scope for this working group <a id="not-in-scope" href="#not-in-scope" class="permalink">🔗</a>

* Live grid operations and controls (actual demand response signaling for equipment, solar inverter control and generation curtailment, EV charging shut-off signals, etc.)

* Financial transactions and settlements (customer utility bill payments, load management program participation financial payouts and settlement, etc.)

* Modifying customer accounts (changing a customer's rate plan, starting or stopping utility services, etc.)

* Providing data access to region-level datasets (ISO load and generation curves, capacity market live pricing data, etc.)

* Disaggregation and analysis methods for aggregate datasets, either for single meter disaggregation (e.g. home appliance enumeration) or multi-meter analysis (e.g. whole-building-to-individual-tenant)
