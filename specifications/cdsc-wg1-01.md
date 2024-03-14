# CDSC-WG1-01 - Server Metadata

## Abstract <a id="abstract" href="#abstract" class="permalink">🔗</a>

This specification defines how utilities and other entities may provide structured "metadata", such as reference information about them, functionality they offer, and how organizations can interoperate with them. The defined base metadata endpoint is intended to act as a starting point for organizations to discover details and capabilities of energy utilities and other similar entities.

## Status <a id="status" href="#status" class="permalink">🔗</a>

<b style="color:red">WARNING: This specification is a DRAFT and has not achieved consensus by the working group.</b>

## Copyright <a id="copyright" href="#copyright" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## Table of Contents <a id="table-of-contents" href="#table-of-contents" class="permalink">🔗</a>

* [1. Introduction](#introduction)  
* [2. Terminology](#terminology)  
* [3. Metadata Endpoint](#metadata-endpoint)  
    * [3.1. Metadata Well-Known URI](#metadata-well-known-uri)  
    * [3.2. Metadata Object Format](#metadata-object-format)  
    * [3.3. Metadata Endpoint Organization](#metadata-endpoint-organization)  
    * [3.4. Infrastructure Types](#infrastructure-types)
    * [3.5. Commodity Types](#commodity-types)
    * [3.6. Server Capabilities](#server-capabilities)
* [4. Coverage Endpoint](#coverage-endpoint)  
    * [4.1. Coverage Object Format](#coverage-object-format)  
    * [4.2. Coverage Entry Format](#coverage-entry-format)  
    * [4.3. Coverage Entry Types](#coverage-entry-types)
* [5. Server Migration](#server-migration)  
* [6. Extensions](#extensions)  
* [7. Examples](#examples)  
* [8. Security Considerations](#security)  
    * [8.1. Restricted Access](#restricted-access)  
    * [8.2. Rate Limiting](#rate-limiting)  
* [9. References](#references)  
* [10. Acknowledgments](#acknowledgments)  
* [11. Authors' Addresses](#authors-addresses)  

## 1. Introduction <a id="introduction" href="#introduction" class="permalink">🔗</a>

This specification was developed as part of the global effort to combat the climate crisis. Specifically, in order to scalably measure carbon emissions of organizations and calculate the impact of deploying and operating clean energy technologies, companies need an efficient means to discover the details and capabilities of energy utilities and other similar entities.

There are thousands of utilities serving customers across the world, and each have their own way of organizing and structuring data. This specification defines a way for these utilities and other entities to provide standardized, structured reference information about them, the functionality they offer, and how organizations can interoperate with them. By serving "metadata" defined in this specification, utilities and other entities can automatically incorporate their details and capabilities into carbon tracking websites, apps, products, and other clean energy technologies.

This specification is intended to be a starting point for providing basic information about utilities and other similar entities, then extended by other specifications to define additional information and functionality. For example, this specification may be extended to define how organizations can dynamically register with a utility in order to gain access to customer-authorized energy usage data.

## 2. Terminology <a id="terminology" href="#terminology" class="permalink">🔗</a>

<a id="server" href="#server" class="permalink">🔗</a> **"Server"** - The entity hosting the metadata endpoint. A Server can be an energy utility or another type of entity that want to provide structured information and capabilities about themselves. These entities can include, but are not limited to, distribution utilities, grid operators, electric retailers, community choice aggregators, government agencies, data warehouses, and private infrastructure providers.

<a id="client" href="#client" class="permalink">🔗</a> **"Client"** - The entity requesting Server's metadata endpoints. A Client can be any organization or user seeking the Server's metadata on their details and capabilities. These entities can include, but are not limited to, carbon tracking applications, electric vehicle companies, clean energy technology providers, commercial utility customers, grid management applications, and energy efficiency organizations.

<a id="referenced-technologies" href="#referenced-technologies" class="permalink">🔗</a> Referenced Technologies: "[HTTPS](https://www.rfc-editor.org/rfc/rfc9110#name-https-uri-scheme)", "[URL](https://www.rfc-editor.org/rfc/rfc3986.html#section-1.1.3)", "[Request Methods](https://www.rfc-editor.org/rfc/rfc9110#name-methods)", "[Status Codes](https://www.rfc-editor.org/rfc/rfc9110#name-status-codes)", "[JSON](https://www.rfc-editor.org/rfc/rfc8259)", "[Well-Known URI](https://www.rfc-editor.org/rfc/rfc5785)", "[ISO8601](https://www.iso.org/iso-8601-date-and-time-format.html)", "[OAuth](https://oauth.net/specs/)", "[GeoJSON](https://datatracker.ietf.org/doc/html/rfc7946)", <span style="background-color:yellow">TODO: add more as needed</span> are defined by their referenced standards documents.

<a id="key-words" href="#key-words" class="permalink">🔗</a> Key Words: "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" are defined in accordance with [BCP 14](https://www.rfc-editor.org/info/bcp14).

## 3. Metadata Endpoint <a id="metadata-endpoint" href="#metadata-endpoint" class="permalink">🔗</a>

Servers supporting this specification SHALL offer one or more HTTPS URLs from which a Client can perform a GET request to retrieve Server metadata, and the Server will respond with the Server's metadata JSON object.

For successful responses, Servers MUST respond with a "200 OK" Status Code and body containing a JSON object that is formatted as defined in [Metadata Object Format](#metadata-object-format). Cache-optimized responses, such as "304 Not Modified", to Client requests with cached value headers, such as `If-None-Match`, is also acceptable.

For invalid requests and error responses, Servers MUST respond with the appropriate Response Code for the type of issue or error (e.g. "503 Service Unavailable" if the Server is temporarily down for maintenance).

### 3.1. Metadata Well-Known URI <a id="metadata-well-known-uri" href="#metadata-well-known-uri" class="permalink">🔗</a>

If the Server wishes to provide metadata publicly, the Server MUST support a metadata endpoint at the Well-Known URI `"/.well-known/carbon-data-spec.json"` on their hostname (e.g. https://example.com/.well-known/carbon-data-spec.json).

Servers MAY additionally support other public and restricted URLs for special case or private metadata endpoints, as needed.

### 3.2. Metadata Object Format <a id="metadata-object-format" href="#metadata-object-format" class="permalink">🔗</a>

Metadata objects are formatted as JSON objects and contain named values, some of which are required and some of which are optional. The following values are included in the default list available in metadata objects.

* `cds_metadata_version` - _string_ - (REQUIRED) The version of metadata object format this Server follows, which for this version of the specification is `v1`
* `cds_metadata_url` - _string_ - (REQUIRED) A URL link to this metadata object's canonical network location
* `created` - _ISO8601 datetime_ - (REQUIRED) When the metadata url was first made available
* `updated` - _ISO8601 datetime_ - (REQUIRED) When this metadata object was last modified
* `name` - _string_ - (REQUIRED) The name of the utility or entity (e.g. "Demo Gas & Electric")
* `description` - _string_ - (REQUIRED) A brief description about the utility or entity (e.g. "An electric and gas utility serving customers in Northern California")
* `website` - _URL_ - (REQUIRED) Where users can learn more about the utility or entity and its capabilities
* `documentation` - _URL_ - (REQUIRED) Where Clients can find the utility or entity's technical reference documentation
* `support` - _URL_ - (REQUIRED) Where Clients can find contact information for technical support on the Server's capabilities
* `infrastructure_types` - _Array[[InfrastructureType](#infrastructure-types)]_ - (REQUIRED) A list of infrastructure categories that are applicable to this utility or entity, which may be an empty array if the Server is not any of the possible infrastructure types
* `commodity_types` - _Array[[CommodityType](#commodity-types)]_ - (REQUIRED) A list of services or commodities that are applicable to this utility or entity, which may be an empty array if the Server does not have an applicable commodity
* `capabilities` - _Array[[ServerCapability](#server-capabilities)]_ - (REQUIRED) What capabilities and functionality this Server supports, which may be an empty array if the Server is not offering any additional capabilities beyond just this metadata object
* `coverage` - _URL_ - (OPTIONAL) Where to find the [Coverage Endpoint](#coverage-endpoint)
* `related_metadata` - _Array[URL]_ - (OPTIONAL) Where to find other related [Metadata Endpoints](#metadata-endpoint)

Values and arrays of values in the metadata object is assumed to only related to the array of capabilities the Server is offering. For example, if a utility that offers both electricity and natural gas, but is only offering data access capabilities to electric service accounts, the Server only needs to include `electricity` in its `commodity_types` array and not `natural_gas`.

### 3.3. Metadata Endpoint Organization <a id="metadata-endpoint-organization" href="#metadata-endpoint-organization" class="permalink">🔗</a>

Many utilities and other similar entities are structured as multiple divisions, operating companies, territories, legal constructs, or other types of groupings. These organizational complexities and legal structures can make it difficult to publish a single representative metadata endpoint for an entire entity.

When utilities and other similar entities wish to publicly provide multiple metadata objects that more cleanly define the metadata and capabilities for their entity, their Server MUST publish a single metadata endpoint at the [well-known URI](metadata-well-known-uri) and within that metadata object include an array of `related_metadata` URLs that link the Client to the various subdivided or related metadata endpoints.

It is acceptable for the initial well-known metadata endpoint object to include a minimal or empty array of `capabilities`, as it represents the entire entity, and leave enumerating the `capabilities` to the related metadata endpoints.

### 3.4. Infrastructure Types <a id="infrastructure-types" href="#infrastructure-types" class="permalink">🔗</a>

Infrastructure types are general categories of utility and energy grid entities that are likely to need to provide access to metadata and capabilities under this specification. The following list of strings are an enumerated set of infrastructure types that MAY be included in the `infrastructure_types` array of values in the metadata object.

* `distribution_utility` - A electric, natural gas, and/or water utility that distributes the utility service to the end customer (e.g. "who maintains the wires to your house")
* `metering_provider` - An entity that maintains the utility metering infrastructure and/or reads end customer meters (e.g. "who reads your meter")
* `supplier` - An energy supplier for the end customer (e.g. "who you buy power from")
* `central_repository` - A government mandated entity that collects customer usage information into a centralized repository for re-distribution (e.g. a state-level meter data warehouse for deregulated jurisdictions)

### 3.5. Commodity Types <a id="commodity-types" href="#commodity-types" class="permalink">🔗</a>

Commodity types are what general categories of services a utility or entity provides to end customers. The following list of strings are an enumerated set of commodity types that MAY be included in the `infrastructure_types` array of values in the metadata object.

* `electricity` - Has metadata or capabilities around utility electric services
* `natural_gas` - Has metadata or capabilities around utility natural gas services
* `fuel_oil` - Has metadata or capabilities around utility fuel oil services
* `water` - Has metadata or capabilities around utility water services

### 3.6. Server Capabilities <a id="server-capabilities" href="#server-capabilities" class="permalink">🔗</a>

Server capabilities are what specific interoperability or informational capabilities a Server is providing. The following list of strings are an enumerated set of capabilities that are defined by default in this specification.

* `coverage` - The Server is providing coverage details related to itself as it relates the other listed capabilities. If included, a `coverage` value is REQUIRED in the metadata object.

Other specifications that define interoperability or informational capabilities for utilities and other entities are encouraged to define an extension that adds their capability as a string to the above list. See the [Extensions](#Extensions) section for details on how to extend this list of Server capabilities.


## 4. Coverage Endpoint <a id="coverage-endpoint" href="#coverage-endpoint" class="permalink">🔗</a>

If Servers include the `coverage` [Server capability](#server-capabilities), a URL to the utility or entity's coverage MUST be included in the metadata object.

When the URL is requested and the request is valid, the Server MUST respond with a "200 OK" Status Code and body containing JSON object formatted according to the [Coverage Object Format](#coverage-object-format). Cache-optimized responses, such as "304 Not Modified", to Client requests with cached value headers, such as `If-None-Match`, is also acceptable.

For invalid requests and error responses, Servers MUST respond with the appropriate Response Code for the type of issue or error (e.g. "503 Service Unavailable" if the Server is temporarily down for maintenance).

### 4.1. Coverage Object Format <a id="coverage-object-format" href="#coverage-object-format" class="permalink">🔗</a>

Coverage objects are formatted as JSON objects and contain the following named values. This object serves mostly as an object wrapper around a list of [coverage entries](#coverage-entry-format), so that the list of coverage entries can be paginated by the Server if too long for one response.

* `coverage_entries` - _Array[[CoverageEntry](#coverage-entry-format)]_ - (REQUIRED) A list of segments this Server covers
* `next` - _`null` or URL_ - (REQUIRED) Link to the next page of coverage entries (`null` if no more subsequent pages)
* `previous` - _`null` or URL_ - (REQUIRED) Link to the previous page of coverage entries (`null` if no more prior pages)

### 4.2. Coverage Entry Format <a id="coverage-entry-format" href="#coverage-entry-format" class="permalink">🔗</a>

Coverage entries are formatted as JSON objects and contain named values, some of which are required and some of which are optional. The following values are included in the default list available in coverage entries.

* `id` - _string_ - (REQUIRED) A unique identifier for the coverage entry
* `type` - _[CoverageEntryType](#coverage-entry-types)_ - (REQUIRED) Which Coverage Entry Type this coverage entry is
* `updated` - _ISO8601 datetime_ - (REQUIRED) When this coverage entry was last modified
* `name` - _string_ - (REQUIRED) A human readable name for the coverage area or category (e.g. "Upstate New York")
* `description` - _string_ - (OPTIONAL) A brief description the coverage area or category (e.g. "Most of the northern half of New York state")
* `map_resource` - _URL_ - (OPTIONAL) Link to a map of the coverage territory
* `map_content_type` - _MIME type_ - (OPTIONAL) Content-Type format of the `map_resource`
* `geojson_resource` - _URL_ - (OPTIONAL) Link to a GeoJSON object mapping the coverage territory

When `type` is a geographic entry type, one or both of `map_resource` and `geojson_resource` MUST be provided. If `map_resource` is provided, then `map_content_type` MUST also be provided.

### 4.3. Coverage Entry Types <a id="coverage-entry-types" href="#coverage-entry-types" class="permalink">🔗</a>

Coverage entry types describe what geographic territory is being detailed in the coverage entry. Many utilities have different geographic coverage for their different service types (e.g. their electric service territory is different from their natural gas service territory), so Servers may include multiple coverage entries for different types of service without having to publish multiple metadata endpoints.

The following list of strings are an enumerated set of coverage entry types that are valid `type` values in the coverage entry object.

* `electric_service_territory` - Geographic area where metadata or capabilities for utility electric services is supported
* `natural_gas_service_territory` - Geographic area where metadata or capabilities for utility natural gas services is supported
* `fuel_oil_service_territory` - Geographic area where metadata or capabilities for utility fuel oil services is supported
* `water_service_territory` - Geographic area where metadata or capabilities for utility water services is supported

## 5. Server Migration  <a id="server-migration" href="#server-migration" class="permalink">🔗</a>

Utilities and other entities frequently change their organizational structures, such as buying another utility and merging the utility territory together. As utilities and other entities evolve, their Server metadata endpoints, including the domains from which they are served, may no longer be valid.

This section describes how Servers MUST transition their [well-known metadata endpoint](#metadata-well-known-uri) when migrating or merging into another Server.

For organizational changes where the utility or other entity is not changing their domain, the Server MUST update their existing well-known metadata endpoint in place to match the new organizational structure.

For organizational changes where the new entity structure will not match the existing domain, the Server MUST create a new well-known metadata endpoint on their new domain and update the metadata contents to match the new organization. The Server MUST also respond to requests to the previous well-known metadata endpoint with a "301 Moved Permanently" or "302 Found" Status Code with a `Location` header containing the URL of the new updated metadata endpoint so that Clients may be automatically redirected to the overriding. The Server MUST maintain the redirect response for as long as the Server retains control over the domain or up to 3 years, whichever is less.

## 6. Extensions <a id="extensions" href="#extensions" class="permalink">🔗</a>

Other specifications MAY extend this specification to allow for seamless expansion in Server metadata and capabilities.

[Metadata Object](#metadata-object-format), [Coverage Object](#coverage-object-format), and [Coverage Entry](#coverage-entry-format) MAY be extended by other specifications to allow for additional values to be possible in their object formats. When extending the object format, other specifications MUST reference the relevant section in this specification and denote that they are extending the object to add a new named value. The additional named value MUST be specified with a general description, the value's format, and whether the value is REQUIRED or OPTIONAL.

The enumerated lists for valid [Infrastructure Types](#infrastructure-types), [Commodity Types](#commodity-types), [Server Capabilities](#server-capabilities), and [Coverage Entry Types](#coverage-entry-types) MAY be extended by other specifications to allow for additional strings to be valid. When extending enumerated list, other specifications MUST reference the relevant section in this specification and denote that they are extending the list to add a new string. The additional string MUST be specified with a description of what that string means when it is included in the relevant array.

To facilitate forwards compatibility, Clients MUST ignore unknown or undocumented object values and enumerated strings. If a Client cannot provide adequate functionality based on too many unknown or undocumented object values or enumerated strings, the Client SHOULD refer to the Server's technical documentation (the `documentation` value in the metadata object) or contact the Server's technical support (via the `support` value in the metadata object).

## 7. Examples <a id="examples" href="#examples" class="permalink">🔗</a>

The following is a non-normative example of a Client request and Server response to a metadata endpoint.

```
==Request==
GET /.well-known/carbon-data-spec.json HTTP/1.1
Host: example.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "cds_metadata_version": "v1",
    "cds_metadata_url": "https://example.com/.well-known/carbon-data-spec.json",

    "created": "2022-01-01T00:00:00.000000Z",
    "updated": "2022-06-01T00:00:00.000000Z",

    "name": "Demo Gas & Electric",
    "description": "A fictional utility that can be used for testing and demonstration purposes.",
    "website": "https://example.com/data-access",
    "documentation": "https://example.com/data-access/docs",
    "support": "https://example.com/developers/contact",
    "infrastructure_types": [
        "distribution_utility",
        "metering_provider,
        "supplier"
    ],
    "commodity_types": [
        "electricity",
        "natural_gas"
    ],
    "capabilities": [
        "coverage",
    ],

    "coverage": "https://static.example.com/cds-coverage.json"
}
```

The following is a non-normative example of a Client request and Server response to a coverage endpoint.

```
==Request==
GET /cds-coverage.json HTTP/1.1
Host: static.example.com

==Response==
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "coverage_entries": [
        {
            "id": "norcal",
            "type": "electric_service_territory",
            "updated": "2022-06-01T00:00:00.000000Z",
            "name": "DG&E Electric Service Territory",
            "description": "Covers most of northern California from Fresno to Redding",
            "map_resource": "https://static.example.com/cds-coverage-map.png",
            "map_content_type": "image/png",
            "geojson_resource": "https://static.example.com/cds-coverage-map-geo.json"
        }
    ],
    "next": null,
    "previous": null
}
```

## 8. Security Considerations <a id="security" href="#security" class="permalink">🔗</a>

This specification involves a utility or other entity publishing details about itself. Server operators MUST review all material published in the metadata and coverage endpoints and make sure it is information that is allowed to be made available to Clients. This is especially true for [well-known metadata endpoints](#metadata-well-known-uri), as not only are these endpoints public, they are intentionally published with a URL structure that allows them to auto-discovered by Clients.

### 8.1. Restricted Access <a id="restricted-access" href="#restricted-access" class="permalink">🔗</a>

Servers that wish to restrict access to a metadata or coverage endpoint to certain Clients MUST configure well established authentication processes for Clients to ensure that only the approved Clients may access the restricted endpoint.

This specification does not describe specifically how Servers will authenticate Clients, as these restricted access protocols are context dependent. For example, if a Server is providing the metadata endpoint as part of an existing logged in portal, then they can use that logged in portal's session cookie to authenticate Client requests to the metadata endpoint.

[Well-known metadata endpoints](#metadata-well-known-uri) MUST NOT require Client authentication to access, since these metadata endpoints are intended to be published publicly.

### 8.2. Rate Limiting <a id="rate-limiting" href="#rate-limiting" class="permalink">🔗</a>

For [well-known metadata endpoints](#metadata-well-known-uri) and other publicly accessible metadata and coverage endpoints, Serves SHOULD configure rate limiting restrictions so that bots and misconfigured scripts will not flood and overwhelm the endpoints with requests, while still allowing legitimate and low-volume requests have access to the endpoints.

## 9. References <a id="references" href="#references" class="permalink">🔗</a>

<span style="background-color:yellow">TODO</span>

## 10. Acknowledgments <a id="acknowledgments" href="#acknowledgments" class="permalink">🔗</a>

The authors would like to thank the late Shuli Goodman, who was the Executive Director of LFEnergy, for her incredible leadership in initially organizing the Carbon Data Specification.

## 11. Authors' Addresses <a id="authors-addresses" href="#authors-addresses" class="permalink">🔗</a>

Daniel Roesler  
UtilityAPI  
Email: [daniel@utilityapi.com](mailto:daniel@utilityapi.com)  
URI: [https://utilityapi.com/](https://utilityapi.com/)

