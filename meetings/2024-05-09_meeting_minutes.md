# CDSC WG1 (Customer Data) Meeting 2024-05-09

Recording: https://zoom.us/rec/share/mcvtnpiB1VblAUBHPcoX9S57nnUqj67VPYpMaFMPZbCBBJ_CnsVoTfvTeKrh4afN.KywKAV9Rv2YrIc2_

## Agenda
* Welcome
* Planning mid-2024 schedule (webinars, presentations, etc.)
* Discussion of working group organization
* (if time allows) continuing review of specification pull request feedback

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Don Coffin (Green Button Alliance)
* Eloi Ferrer (FlexiDAO)
* Hallie Cramer (Google)

## Minutes
* Welcome and Introductions
* Presentation debrief from Open Sustainability Policy Summit (May 2, 2024)
    * https://docs.google.com/presentation/d/1u5ZWG1ZoiU_GpWdFD5YqLx4ZvY80LQCgNLUiWap7WL4/edit?usp=sharing
    * [Daniel] Received positive feedback around clearly conveying the information
    * [Hallie] much of the same themes about need for data standardization
        * How do we build a bridge to those who might have different perspective
* Other outreach/presentations/submissions:
    * UtilityAPI has submitted an application to the [Digitizing Utilities Prize: Round 2](https://americanmadechallenges.org/challenges/digitizingutilities/round-2) for planning an implementation with a utility for the CDSC specs.
        * submitted quickly, so not sure if this will be awarded
    * Submitted a talk to [FERC: Increasing Real-Time and Day-ahead Market and Planning Efficiency Through Improved Software](https://www.ferc.gov/news-events/events/increasing-real-time-and-day-ahead-market-and-planning-efficiency-through-1) (Jul 9, 2024)
        * haven't heard back yet on whether talk is accepted
        * talk is mainly focused first two specs (metadata and registration)
    * Upcoming LFEnergy summit (CFP due May 19, 2024)
        * Default plan: Eloi and Daniel can co-present again
        * [Hallie] Maybe a panel? Focused on why this matters (maybe Savannah Goodman from Google can moderate?)
        * [Daniel] Maybe we submit two talks (one panel and one presentation)?
        * [Daniel+Hallie+Eloi] Need to figure out who would be on the panel
        * [Daniel] Maybe a demo also?
        * [Hallie] Maybe two of the three?
    * Webinar in June (organized by Hallie)
        * [Hallie] screenshare draft agenda/description

* Working group org structure
    * [Hallie] Would like to figure this out before webinar in June
    * [Daniel] So customerdata.carbondataspec.org would stay
    * [Hallie]
        * WG1 - "Connectivity" Working Group? (keep CDSC-WG1-01 and CDSC-WG1-02)
        * WG3 - "Customer Data" Working Group (moves CDSC-WG1-03 --> CDSC-WG3-01)
    * [Eloi] In aggrement
    * [Hallie] in CDSC-WG1-02, would be good to have protocol/guidance for how extensions should define their scope requirements
    * [Daniel+Hallie] for new "", what are the use cases for 
        * [Hallie] Scope and purpose instead of use cases? Listing the onese we know (Customer Data, Power Systems Data, Super Advanced Meter, etc.)
        * [Daniel] So instead of Use Cases on homepage, have applicability? ("how does this matter?")
        * [Daniel] What about the "what's NOT in scope?"
        * [Hallie] Not really applicable here, since it's open ended
        * [Daniel+Hallie] Types of connectivity that is in scope and types that aren't
        * [Eloi] Examples of service and link to data on other working groups? Wait for deciding what's out of scope until we get feedback?

* Possible split steps:
    * Create new subdomain (connectivity.carbondata.org?) (connectivity.lfess.org?) (wg1.carbondata.org?)
    * Create new github repo (/carbon-data-specification/Connectivity?) (/lfess/WG1?)
    * [Hallie] Need Alex's opinion
    * Create new mailing list + calendar
        * [Hallie] WG meetings focused on feedback on actual specs? Maybe 30min on each spec?
        * [Hallie] Maybe every other time (so 1 WG meeting per month?)
        * [Daniel] I like the 1-per-month alternating
    * Create new website content
    * Move specs, issues, and pull requests to new repo


## Closing Discussion
* Consensus to commit this to repo? Yes
