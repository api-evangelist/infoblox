# Infoblox (infoblox)

Infoblox is a networking and cybersecurity company providing DDI (DNS, DHCP,
and IPAM) solutions and protective DNS-layer security services. Its product
portfolio spans the Universal DDI suite for unified hybrid and multi-cloud
network services, NIOS DDI for on-premises deployments, NIOS-X as a Service,
Threat Defense for DNS-layer security, threat intelligence (TIDE) and
research (Dossier), and NetMRI for network change and configuration
management.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/infoblox/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags:

 - Cloud, DDI, DHCP, DNS, IPAM, Network Management, Security, Threat Intelligence

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-04-28

## APIs

### Infoblox WAPI (Web API)

RESTful API for managing Infoblox NIOS DDI (DNS, DHCP, IPAM) services, network objects, and configuration. The WAPI uses standard HTTP methods for CRUD operations and supports JSON and XML input and output formats.

**Human URL:** [https://www.infoblox.com/products/ddi/](https://www.infoblox.com/products/ddi/)

**Base URL:** https://{grid-master}/wapi/v2.12

#### Tags:

 - DDI, DHCP, DNS, IPAM, Network Management

#### Properties

- [Documentation](https://docs.infoblox.com/)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/infoblox/refs/heads/main/openapi/infoblox-wapi-openapi.yml)
- [Reference](https://docs.infoblox.com/space/niosapi/)
- [Authentication](https://docs.infoblox.com/space/niosapi/22644231/WAPI+Authentication)
- [Swagger](https://{grid-master}/wapidoc/)
- [Change Log](https://docs.infoblox.com/space/nios90/318210347/What's+New)
- [Client Libraries](https://github.com/infobloxopen/infoblox-go-client)

### Infoblox BloxOne API

Cloud-native API for Infoblox BloxOne DDI and Threat Defense services. Provides RESTful web services for interacting with the Infoblox Cloud Service Platform (CSP) to manage and automate DDI services in the cloud.

**Human URL:** [https://www.infoblox.com/products/bloxone-ddi/](https://www.infoblox.com/products/bloxone-ddi/)

**Base URL:** https://csp.infoblox.com/api

#### Tags:

 - Cloud, DHCP, DNS, IPAM, Security, Threat Defense

#### Properties

- [Documentation](https://docs.infoblox.com/space/BloxOneDDI/)
- [OpenAPI](https://csp.infoblox.com/apidoc/)
- [API Portal](https://csp.infoblox.com/)
- [Authentication](https://docs.infoblox.com/space/BloxOneDDI/35430405/Authentication)
- [Getting Started](https://www.infoblox.com/developer-portal/getting-started/)

### Infoblox BloxOne DNS Configuration API

API for configuring DNS settings within the BloxOne platform. Manages DNS server configurations, views, ACLs, forwarding rules, and other DNS infrastructure settings through the Cloud Service Platform.

**Human URL:** [https://csp.infoblox.com/apidoc/?url=https%3A%2F%2Fcsp.infoblox.com%2Fapidoc%2Fdocs%2FDnsConfig](https://csp.infoblox.com/apidoc/?url=https%3A%2F%2Fcsp.infoblox.com%2Fapidoc%2Fdocs%2FDnsConfig)

**Base URL:** https://csp.infoblox.com/api/ddi/v1

#### Tags:

 - Cloud, Configuration, DNS

### Infoblox BloxOne DNS Data API

API for managing DNS data records within the BloxOne platform. Provides endpoints for creating, reading, updating, and deleting DNS resource records including A, AAAA, CNAME, MX, TXT, and other record types.

**Base URL:** https://csp.infoblox.com/api/ddi/v1

#### Tags:

 - Cloud, DNS, Records

### Infoblox BloxOne IPAM/DHCP API

API for IP address management and DHCP protocol features within the BloxOne platform. Provides visibility and provisioning tools for managing networking spaces, monitoring IP address infrastructures, and integration with DNS and DHCP protocols.

**Base URL:** https://csp.infoblox.com/api/ddi/v1

#### Tags:

 - Cloud, DHCP, IPAM, Network Management

### Infoblox BloxOne DDI Keys API

API for managing TSIG and other keys used in DDI operations within the BloxOne platform. Handles creation and management of authentication keys used for securing DNS zone transfers and dynamic updates.

**Base URL:** https://csp.infoblox.com/api/ddi/v1

#### Tags:

 - Authentication, DNS Security, Keys

### Infoblox BloxOne Anycast Configuration API

API for managing anycast configurations within the BloxOne platform. Enables high availability configuration of Infoblox applications running on customer premises by managing anycast addressing and routing.

**Base URL:** https://csp.infoblox.com/api/anycast/v1

#### Tags:

 - Anycast, High Availability, Network Management

### Infoblox BloxOne Infrastructure Management API

API for managing BloxOne Cloud infrastructure components. Provides endpoints for managing on-premises hosts, service configurations, and infrastructure resources within the Infoblox Cloud Service Platform.

**Base URL:** https://csp.infoblox.com/api/infra/v1

#### Tags:

 - Cloud, Infrastructure, Management

### Infoblox BloxOne Host Activation API

API for provisioning and activating on-premises hosts within the BloxOne platform. Handles the host activation workflow including zero touch provisioning and bootstrap configuration for on-prem deployments.

**Base URL:** https://csp.infoblox.com/api/host_app/v1

#### Tags:

 - Host Activation, Infrastructure, Provisioning

### Infoblox BloxOne DNS Forwarding Proxy API

API for managing DNS Forwarding Proxy (DFP) configurations within BloxOne Threat Defense. Enforces DNS client-based security policies at remote sites by forwarding DNS queries through the Infoblox cloud for threat inspection and policy enforcement.

**Base URL:** https://csp.infoblox.com/api/atcdfp/v1

#### Tags:

 - DNS, Forwarding Proxy, Security

### Infoblox BloxOne Firewall API

API for managing BloxOne Threat Defense Cloud firewall policies and security lists. Provides visibility into infected and compromised devices on the network and allows management of security policies, custom lists, and named lists for DNS-based threat defense.

**Base URL:** https://csp.infoblox.com/api/atcfw/v1

#### Tags:

 - Firewall, Security, Threat Defense

### Infoblox BloxOne Redirect API

API for configuring BloxOne Threat Defense Cloud redirect behavior. Allows configuring traffic redirection to the Infoblox server or custom destinations when threats are detected, and manages redirect pages and custom URL filtering rules.

**Base URL:** https://csp.infoblox.com/api/atcfw/v1

#### Tags:

 - Redirect, Security, Threat Defense

### Infoblox BloxOne Upgrade Policy API

API for managing software upgrade policies for BloxOne on-premises hosts. Allows scheduling and configuring software and configuration updates for deployed BloxOne infrastructure components.

**Base URL:** https://csp.infoblox.com/api/upgrade_policy/v1

#### Tags:

 - Infrastructure, Policy, Upgrade

### Infoblox Threat Defense API

API for threat intelligence, security analytics, and DNS firewall capabilities. Provides programmatic access to BloxOne Threat Defense features including security policy management, threat feeds, and DNS-layer security controls.

**Human URL:** [https://www.infoblox.com/products/threat-defense/](https://www.infoblox.com/products/threat-defense/)

**Base URL:** https://csp.infoblox.com/tide/api

#### Tags:

 - DNS Security, Firewall, Security, Threat Intelligence

### Infoblox TIDE API

Threat Intelligence Data Exchange (TIDE) API for submitting and retrieving threat indicators. Provides access to indicators of compromise in the TIDE database in multiple formats including JSON, XML, STIX, CEF, and CSV. Used for threat intelligence sharing and enrichment workflows.

**Base URL:** https://csp.infoblox.com/tide/api

#### Tags:

 - Indicators, Security, Threat Intelligence, TIDE

### Infoblox Dossier API

Threat research API that provides contextual information from multiple sources simultaneously for a given indicator. Supports lookups on IPs, URLs, domains, hostnames, email addresses, and file hashes (MD5, SHA1, SHA256) to enrich SIEM and security tool data.

**Base URL:** https://csp.infoblox.com/tide/api

#### Tags:

 - Dossier, Research, Security, Threat Intelligence

### Infoblox NetMRI API

RESTful API for the Infoblox NetMRI network change and configuration management platform. Enables automation of network device provisioning, security compliance checks, configuration management, and network discovery workflows.

**Human URL:** [https://www.infoblox.com/products/netmri/](https://www.infoblox.com/products/netmri/)

**Base URL:** https://{netmri-server}/api

#### Tags:

 - Compliance, Configuration Management, Network Automation

## Common Properties

- [Portal](https://www.infoblox.com/developer-portal/)
- [Getting Started](https://www.infoblox.com/developer-portal/getting-started/)
- [Documentation](https://docs.infoblox.com/)
- [Blog](https://blogs.infoblox.com/)
- [Community](https://community.infoblox.com/)
- [Status](https://status.infoblox.com/)
- [Support](https://www.infoblox.com/support/)
- [Website](https://www.infoblox.com/)
- [Privacy Policy](https://www.infoblox.com/company/legal/privacy-policy/)
- [Terms of Service](https://www.infoblox.com/company/legal/website-terms-and-conditions/)
- [GitHub Organization](https://github.com/infobloxopen)
- [Change Log](https://docs.infoblox.com/space/BloxOneInfrastructure/332366018/BloxOne+Release+Notes)
- [Console](https://csp.infoblox.com/)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
