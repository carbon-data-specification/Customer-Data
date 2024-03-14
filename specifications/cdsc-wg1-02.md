# CDSC-WG1-02 - Client Registration

## Abstract <a id="abstract" href="#abstract" class="permalink">🔗</a>

This specification defines how utilities and other central entities ("Servers") may allow third parties ("Clients") to register, configure, and maintain connectivity with the utility or other central entity. This specification mostly extends various OAuth specifications ([Dynamic Client Registration](https://www.rfc-editor.org/rfc/rfc7591), [Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414), and more) to create a robust framework for offering secure, streamlined, and standardized connectivity between utilities and third parties.

## Status <a id="status" href="#status" class="permalink">🔗</a>

<b style="color:red">WARNING: This specification is a DRAFT and has not achieved consensus by the working group.</b>

## Copyright <a id="copyright" href="#copyright" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## Table of Contents <a id="table-of-contents" href="#table-of-contents" class="permalink">🔗</a>

* [1. Introduction](#introduction)  
* [2. Terminology](#terminology)  
* [3. Authorization Server Metadata](#auth-server-metadata)  
    * [3.1. Metadata URL](#auth-server-metadata-url)  
    * [3.2. Metadata Object Format](#auth-server-metadata-format)  
    * [3.3. Scope Descriptions Object Format](#scope-descriptions-format)  
    * [3.4. Registration Field Object Format](#registration-field-format)  
    * [3.5. Registration Field Types](#registration-field-types)  
    * [3.6. Registration Field Formats](#registration-field-formats)  
    * [3.7. Authorization Details Field Object Format](#auth-details-fields-format)  
    * [3.8. Authorization Details Field Formats](#auth-details-field-formats)  
* [4. Client Registration Process](#client-registration-process)  
    * [4.1. Client Registration Request](#registration-request)  
    * [4.2. Client Registration Response](#registration-response)  
* [5. Clients API](#clients-api)  
    * [5.1. Client Object Format](#client-format)  
    * [5.2. Listing Clients](#clients-list)  
    * [5.3. Retrieving Individual Clients](#clients-get)  
    * [5.4. Modifying Clients](#clients-modify)  
* [6. Client Settings API](#client-settings-api)  
    * [6.1. Client Settings Object Format](#client-settings-format)
    * [6.2. Profile Visibilities](#profile-visibilities)  
    * [6.3. Button Styles](#button-styles)  
    * [6.4. Modifying Client Settings](#clients-settings-modify)  
* [7. Client Updates API](#client-updates-api)  
    * [7.1. Client Update Object Format](#client-update-format)  
    * [7.2. Client Update Types](#client-update-types)  
    * [7.3. Client Update Statuses](#client-update-statuses)  
    * [7.4. Client Update Request Object Format](#client-update-request-format)  
    * [7.5. Listing Client Updates](#clients-updates-list)  
    * [7.6. Creating Client Updates](#clients-updates-create)  
    * [7.7. Modifying Client Updates](#clients-updates-modify)  
* [8. Scope Credentials API](#scope-creds-api)  
    * [8.1. Scope Credentials Object Format](#scope-creds-format)  
    * [8.2. Scope Credentials Statuses](#scope-creds-statuses)  
    * [8.3. Evaluating Authorization Requests](#auth-request-scope-evaluation)  
    * [8.4. Listing Scope Credentials](#scope-creds-list)  
    * [8.5. Retrieving Individual Scope Credentials](#scope-creds-get)  
    * [8.6. Creating Scope Credentials](#scope-creds-create)  
    * [8.7. Modifying Scope Credentials](#scope-creds-modify)  
* [9. Grants API](#grants-api)  
    * [9.1. Grant Object Format](#grant-format)  
    * [9.2. Grant Statuses](#grant-statuses)  
    * [9.3. Listing Grants](#grants-list)  
    * [9.4. Retrieving Individual Grants](#grants-get)  
    * [9.5. Modifying Grants](#grants-modify)  
* [10. Directory API](#directory-api)  
    * [10.1. Directory Entry Object Format](#directory-entry-format)  
    * [10.2. Listing Directory Entries](#directory-list)  
    * [10.3. Publicly Accessible Web Directory](#public-directory)  
* [11. Extensions](#extensions)  
* [12. Examples](#examples)  
* [13. Security Considerations](#security)  
    * [13.1. Restricted Access](#restricted-access)  
    * [13.2. Rate Limiting](#rate-limiting)  
* [14. References](#references)  
* [15. Acknowledgments](#acknowledgments)  
* [16. Authors' Addresses](#authors-addresses)  

## 1. Introduction <a id="introduction" href="#introduction" class="permalink">🔗</a>

This specification was developed as part of the global effort to combat the climate crisis. Specifically, in order to scalably measure carbon emissions of organizations and calculate the impact of deploying and operating clean energy technologies, companies need an efficient means to register and interact with energy utilities and other similar entities.

There are thousands of utilities serving customers across the world, and each have their own way of providing access to privileged functionality and data. This specification defines a way for these utilities and other entities ("Servers") to provide a standardized, structured process for external users and companies ("Clients") to register and obtain secure access to privileged functionality and data. By offering a standardized Client registration and management protocol, utilities and other entities can enable secure interoperability with other external systems providing climate-change fighting services such as carbon tracking, decarbonization measures, grid flexibility capabilities, and energy benchmarking.

This specification does NOT describe what specific privileged functionality or data is offered to Clients as part of their registration. Instead, relevant stakeholders are encouraged to write [Extensions](#extensions) to this specification that enable various use cases that need access to privileged functionality or data. For example, this specification may be extended to define a method for Clients to be able to access customer-authorized energy usage data.

## 2. Terminology <a id="terminology" href="#terminology" class="permalink">🔗</a>

<a id="server" href="#server" class="permalink">🔗</a> **"Server"** - The entity hosting the specified endpoints. A Server can be an energy utility or another type of entity that want to provide access to privileged functionality or data. These entities can include, but are not limited to, distribution utilities, grid operators, electric retailers, community choice aggregators, government agencies, data warehouses, and private infrastructure providers.

<a id="client" href="#client" class="permalink">🔗</a> **"Client"** - The entity requesting Server's metadata endpoints. A Client can be any organization or user seeking to register with a Server for a specific scope of access. These entities can include, but are not limited to, carbon tracking applications, electric vehicle companies, clean energy technology providers, commercial utility customers, grid management applications, and energy efficiency organizations.

<a id="referenced-technologies" href="#referenced-technologies" class="permalink">🔗</a> Referenced Technologies: "[HTTPS](https://www.rfc-editor.org/rfc/rfc9110#name-https-uri-scheme)", "[URL](https://www.rfc-editor.org/rfc/rfc3986.html#section-1.1.3)", "[Request Methods](https://www.rfc-editor.org/rfc/rfc9110#name-methods)", "[Status Codes](https://www.rfc-editor.org/rfc/rfc9110#name-status-codes)", "[JSON](https://www.rfc-editor.org/rfc/rfc8259)", "[OAuth](https://oauth.net/specs/)", <span style="background-color:yellow">TODO: add more as needed</span> are defined by their referenced standards documents.

<a id="key-words" href="#key-words" class="permalink">🔗</a> Key Words: "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" are defined in accordance with [BCP 14](https://www.rfc-editor.org/info/bcp14).


## 3. Authorization Server Metadata <a id="auth-server-metadata" href="#auth-server-metadata" class="permalink">🔗</a>

To enable automated Client registration, Servers MUST host an endpoint with structured metadata about how to submit a [registration request](#registration-request), as well as functionality and data capabilities offered by the Server. The requirements for hosting this metadata endpoint follows [OAuth 2.0 Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414) with several additions for Carbon Data Specification (CDS) functionality described in the following sections.

### 3.1. Metadata URL <a id="auth-server-metadata-url" href="#auth-server-metadata-url" class="permalink">🔗</a>

Following OAuth's [Obtaining Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414#section-3) process, a Server's Authorization Server Metadata Object is retrieved by making an HTTPS request to a specified URL.

To ensure discoverability to the specified URL, this specification extends [CDSC-WG1-01 Server Capabilities](/specs/cdsc-wg1-01/#server-capabilities) to require the following values:

* `oauth` - _string_ - (REQUIRED) Including Client Registration via OAuth in the list of a Server's available capabilities

As well as extending the [CDSC-WG1-01 Metadata Object Format](/specs/cdsc-wg1-01/#metadata-object-format) to require the following values:

* `oauth_metadata` - _URL_ - (REQUIRED) Where Clients can obtain the Server's Authorization Server Metadata Object

In addition to requiring that the URL be included in the [CDSC-WG1-01 Metadata Object Format](/specs/cdsc-wg1-01/#metadata-object-format), Servers MAY also configure the URL such that it conforms to the default [Well-Known URI](#https://www.rfc-editor.org/rfc/rfc8414#section-7.3) format, which can increase interoperability beyond the above specified CDSC-WG1-01 extension.

### 3.2. Metadata Object Format <a id="auth-server-metadata-format" href="#auth-server-metadata-format" class="permalink">🔗</a>

A Server's Authorization Server Metadata Object follows OAuth's [Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414#section-2) object format with the following modifications from OPTIONAL or RECOMMENDED to REQUIRED:

* `registration_endpoint` - _URL_ - (REQUIRED) OAuth's [Dynamic Client Registration](https://www.rfc-editor.org/rfc/rfc7591) functionality is required to enable the [Client Registration Process](#client-registration-process).
* `scopes_supported` - _Array[string]_ - (REQUIRED) Disclosure of available scopes is required to enable integration capabilities into other platforms. This array MUST contain the `client_admin` scope.
* `service_documentation` - _URL_ - (REQUIRED) Developer documentation is required by the Server to help streamline Client integration.
* `op_policy_uri` - _URL_ - (REQUIRED) Policies for Clients registering is required.
* `op_tos_uri` - _URL_ - (REQUIRED) Terms of use for Clients registering is required.
* `revocation_endpoint` - _URL_ - (REQUIRED) OAuth's [Token Revocation](https://www.rfc-editor.org/rfc/rfc7009) functionality is required.
* `introspection_endpoint` - _URL_ - (REQUIRED) OAuth's [Token Introspection](https://www.rfc-editor.org/rfc/rfc7662) functionality is required.
* `code_challenge_methods_supported` - _Array[string]_ - (REQUIRED) OAuth's [Proof Key for Code Exchange by OAuth Public Clients](https://www.rfc-editor.org/rfc/rfc7636) functionality is required. Servers MUST offer `S256` and MUST NOT offer `plain` code verifier methods.

In addition to the standard set of OAuth [Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414#section-2) values, this specification also requires the following OAuth extension capabilities to be included in the metadata object values:

* `authorization_details_types_supported` - _Array[string]_ - (REQUIRED) OAuth's [Rich Authorization Requests](https://www.rfc-editor.org/rfc/rfc9396) functionality is required. This array of values MUST be the same as `scopes_supported`.
* `pushed_authorization_request_endpoint` - _URL_ - (REQUIRED) OAuth's [Pushed Authorization Requests](https://www.rfc-editor.org/rfc/rfc9126) functionality is required.

In addition to the above additionally required set of OAuth [Authorization Server Metadata](https://www.rfc-editor.org/rfc/rfc8414#section-2) values, this specification clarifies use of the following OAuth sandard values:

* `response_types_supported` - _Array[string]_ - (REQUIRED) The response types in this array MUST represent a union of all `response_types_supported` values contained in the `cds_scope_descriptions` object.
* `grant_types_supported` - _Array[string]_ - (REQUIRED) The response types in this array MUST represent a union of all `grant_types_supported` values contained in the `cds_scope_descriptions` object.
* `token_endpoint_auth_methods_supported` - _Array[string]_ - (REQUIRED) The response types in this array MUST represent a union of all `token_endpoint_auth_methods_supported` values contained in the `cds_scope_descriptions` object.

In addition to OAuth capabilities included in the metadata object, this specification adds the following Carbon Data Specification (CDS) values:

* `cds_oauth_version` - _string_ - (REQUIRED) The version of the CDS-WG1-02 Client Registration specification that the Server has implemented, which for this version of the specification is `v1`
* `cds_human_registration` - _URL_ - (REQUIRED) Where Clients who do not have the technical capacity to use the `registration_endpoint` can visit to manually register a Client using a web browser
* `cds_human_directory` - _URL_ - (REQUIRED) A public web interface where users may browse the list of Clients who have registered and set their Client Settings `profile_visibility` to `listed`
* `cds_test_accounts` - _URL_ - (REQUIRED) Where Clients can find developer documentation on what test account credentials may be used for testing OAuth `response_type=code` authorization requests
* `cds_clients_api` - _URL_ - (REQUIRED) The base url for the [Clients API](#clients-api)
* `cds_client_settings_api` - _URL_ - (REQUIRED) The base url for the [Client Settings API](#client-settings-api)
* `cds_client_updates_api` - _URL_ - (REQUIRED) The base url for the [Client Updates API](#client-updates-api)
* `cds_scope_credentials_api` - _URL_ - (REQUIRED) The base url for the [Scope Credentials API](#scope-creds-api)
* `cds_grants_api` - _URL_ - (REQUIRED) The base url for the [Grants API](#grants-api)
* `cds_directory_api` - _URL_ - (REQUIRED) The base url for the [Directory API](#directory-api)
* `cds_scope_descriptions` - _Map[[ScopeDescription](#scope-descriptions-format)]_ - (REQUIRED) An object providing additional information about what Scope values listed in `scopes_supported` mean. This object MUST include a key for each Scope listed in `scopes_supported` with a [Scope Description](#scope-descriptions-format) as that key's value.
* `cds_registration_fields` - _Map[[RegistrationField](#registration-field-format)]_ - (REQUIRED) An object providing additional information about Registration Field that are referenced in [Scope Description's](#scope-descriptions-format) `registration_requirements` list. This object MUST include a key for each Registration Field `id` included in the `registration_requirements` lists in the metadata object with a [Registration Field](#registration-field-format) as that key's value. If all `registration_requirements` lists are empty, this reference object is an empty object (`{}`).

Other values not mentioned here but listed in specifications for the Authorization Server Metadata specification or other extensions MAY be included as described in their respective specifications.

### 3.3. Scope Descriptions Object Format <a id="scope-descriptions-format" href="#scope-descriptions-format" class="permalink">🔗</a>

Scope Description objects are formatted as JSON objects and contain named values. The following values are included in the default list available in scope description objects.

* `id` - _string_ - (REQUIRED) The unique identifier of the scope. This MUST be the same value as the object key the Metadata Object's `cds_scope_descriptions` object.
* `name` - _string_ - (REQUIRED) A human-readable name of the scope.
* `description` - _string_ - (REQUIRED) A human-readable description of what access or actions the scope will enable.
* `documentation` - _URL_ - (REQUIRED) Where developers can find documentation for the scope.
* `registration_requirements` - _Array[string]_ - (REQUIRED) A list of any registration fields that MUST be submitted with [Client Registration Requests](#registration-request) or requirements that must be completed after registration before the scope is available to use in the Server's production environment. All values in this array MUST be included in the Metadata Object's `cds_registration_fields` object for a complete description of the requirement. If no additional requirements are needed, this value is an empty array (`[]`).
* `registration_optional` - _Array[string]_ - (REQUIRED) A list of any registration fields that Clients MAY submit with the [Client Registration Requests](#registration-request). If no additional fields are available, this value is an empty array (`[]`).
* `response_types_supported` - _Array[string]_ - (REQUIRED) The OAuth `response_type` values that can be used with this scope. This value follows the same behavior as OAuth's [Metadata object `response_types_supported`](https://www.rfc-editor.org/rfc/rfc8414#section-2), except that this value represents the response types supported for this individual scope and not all scopes for the Client. If a scope is not available for OAuth authorization requests (e.g. a `client_credentials`-only scope), this value is an empty array (`[]`).
* `grant_types_supported` - _Array[string]_ - (REQUIRED) The OAuth grant type values that can be used with this scope. This value follows the same behavior as OAuth's [Metadata object `grant_types_supported`](https://www.rfc-editor.org/rfc/rfc8414#section-2), except that this value represents the grant types supported for this individual scope and not all scopes for the Client. This array MUST contain at least one grant type.
* `token_endpoint_auth_methods_supported` - _Array[string]_ - (REQUIRED) The OAuth client authentication methods that can be used for granting tokens with this scope. This value follows the same behavior as OAuth's [Metadata object `token_endpoint_auth_methods_supported`](https://www.rfc-editor.org/rfc/rfc8414#section-2), except that this value represents the client authentication methods supported for this individual scope and not all scopes for the Client. A value of `"none"` this array indicates that the scope may be used for public application without using a client secret.
* `authorization_details_fields` - _Array[[AuthorizationDetailsField](#auth-details-fields-format)]_ - (REQUIRED) A list of fields that MAY be included in [Rich Authorization Requests](https://www.rfc-editor.org/rfc/rfc9396) the authorization details object for this scope `type`. If no extra authorization details fields are available, this value is an empty list (`[]`).

### 3.4. Registration Field Object Format <a id="registration-field-format" href="#registration-field-format" class="permalink">🔗</a>

Registration Field objects are formatted as JSON objects and contain named values. The following values are included in the default list available in registration fields objects.

* `id` - _string_ - (REQUIRED) The unique identifier of the registration field. This MUST be the same value as the object key the Metadata Object's `cds_registration_fields` object.
* `type` - _[RegistrationFieldType](#registration-field-types)_ - (REQUIRED) What type of Registration Field this entry is.
* `description` - _string_ - (REQUIRED) A human-readable description of what should be submitted or expected for this registration field.
* `documentation` - _URL_ - (REQUIRED) Where developers can find more information about this registration field.
* `field_name` - _string_ - (OPTIONAL) If type is `registration_field`, this is the name of the field to submit in the [Client Registration Request](#registration-request) and MUST start with `cds_`.
* `format` - _[RegistrationFieldFormats](#registration-field-formats)_ - (OPTIONAL) If type is `registration_field`, this is the data format that MUST be used in the value of the field.
* `default` - _various_ - (OPTIONAL) If type is `registration_field` and the field is optional, this is the default value that will be used in lieu of the Client submitting a value themselves. Including this `default` value in the object indicates the registration field is optional.
* `max_length` - _integer_ - (OPTIONAL) If format is one of `string`, `string_or_null`, `url`, `url_or_null`, `email`, or `email_or_null`, this is the maximum length of the submitted value, if not `null`.
* `max_size` - _integer_ - (OPTIONAL) If format is one of `image`, `image_or_null`, `pdf`, or `pdf_or_null`, this is the maximum file size of the submitted value before encoding into [Base64](https://en.wikipedia.org/wiki/Base64), if not `null`.
* `amount` - _decimal_ - (OPTIONAL) If type is `payment_required`, this is the amount in `currency` that will be required to complete registration.
* `currency` - _string_ - (OPTIONAL) If type is `payment_required`, this is the monetary currency in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) currency code.

### 3.5. Registration Field Types <a id="registration-field-types" href="#registration-field-types" class="permalink">🔗</a>

Registration Field types define which type of action the Client or Server will take for that registration field. Registration Fields can be either something that MUST or MAY be submitted as part of the [Client Registration Request](#registration-request), depending on the submitted scope's `registration_requirements` and `registration_optional` values, or can be something that a Client must do after registration in order to be full approved for use in the production environment.

The following list of strings are an enumerated set of registration field types that are valid `type` values in the registration field object.

* `registration_field` - This field should be submitting with the [Client Registration Request](#registration-request) as the `field_name`. This type of registration field MUST also have `field_name` and `format` values. If this field is optional as part of registration, `default` must also be defined in the registration field object.
* `manual_review` - This field indicates that the Server will manually review the registration before approving it for production use. Notifications and communication about the status of this manual review will be conveyed using the [Client Updates API](#client-updates-api).
* `payment_required` - This field indicates that a setup payment will be required before the Server will approve the Client for production use. Notifications and communication about how to pay and confirmation of payment will be conveyed using the [Client Updates API](#client-updates-api).
* `email_verification` - This field indicates that the Client must verify their email before the Server will approve the Client for production use. Notifications and communication about how to verify the Client's contact email will be conveyed using the [Client Updates API](#client-updates-api).

### 3.6. Registration Field Formats <a id="registration-field-formats" href="#registration-field-formats" class="permalink">🔗</a>

Registration Field formats define the data type of submitted values for these fields in [Client Registration Requests](#registration-request).

The following list of strings are an enumerated set of registration field formats that are valid `format` values in the registration field object.

* `string` - If required, a string value MUST be submitted.
* `string_or_null` - Same as `string`, only with `null` being an additional possible value.
* `url` - If required, a URL value MUST be submitted.
* `url_or_null` - Same as `url`, only with `null` being an additional possible value.
* `email` - If required, a valid email address string MUST be submitted.
* `email_or_null` - Same as `email`, only with `null` being an additional possible value.
* `boolean` - If required, either `true` or `false` MUST be submitted.
* `boolean_or_null` - Same as `boolean`, only with `null` being an additional possible value.
* `image` - If required, a valid image file formatted as `image/jpeg` or `image/png` encoded as a string using [Base64](https://en.wikipedia.org/wiki/Base64) MUST be submitted.
* `image_or_null` - Same as `image`, only with `null` being an additional possible value.
* `pdf` - If required, a valid pdf file formatted encoded using [Base64](https://en.wikipedia.org/wiki/Base64) as a string MUST be submitted.
* `pdf_or_null` - Same as `pdf`, only with `null` being an additional possible value.

### 3.7. Authorization Details Field Object Format <a id="auth-details-fields-format" href="#auth-details-fields-format" class="permalink">🔗</a>

Authorization Details Field objects are formatted as JSON objects and contain named values. The following values are included in the default list available in authorization details field objects.

* `id` - _string_ - (REQUIRED) The unique identifier of the authorization details field. This value is used as the key for the field when added to `authorization_details` data fields as part of OAuth's [Rich Authorization Requests](https://www.rfc-editor.org/rfc/rfc9396).
* `name` - _string_ - (REQUIRED) A human-readable name of the authorization details field.
* `description` - _string_ - (REQUIRED) A human-readable description of what submitting values for this authorization details field means.
* `documentation` - _URL_ - (REQUIRED) Where developers can find more information about this authorization details field.
* `format` - _[AuthorizationDetailsFieldFormats](#auth-details-field-formats)_ - (OPTIONAL) The data format that MUST be used in the value of the field when including it as a data field in `authorization_details` objects.
* `default` - _various_ - (REQUIRED) The default value that will be used in lieu of the Client submitting a value themselves. This is also the value that will be used if a basic OAuth `scope` string parameter is used instead of an `authorization_details` parameter.
* `relative_date_limit` - _integer_ - (OPTIONAL) If `format` is `relative_or_absolute_date`, this is the largest relative date range that may be submitted. Servers MUST validate both submitted absolute dates and relative dates against the relative date limit, where when comparing to a submitted absolute date, the current Server date in the Server's local timezone is used as the relative point of reference.
* `absolute_date_limit` - _integer_ - (OPTIONAL) If `format` is `relative_or_absolute_date`, this is the furthest away date that may be submitted. Servers MUST validate both submitted absolute dates and relative dates against the absolute date limit, where when comparing to a submitted relative date, the current Server date in the Server's local timezone is used as the relative point of reference.
* `limit` - _integer_ - (OPTIONAL) If format is one of `int` or `decimal`, this is the largest value that can be the submitted.

### 3.8. Authorization Details Field Formats <a id="auth-details-field-formats" href="#auth-details-field-formats" class="permalink">🔗</a>

Authorization Details Field formats define the data type of submitted values for these fields in `authorization_details` for OAuth's [Rich Authorization Requests](https://www.rfc-editor.org/rfc/rfc9396).

The following list of strings are an enumerated set of authorization details field formats that are valid `format` values in the [Authorization Details Field objects](#auth-details-fields-format).

* `relative_or_absolute_date` - A relative or absolute date string. Relative dates are formatted as a positive integer followed by a `y`, `m`, `w`, or `d` character, where the character represents the unit of duration (year, month, week, and day), and the integer represents the number of units for that duration. For example, `3y` represents a relative date range of 3 years. Absolute dates are formatted as ISO8601 dates (`YYYY-MM-DD`). For example, `2024-01-02` represents the 2nd of January, 2024. Dates are defined as the date from the perspective of the Server's local timezone.
* `int` - An integer value.
* `decimal` - A decimal value, which can have any number of significant units, but MUST NOT be stored or handled as a float value, in order to retain the precision of the value throughout Server and Client processing.

## 4. Client Registration Process <a id="client-registration-process" href="#client-registration-process" class="permalink">🔗</a>

OAuth's [Dynamic Client Registration](https://www.rfc-editor.org/rfc/rfc7591) is used as the basis for initially registering Clients with Servers. To perform the dynamic registration process, the Client submits a request to the Server's `registration_endpoint` provided in the Server's [Metadata object](#auth-server-metadata-format) as described in [Client Registration Request](#registration-request). The Server then responds with either an error or a generated Client registration response as described in [Client Registration Response](#registration-response).

### 4.1. Client Registration Request <a id="registration-request" href="#registration-request" class="permalink">🔗</a>

This specification requires Clients and Servers follow the process described in OAuth's [Client Registration Request](https://www.rfc-editor.org/rfc/rfc7591#section-3.1), with the following modifications.

* Clients MAY submit additional named values that are defined as part of scope `registration_requirements` and `registration_optional` arrays in `cds_scope_descriptions` objects, using the registration field reference's `field_name` value as the submitted key in the registration request.

### 4.2. Client Registration Response <a id="registration-response" href="#registration-response" class="permalink">🔗</a>

This specification requires Servers follow the process described in OAuth's [Client Registration Response](https://www.rfc-editor.org/rfc/rfc7591#section-3.2), with the following modifications to OAuth's [Client Information Response](https://www.rfc-editor.org/rfc/rfc7591#section-3.2.1) object.

* A `client_secret` value MUST be present in the response and be limited to `client_admin` scope use only.
* The `scope` value MUST include the `client_admin` scope.
* The `redirect_uris`, `grant_types`, and `response_types` values, if included, MUST be dynamically determined by the Server as a union of all of their respective values in the Client's [Scope Credentials](#scope-creds-format).
* The `token_endpoint_auth_method` MUST always be set to `client_secret_basic`.

Additionally, the following additional named values MUST be included in the response.

* `cds_server_metadata` - _URL_ - (REQUIRED) Where the Client can find their registration-specific version of the [CDSC-WG1-01 Server Metadata](/specs/cdsc-wg1-01/). If the Client's CDSC server metadata is no different from the public CDSC server metadata, Servers MAY simply link to the public URL. If this metadata endpoint requires authentication, Servers MUST authenticate Client requests to this endpoint via Bearer access token obtained using OAuth's `client_credentials` grant with a scope of `client_admin`, and reject unauthenticated requests with a `401 Unauthorized` response code. Clients know that they must use a Bearer token when Servers return a `401` response code for this endpoint when the Client makes an unauthenticated request to the endpoint.
* `cds_clients_api` - _URL_ - (REQUIRED) The base url for the [Clients API](#clients-api).
* `cds_client_settings_api` - _URL_ - (REQUIRED) The url to a Client's Settings object for the [Client Settings API](#client-settings-api).
* `cds_client_updates_api` - _URL_ - (REQUIRED) The base url for the [Client Updates API](#client-updates-api).
* `cds_scope_credentials_api` - _URL_ - (REQUIRED) The base url for the [Scope Credentials API](#scope-creds-api).
* `cds_grants_api` - _URL_ - (REQUIRED) The base url for the [Grants API](#grants-api).

Upon valid registration, Servers MUST generate a [listed Scope Credential](#scope-creds-list) that is scoped to only `client_admin`, where the value of the Scope Credential's `client_secret` and the registration response `client_secret` are the same. Servers MUST also create [listed Scope Credentials](#scope-creds-list) that cover all additional valid scopes submitted, if any, where the Scope Credential objects are grouped by scopes that have the same `response_types`, `grant_types`, and `token_endpoint_auth_method` so as to maximize the number of scopes that may be accessed using the same `client_secret`.

Severs MUST assign the submitted `redirect_uris` to all [Scope Credentials](#scope-creds-format) in the [Scope Credentials API](#scope-creds-api) that have `response_types`. Clients MAY subsequently manage which `redirect_uris` values are assigned to specific Scope Credentials using the [Scope Credentials API](#scope-creds-api).

While Servers MAY support OAuth's [Dynamic Client Registration Management Protocol](https://www.rfc-editor.org/rfc/rfc7592) by including the `registration_client_uri` and `registration_access_token` values in their registration response, this specification requires that Servers MUST support the [Clients API](clients-api) by including the `cds_clients_api` value in the registration response as a way for Clients to manage their registrations.

## 5. Clients API <a id="clients-api" href="#clients-api" class="permalink">🔗</a>

This specification requires Servers provide a set of Application Programming Interfaces (APIs) allowing Clients to view and edit their Client registrations. These APIs are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope.

### 5.1. Client Object Format <a id="client-format" href="#client-format" class="permalink">🔗</a>

Client objects are formatted as JSON objects and contain named values. Client objects are required to follow the same object format as the [Client Registration Response](#registration-response), with the addition of the following named values.

* `cds_created` - _ISO8601 datetime_ - (REQUIRED) When the Client was created.
* `cds_modified` - _ISO8601 datetime_ - (REQUIRED) When the Client was last modified.
* `cds_client_uri` - _URL_ - (REQUIRED) Where to submit modifications using the Clients API [Modifying Clients](#clients-modify) functionality. Servers MUST make this URL unique for each Client registration.

Additionally, while the [Client Registration Response](#registration-response) MUST contain the `client_secret` field. Client objects returned from the Clients API MUST NOT include the `client_secret` or `client_secret_expires_at` fields. Clients MUST instead use the [Scope Credentials API](#scope-creds-api) to obtain `client_secret` values for use in other APIs.

### 5.2. Listing Clients <a id="clients-list" href="#clients-list" class="permalink">🔗</a>

Clients may request to list Client objects that they have access to by making an HTTPS `GET` request, authenticated with a valid Bearer `access_token` scoped to the `client_admin` scope, to the `cds_clients_api` URL included in the [Client Registration Response](#registration-response). The Client listing request responses are formatted as JSON objects and contain the following named values.

* `clients` - _Array[[Client](#client-format)]_ - (REQUIRED) A list of Clients to which the requesting `access_token` is scoped to have access. If no Clients are accessible, this value is an empty list (`[]`). If more than 100 Clients are available to be listed, Servers MAY truncate the list and use the `next` value to link to the next segment of the list of Clients.
* `next` - _URL_ or `null` - Where to request the next segment of the list of Clients. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `previous` - _URL_ or `null` - Where to request the previous segment of the list of Clients. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.

Listings of Client objects MUST be ordered in reverse chronological order by `cds_modified` timestamp, where the most recently updated relevant Client MUST be first in each listing.

### 5.3. Retrieving Individual Clients <a id="clients-get" href="#clients-get" class="permalink">🔗</a>

The URL to be used to send `GET` requests for retrieving individual Client objects MUST be the `cds_client_uri` provided in the [Client object](#client-format). If a Server has optionally implemented OAuth's [Dynamic Client Registration Management Protocol](https://www.rfc-editor.org/rfc/rfc7592), the value of `cds_client_uri` MUST be the same as `registration_client_uri`, and access tokens issued from either a `client_credentials` grant with the scope `client_admin` or the access token provided as the `registration_access_token` MUST be valid access tokens to interact with the client retrieval endpoint (`cds_client_uri`).

### 5.4. Modifying Clients <a id="clients-modify" href="#clients-modify" class="permalink">🔗</a>

This specification requires that the procedure to modify Clients MUST follow OAuth's [Client Update Request](https://www.rfc-editor.org/rfc/rfc7592) section in [Dynamic Client Registration Management Protocol](https://www.rfc-editor.org/rfc/rfc7592).

The URL to be used to send `PUT` requests for updating clients MUST be the `cds_client_uri` provided in the [Client object](#client-format). If a Server has optionally implemented OAuth's [Dynamic Client Registration Management Protocol](https://www.rfc-editor.org/rfc/rfc7592), the value of `cds_client_uri` MUST be the same as `registration_client_uri`, and access tokens issued from either a `client_credentials` grant with the scope `client_admin` or the access token provided as the `registration_access_token` MUST be valid access tokens to interact with the client update endpoint.

Servers MUST ignore updated values to the following fields and keep the Server-defined values set:

* `client_id` - This value is immutable from when it was assigned upon Client registration.
* `client_id_issued_at` - This value is immutable from when the Client initially registered.
* `client_secret` - This value is NOT included in any Client object response, except for the initial Client registration request. Clients MUST use the [Scope Credentials API](#scope-creds-api) to manage client secrets.
* `client_secret_expires_at` - This value is NOT included in any Client object response, except for the initial Client registration request. Clients MUST use the [Scope Credentials API](#scope-creds-api) to discover when a client secret will expire.
* `redirect_uris` - This list is dynamically determined by the Server as a union of all `redirect_uris` values in the Client's [Scope Credentials](#scope-creds-format).
* `grant_types` - This list is dynamically determined by the Server as a union of all `grant_types` values in the Client's [Scope Credentials](#scope-creds-format).
* `response_types` - This list is dynamically determined by the Server as a union of all `response_types` values in the Client's [Scope Credentials](#scope-creds-format).
* `token_endpoint_auth_method` - Always `client_secret_basic`.
* `cds_server_metadata` - This is a URL set by the Server.
* `cds_clients_api` - This is a URL set by the Server.
* `cds_client_settings_api` - This is a URL set by the Server.
* `cds_client_updates_api` - This is a URL set by the Server.
* `cds_scope_credentials_api` - This is a URL set by the Server.
* `cds_grants_api` - This is a URL set by the Server.

All other fields MAY be submitted for updating by the Client. However, the Server MUST determine the validity of the submitted Client fields and reject with a 400 Bad Response if not all submitted fields are either the same as previously set, or invalid values for that field.

If a Client does not include a field that is included in the Client object, this indicates that the Client wishes to reset the value of that field to the Server default.

If a Server needs to asynchronously review and approve changes to any submitted Client object fields that have been submitted by the Client and are different from the current values, for valid update requests the Server MUST respond with a `202 Accepted` response, which indicates that the submission was accepted but not fully saved as completed yet. Any fields that have not been synchronously updated as part of the request and response MUST remain in the response as their previous values, and the Server MUST add one or more entries to the [listed Client Updates](#clients-updates-list) for the modified fields that need to be asynchronously reviewed and approved. Clients MAY then use the [Client Updates API](#client-updates-api) to track the asynchronous review of the modification request. If all submitted fields have been synchronously updated as part of the response, Servers MUST respond with a `200 OK` response.

## 6. Client Settings API <a id="client-settings-api" href="#client-settings-api" class="permalink">🔗</a>

This specification requires Servers provide an API allowing Clients to view and manage their Client settings. While the settings fields are directly related to a specific registered Client, they are not included in the Client object itself in order to allow Clients to make partial updates to their settings values using an HTTPS `PATCH` request instead of a PUT request, which is required for the Client object updates to remain compatible with OAuth's [Dynamic Client Registration Management Protocol](https://www.rfc-editor.org/rfc/rfc7592).

The Client Settings API are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope.

Clients request their current [Client Settings object](#client-settings-format) my making an authenticated HTTPS `GET` request to the `cds_client_settings_api` endpoint provided in the [Client object](#client-format).

### 6.1. Client Settings Object Format <a id="client-settings-format" href="#client-settings-format" class="permalink">🔗</a>

Client Settings objects are formatted as JSON objects and contain the following named values:

* `default_scope` - _string_ - (REQUIRED) A space-separated list of scopes the Server will use for OAuth's [Authorization Requests](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1) if the Client does not supply a `scope` or `authorization_details` parameter in the request.
* `profile_visibility` - _[ProfileVisibility](#profile-visibilities)_ - (REQUIRED) This is visibility configuration of a Client in the [Directory API](#directory-api).
* `profile_visibility_options` - _Array[[ProfileVisibility](#profile-visibilities)]_ - (REQUIRED) This is the list of available Profile Visibility values that the Client may choose to set as their `profile_visiblity`.
* `profile_description` - _string_ - (REQUIRED) This is the description that the Client wishes to be displayed in their public directory entry, if `profile_visibility` is set to `autolist`, `unlisted`, or `listed`.
* `profile_uri` - _URL_ - (REQUIRED) This is the URL that links directly to the Client's entry in the Server's publicly accessible directory web interface, if `profile_visibility` is set to `autolist`, `unlisted`, or `listed`. If a Client has set their `profile_visibility` to `disabled`, the Server MUST respond to requests to this URL with a 404 Not Found response code.
* `profile_slug` - _string_ - (OPTIONAL) For Servers that have the ability to partially customize the `profile_uri` string to be a more human-readable URL, this is the part of the URL that is customizeable by the Client.
* `profile_button_uri` - _URL or `null`_ - (REQUIRED) In the profile entry for a Client, Servers MUST offer the ability for the Client to link users to a Client-provided URL. Servers MUST implement this as an anchor link styled as one of the specified [Button Styles](#button-styles) that opens a new tab via the `target="_blank"` anchor attribute for the user. If a Client sets this value to `null`, then the Server MUST NOT render the button link in the Client's directory profile entry.
* `profile_button_style` - _[ButtonStyle](#button-styles)_ - (REQUIRED) This is the style of button the Server has set for the `profile_button_uri`.
* `profile_button_style_options` - _Array[[ButtonStyle](#button-styles)]_ - (REQUIRED) This is a list of [Button Styles](#button-styles) available for the Client to set as their button style in their directory entry.
* `profile_contact_name` - _string_ - (REQUIRED) This the contact name to be listed in the public directory entry for the Client.
* `profile_contact_email` - _[E.123](https://en.wikipedia.org/wiki/E.123) email address_ - (REQUIRED) This the contact email to be listed in the public directory entry for the Client.
* `profile_contact_phone` - _[E.123](https://en.wikipedia.org/wiki/E.123) international phone number or `null`_ - (REQUIRED) This the contact phone number to be listed in the public directory entry for the Client. If the Client sets this to `null`, the phone number field MUST be hidden on the Client's public directory profile entry by the Server.
* `profile_contact_website` - _URL or `null`_ - (REQUIRED) This is a link to a website the Client wishes the user to visit for more information on how to contact them. If the Client sets this to `null`, the website field MUST be hidden on the Client's public directory profile entry by the Server.

### 6.2. Profile Visibilities <a id="profile-visibilities" href="#profile-visibilities" class="permalink">🔗</a>

Servers MUST make available the following Profile Visibility options in the `profile_visibility_options` list:

* `listed` - Servers MUST include the Client profile entry in both the [Directory API list](#directory-list) and [Publicly Accessible Web Directory](#public-directory). If Servers are asynchronously reviewing Clients before approving production access to scopes, Servers MUST NOT include this option in the list of `profile_visibility_options` until the Server has completed and approve the Client for production access to at least one of the non-`client_admin` scopes, and instead include `autolist` in the list of `profile_visibility_options`. For Client profile entries, Servers MUST NOT render the profile entry with `X-robots-tag` or `<meta name="robots" ...>` HTML head tags with a value of `noindex`, so that Client profile entries may be indexed by web search engines.
* `autolist` - If Servers are asynchronously reviewing Clients before approving production access to scopes, Servers MUST include this option in the list of `profile_visibility_options` until the Server has completed and approve the Client for production access to at least one of the non-`client_admin` scopes and NOT include `listed` in the list of `profile_visibility_options`. If the Client has set their `profile_visibility` to `autolist`, when the Server approves at least one non-`client_admin` scope for production use, the Server MUST automatically switch the Client's `profile_visibility` setting from `autolist` to `listed` and remove `autolist` from the list of `profile_visibility_options`. The behavior of this option is the same as the `unlisted` Profile Visibility option, with the exception that the Server MUST prominently display a banner message in the rendered profile entry to users that the Client has not yet been approved for production use.
* `unlisted` - Servers MUST NOT include the Client profile entry in the [Directory API list](#directory-list) or [Publicly Accessible Web Directory](#public-directory). However, the `profile_uri` will be publicly visible when requested directly by a user directly and the response to the `profile_uri` MUST include a `X-robots-tag` response header with `noindex` in the header values or a `<meta name="robots" ...>` HTML head tag with `noindex` included in the `content` attribute, so that web search engines do not index the profile entry.
* `disabled` - Servers MUST NOT include the Client profile entry in the [Directory API list](#directory-list) or [Publicly Accessible Web Directory](#public-directory). The Server MUST also return a 404 Not Found response code for requests made to the Client's `profile_uri`.

### 6.3. Button Styles <a id="button-styles" href="#button-styles" class="permalink">🔗</a>

Clients may have registered to a server for different purposes, so their Client profile entry button links may need to be styled as different actions based on the Client's use case. Servers MUST offer the following button styles for Clients to set as their `profile_button_style`:

* `authorize` - Rendered as a button indicating to the user that the button will allow the user to authorize the Client in some fashion, such as a button saying "Authorize {client_name}".
* `link` - Rendered as a button indicating to the user that the button will allow the user to link or connect the user's account to the Client, such as a button saying "Link your account with {client_name}".
* `goto` - Rendered as a button indicating to the user that the button will allow the user to go to the Client's website, such as a button saying "Visit the {client_name} website".

### 6.4. Modifying Client Settings <a id="clients-settings-modify" href="#clients-settings-modify" class="permalink">🔗</a>

Clients may modify fields in the Client Settings API by sending an authenticated HTTPS `PATCH` request to the `cds_client_settings_api` endpoint with the body of the request formatted a JSON object. The fields included in JSON object are the fields the Client intends to update with the submitted fields' values. If a field is not included in the `PATCH` request, the Server MUST leave the field unmodified from its current value.

The following are fields that MAY be included in the `PATCH` request, and modification MUST be supported by Servers:

* `default_scope`
* `profile_visibility`
* `profile_description`
* `profile_slug`
* `profile_button_uri`
* `profile_button_style`
* `profile_contact_name`
* `profile_contact_email`
* `profile_contact_phone`
* `profile_contact_website`

Servers MUST reject requests with a `400 Bad Request` response when fields are submitted that are not able to be modified by the Client or the submitted values are invalid. For valid `PATCH` requests from Clients, Servers MUST respond with a `200 OK` or `202 Accepted` response with an updated JSON object of the complete current Client Settings object.

If a Server needs to asynchronously review and approve changes to any submitted Client Settings object fields that have been submitted by the Client and are different from the current values, for valid modification requests the Server MUST respond with a `202 Accepted` response, which indicates that the submission was accepted but not fully saved as completed yet. Any fields that have not been synchronously updated as part of the request and response MUST remain in the response as their previous values, and the Server MUST add one or more entries to the [listed Client Updates](#clients-updates-list) for the modified fields that need to be asynchronously reviewed and approved. Clients MAY then use the [Client Updates API](#client-updates-api) to track the asynchronous review of the modification request. If all submitted fields have been synchronously updated as part of the response, Servers MUST respond with a `200 OK` response.

## 7. Client Updates API <a id="client-updates-api" href="#client-updates-api" class="permalink">🔗</a>

To facilitate automated integration between Servers and Clients, this specification requires that official communication between Servers and Clients be performed using the Client Updates APIs. Servers MAY implement other means of communications for exchanging messages and notifications, such as email support, but they MUST also mirror any official communications that impact Client or Grant statuses, settings, or access using the Client Updates API.

The Client Updates API endpoints are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope.

### 7.1. Client Update Object Format <a id="client-update-format" href="#client-update-format" class="permalink">🔗</a>

Client Update objects are formatted as JSON objects and contain the following named values:

* `uri` - _URL_ - (REQUIRED) Where to retrieve or modify this specific Client Update object.
* `previous_uri` - _URL or `null`_ - (REQUIRED) Where to find the previous Client Update to which this Client Update has been created as a reply.
* `type` - _[ClientUpdateType](#client-update-types)_ - (REQUIRED) The type of Client Update.
* `read` - _boolean_ - (REQUIRED) Whether the object has been marked as read by a Client. When the Server creates a Client Update, this value MUST be `false` by default, so that the Client Update appears in the [unread](#clients-updates-list) list.
* `creator` - _string or `null`_ - (REQUIRED) If the Server created the Client Update, this value is `null`. If the Client created the Client Update, this value is the Client's `client_id`.
* `created` - _ISO8601 datetime_ - (REQUIRED) When the Client Update was created.
* `modified` - _ISO8601 datetime_ - (REQUIRED) When the Client Update was last modified.
* `status` - _[ClientUpdateStatus](#client-update-statuses)_ - (REQUIRED) The current status of the Client Update.
* `name` - _string_ - (REQUIRED) A human-readable name of the Client Update. If the Client Update `type` is `notification`, `private_message`, or `support_request`, this is the message subject.
* `description` - _string_ - (REQUIRED) A human-readable description of the Client Update. If the Client Update `type` is `notification`, `private_message`, or `support_request`, this is the message body.
* `updates_requested` - _Array[[ClientUpdateRequest](#client-update-request-format)]_ - (OPTIONAL) The list of values that a Client has requested to be updated. This field is required for Client Updates with a `type` value of `field_changes` or `server_request`.
* `related_uri` - _URL or `null`_ - (OPTIONAL) If the Client Update `type` is `notification` or `private_message`, this value is where the Client can find more information, if available. If the Client Update `type` is `support_request`, this value is a relevant URL for which the Client is requesting technical support. If the Client Update `type` is `field_changes`, this is where the Client can retrieve the object that has been requested to be modified. If the Client Update `type` is `payment_request`, this is where the Client can submit their payment to the Server or if paid, a link to the payment receipt. If the Client Update `type` is `server_request`, this is where the Client can find more information about what information is being requested by the Server.
* `amount` - _decimal_ - (OPTIONAL) If the Client Update `type` is `payment_request`, this amount the Client needs to pay to satisfy the payment request.
* `currency` - _string_ - (OPTIONAL) If the Client Update `type` is `payment_request`, this is the monetary currency for the `amount` in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) currency code.

### 7.2. Client Update Types <a id="client-update-types" href="#client-update-types" class="permalink">🔗</a>

Client Update object `type` values MUST be one of the following:

* `notification` - The Server is sending the Client at notification message that is relevant to the Client. This message is considered to be not individually tailored to the Client specifically, but instead directed to all relevant Clients.
* `private_message` - The Server or Client is sending a private message to the opposite party. This message is considered to be individually tailored and relevant only to that Client or Server.
* `support_request` - The Client is submitting a technical support request to the Server.
* `field_changes` - This Client Update represents that the Client has submitted changes to field values in other API objects, listed in the `updates_requested` list, but these changes were not synchronously approved by the Server and need to be reviewed asynchronously by the Server. While the Client originally triggered this Client Update to be created by submitting field changes that need to be asynchronously reviewed, the Server is responsible for creating this Client Update, so the `creator` value is `null`.
* `server_request` - The Server is requesting the Client submit a new Client Update of type `client_submission` with the fields listed in `updates_requested`.
* `client_submission` - The Client is submitting a response to a `server_request` to update one or more fields of a specific object. Both Clients and Servers may create update requests.
* `payment_request` - The Server is requesting payment by the Client to complete a financial payment before the Client may proceed with either registration approval or completing actions listed in the `updates_requested` list.

### 7.3. Client Update Statuses <a id="client-update-statuses" href="#client-update-statuses" class="permalink">🔗</a>

Client Update object `status` values MUST be one of the following:

* `complete` - For Client Updates with `type` values of `notification`, `private_message`, or `client_submission`, the `status` MUST be set as `complete`. For Client Updates with `type` values of `support_request`, `field_changes`, `server_request`, or `payment_request`, this represents the Server has completed and approved or resolved the Client's technical support request, field changes, submission, or payment.
* `open` - For Client Updates with `type` values of `server_request` or `payment_request`, this represents that the Client has not yet submitted a response to the Server's submission or payment request.
* `pending` - For Client Updates with `type` values of `support_request`, `field_changes`, `server_request`, or `payment_request`, this represents the Server has not yet completed it's review of the Client's technical support request, field changes, submission, or payment.
* `rejected` - For Client Updates with `type` values of `field_changes`, `server_request`, or `payment_request`, this represents the Server has completed and rejected the Client's requested field changes, submission, or payment.
* `errored` - For Client Updates with `type` values of `field_changes`, `server_request`, or `payment_request`, this represents the Server encountered an issue while processing the Client's field changes, submission, or payment. The Client is RECOMMENDED to submit a `support_request` Client Update with the `related_uri` as this Client Update's `uri`.

### 7.4. Client Update Request Object Format <a id="client-update-request-format" href="#client-update-request-format" class="permalink">🔗</a>

Client Update Request objects are formatted as JSON objects and contain the following named values:

* `field` - _string_ - (REQUIRED) The field name of the field that is being requested to be updated. For Client Updates with `type` values of `field_changes`, this is the name of the object's field on the API. For Client Updates with `type` values of `server_request`, this is the Server's identifier for the submission being requested from the client.
* `name` - _string_ - (OPTIONAL) For Client Updates with `type` values of `server_request`, this MUST be a human-readable name of the submission type being requested as the client.
* `description` - _string_ - (OPTIONAL) For Client Updates with `type` values of `server_request`, this MUST be a human-readable description providing the Client with more information about what this submission request item is.
* `submitted_uri` - _URL_ - (OPTIONAL) For Client Updates with `type` values of `client_submission`, this MAY be a URL that the Client is submitting as their response to the Server's `server_request`, when the Server's requested field is for a remote resource, such as an logo or binary file.
* `previous_value` - _various_ - (OPTIONAL) For Client Updates with `type` values of `field_changes`, this MUST be the value of the field that the is being requested to be changed from.
* `new_value` - _various_ - (OPTIONAL) For Client Updates with `type` values of `field_changes`, this MUST be the value of the field that the is being requested to be changed to.

### 7.5. Listing Client Updates <a id="clients-updates-list" href="#clients-updates-list" class="permalink">🔗</a>

Clients may request to list Client Update objects that they have access to by making an HTTPS `GET` request, authenticated with a valid Bearer `access_token` scoped to the `client_admin` scope, to the `cds_client_updates_api` URL included in the [Client Registration Response](#registration-response) or [Clients API](#client-format). The Client Update listing request responses are formatted as JSON objects and contain the following named values.

* `outstanding` - _Array[[ClientUpdate](#client-update-format)]_ - (REQUIRED) A list of Client Updates where the `status` is `open` or `pending`.
* `outstanding_next` - _URL_ or `null` - Where to request the next segment of the list of outstanding Client Updates. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `outstanding_previous` - _URL_ or `null` - Where to request the previous segment of the list of outstanding Client Updates. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.
* `unread` - _Array[[ClientUpdate](#client-update-format)]_ - (REQUIRED) A list of Client Updates where the `read` is `false`.
* `unread_next` - _URL_ or `null` - Where to request the next segment of the list of unread Client Updates. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `unread_previous` - _URL_ or `null` - Where to request the previous segment of the list of unread Client Updates. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.
* `read` - _Array[[ClientUpdate](#client-update-format)]_ - (REQUIRED) A list of Client Updates where the `read` is `true`.
* `read_next` - _URL_ or `null` - Where to request the next segment of the list of read Client Updates. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `read_previous` - _URL_ or `null` - Where to request the previous segment of the list of read Client Updates. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.

Responses to `outstanding_next`, `outstanding_previous`, `unread_next`, `unread_previous`, `read_next`, or `read_previous` MUST be formatted the same as the initial Client Update listing, and MUST only include listings for the relevant next segment. For example, if the Client requests a `unread_next`, the Server's response MUST have `outstanding` and `read` lists be empty lists (`[]`).

Listings of Client Update objects MUST be ordered in reverse chronological order by `modified` timestamp, where the most recently updated relevant Client Update MUST be first in each listing.

### 7.6. Creating Client Updates <a id="clients-updates-create" href="#clients-updates-create" class="permalink">🔗</a>

Clients create new Client Updates by sending an authenticated HTTPS `POST` request to the `cds_client_updates_api` endpoint with the body of the request formatted a JSON object. The fields included in JSON object MUST include the following:

* `previous_uri` - _URL or `null`_ - If submitting a Client Update with a `type` value of `client_submission`, this value MUST be the Client Update `uri` that this Client Update is being submitted in response to (i.e. must have a `type` value of `server_request`). If submitting a Client Update with a `type` value of `support_request` or `private_message`, if the Client is responding to a previous Client Update, this value MUST be the Client Update `uri` of that Client Update. If submitting a Client Update with a `type` value of `support_request` or `private_message` that is not responding to another specific Client Update, this value MUST be `null`.
* `type` - _[ClientUpdateType](#client-update-types)_ - This value MUST be one of `private_message`, `support_request`, or `client_submission`.
* `name` - _string_ - If submitting a Client Update with a `type` value of `client_submission`, this value MUST be an empty string (`""`). If submitting a Client Update with a `type` value of `support_request` or `private_message`, this value MUST be the subject line of the message.
* `description` - _string_ - If submitting a Client Update with a `type` value of `client_submission`, this value MUST be an empty string (`""`). If submitting a Client Update with a `type` value of `support_request` or `private_message`, this value MUST be the body of the message.
* `updates_requested` - _Array[[ClientUpdateRequest](#client-update-request-format)]_ - If submitting a Client Update with a `type` value of `client_submission`, this value MUST be a list of [Client Update Request](#client-update-request-format) objects with `field` values matching the `field` values in the corresponding `server_request` Client Update Request objects, and `description` or `submitted_uri` values being the Client's submission response to the Server's request for that `field`.
* `related_uri` - _URL or `null`_ - If submitting a Client Update with a `type` value of `support_request`, this value MAY be a URL to the relevant API endpoint for the support request. If there is no relevant API endpoint, the Client MUST set this value as `null`.

Servers MUST reject requests with a `400 Bad Request` response when a Client submits an incomplete request or the submitted values are invalid. For valid `POST` requests from Clients, Servers MUST respond with a `201 Created` response with an updated JSON object of the complete current Client Update object. When committing Client Updates created by Clients, Servers MUST populate the following fields in addition to the Client's submitted fields:

* `uri` - _URL_ - The endpoint where the Client can retrieve the newly created Client Update object.
* `read` - _boolean_ - Always set to `true`.
* `creator` - _string_ - Always set to the Client's `client_id`.
* `created` - _ISO8601 datetime_ - Always set to the Server's timestamp for when the Client Update was created.
* `modified` - _ISO8601 datetime_ - Always the same as `created`.
* `status` - _[ClientUpdateStatus](#client-update-statuses)_ - For `type` values of `private_message` or `client_submission`, this value MUST be `complete`. For `type` values of `support_request`, this value MUST be `pending`.

When Clients submit Client Updates with `type` value of `client_submission`, if the Client Update referenced in the `previous_uri` has a `status` of `open`, then the Server MUST update the `status` of that referenced Client Update to `pending`, which indicates that the Client has submitted a response for Server review.

### 7.7. Modifying Client Updates <a id="clients-updates-modify" href="#clients-updates-modify" class="permalink">🔗</a>

Clients may modify fields in a Client Updates object by sending an authenticated HTTPS `PATCH` request to the Client Update `uri` endpoint with the body of the request formatted a JSON object. The fields included in JSON object are the fields the Client intends to update with the submitted fields' values. If a field is not included in the `PATCH` request, the Server MUST leave the field unmodified from its current value.

The following are fields that MAY be included in the `PATCH` request, and modification MUST be supported by Servers:

* `read` - Servers MUST accept values of `true` and `false` from the Client.

If a Client wishes to modify a previously submitted Client Update of type `client_submission` they created, the Client MUST [create a new Client Update](#clients-updates-create) with the same `previous_uri` value as the Client Update the Client is wishing to supersede. Severs MUST process newer Client Updates created by the Client as overriding the Client's previous submission.

If a Client wishes to amend a previously created Client Update of type `private_message` or `support_request` they created, the Client MUST [create a new Client Update](#clients-updates-create) with the `previous_uri` value set as the Client Update `uri` for which they are wanting to amend. Severs MUST consider newer Client Updates created by the Client as amending the Client's previous support request or message.

## 8. Scope Credentials API <a id="scope-creds-api" href="#scope-creds-api" class="permalink">🔗</a>

To allow Clients to manage `client_secret` values used for authentication to APIs, this specification requires that Server implement a Scope Credentials API. Servers MAY implement other means of managing Scope Credentials, such as a web interface, but they MUST also mirror any Scope Credentials managed by other means on this required Scope Credentials API.

The Scope Credentials API endpoints are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope.

### 8.1. Scope Credentials Object Format <a id="scope-creds-format" href="#scope-creds-format" class="permalink">🔗</a>

Scope Credentials objects are formatted as JSON objects and contain the following named values:

* `credential_id` - _string_ - (REQUIRED) The unique identifier for the Scope Credential on the Server's system.
* `uri` - _URL_ - (REQUIRED) Where to retrieve, modify, or delete this specific Scope Credential object.
* `client_id` - _string_ - (REQUIRED) Which Client this Scope Credential belongs to.
* `created` - _ISO8601 datetime_ - (REQUIRED) When the Scope Credential was created.
* `modified` - _ISO8601 datetime_ - (REQUIRED) When the Scope Credential was last modified.
* `scope` - _string_ - (REQUIRED) The scopes for which this Scope Credential may obtain access.
* `authorization_details` - _Array[[OAuth AuthorizationDetail](https://www.rfc-editor.org/rfc/rfc9396#section-7.1)]_ - (REQUIRED) Any authorization details scopes that this Scope Credential may obtain access, in addition to this object's `scope` value. If no authorization details scopes are configured in addition to the `scope` string, this value is an empty array (`[]`). If the `type` field of an authorization detail object in this array is the same as a value in the `scope` string, the authorization detail object replaces the scope with additional more refined access details for the scope.
* `client_secret` - _string or `null`_ - (REQUIRED) A sufficiently random value generated by the Server that can be used by the Client to authenticate themselves when obtaining an `access_token` from the Server's OAuth [token endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-3.2). For Scope Credentials that have a `token_endpoint_auth_method` value of `none`, this value MUST be `null`.
* `client_secret_expires_at` - _ISO8601 datetime or `null`_ - (REQUIRED) When the `client_secret` will expire. If the `client_secret` is not currently set to expire, this value is `null`.
* `status` - _[ScopeCredentialStatus](#scope-creds-statuses)_ - (REQUIRED) The current status of accessibility for this Scope Credential.
* `status_options` - _Array[[ScopeCredentialStatus](#scope-creds-statuses)]_ - (REQUIRED) What `status` values to which the Client MAY change the Scope Credential when [modifying](#scope-creds-modify) it. This list MUST always contain at least the values of `sandbox_only` and `disabled`.
* `response_types` - _Array[[OAuth ResponseType](https://www.rfc-editor.org/rfc/rfc7591#section-2)]_ - (REQUIRED) What type of OAuth [`response_types`](https://www.rfc-editor.org/rfc/rfc7591#section-2) are available for use with this Scope Credential. Only a `response_type` value of `code` is supported by this specification.
* `grant_types` - _Array[[OAuth GrantType](https://www.rfc-editor.org/rfc/rfc7591#section-2)]_ - (REQUIRED) What type of OAuth [`grant_types`](https://www.rfc-editor.org/rfc/rfc7591#section-2) are available for use with this Scope Credential.
* `token_endpoint_auth_method` - _[OAuth TokenEnpointAuthMethod](https://www.rfc-editor.org/rfc/rfc7591#section-2)_ - (REQUIRED) What type of OAuth [`token_endpoint_auth_method`](https://www.rfc-editor.org/rfc/rfc7591#section-2) MUST be used when requesting an `access_token` from the Server's OAuth [token endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-3.2). This value MUST be `client_secret_basic` for which scopes the Server requires a non-public Client. This value MAY be `none` when the Server allows the scope to be used by public Clients.
* `redirect_uris` - _Array[URL]_ - (REQUIRED) A list of URLs that the Client MAY use as `redirect_uri` parameter values in the Server's OAuth [authorization endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1). Servers MUST support public domain name URLs (e.g. "https://example.com/redirect"), as well as internal development URLs (e.g. "http://localhost:4000/redirect") and IP addresses in the host of the URL (e.g. "http://127.0.0.1:9999/redirect"). Servers MUST support both `http` and `https` schemas in URLs. Servers MUST also support the addition of parameters in the URL, and when redirected to, append the Server's parameters (e.g. `code=...&state=...`) properly to the Client's `redirect_uri` even in cases where the Client's `redirect_uri` already has additional parameters. For example, if the Client's `redirect_uri` is "https://example.com/redirect?pageid=123", the Server's redirect would be "https://example.com/redirect?pageid=123&code=aaaaaaa&state=bbbbbbb" and not "https://example.com/redirect?pageid=123?code=aaaaaaa&state=bbbbbbb".
* `authorization_endpoint` - _URL_ - (OPTIONAL) A specific OAuth [authorization endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1) that overrides the default Client `authorization_endpoint` for this specific Scope Credential. This MAY be added by Servers who have different authorization interfaces for different sets of scopes.
* `token_endpoint` - _URL_ - (OPTIONAL) A specific OAuth [token endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-3.2) that overrides the default Client `token_endpoint` for this specific Scope Credential. This MAY be added by Servers who have different token interfaces for different sets of scopes.

### 8.2. Scope Credentials Statuses <a id="scope-creds-statuses" href="#scope-creds-statuses" class="permalink">🔗</a>

Scope Credential object `status` values MUST be one of the following:

* `production_only` - The `scope`, `authorization_details`, and `client_secret` MAY be used by the Client to request access on the Server's production systems. For scopes that require user authorization (i.e. `response_type` values of `code`), this `status` indicates that the Client may request authorization from real users.
* `production_and_sandbox` - The `scope`, `authorization_details`, and `client_secret` MAY be used by the Client to request access on the Server's production or test environment systems. For scopes that require user authorization (i.e. `response_type` values of `code`), this `status` indicates that the Client may request authorization from real or test users, as provided in the Server's `cds_test_accounts` documentation.
* `sandbox_only` - The `scope`, `authorization_details`, and `client_secret` MAY be used by the Client to request access on the Server's test environment systems. For scopes that require user authorization (i.e. `response_type` values of `code`), this `status` indicates that the Client may request authorization from fictional test users, as provided in the Server's `cds_test_accounts` documentation.
* `disabled` - The Scope Credential is disabled.

### 8.3. Evaluating Authorization Request Scopes <a id="auth-request-scope-evaluation" href="#auth-request-scope-evaluation" class="permalink">🔗</a>

When responding to an OAuth [authorization request](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1), Servers MUST evaluate the requested `scope` or `authorization_details` against the `scope` and `authorization_details` listed in all of the Client's Scope Credentials objects. If the authorization request's `scope` or `authorization_details` is compatible with all or a subset of an individual Scope Credential's `scope` or `authorization_details`, and the `status` of the Scope Credential is compatible with the type of authenticated user (`production_and_sandbox` for any test or real users, `sandbox_only` for test users, `production_only` for real users), and the `redirect_uri` parameter in the authorization request is listed in the Scope Credential.

If a Server finds that an authorization request is compatible with multiple Scope Credentials, the Server MUST accept the authorization request as valid. When the user authorizes, the `code` parameter created by the Server and sent to the Client via the `redirect_uri` parameter MUST be able to be used to obtain an `access_token` via the token endpoint using any of the matching Scope Credentials' `client_secret` values. If one of the compatible Scope Credentials 

### 8.4. Listing Scope Credentials <a id="scope-creds-list" href="#scope-creds-list" class="permalink">🔗</a>

Clients may request to list Scope Credential objects that they have access to by making an HTTPS `GET` request, authenticated with a valid Bearer `access_token` scoped to the `client_admin` scope, to the `cds_scope_credentials_api` URL included in the [Client Registration Response](#registration-response) or [Clients API](#client-format). The Scope Credential listing request responses are formatted as JSON objects and contain the following named values.

* `scope_credentials` - _Array[[ScopeCredential](#scope-creds-format)]_ - (REQUIRED) A list of Scope Credentials to which the requesting `access_token` is scoped to have access. If no Scope Credentials are accessible, this value is an empty list (`[]`). If more than 100 Scope Credentials are available to be listed, Servers MAY truncate the list and use the `next` value to link to the next segment of the list of Scope Credentials.
* `next` - _URL_ or `null` - Where to request the next segment of the list of Scope Credentials. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `previous` - _URL_ or `null` - Where to request the previous segment of the list of Scope Credentials. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.

Servers MUST support Clients adding any of the following URL parameters to the `GET` request, which will filter the list of Scope Credentials to be the intersection of results for each of the URL parameters filters:

* `statuses` - A space-separated list of `status` values for which the Servers MUST filter the Scope Credentials.
* `client_ids` - A space-separated list of `client_id` values for which the Servers MUST filter the Scope Credentials.
* `cds_client_uris` - A space-separated list of `cds_client_uris` values for which the Servers MUST filter the Scope Credentials.
* `scopes` - A space-separated list of `scope` values for which the Server MUST filter the Scope Credentials, where the included `scope` values are values within the Scope Credential `scope` (space separated) or as a `type` value in the `authorization_details` list.
* `after` - An ISO8601 datetime for which the Server MUST filter Scope Credentials that were created after or on the datetime.
* `before` - An ISO8601 datetime for which the Server MUST filter Scope Credentials that were created before or on the datetime.

Listings of Scope Credential objects MUST be ordered in reverse chronological order by `modified` timestamp, where the most recently updated relevant Scope Credential MUST be first in each listing.

### 8.5. Retrieving Individual Scope Credentials <a id="scope-creds-get" href="#scope-creds-get" class="permalink">🔗</a>

The URL to be used to send `GET` requests for retrieving individual Scope Credential objects MUST be the Scope Credential `uri` provided in the [Scope Credential object](#scope-creds-format).

### 8.6. Creating Scope Credentials <a id="scope-creds-create" href="#scope-creds-create" class="permalink">🔗</a>

Clients create new Scope Credentials by sending an authenticated HTTPS `POST` request to the `cds_scope_credentials_api` endpoint with the body of the request formatted a JSON object. The fields included in JSON object MUST include the following:

* `scope` - _string_ - This value is a space-separated list of scopes for which the new Scope Credentials is requesting to be provisioned.
* `authorization_details` - _Array[[OAuth AuthorizationDetail](https://www.rfc-editor.org/rfc/rfc9396#section-7.1)]_ - This value is a list of additional authorization detail objects that specify more granular access than simple scope strings. If the `type` field of an authorization detail object in this list is the same as a value in the `scope` string, the authorization detail object replaces the scope with additional more refined access details for the scope.
* `redirect_uris` - _Array[URL]_ - A list of URLs that the Client MAY use as `redirect_uri` parameter values in the Server's OAuth [authorization endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1) when requesting user authorization for the scopes (`scope` or `authorization_details`). If the scopes do not require user authorization (e.g. a `grant_type` value of`client_credentials`), this list may be an empty list (`[]`). For scopes that require user authorization (e.g. a `response_type` value of `code`), this list may also be empty (`[]`) and updated by the Client later using the [Scope Credentials modification API](#scope-creds-modify).
* `token_endpoint_auth_method` - _[OAuth TokenEnpointAuthMethod](https://www.rfc-editor.org/rfc/rfc7591#section-2)_ - Either `none` or `client_secret_basic`, depending on if the Client is adding a Scope Credential for a public or non-public use case, respectively. Server MUST only allow `none` to be valid in cases where the requested scopes require user authorization and authorization requests are permitted by public Clients.

Servers MUST reject requests with a `400 Bad Request` response when a Client submits an incomplete request or the submitted values are invalid. Scopes for which user authorization is required (i.e. `response_type` value of `code`) MUST NOT be included with scopes that do not require user authorization (i.e. `grant_type` value of `client_credentials`), and if submitted together, MUST be rejected by the Server as invalid.  For valid `POST` requests from Clients, Servers MUST respond with a `201 Created` response with an updated JSON object of the complete current Scope Credential object. When committing Scope Credentials created by Clients, Servers MUST populate the following fields in addition to the Client's submitted fields:

* `credential_id` - _string_ - The unique identifier for the Scope Credential on the Server's system.
* `uri` - _URL_ - The endpoint where the Client can retrieve the newly created Scope Credential object.
* `created` - _ISO8601 datetime_ - Always set to the Server's timestamp for when the Scope Credential was created.
* `modified` - _ISO8601 datetime_ - Always the same as `created`.
* `status` - _[ScopeCredentialStatus](#scope-creds-statuses)_ - Always set to `sandbox_only`.
* `status_options` - _Array[[ScopeCredentialStatus](#scope-creds-statuses)]_ - Always a list containing at least two values: `sandbox_only` and `disabled`. If the Client has already previously been approved for production for the same scopes, the Server MUST include any of `production_only` or `production_and_sandbox` in the list. If the Server can synchronously approve the Scope Credential for production mode, the Server MAY also include any of `production_only` or `production_and_sandbox` values in the list. If the Server will be reviewing the Scope Credential creation for production approval, Servers MUST also create a [Client Update entry](#client-updates-api) of type `field_changes` with a [Client Update Request](#client-update-request-format) entry with a `field` value of `status_options`, indicating that the Client has requested the Server to review production access approval for the new Scope Credential.
* `response_types` - _Array[[OAuth ResponseType](https://www.rfc-editor.org/rfc/rfc7591#section-2)]_ - For scopes for which user authorization is required, this is always a single-entry list with the value `code` in the list. For scopes for which user authorization is not required, this is always an empty list (`[]`).
* `grant_types` - _Array[[OAuth GrantType](https://www.rfc-editor.org/rfc/rfc7591#section-2)]_ - For scopes for which user authorization is required, this is always a two-entry list with the values `authorization_code` and `refresh_token`. For scopes for which user authorization is not required, this is always a single-entry list with the value `client_credentials` in the list.
* `authorization_endpoint` - _URL_ - (OPTIONAL) If different from the Client object's `authorization_endpoint` value.
* `token_endpoint` - _URL_ - (OPTIONAL) If different from the Client object's `token_endpoint` value.

### 8.7. Modifying Scope Credentials <a id="scope-creds-modify" href="#scope-creds-modify" class="permalink">🔗</a>

Clients may modify fields in the Scope Credentials API by sending an authenticated HTTPS `PATCH` request to the Scope Credential `uri` endpoint with the body of the request formatted a JSON object. The fields included in JSON object are the fields the Client intends to update with the submitted fields' values. If a field is not included in the `PATCH` request, the Server MUST leave the field unmodified from its current value.

The following are fields that MAY be included in the `PATCH` request, and modification MUST be supported by Servers:

* `status` - Servers MUST only accept a value list in the object's `status_options` from the Client.
* `status_options` - This value is a list of [Scope Credential Status](#scope-creds-statuses) values for which the Client is requesting approval. This list MUST always contain `disabled` and `sandbox_only`, and if these values are not submitted by the Client, the Server MUST automatically add them to the Client-submitted list.
* `scope` - _string_ - This value is a space-separated list of scopes for which the new Scope Credentials is requesting to be provisioned.
* `authorization_details` - _Array[[OAuth AuthorizationDetail](https://www.rfc-editor.org/rfc/rfc9396#section-7.1)]_ - This value is a list of additional authorization detail objects that specify more granular access than simple scope strings. If the `type` field of an authorization detail object in this list is the same as a value in the `scope` string, the authorization detail object replaces the scope with additional more refined access details for the scope.
* `redirect_uris` - _Array[URL]_ - A list of URLs that the Client MAY use as `redirect_uri` parameter values in the Server's OAuth [authorization endpoint](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.1) when requesting user authorization for the scopes (`scope` or `authorization_details`). If the scopes do not require user authorization (e.g. a `grant_type` value of`client_credentials`), this list may be an empty list (`[]`). For scopes that require user authorization (e.g. a `response_type` value of `code`), this list may also be empty (`[]`) and updated by the Client later using the [Scope Credentials modification API](#scope-creds-modify).

Servers MUST reject requests with a `400 Bad Request` response when fields are submitted that are not able to be modified by the Client or the submitted values are invalid. If a Server needs to asynchronously review and approve changes to any submitted Scope Credential object fields that have been submitted by the Client and are different from the current values, for valid update requests the Server MUST respond with a `202 Accepted` response, which indicates that the submission was accepted but not fully saved as completed yet. Any fields that have not been synchronously updated as part of the request and response MUST remain in the response as their previous values, and the Server MUST add one or more entries to the [listed Client Updates](#clients-updates-list) for the modified fields that need to be asynchronously reviewed and approved. Clients MAY then use the [Client Updates API](#client-updates-api) to track the asynchronous review of the modification request. If all submitted fields have been synchronously updated as part of the response, Servers MUST respond with a `200 OK` response.

If a Client updates the `status` of a Scope Credential to `disabled`, the Server MUST assume the Scope Credential is compromised and synchronously disable the Scope Credential's `client_secret` from being used on the token endpoint and revoke any `access_token` or `refresh_token` values issued by the token endpoint as a result of using the now-disabled Scope Credential.

## 9. Grants API <a id="grants-api" href="#grants-api" class="permalink">🔗</a>

This specification requires Servers provide an API allowing Clients to view and edit OAuth user authorizations and client credentials grants ("Grants") related to their registration. These APIs are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope.

### 9.1. Grant Object Format <a id="grant-format" href="#grant-format" class="permalink">🔗</a>

Grant objects are formatted as JSON objects and contain the following named values:

* `grant_id` - _string_ - (REQUIRED) The unique identifier for the Grant on the Server's system.
* `uri` - _URL - (REQUIRED) A link to this specific Grant that can be used to [retrieve](#grants-get) or [modify](#grants-modify) the individual Grant.
* `replacing` - _Array[URL]_ - (REQUIRED) If this Grant is superseding another Grant, this is the list of Grant `uri` values of the superseded Grants. If this grant is not superseding any other Grants, this value is an empty list (`[]`).
* `replaced_by` - _Array[URL]_ - (REQUIRED) If this Grant has been superseded by other Grants, this is the list of Grant `uri` values of the superseding Grants. If no other Grants have superseded this Grant, this value is an empty list (`[]`).
* `parent` - _URL or `null`_ - (REQUIRED) If this Grant represents an individual sub-authorization that is part of another Grant that required multiple authorizations, this is where to find the parent Grant. If this Grant is not a sub-authorization, this value is `null`.
* `children` - _Array[URL]_ - (REQUIRED) If this Grant represents a parent Grant that has multiple sub-authorizations underneath it, this is a list of Grant `uri` values for where to find the sub-authorizations. If this Grant does not have any sub-authorizations, this value is an empty list (`[]`).
* `created` - _ISO8601 datetime_ - (REQUIRED) When the Grant was created.
* `modified` - _ISO8601 datetime_ - (REQUIRED) When the Grant was most recently modified. If the Grant has not been modified since creation, this is the same value as `created`.
* `not_before` - _ISO8601 datetime or `null`_ - (REQUIRED) When a Grant that is for future access, Grant's `status` will be switched from `future` to another value. If the Grant is not for future access and access is available immediately upon creation, this value is `null`.
* `not_after` - _ISO8601 datetime or `null`_ - (REQUIRED) When a Grant has access that will expire in the future, this value indicates when the Grant's `status` will be switched to `expired`. If the Grant does not expire, this value is `null`.
* `eta` - _ISO8601 datetime or `null`_ - (REQUIRED) When a Grant has a `status` with the value `pending`, this value indicates an estimated time for when the status is expected to be switched to another value. If the Grant's `status` is not `pending` this value is `null`.
* `expires` - _ISO8601 datetime or `null`_ - (REQUIRED) When the Grant will expire and access will be removed by the Server. If the Grant is to continue indefinitely, this value is `null`.
* `status` - _[GrantStatus](#grant-status)_ - (REQUIRED) The current [Grant Status](#grant-status) of the Grant.
* `client_id` - _string_ - (REQUIRED) Which Client for which this Grant is issued.
* `cds_client_uri` - _URL_ - (REQUIRED) Where to retrieve using the [Clients API](#clients-get) the Client for which the Grant is issued.
* `scope` - _string_ - (REQUIRED) The scopes for which this Grant has issued access.
* `authorization_details` - _Array[[OAuth AuthorizationDetail](https://www.rfc-editor.org/rfc/rfc9396#section-7.1)]_ - (REQUIRED) Any authorization details scopes that are granted in addition to this object's `scope` value. If no authorization details scopes are configured in addition to the `scope` string, this value is an empty array (`[]`). If the `type` field of an authorization detail object in this array is the same as a value in the `scope` string, the authorization detail object replaces the scope with additional more refined access details for the scope.
* `receipt_confirmations` - _Array[string]_ - (REQUIRED) For Grants with scopes that can be obtained via user authorization (`grant_types` contains `authorization_code`), this is a list of receipt confirmation codes that were provided to the end users who authorized the access. If no receipt was provided or the Grant did not get issued via `authorization_code` then this value is an empty list (`[]`).
* `enabled_scope` - _string_ - For Grants where access has been partially granted, but some access is still disabled, this value is the `scope` that has been enabled by the server. For Grants where access has been fully granted, this value is the same as the `scope` value. For Grants that have had their access removed (e.g. `disabled`), this value is an empty string (`""`).
* `enabled_authorization_details` - _Array[[OAuth AuthorizationDetail](https://www.rfc-editor.org/rfc/rfc9396#section-7.1)]_ - For Grants where access has been partially granted, but some access is still disabled, this value is the `authorization_details` that has been enabled by the server. For Grants where access has been fully granted, this value is the same as the `authorization_details` value. For Grants that have had their access removed (e.g. `disabled`), this value is an empty list (`[]`).
* `sub_authorization_scopes` - _Array[string]_ - (REQUIRED) For Grants that require sub-authorizations where users must provide additional authorization to enable access, this is the outstanding list of `scope` values that have yet to be authorized individually by users.

### 9.2. Grant Statuses <a id="grant-statuses" href="#grant-statuses" class="permalink">🔗</a>

Grants object `status` values MUST be one of the following:

* `active` - The Grant is active and access for the features and data specified in the `scope` or `authorization_details` is currently enabled. For Grants that provide access to data APIs that are being regularly updated, this status also indicates that the Server is currently on schedule to provide the expected ongoing data updates.
* `future` - The Grant will be made in the future, and the Client should check the `not_before` value for when the Grant will have its status switched to `active`.
* `pending` - The Grant has been create and is valid, but the Server is still processing or reviewing the Grant and the status will be changed to another status at approximately the time provided in the Grant's `eta` value. While a Grant's status is `pending`, Servers MUST provide access to the granted scope's features or data as the Server processes and the features or data becomes available.
* `partial` - The Grant was submitted originally with the `scope` and `authorization_details` values, but the Server has limited the Client's access a subset of the Grant's `scope`. The enabled access is listed in the `enabled_scope` and `enabled_authorization_details` values.
* `needs_authorization` - The Grant has been created, but access is limited to the `enabled_scope` and `enabled_authorization_details` until a user authorizes the listed `scope` and `authorization_details` values using an authorization URL with a `cds_grant_id` parameter of this `grant_id`.
* `needs_sub_authorizations` - The Grant has been created, but access is limited to the `enabled_scope` and `enabled_authorization_details` until user sub-authorizations, listed in the `sub_authorization_scopes` value, are granted using an authorization URL with a `cds_parent_id` parameter of this `grant_id`.
* `disabled` - The Grant has been indefinitely disabled by the Server, and the Client SHOULD NOT expect the Grant's status to be updated in the future.
* `suspended` - The Grant has been temporarily disabled by the Server or user who authorized access, and the Client SHOULD expect the Grant's status to be updated in the future.
* `revoked` - For Grants with scopes that can be obtained via user authorization (`grant_types` contains `authorization_code`), this status means the user has revoked access.
* `closed` - The Grant has been revoked by the Client via the [Modifying Grants](#grants-modify) API.
* `expired` - The Grant has expired and access has been removed. The Grant's `not_after` value indicates when the Grant's access was removed and the Grant is considered expired.
* `delayed` - For Grants that provide access to data APIs that are being regularly updated, this status indicates that the data being provided is behind schedule and will be updated when the Server resolves its internal delay issues.
* `stopped` - For Grants that provide access to data APIs that are being regularly updated, this status indicates that the data being provided has stopped being updated either by the Server or the user who originally authorized the access. Access to existing data is still available, but the Client should not expect updates to the data being provided.
* `errored` - The Server has encountered an internal error for this Grant, and Client access cannot be confirmed by the Server.

Grant `status` values of `future`, `disabled`, `suspended`, `revoked`, `closed`, and `expired` indicate that access to all features and data that were accessible via this Grant are no longer accessible.

### 9.3. Listing Grants <a id="grants-list" href="#grants-list" class="permalink">🔗</a>

Clients may request to list Grant objects that they have access to by making an HTTPS `GET` request, authenticated with a valid Bearer `access_token` scoped to the `client_admin` scope, to the `cds_grants_api` URL included in the [Client Registration Response](#registration-response) or [Clients API](#client-format). The Grant listing request responses are formatted as JSON objects and contain the following named values.

* `grants` - _Array[[Grant](#grant-format)]_ - (REQUIRED) A list of Grants to which the requesting `access_token` is scoped to have access. If no Grants are accessible, this value is an empty list (`[]`). If more than 100 Grants are available to be listed, Servers MAY truncate the list and use the `next` value to link to the next segment of the list of Grants.
* `next` - _URL_ or `null` - Where to request the next segment of the list of Grants. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `previous` - _URL_ or `null` - Where to request the previous segment of the list of Grants. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.

Servers MUST support Clients adding any of the following URL parameters to the `GET` request, which will filter the list of Grants to be the intersection of results for each of the URL parameters filters:

* `statuses` - A space-separated list of `status` values for which the Servers MUST filter the Grants.
* `client_ids` - A space-separated list of `client_id` values for which the Servers MUST filter the Grants.
* `cds_client_uris` - A space-separated list of `cds_client_uri` values for which the Servers MUST filter the Grants.
* `scopes` - A space-separated list of `scope` values for which the Server MUST filter the Grants, where the included `scope` values are values within the Grant `scope` (space separated) or as a `type` value in the `authorization_details` list.
* `receipt_confirmations` - A space-separated list of receipt confirmation codes for which the Server MUST filter the Grants.
* `after` - An ISO8601 datetime for which the Server MUST filter Grants that were created after or on the datetime.
* `before` - An ISO8601 datetime for which the Server MUST filter Grants that were created before or on the datetime.

Listings of Grant objects MUST be ordered in reverse chronological order by `modified` timestamp, where the most recently updated relevant Grant MUST be first in each listing.

### 9.4. Retrieving Individual Grants <a id="grants-get" href="#grants-get" class="permalink">🔗</a>

The URL to be used to send `GET` requests for retrieving individual Grant objects MUST be the Grant `uri` provided in the [Grant object](#grant-format).

### 9.5. Modifying Grants <a id="grants-modify" href="#grants-modify" class="permalink">🔗</a>

Clients may modify fields in the Grants API by sending an authenticated HTTPS `PATCH` request to the Grant `uri` endpoint with the body of the request formatted a JSON object. The fields included in JSON object are the fields the Client intends to update with the submitted fields' values. If a field is not included in the `PATCH` request, the Server MUST leave the field unmodified from its current value.

The following are fields that MAY be included in the `PATCH` request, and modification MUST be supported by Servers:

* `status` - Servers MUST only accept a value of `closed` from the Client.
* `scope` - Servers MUST evaluate the updated scope for whether another user authorization is required. Servers MUST not require another user authorization if the updated scope is a reduction in scope of access (e.g. removal of a scope value from the scope string). If a new user authorization or sub-authorizations are required, the Server MUST update the `status` to one of `needs_authorization` or `needs_sub_authorizations` and update the `enabled_scope` to be the value of the current scope for which the Client is allowed access.
* `authorization_details` - Servers MUST evaluate the updated authorization details for whether another user authorization is required. Servers MUST not require another user authorization if the updated scope is a reduction in scope of access (e.g. removal of a scope value from the scope string). If a new user authorization or sub-authorizations are required, the Server MUST update the `status` to one of `needs_authorization` or `needs_sub_authorizations` and update the `enabled_authorization_details` to be the value of the current authorization details for which the Client is allowed access.

Servers MUST reject requests with a `400 Bad Request` response when fields are submitted that are not able to be modified by the Client or the submitted values are invalid. For valid `PATCH` requests from Clients, Servers MUST respond with a `200 OK` response with an updated JSON object of the complete current Grant object.

If a Server needs to asynchronously review and approve changes to any submitted Grant object fields that have been submitted by the Client and are different from the current values, for valid modification requests the Server MUST update the Grant's `status` to `pending` in the response. Additionally, if the `scope` or `authorization_details` has been updated, the Server MUST update the `enabled_scope` and `enabled_authorization_details` to reflect for what the Client currently has access while the Grant is pending.

## 10. Directory API <a id="directory-api" href="#directory-api" class="permalink">🔗</a>

Servers MUST provide both an authenticated API-based directory [list of Clients](#directory-list), as well as [publicly accessible web directory](#public-directory) interface of Clients who have been configured to be listed.

The Directory APIs are authenticated using a Bearer `access_token` granted to Clients using OAuth's [`client_credentials` grant](https://www.rfc-editor.org/rfc/rfc6749#section-4.4) and the `client_secret` provided in the initial [Client Registration Response](#registration-response) or `client_secret` values from the [Scope Credentials API](#scope-creds-api) that include the `client_admin` scope. However, the [Publicly Accessible Web Directory](#public-directory) not authenticated, as it is intended to be publicly accessible to browser users.

### 10.1. Directory Entry Object Format <a id="directory-entry-format" href="#directory-entry-format" class="permalink">🔗</a>

Directory Entry objects are formatted as JSON objects and contain the following named values:

* `client_id` - From the [Client object](#client-format)
* `client_name` - From the [Client object](#client-format)
* `client_uri` - From the [Client object](#client-format)
* `tos_uri` - From the [Client object](#client-format)
* `policy_uri` - From the [Client object](#client-format)
* `logo_uri` - From the [Client object](#client-format)
* `scope` - From the [Client object](#client-format), containing the list of scopes approved for production use, and NOT containing the `client_admin` scope.
* `profile_visibility` - From the [Client Settings object](#client-settings-format)
* `profile_uri` - From the [Client Settings object](#client-settings-format)
* `profile_description` - From the [Client Settings object](#client-settings-format)
* `profile_button_uri` - From the [Client Settings object](#client-settings-format)
* `profile_button_style` - From the [Client Settings object](#client-settings-format)
* `profile_contact_name` - From the [Client Settings object](#client-settings-format)
* `profile_contact_email` - From the [Client Settings object](#client-settings-format)
* `profile_contact_phone` - From the [Client Settings object](#client-settings-format)
* `profile_contact_website` - From the [Client Settings object](#client-settings-format)

### 10.2. Listing Directory Entries <a id="directory-list" href="#directory-list" class="permalink">🔗</a>

Clients may request to list Directory Entry objects that they have access to by making an HTTPS `GET` request, authenticated with a valid Bearer `access_token` scoped to the `client_admin` scope, to the `cds_directory_api` URL included in the [Client Registration Response](#registration-response) or [Client object](#client-format). The Client listing request responses are formatted as JSON objects and contain the following named values.

* `entries` - _Array[[DirectoryEntry](#directory-entry-format)]_ - (REQUIRED) A list of Directory Entry objects for Clients who have set their `profile_visiblity` to `listed`. If no Clients are listed, this value is an empty list (`[]`). If more than 100 Directory Entry objects are available to be listed, Servers MAY truncate the list and use the `next` value to link to the next segment of the list of Directory Entry objects.
* `next` - _URL_ or `null` - Where to request the next segment of the list of Directory Entry objects. If no next segment exists (i.e. the requester is at the end of the list), this value is `null`.
* `previous` - _URL_ or `null` - Where to request the previous segment of the list of Directory Entry objects. If no previous segment exists (i.e. the requester is at the front of the list), this value is `null`.

### 10.3. Publicly Accessible Web Directory <a id="public-directory" href="#public-directory" class="permalink">🔗</a>

Additionally, Servers MUST provide a publicly accessible directory web interface that allows users to browse and view the Client profile entries that are listed in the Directory API. Servers MUST NOT require authentication for users to browse the directory. Server MUST include searching capabilities in the web interface that allows users to search for Clients by name, description, and website. Servers MUST also include filtering capabilities in the web interface that allows users to filter the list of Clients by scope. Servers MUST also enable linking directly to a Client profile entry as defined by the [Client Settings `profile_uri`](#client-settings-format). Servers MUST design the publicly accessible directory to be compatible for desktop, mobile, and accessibility-focused browsers and tools, such as vision impaired screen readers. Servers MAY include other features and functionality in addition to these requirements for the publicly accessible directory.

For Client profile entries, Servers MUST render the Client profile entry with at least the following contents:

* `client_name` - From the [Client object](#client-format), as the name of the Client.
* `client_uri` - From the [Client object](#client-format), as a link to the Client's website.
* `tos_uri` - From the [Client object](#client-format), as a link to the Client's terms of service.
* `policy_uri` - From the [Client object](#client-format), as a link to the Client's privacy policy.
* `logo_uri` - From the [Client object](#client-format), as an image and embedded in the rendered Client profile. Servers MAY fetch and cache logos set by Clients when they are configured as part of the [Client Registration request](#registration-request) or when a Client modifies their registration on the [Clients API](#clients-modify). If a Client sets this value to `null`, then the Server MUST render the logo as a placeholder image, such as an image with the words "No Logo Provided".
* `scope` - From the [Client object](#client-format), as a list of scopes for which the Client is approved for production use, except for the `client_admin` scope.
* `profile_description` - From the [Client Settings object](#client-settings-format), as a block of text as a description of the Client. Servers MUST NOT render URLs, phone numbers, emails, and other text that may be auto-detected as a link as links, and instead MUST render the description text as text. Servers MUST render line breaks in the profile entry as submitted by the Client.
* `profile_button_uri` - From the [Client Settings object](#client-settings-format), as an anchor link styled as one of the specified [Button Styles](#button-styles) that opens a new tab via the `target="_blank"` anchor attribute for the user. If a Client sets this value to `null`, then the Server MUST NOT render this button link.
* `profile_button_uri` - From the [Client Settings object](#client-settings-format), as an anchor link styled as the specified `profile_button_style` [Button Styles](#button-styles) and when clicked opens a new tab via the `target="_blank"` and `rel="noopener noreferrer nofollow"` anchor attributes. If a Client sets this value to `null`, then the Server MUST NOT render this button link.
* `profile_contact_name` - From the [Client Settings object](#client-settings-format), as text of the Client's contact name.
* `profile_contact_email` - From the [Client Settings object](#client-settings-format), as a `mailto:` link to the Client's contact email.
* `profile_contact_phone` - From the [Client Settings object](#client-settings-format), as a `tel:` link to the Client's contact phone number, where the link `href` is formatted as an [E.123](https://en.wikipedia.org/wiki/E.123) international phone number and the link text is displayed as the Server's locale format. If a Client sets this value to `null`, then the Server MUST NOT render this contact phone number link.
* `profile_contact_website` - From the [Client Settings object](#client-settings-format), as an anchor link when clicked opens a new tab via the `target="_blank"` and `rel="noopener noreferrer nofollow"` anchor attributes. If a Client sets this value to `null`, then the Server MUST NOT render this contact website link.

Additionally, for Clients registered and approved for scopes that have `authorization_code` in the scope's `grant_types` (thus allowing the Client to obtain user authorizations), Server MUST render a link on the Client profile entry for where users may go to view their current and previous authorization grants with the Client.

## 11. Extensions <a id="extensions" href="#extensions" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## 12. Examples <a id="examples" href="#examples" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## 13. Security Considerations <a id="security" href="#security" class="permalink">🔗</a>

This specification describes a protocol by which a utility or other entity (a Server) can allow third parties (Clients) to register and obtain privileged access to the Server's offered capabilities and data. Because the functionality described in this specification enables access to private Server functionality and data, Servers MUST follow industry cybersecurity best practices when securing their implementations of this specification to prevent unintended or inadvertent access to privileged functionality or data to Clients who are not authorized. These best practices include requiring HTTPS for API endpoints using the latest widely adopted encryption standards, undergoing regular security audits and penetration tests, and internally requiring security-focused process controls and data handling procedures.

<span style="background-color:yellow">TODO: Security considerations on public directory descriptions, buttons, etc.</span>

### 13.1. Restricted Access <a id="restricted-access" href="#restricted-access" class="permalink">🔗</a>

For unauthenticated endpoints ([Authorization Server Metadata](#auth-server-metadata), [Client Registration Process](#client-registration-process)), while Servers can add [rate limiting](#rate-limiting) configurations to protect their systems from being overwhelmed with requests, Servers MUST NOT add anti-bot blocking measures (e.g. captchas) that prevent automated requests from other systems. The functionality described in this specification is intended to be able to be integrated in other platforms to allow those platforms to automate interactions with Servers on their users' behalf.

If [Authorization Server Metadata](#auth-server-metadata) is referenced in a public [CDSC-WG1-01 Server Metadata endpoint](/specs/cdsc-wg1-01/#metadata-endpoint), then the [Authorization Server Metadata](#auth-server-metadata) and [Client Registration Process](#client-registration-process) must also be public.

Servers that wish to restrict access of by-default unauthenticated endpoints to certain Clients MUST configure well established authentication processes for Clients to ensure that only the approved Clients may access the restricted endpoint. This specification does not describe specifically how Servers will authenticate Clients for by-default unauthenticated endpoints, as these restricted access protocols are context dependent. For example, if a Server providing a private Client Registration endpoint as part of an existing logged in portal, then they can use that logged in portal's session cookie to authenticate Client requests to the registration endpoint.

For authenticated endpoints ([Clients API](#clients-api), [Client Settings API](#client-settings-api), [Client Updates API](#client-updates-api), [Scope Credentials API](#scope-creds-api), [Grants API](#grants-api)), Servers MUST authenticate requests using OAuth's [Authorization Request Header Field](https://www.rfc-editor.org/rfc/rfc6750#section-2.1) with access tokens obtained using the OAuth's [Issuing an Access Token](https://www.rfc-editor.org/rfc/rfc6749#section-5) process.

### 13.2. Rate Limiting <a id="rate-limiting" href="#rate-limiting" class="permalink">🔗</a>

For unauthenticated endpoints ([Authorization Server Metadata](#auth-server-metadata), [Client Registration Process](#client-registration-process)), Servers SHOULD configure rate limiting restrictions so that bots and misconfigured scripts will not flood and overwhelm the endpoints with requests, while still allowing legitimate and low-volume automated requests have access to the endpoints.

For authenticated endpoints ([Clients API](#clients-api), [Client Settings API](#client-settings-api), [Client Updates API](#client-updates-api), [Scope Credentials API](#scope-creds-api), [Grants API](#grants-api)), Servers SHOULD configure rate limiting by Client and Scope Credential to ensure that individual Clients do not overwhelm Servers with authenticated API requests. Additionally, Servers SHOULD configure rate limiting for unauthenticated or failed authentication requests to authenticated API endpoints to prevent brute force attempts to gain access to authenticated APIs.

## 14. References <a id="references" href="#references" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## 15. Acknowledgments <a id="acknowledgments" href="#acknowledgments" class="permalink">🔗</a>

The authors would like to thank the late Shuli Goodman, who was the Executive Director of LFEnergy, for her incredible leadership in initially organizing the Carbon Data Specification.

## 16. Authors' Addresses <a id="authors-addresses" href="#authors-addresses" class="permalink">🔗</a>

Daniel Roesler  
UtilityAPI  
Email: [daniel@utilityapi.com](mailto:daniel@utilityapi.com)  
URI: [https://utilityapi.com/](https://utilityapi.com/)

