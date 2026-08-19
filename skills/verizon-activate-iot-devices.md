---
name: Activate IoT devices on a Verizon ThingSpace account
description: >-
  Authenticate against Verizon ThingSpace, then activate one or more IoT devices on a
  service plan and collect the asynchronous result from a registered callback.
api: openapi/verizon-devices-api-openapi.yml
operations:
  - loginSession
  - getAccountInformation
  - activateDevices
  - registerCallback
provider: Verizon
authored_by: API Evangelist
provider_published: false
generated: '2026-08-04'
method: generated
---

# Activate IoT devices on a Verizon ThingSpace account

Verizon ThingSpace activation is **asynchronous**. `activateDevices` returns a
`requestId`, not an outcome. The real result arrives later on the `CarrierService`
callback. Plan for that before you start, or you will report success for a device
that never activated.

## Before you start

- ThingSpace application key and secret (ThingSpace console → Account Settings → Key Management → My Keys).
- UWS (Unified Web Services) username and password for the Connectivity Management account.
- An HTTPS endpoint that can receive callbacks, if you want the outcome.
- Base URL: `https://thingspace.verizon.com/api/m2m/v2`

## 1. Mint a ThingSpace access token

`POST https://thingspace.verizon.com/api/ts/v1/oauth2/token` with
`Authorization: Basic base64(key:secret)` and `grant_type=client_credentials`.

The token is valid for **one hour**. Repeat requests inside that hour return the same
token — do not treat a repeated value as a bug, and do not mint one per call.

## 2. Open a Connectivity Management session — `loginSession`

`POST /session/login` carrying the bearer token plus the UWS username and password.
The response is a `SessionLoginResponse` containing the session token.

Send it on every subsequent call as the `VZ-M2M-Token` header, alongside the
`Authorization: Bearer` header. **Both** are required.

The session token expires after **20 minutes of inactivity**. If you get
`REQUEST_FAILED.SessionToken.Expired`, re-run `loginSession`; do not retry the
original call blind.

## 3. Register the callback listener first — `registerCallback`

`POST /callbacks/{accountName}` with the service name `CarrierService` and your
listener URL. Register **before** activating, or the activation result has nowhere
to land.

One registration per callback service per account. Verizon retries a failed delivery
3 times at 5-minute intervals (4 attempts total) and archives failures for 30 days.

## 4. Confirm the account — `getAccountInformation`

`GET /accounts/{accountName}` returns the account, its features, carrier information
and IP pools. Use it to confirm the `accountName` format
(`<billing account>-<sub account>`, e.g. `0000123456-00001`) and that the service
plan you intend to use exists. `REQUEST_FAILED._servicePlan_.NotFound` is the error
you avoid by doing this.

## 5. Activate — `activateDevices`

`POST /accounts/{accountName}/devices/actions/activate` with an
`ActivateDevicesRequest`: the target `deviceIds[]` as `{kind, id}` pairs and the
service plan.

Valid `kind` values: `imei`, `meid`, `esn`, `iccid`, `min`, `mdn`, `otaid`.

**Batch limits are hard:** at most **200 devices per request** and **10,000 devices
across a request set**. Exceeding either returns `INPUT_INVALID.NumberofDevices` or
`INPUT_INVALID.MaxRequestsExceeded`.

The response is a `DeviceRequestResponse` with a `requestId`. Store it — it is the
only key that ties the callback back to this call.

## 6. Wait for the callback

A `CarrierService` message arrives at your listener carrying the same `requestId`.
On failure it is a `faultResponse` with `faultcode`, `faultstring`, `status: Failed`
and the affected `deviceIds`.

`faultcode` is `<ServiceName>.<CLASS>.<Specific>`, e.g.
`UnifiedWebService.REQUEST_FAILED.DeviceAlreadyActive`. Verizon documents the **code**
as stable across releases and the message text as not stable — branch on the code.

## Rules that will bite you

- **There is no idempotency key.** Verizon documents no replay contract. If you retry
  `activateDevices` after a timeout you may activate the batch twice. Guard with your
  own dedupe on `requestId` and check device state before retrying.
- **`REQUEST_FAILED.DeviceAlreadyActive` is not a failure** in most workflows — treat
  it as a no-op.
- **Rate limits are contractual, not published.** Expect `429` with `Retry-After`.
- Illegal characters (apostrophe, `<`, backslash) anywhere in the request return
  `INPUT_INVALID.Request.InvalidCharacter`.

## Test first

Use the ThingSpace API Console simulator. While on the simulator, any value is
accepted for `VZ-M2M-Token`. See `sandbox/verizon-sandbox.yml`.

## References

- `authentication/verizon-authentication.yml`
- `conventions/verizon-conventions.yml`
- `errors/verizon-error-codes.yml`
- `asyncapi/verizon-thingspace-callbacks-webhooks.yml`
