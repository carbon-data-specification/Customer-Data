# CDSC WG1 (Customer Data) Meeting 2024-03-28

Recording: https://zoom.us/rec/share/USRyo1OPoCuOgVNLLDgphHFm4sm_3hOBumVctSP-dc2k3fxhZpcUsI7bLzhimyVo.b-CB82fuFQCI4DLW

## Agenda
* Welcome
* Review the CDSC-WG1-03 (Customer Data) pull request
    * Pull Request:
        * https://github.com/carbon-data-specification/Customer-Data/pull/26
    * Maintainer's Draft:
        * Specification - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/
        * Overview - https://daniel-utilityapi.github.io/Customer-Data/specs/cdsc-wg1-03/overview

## Attendees
* Daniel Roesler (UtilityAPI) (Maintainer)
* Hallie Cramer (Google)
* Eloi Ferrer (FlexiDAO)
* Madhuban Kumar (CarbonLaces)
* Celina Bonugli (APS)

## Minutes
* Welcome and attendance taking
* [Daniel] Overview of Pull Request #26
    * [Hallie] What parts are uncertain vs. TODO?
    * [Daniel]
        * Authorization Scopes specifics on which fields are granted with each scope, what `authorization_details` values are allowed for each scope, and what scopes overlap and why.
            * [Hallie] It could be parameter-based?
            * [Daniel] Yes, could also be use-case based
            * [Eloi] Need to discuss granularity for the various scopes
         * Need to add Energy Attribute Certificates (EACs)
            * [Hallie] provided example document to add to Customer Data APIs
            * [Daniel] potential collaboration between WG2 for format of source emissions data?
            * [Eloi] Difference between two working groups is that the data is contract-specific vs. generic emissions data
            * [Madhuban] Relevant to discussion in UK (Perseus program). Regional mix important as well.
            * [Hallie] in this WG, we have opportunity to determine emissions for individual, rather than system-wide
            * [Daniel] For one-off tariffs, is the `rateplan_code` confidential or publicly listed
            * [Celina] For one-off "contracts", those tend to be confidential. For tariffs, they are public, but can have granular options. For 24/7, need a portfolio options (DR, etc.), so may not just be a single tariff or contract or rate plan that represents the 24/7 emissions result.
            * [Hallie] For rateplan_codes that are confidential, this data still requires Customer consent, so that's not a problem.
            * [Madhuban] In UK, corporate data may be open data, so may be aggregated at regional basis or for corporations may not require Customer consent to access.

## Closing Discussion
* Consensus to commit this to repo? Yes
