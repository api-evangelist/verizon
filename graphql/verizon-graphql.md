# Verizon GraphQL Schema

## Overview

This conceptual GraphQL schema models Verizon's telecom, network, and connectivity services as exposed through the ThingSpace IoT platform, 5G Edge computing infrastructure, TM Forum service management APIs, and consumer wireless account management capabilities. The schema spans consumer account management, device lifecycle, network quality, billing, IoT device management, fleet tracking, and security features.

## Source APIs

- **ThingSpace Connectivity API** — IoT device activation, management, SMS, callbacks
- **5G Edge Portal API** — 5G edge compute access, MEC node allocation
- **TM Forum Service Management APIs** — incident, change, order, billing, inventory management
- **CPaaS Voice API** — IVR, call routing, call detail reporting
- **Developer Portal** — https://developer.verizon.com / https://developers.verizon.com

## Schema Design

The schema is organized around the following domains:

### Account and Identity
- `Account`, `AccountHolder`, `MyVerizon`, `PhoneNumber`, `LineOfService`
- Authentication objects: `APIKey`, `OAuthToken`

### Device Management
- `Device`, `DeviceID`, `IMEI`, `SIM`, `eSIM`
- IoT: `IoTDevice`, `ThingspaceDevice`, `ThingsborneDevice`, `ConnectCarDevice`, `HumDevice`
- Fleet: `FleetTracking`

### Plans and Services
- `Plan`, `ConnectPlan`, `DataPlan`, `VoicePlan`, `TextPlan`
- `SharedData`, `MobileHotspot`, `TravelPass`, `International`, `RoamingBenefit`

### Usage and Reporting
- `DataUsage`, `UsageSummary`

### Communications
- `VoiceCall`, `CallLog`, `SMS`, `MMS`, `Voicemail`

### Network
- `NetworkQuality`, `NetworkNotification`, `FiveGAccess`, `FiveGNSA`, `FiveGUW`
- `FiveGCoverage`, `LTECoverage`, `CoverageMap`, `Location`, `DeviceLocation`

### Security and Controls
- `SafetyMode`, `SecureNet`, `CallFilter`, `ContentFilter`, `FamilyBase`, `DigitalSecure`

### Billing and Payments
- `Invoice`, `BillingStatement`, `AutoPay`, `PaymentMethod`, `DevicePayment`

### Device Commerce and Protection
- `DeviceUpgrade`, `TradeInEstimate`, `DeviceProtect`, `SquareTrade`, `AsurionClaim`

### Support
- `CustomerCare`, `SupportRequest`

### Webhooks and Events
- `Webhook`

## Type Count

65+ named types including scalars, enums, interfaces, and object types.

## Notes

- Verizon API access is primarily via partner or B2B contracts; no public self-serve pricing is published.
- ThingSpace IoT APIs expose the most developer-accessible REST endpoints and form the basis for device management types.
- The 5G Edge APIs target enterprise/MEC partner scenarios via AWS Wavelength and Google Cloud MEC integrations.
- TM Forum API types (incident, change, order, billing) reflect ITIL-aligned enterprise service management workflows.
- CPaaS types (VoiceCall, CallLog) are scoped to IP Contact Center (IPCC) customers only.
