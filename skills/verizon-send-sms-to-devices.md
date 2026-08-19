---
name: Send SMS to Verizon ThingSpace IoT devices
description: >-
  Authenticate against Verizon ThingSpace and send an SMS message to one or more IoT
  devices, collecting delivery confirmation from the EnhancedConnectivityService
  callback.
api: openapi/verizon-sms-api-openapi.yml
operations:
  - loginSession
  - registerCallback
  - sendSmsToDevices
provider: Verizon
authored_by: API Evangelist
provider_published: false
generated: '2026-08-04'
method: generated
---

# Send SMS to Verizon ThingSpace IoT devices

ThingSpace SMS is machine-to-machine messaging over the Connectivity Management API.
Sending is asynchronous: `sendSmsToDevices` returns a `requestId` and the delivery
confirmation arrives on the `EnhancedConnectivityService` callback.

## 1. Authenticate

Two tokens, both required on every call:

1. `POST https://thingspace.verizon.com/api/ts/v1/oauth2/token`,
   `Authorization: Basic base64(key:secret)` → bearer token, 1 hour TTL.
2. `loginSession` (`POST /session/login`) → session token, sent as `VZ-M2M-Token`,
   expires after 20 minutes of inactivity.

## 2. Register the delivery callback — `registerCallback`

`POST /callbacks/{accountName}` naming the `EnhancedConnectivityService` callback
service and your HTTPS listener URL.

That same service carries **both** directions:

- **Outbound**: SMS delivery confirmations for messages you sent.
- **Inbound**: SMS that devices send *to* ThingSpace, so this is also how you receive
  device-originated messages.

If you only send and never register, you get no delivery signal at all.

## 3. Send — `sendSmsToDevices`

`POST /sms/{accountName}/actions/send` with a `SendSmsRequest`:

- `deviceIds[]` — `{kind, id}` pairs. Valid kinds: `imei`, `meid`, `esn`, `iccid`,
  `min`, `mdn`, `otaid`.
- the message body.

**Length limits are enforced:** 160 characters for a 7-bit message, 140 for 8-bit.
Over either returns `INPUT_INVALID.SmsMessage.TooLong`. An empty message returns
`INPUT_INVALID.SmsMessage.Null`.

Batch limits are the same as elsewhere on this API: 200 devices per request.

The response is a `DeviceRequestResponse` carrying the `requestId`.

## 4. Reconcile on the callback

Match the inbound `EnhancedConnectivityService` message on `requestId`. A failure
arrives as a `faultResponse` — branch on `faultcode`, not `faultstring`.

## Rules that will bite you

- **No idempotency key.** A retried send delivers the message twice. If duplicate
  delivery matters, dedupe on your own key before calling.
- Devices must be in the `active` state; otherwise
  `INPUT_INVALID.DeviceState.Invalid`.
- `REQUEST_FAILED.DeviceNotFound` means the device is not on this account, not that
  it is offline.
- No pagination or filtering exists on this surface — selection happens entirely in
  the request body.

## References

- `authentication/verizon-authentication.yml`
- `errors/verizon-error-codes.yml`
- `asyncapi/verizon-thingspace-callbacks-webhooks.yml`
- `conventions/verizon-conventions.yml`
