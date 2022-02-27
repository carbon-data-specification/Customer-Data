# CDSC WG1 (Customer Data) Kickoff Meeting 2022-01-27

## Agenda
* Welcome/Introductions
* Elect maintainer(s)
* Review GH repo ( https://github.com/carbon-data-specification/Customer-Data )
* Any topics introduced by the maintainers
* Determine meeting cadence

## Attendees
* Daniel Roesler (UtilityAPI)
* John Mertic (Linux Foundation)
* Sebnem Tugce Pala (UtilityAPI)
* Simone Accorneo (FlexiDAO)
* Stephen Suffian (WattCarbon)

## Minutes
* John
    * Intros: John, Daniel, Seb, Simone, Stephen
    * Elect Maintainers:
        * Nominees: Daniel Roesler, Martin Hansen
        * Elected by unanimous consent
* Daniel
    * Goals
        * Focus on meeting use case needs and actually getting used
        * Make standard "accessible" - Lots of surrounding documentation
        * Awareness of reality - regulatory, legislation, privacy
    * Enumerating use cases will be a big part of the start of this working group (WG)
        * submetering?
        * Simone: how to allocate behind the meter production?
    * Process
        * Structure of the repo (see below)
        * Make as much as possible asynchronous (via pull requests/approvals)


## Structure of repo
```
/meeting_minutes/
/meeting_minutes/2022-01-27_...md
/meeting_minutes/...

/specifications/
/specifications/00_core_framework.md
/specifications/...

/docs/      (Stephen: need to consider if lower standards for merging to main)
            (Daniel: need domain)
            (John: flexible, can be TLD, e.g. carbondataspec.org, or subdomain, cdsc.lfenergy.org)
            (John: should ask other WG for what they want to)
            (Stephen: possible two documentations, one for legislative and one for technical)
/docs/index.html
/docs/...

/tests/     (Daniel: can migrate to separate repo if gets too complex)
/tests/...  (Github Actions w/ python test cases)

/README.md
/LICENSE.md (John: already there for whole CDSC)
/CONTRIBUTING.md (Daniel: outline our process)
```

## Pull-Request process
* Coming from forked repos
* Need process for approvals
    * Daniel: how to assign reviewers?
    * John: need to add people to org maybe with edit/review flow
    * Daniel: really like how pull request reviewers can suggest changes (e.g. https://github.com/mdn/browser-compat-data/pull/13300)
    * John: could have some threshold, can also be a manual mix of comments and reviewers
* Minutes don't need pull request
    * Approved at end of meeting since taken visibly (screenshare) during meeting

## Closing Discussion
* Simone: next meeting discuss use cases for legislation, etc.
* Seb: roles for people?
* Simone: how many people expected
* Daniel: I can make pull request for use cases
* Consensus to commit this to repo

