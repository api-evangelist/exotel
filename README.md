# Exotel (exotel)

Exotel is an Indian cloud telephony and customer-engagement (CPaaS) platform offering programmable voice, SMS, virtual numbers (ExoPhones), IVR/call flows, call campaigns, and call-center tooling. Its Twilio-style REST APIs place outbound calls, send SMS, return call and number metadata, and manage campaigns. Exotel AgentStream adds a documented WebSocket voice-streaming API for real-time voicebots.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/exotel/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/exotel/refs/heads/main/apis.yml)

## Access Model (Read This First)

- **Authentication:** HTTP Basic. Your **API Key** is the username and your **API Token** is the password. Both, along with your **Account SID**, come from the Exotel Dashboard → Settings → API Settings. Credentials can be passed via the `Authorization: Basic base64(key:token)` header (recommended) or embedded in the URL as `https://<api_key>:<api_token>@<subdomain>/...`.
- **Account SID:** Appears in every path: `/v1/Accounts/<account_sid>/...` (and `/v2/accounts/<account_sid>/...` for Campaigns).
- **Region subdomains:** `api.exotel.com` (Singapore cluster, default) and `api.in.exotel.com` (Mumbai / India cluster). Use the subdomain that matches where your account is provisioned.
- **Response format:** Exotel APIs return **XML by default**. Append `.json` to a resource path to receive JSON.
- **India regulatory:** SMS to Indian numbers requires **DLT** registration (`DltEntityId`, and typically a `DltTemplateId`).
- **AgentStream WebSocket direction:** For real-time voice streaming, **Exotel is the WebSocket client** — it connects out to a `wss://` endpoint that **you** host and configure on a Voicebot/Stream applet. There is no fixed Exotel-hosted `wss://` URL to dial.

## Real vs Modeled

Endpoint **paths and methods** for `Calls/connect`, `Calls/{CallSid}`, `Numbers/{Number}`, `Sms/send`, and the v2 `campaigns` resource are **confirmed** from Exotel's developer docs. The bulk `Calls` list and `Sms/Messages/{SmsSid}` details paths are **modeled** on Exotel's Twilio-style conventions (documented as supported; verify exact paths). Request/response **field schemas** in the OpenAPI are modeled from documented parameter lists — Exotel does not publish a machine-readable OpenAPI. The AgentStream AsyncAPI message shapes are grounded in the documented example JSON messages.

## Tags

- Cloud Telephony
- Voice
- SMS
- India
- CPaaS
- Call Center
- IVR
- Numbers
- Communications
- Customer Engagement

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Exotel Voice Call API

Place outbound voice calls via `POST /v1/Accounts/{sid}/Calls/connect` — connect two phone numbers (call `From`, then bridge to `To`) or connect a number to an Exotel call flow / applet via the `Url` parameter. Supports recording, time limits, wait audio, and status callbacks.

- **Human URL:** [https://developer.exotel.com/api/make-a-call-api](https://developer.exotel.com/api/make-a-call-api)
- **Base URL:** `https://api.exotel.com/v1/Accounts`

#### Tags

- Voice
- Calls
- IVR

#### Properties

- [Documentation](https://developer.exotel.com/api/make-a-call-api)
- [API Reference](https://developer.exotel.com/api/make-a-call-api)
- [OpenAPI](openapi/exotel-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/exotel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/exotel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Exotel Call Details API

Retrieve details of a single call by Sid (`GET /v1/Accounts/{sid}/Calls/{CallSid}`) including status, direction, duration, price, and recording URL, plus bulk call queries filterable by date and status.

- **Human URL:** [https://developer.exotel.com/api](https://developer.exotel.com/api)
- **Base URL:** `https://api.exotel.com/v1/Accounts`

#### Tags

- Calls
- Call Details
- Reporting

#### Properties

- [Documentation](https://developer.exotel.com/api)
- [OpenAPI](openapi/exotel-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/exotel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/exotel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Exotel SMS API

Send single SMS from an ExoPhone or approved Sender ID via `POST /v1/Accounts/{sid}/Sms/send`, with India DLT entity/template support, encoding and priority options, delivery status callbacks, and message-detail lookup.

- **Human URL:** [https://developer.exotel.com/api/sms](https://developer.exotel.com/api/sms)
- **Base URL:** `https://api.exotel.com/v1/Accounts`

#### Tags

- SMS
- Messaging
- DLT

#### Properties

- [Documentation](https://developer.exotel.com/api/sms)
- [API Reference](https://developer.exotel.com/docs/sms-api/api-reference/send-sms)
- [OpenAPI](openapi/exotel-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/exotel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/exotel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Exotel Numbers API

Look up telecom metadata for a phone number via `GET /v1/Accounts/{sid}/Numbers/{Number}` — operator/circle, number type, and DND status where available for Indian numbers.

- **Human URL:** [https://developer.exotel.com/api](https://developer.exotel.com/api)
- **Base URL:** `https://api.exotel.com/v1/Accounts`

#### Tags

- Numbers
- Metadata
- Telecom

#### Properties

- [Documentation](https://developer.exotel.com/api)
- [OpenAPI](openapi/exotel-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/exotel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/exotel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Exotel Campaigns API

Create, list, get, update (pause/resume), and delete bulk outbound call campaigns under the v2 API (`POST/GET/PUT/DELETE /v2/accounts/{sid}/campaigns`), and pull per-call records via `campaigns/{id}/call-details`.

- **Human URL:** [https://developer.exotel.com/api](https://developer.exotel.com/api)
- **Base URL:** `https://api.exotel.com/v2/accounts`

#### Tags

- Campaigns
- Outbound
- Bulk

#### Properties

- [Documentation](https://developer.exotel.com/api)
- [OpenAPI](openapi/exotel-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/exotel.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/exotel.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Exotel AgentStream Voice Streaming API

Documented WebSocket (`wss://`) voice-streaming API. When a call reaches a Voicebot or Stream applet, Exotel opens a secure WebSocket to your endpoint and streams base64 linear-PCM audio in ~100 ms frames (`connected`/`start`/`media`/`dtmf`/`mark`/`stop`); the Voicebot applet is bidirectional so your server sends `media`/`mark`/`clear` back to speak to the caller and barge in. Exotel is the WebSocket client; you host the endpoint.

- **Human URL:** [https://developer.exotel.com/docs/agentstream/developer-guide](https://developer.exotel.com/docs/agentstream/developer-guide)
- **Base URL:** `wss://your-bot-host.example.com`

#### Tags

- WebSocket
- Voice Streaming
- Voicebot
- Real Time

#### Properties

- [Documentation](https://developer.exotel.com/docs/agentstream/developer-guide)
- [AsyncAPI](asyncapi/exotel-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/v2.6.0)

## Common Properties

- [Domain Security](security/exotel-domain-security.yml)
- [Authentication](authentication/exotel-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/exotel)
- [Website](https://exotel.com)
- [Documentation](https://developer.exotel.com)
- [Plans](plans/exotel-plans-pricing.yml)
- [Rate Limits](rate-limits/exotel-rate-limits.yml)
- [Fin Ops](finops/exotel-finops.yml)
- [Blog](https://exotel.com/blog/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
