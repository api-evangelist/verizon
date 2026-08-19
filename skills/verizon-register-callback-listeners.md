---
name: Register Verizon ThingSpace callback listeners
description: >-
  Stand up and register the ThingSpace callback (webhook) listeners that carry every
  asynchronous result and notification on the Connectivity Management API.
api: openapi/verizon-callbacks-api-openapi.yml
operations:
  - loginSession
  - listRegisteredCallbacks
  - registerCallback
provider: Verizon
authored_by: API Evangelist
provider_published: false
generated: '2026-08-04'
method: generated
---

# Register Verizon ThingSpace callback listeners

Almost everything interesting on the Connectivity Management API is asynchronous.
The synchronous response is a `requestId`; the answer arrives on a callback. If you
have not registered a listener, the answer is simply lost. Do this first.

## 1. Authenticate

Bearer token from `https://thingspace.verizon.com/api/ts/v1/oauth2/token` (1 hour),
then `loginSession` for the `VZ-M2M-Token` session token (20 minutes idle timeout).

## 2. Check what is already registered — `listRegisteredCallbacks`

`GET /callbacks/{accountName}` returns the `CallbackSummary` set for the account.

**Registration is one listener per callback service per account.** Registering a
second URL for a service you already registered will not give you two listeners —
check first.

## 3. Register — `registerCallback`

`POST /callbacks/{accountName}` with a `RegisterCallbackRequest`: the callback
service name and your listener URL.

### Callback services you can register

**Asynchronous API responses**

| Service | Delivers |
|---|---|
| `CarrierService` | Activation, suspension, restoration, deactivation results |
| `DeviceService` | Device upload results, device availability checks |
| `DevicePRLInformation` | Current device PRL values |
| `DeviceProfileService` | Profile download / enable / disable / delete results |
| `DeviceSuspensionStatus` | Suspension status after a status inquiry |
| `DeviceUsage` | Aggregated device usage results |
| `DiagnosticsService` | SCEF device registration and monitoring state changes |
| `EnhancedConnectivityService` | SMS delivery confirmation and device message receipt |
| `StateService` | State transition results |

**ThingSpace notifications**

| Service | Delivers |
|---|---|
| `AlertService` | Trigger condition activations |
| `ExternalProvisioningChanges` | Provisioning changes made outside the API |
| `ResumeTrackingNotification` | Seven-day notice before a suspended device auto-resumes |
| `SubscriptionNotificationService` | Data throttling and usage threshold alerts |
| `PromoChanges` | Promotional code expiration and removal |

**Device messages**

`EnhancedConnectivityService` also carries inbound SMS from devices.

## 4. Build the listener to Verizon's delivery contract

- Accept HTTPS with a third-party certificate, or whitelist Verizon source IPs.
- Respond fast. A failed delivery is retried **3 times at 5-minute intervals**
  (4 attempts total), then archived for **30 days**.
- Be idempotent on your own side: because retries exist and no deduplication key is
  guaranteed, the same message can arrive more than once. Key on `requestId`.
- Handle both shapes: a success payload for the service, and a `faultResponse`
  (`faultcode`, `faultstring`, `status: Failed`, `requestId`, `deviceIds`,
  `callbackCount`, `maxCallbackThreshold`).

## 5. Deregistration

A Deregister Callback Listener operation is documented but has no `operationId` in
the harvested OpenAPI — call it against the published reference, not from the spec:
<https://thingspace.verizon.com/documentation/apis/connectivity-management/api-reference/deregister-callback-listener.html>

## References

- `asyncapi/verizon-thingspace-callbacks-webhooks.yml` — the full callback catalogue
- `errors/verizon-error-codes.yml` — `faultcode` classes and codes
- `authentication/verizon-authentication.yml`
