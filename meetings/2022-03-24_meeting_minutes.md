# CDSC WG1 (Customer Data) Meeting 2022-03-24

## Agenda
* Welcome
* Review open pull requests:
    * "Draft proposal for Use Cases" (Pull Request #6):
        * Review updates to: https://github.com/carbon-data-specification/Customer-Data/pull/6
        * Last call for sustained objection
        * Merge if no sustained objection
        * Close Issue #5 (create initial use cases)
* Discuss next set of Github issues:
    * Issue #7 - Create preliminary list of specifications to develop (https://github.com/carbon-data-specification/Customer-Data/issues/7)
* Review and approve minutes

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Joelle (Apple)
* McGee (WattCarbon)
* Hallie (Google)
* Steve (WattCarbon)

## Minutes
* Daniel: welcome and go through recent use cases commits to address comments
* McGee: on Standardized Customer Datasets
    * issue for utility to comply with this is they struggle to map meters to customers accounts
    * hard to maintain backwards compatibility
* Daniel: yes, seen this previously
    * balance between implementation difficulty vs usefulness
    * dataset components live all over the place inside utility
    * how do we address that reality
* McGee:
    * need consistency and cross referencing
    * data dictionaries of what fields mean
* Daniel:
    * in order to fulfill the standardized dataset need for the use cases, perhaps can specify _how_ to publish your data dictionary, rather than requiring specific fields
    * risk of many different data dictionaries
* McGee:
    * that's something the market could solve
    * might only need it for one utility
    * so only need universal dictionary translator if covering wide area
* Hallie:
    * TEACs should be specific callout, not included in the customer datasets
    * granular certification (TEACs) fits more under Use Case 2 specifically
* McGee: can you show the comment
* Daniel: brought up comment
* Hallie:
    * Can we call it "Data Needed for Granular Certification"
* Daniel:
    * Should this be obtained from WG2?
* Hallie:
    * In Europe, get data from Operator (TSO/DSO)
* McGee:
    * Different in Europe than US
* Hallie:
    * Definitely "customer" data
    * The PPA production data that is under contract by the customer is customer data, so not WG2
* Daniel:
    * Where does TEAC data come from? Billing utility? TSO? DSO?
    * I think this should be a github issue to add to the use case needs once we get clear language
* Hallie:
    * Will open a github issue with draft language

* Daniel:
    * went through remaining commits
    * Summary:
        * Hallie to open github issue for granular certification data need under Use Case 2 (to be added when language is settled)
        * Daniel's opinion: Ready to merge if not sustained objection
        * Any sustained objection?
        * No objection
    * merged pull request #6
    * closed github issue #5
    * mention that next step is issue #7

* Daniel:
    * call for anything else?
    * nothing

## Closing Discussion
* Consensus to commit this to repo? Yes
