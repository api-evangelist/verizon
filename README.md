# Verizon (verizon)
Verizon is a leading telecommunications company providing wireless, wireline, broadband, and global enterprise services. Verizon offers developer APIs for IoT device management via ThingSpace, 5G edge computing, TM Forum service management, dynamic network bandwidth, and communications platform APIs for contact center and SMS solutions.

**URL:** [https://developers.verizon.com/](https://developers.verizon.com/)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Wireless, Telecommunications, IoT, 5G, Enterprise, Network APIs

## Timestamps

- **Created:** 2024-11-19
- **Modified:** 2026-05-03

## APIs

### Verizon 5G Edge
Software Management Services API lets customers manage, schedule and distribute software updates to eligible 4G and 5G Internet of Things devices.

**Human URL:** [https://www.verizon.com/business/5g-edge-portal/api-documentation.html](https://www.verizon.com/business/5g-edge-portal/api-documentation.html)

#### Tags:

 - Wireless

#### Properties

- [Documentation](https://www.verizon.com/business/5g-edge-portal/api-documentation.html)
- [Portal](https://www.verizon.com/business/5g-edge-portal/index.html)
- [APIReference](https://www.verizon.com/business/5g-edge-portal/documentation/verizon-5g-edge-discovery-service/api-reference.html)

### Verizon ThingSpace
ThingSpace gives organizations of all sizes all the tools to build IoT solutions or use end-to-end solutions to solve business problems.

**Human URL:** [https://thingspace.verizon.com](https://thingspace.verizon.com)

#### Tags:

 - IoT, Device Management, Connectivity, Wireless

#### Properties

- [Documentation](https://thingspace.verizon.com)
- [APIReference](https://thingspace.verizon.com/resources/documentation/connectivity/API_Reference/)
- [OpenAPI](openapi/verizon-thingspace-connectivity-openapi.yml)
- [SDK - Python SDK](https://github.com/sdks-io/verizon-apis-python-sdk)
- [SDK - PHP SDK](https://packagist.org/packages/sdksio/verizon-apis-sdk)

### Verizon Communications Platform as a Service (CPaaS)
Available exclusively for IP Contact Center (IPCC) customers, providing APIs for inbound and outbound IP interactive voice response (IPIVR) and call detail reporting.

**Human URL:** [https://www.verizon.com/business/en-gb/products/contact-center-cx-solutions/communications-platform-as-a-service/](https://www.verizon.com/business/en-gb/products/contact-center-cx-solutions/communications-platform-as-a-service/)

### Verizon Inventory Management
TM Forum certified inventory management API for enterprise service synchronization.

**Human URL:** [https://developers.verizon.com/#/apis/ns/products/service-management-apis/dep-inventory-management-tmf](https://developers.verizon.com/#/apis/ns/products/service-management-apis/dep-inventory-management-tmf)

### Verizon Dynamic Bandwidth APIs
Real-time network bandwidth provisioning and scaling for enterprise private IP networks.

**Human URL:** [https://developers.verizon.com/#/apis/ns/products/private-ip-apis/dynamic-bandwidth-apis](https://developers.verizon.com/#/apis/ns/products/private-ip-apis/dynamic-bandwidth-apis)

## Common Properties

- [Website](https://www.verizon.com)
- [Portal](https://developers.verizon.com/)
- [Support](https://developers.verizon.com/#/apis/ns/documentation/help)
- [FAQ](https://developers.verizon.com/#/apis/ns/documentation/frequently-asked-questions)
- [Login](https://secure.verizon.com/signin?goto=https://developers.verizon.com/apis/sec/v1/login)
- [PrivacyPolicy](https://www.verizon.com/about/privacy/)
- [TermsOfService](https://www.verizon.com/about/terms-conditions/)

## Features

| Name | Description |
|------|-------------|
| IoT Device Lifecycle Management | Activate, deactivate, and manage IoT devices on Verizon's wireless network via ThingSpace APIs. |
| 5G Software Management | Manage, schedule, and distribute software updates to 4G and 5G IoT devices. |
| Device Diagnostics | Remote device diagnostics, observations, and factory reset capabilities for IoT deployments. |
| TM Forum Service Management | TM Forum-certified ITIL APIs for inventory, incident, change, order, and billing management. |
| Dynamic Bandwidth APIs | Real-time network bandwidth provisioning and scaling for enterprise private IP networks. |
| SMS Messaging to Devices | Send and receive SMS messages to/from IoT devices for remote management and alerts. |
| Callback Subscriptions | Subscribe to device event notifications via webhooks for real-time IoT event processing. |

## Use Cases

| Name | Description |
|------|-------------|
| IoT Fleet Management | Manage large-scale IoT device fleets with activation, deactivation, and status monitoring. |
| Remote Device Management | Remotely diagnose, configure, and update IoT devices over Verizon's wireless network. |
| Enterprise Network Automation | Automate network bandwidth provisioning and IT service management with TM Forum APIs. |
| 5G Edge Applications | Build ultra-low-latency applications on Verizon's 5G edge computing infrastructure. |

## Integrations

| Name | Description |
|------|-------------|
| AWS Wavelength | Deploy 5G Edge applications on Verizon MEC nodes through AWS Wavelength partnership. |
| Google Cloud MEC | Build edge-native applications through Verizon and Google Cloud edge computing integration. |
| ITSM Platforms | Connect TM Forum service management APIs to ServiceNow and other ITSM platforms. |
| IoT Platforms | Integrate ThingSpace device management with enterprise IoT platforms and data lakes. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Verizon ThingSpace Connectivity Management API](openapi/verizon-thingspace-connectivity-openapi.yml)

### JSON Schema

- [thingspace-connectivity-account-information-schema.json](json-schema/thingspace-connectivity-account-information-schema.json)
- [thingspace-connectivity-device-information-schema.json](json-schema/thingspace-connectivity-device-information-schema.json)
- [thingspace-connectivity-device-id-schema.json](json-schema/thingspace-connectivity-device-id-schema.json)
- [thingspace-connectivity-device-list-request-schema.json](json-schema/thingspace-connectivity-device-list-request-schema.json)
- [thingspace-connectivity-device-list-response-schema.json](json-schema/thingspace-connectivity-device-list-response-schema.json)
- [thingspace-connectivity-activate-devices-request-schema.json](json-schema/thingspace-connectivity-activate-devices-request-schema.json)
- [thingspace-connectivity-deactivate-devices-request-schema.json](json-schema/thingspace-connectivity-deactivate-devices-request-schema.json)
- [thingspace-connectivity-send-sms-request-schema.json](json-schema/thingspace-connectivity-send-sms-request-schema.json)
- [thingspace-connectivity-callback-summary-schema.json](json-schema/thingspace-connectivity-callback-summary-schema.json)
- [thingspace-connectivity-device-request-response-schema.json](json-schema/thingspace-connectivity-device-request-response-schema.json)

### JSON Structure

- [thingspace-connectivity-account-information-structure.json](json-structure/thingspace-connectivity-account-information-structure.json)
- [thingspace-connectivity-device-information-structure.json](json-structure/thingspace-connectivity-device-information-structure.json)

### JSON-LD

- [verizon-thingspace-connectivity-context.jsonld](json-ld/verizon-thingspace-connectivity-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Verizon ThingSpace Connectivity Management API](capabilities/shared/thingspace-connectivity.yaml) — 7 operations for device lifecycle, SMS, and callback management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [IoT Device Management](capabilities/iot-device-management.yaml) | Verizon ThingSpace Connectivity | 7 | IoT Platform Engineer, Device Operations Manager, Network Administrator |

## Vocabulary

- [Verizon Vocabulary](vocabulary/verizon-vocabulary.yaml) — Unified taxonomy mapping 4 resources, 7 actions, 1 workflow, and 3 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Verizon Spectral Rules](rules/verizon-spectral-rules.yml) — 29 rules across 11 categories enforcing Verizon API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
