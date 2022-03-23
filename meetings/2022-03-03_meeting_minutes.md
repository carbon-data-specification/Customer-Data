# CDSC WG1 (Customer Data) Meeting 2022-03-03

## Agenda
* Welcome
* Review "Draft proposal for Use Cases" (Pull Request #6):
    * https://github.com/carbon-data-specification/Customer-Data/pull/6
* Discuss timeline for approving Use Cases pull request
    * 2 weeks?
* Discuss next github issues to be opened
    * List of specifications to be created?
    * High-level descriptions on website?
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Sebnem Tugce Pala (UtilityAPI)
* Hallie Cramer (Google)
* Molly Webb (Energy Unlocked)

## Minutes
* Daniel: share screen on pull request
* Molly: can share use cases they've seen
* Molly: asking about where to receive emails
* Molly: power systems working group was the intent
* Daniel: welcome to continuing listen in
* Daniel: gives overview of Use Case 1
* Hallie: seems US-centric, have gotten perspective from Europe?
* Molly: consumption data only?
    * Daniel: consumption is core piece, but also account metadata (rate/tariff, etc.)
    * Hallie: big part is also privacy focus/requirements
* Molly: cost of access?
    * Daniel: not considered currently, but could fall under "Streamlined User Experience"
    * Molly: UK has DCC, high cost for utilities, and another service charges 4 pounds per customer to allow access to customer data, costs along the chain
* Daniel: hardest part of this is that every jurisdiction has different regulations/requirements/etc.
* Molly: consumption, even without account metadata, would still be useful for location-based accounting
* Daniel: goal is to have forwards compatibility with GDPR

* Daniel: Use Case 2
* Molly: Is inclusive live optimization of buildings in scope?
    * Daniel: not in scope
* Molly: Is device-level customer data (e.g. battery charge level) included in the scope?
    * Daniel: not currently, but would love this as a comment for review by others
    * Hallie: need clarity on Use Case 3, since mentions "Apps and devices that participate in demand response..."

* Daniel: discuss Use Case 3
* Hallie: one example, build better forecasting for a specific customer, or third party tool for a customer

* Daniel: discuss Use Case 4
* Molly: https://energy.ec.europa.eu/topics/energy-efficiency/energy-efficient-buildings/energy-performance-buildings-directive_en 
    * Molly: not generally at city-level, mostly at national level
    * Molly: should distinguish between investor-led performance requirements vs. regulated performance requirements
    * Daniel: maybe should add building metadata (e.g. how many faucets) as NOT in scope

* Hallie: want to call out TEAC (time-based energy attribute credits)?
    * Need access to granular generation from PPA assets to calculate

* Daniel: thoughts on timeline for reviewing?
    * Hallie: 1-2 weeks
    * Molly: 2 weeks is fine
    * Seb: 2 weeks if fine, will do policy research
    * Daniel: consensus is 2 weeks

## Closing Discussion
* Consensus to commit this to repo? Yes
