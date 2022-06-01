---
layout: base
nav: specs
title: CDSC-WG1 - 01 Server Metadata - Overview
meta_description: Linux Foundation Energy - Carbon Data Specification Consortium (CDSC) - Customer DataWorking Group (WG1) - Specifications - cdsc-wg1-01 - Server Metadata - Overview
---
[Home]({{ "/" | relative_url }}) / [Specifications]({{ "/specs" | relative_url }}) / [`cdsc-wg1-01` - Server Metadata]({{ "/specs/cdsc-wg1-01" | relative_url }}) / Overview

# Server Metadata - Overview

This is a summary overview of [`cdsc-wg1-01`]({{ "/specs/cdsc-wg1-01" | relative_url }}), which
describes how utility customer data servers ("Servers") provide a structured reference of
information about them, the functionality they offer, and how other entities ("Clients") can
interoperate with them.

**NOTE:** Utility customer data servers ("Servers") are not always run by utilities themselves. They
could be other types of energy companies, such as electric retailers or community choice aggregators
(CCAs). They can also be centralized entities such as state-run data warehouses or private
infrastructure providers. Throughout this overview, the term "utility or entity" is used instead of
just "utility" to describe the organizations providing access to utility customer data.

## Background <a id="background" href="#background" class="permalink">🔗</a>

There are thousands of utilities serving customers across the world, and each has their own way of
organizing and structuring customer data. For [use case]({{ "/use-cases" | relative_url }})
companies needing to obtain customer data, an efficient means of discovering, registering, and
interoperating with these utilities is needed.

## Example <a id="example" href="#example" class="permalink">🔗</a>

Server metedata is provided under the [well-known url](https://datatracker.ietf.org/doc/html/rfc8615)
`"/.well-known/carbon-data-spec.json`. The response is a structured object containing information
about the server, what functionality it offers, and how to interoperate with it.

```
GET /.well-known/carbon-data-spec.json HTTP/1.1
Host: demoutility.com

{
    "server_version": "v1",
    "server_name": "Demo Gas & Electric",
    "server_description": "A fictional utility that can be used for testing and demonstration purposes.",
    "server_url": "https://demoutility.com/data-access",
    "server_documentation": "https://demoutility.com/data-access/docs",
    "server_capabilities": [
        "oauth",
        "customer_data",
        "extra_ieee1547"
    ],

    "oauth_metadata": "https://demoutility.com/.well-known/oauth-authorization-server",
    "oauth_client_registration_human": "https://demoutility.com/data-access/register",
    "oauth_client_registration_additional_metadata": [
        {
            "name": "cds_scopes_of_use",
            "required": true
        },
        {
            "name": "cds_webhook_urls",
            "required": false
        }
    ],

    "customer_data_api": "https://api.demoutility.com/cds/v1",
    "customer_data_human": "https://demoutility.com/client-dashboard",

    "extra_ieee1547_setup": "https://demoutility.com/smart-inverters/setup"
}
```

## Metadata Structure <a id="components" href="#components" class="permalink">🔗</a>

Overall information about the Server is grouped with a `server_*` prefix:

* `server_version` - _string_ - Which version of server metadata structure this server follows (currently `v1` is the only version)
* `server_name` - _string_ - The name of the utility or entity (e.g. "Demo Gas & Electric")
* `server_description` - _string_ - A brief description about the utility or entity (e.g. "An electric and gas utility serving customers in Northern California")
* `server_url` - _URL_ - Where users can learn more about the utility or entity and its data access capabilities
* `server_documentation` - _URL_ - Where users can find the utility or entity's technical reference documentation
* `server_capabilities` - _Array[[Capabilities](#capabilities)]_ - What Carbon Data Specification funcationality the utility supports

Other components are listed in the `server_capabilities`, where each listed component can add
additional metadata fields, prefixed with their capability name. For example, the `oauth` capability
will add additional metadata fields prefixed with `oauth_*`.

## Capabilities <a id="capabilities" href="#capabilities" class="permalink">🔗</a>

Below is the list of officially supported capabilities by the CDS Customer Data working group:

* `oauth` - See [`cdsc-wg1-02` (TODO)] - How Clients can register with the Server, as well as the primary method for obtaining customer consent
* `customer_data` - See [`cdsc-wg1-03` (TODO)] - How Clients can access authorized customer data using standarized API endpoints and formats

Servers can extend their list of capabilities with other non-CDS functionalities, but they MUST be prefixed with `extra_*`. For example, if the utility or entity provides connectivity for smart inverters (e.g. IEEE 1547) and wants to list that as a capability in its metadata, it can include something like `extra_ieee1547` as a capability, so that Clients who know how to interpret that capability can auto-discover it.

Clients MUST ignore any capabilities they do not recognize.
