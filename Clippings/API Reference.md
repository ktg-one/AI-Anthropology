---
title: "API Reference"
source: "https://docs.trillet.ai/v1/api-reference/introduction"
author:
  - "[[Trillet AI]]"
published:
created: 2025-11-15
description: "Complete reference for the Trillet AI Platform API"
tags:
  - "clippings"
---
## Overview

The Trillet AI API provides programmatic access to create and manage AI agents, conversation flows, voice calls, and SMS messaging. Our REST API uses standard HTTP methods and returns JSON responses.

## Base URL

`bash https://api.trillet.ai ` 

## Authentication

All API requests require authentication using an API key in the `x-api-key` header:

```
curl https://api.trillet.ai/v1/api/

  -H "x-api-key: YOUR_API_KEY"

  -H "Content-Type: application/json"
```Content-Type

string

required

Must be set to `application/json`.

Get your API key from [Trillet Settings Dashboard](https://app.trillet.ai/settings)

## API Resources## [Call Agents API](https://docs.trillet.ai/v1/api-reference/endpoints/agents/call/create)

[

Create and manage conversational call agents with unique voices and personalities through our REST API

](https://docs.trillet.ai/v1/api-reference/endpoints/agents/call/create)Omni Flow Agents API

Create and manage messaging AI agents with unique through our REST API

[View original](https://docs.trillet.ai/v1/api-reference/endpoints/agents/omniflow/create)Call Flows API

Design and control call & conversation flows programmatically

[View original](https://docs.trillet.ai/v1/api-reference/endpoints/flows/call-flows/create)Message Flows API

Design and control call & conversation flows programmatically

[View original](https://docs.trillet.ai/v1/api-reference/endpoints/flows/message-flows/create)Voice Calls API

Initiate and manage voice calls via REST endpoints

[View original](https://docs.trillet.ai/v1/api-reference/endpoints/calls/initiate-call)Conversations API

Design and control customer interactions through conversations programmatically

[View original](https://docs.trillet.ai/v1/api-reference/endpoints/conversations/generateMessage)

## Rate Limits

The API has rate limits based on your plan. Contact the Trillet team to increase your limits.

## Webhooks \[Coming Soon!\]

Configure webhooks to receive real-time updates about events in your account. Each webhook request includes an event type and relevant data:

```
{

  "event": "call.completed",

  "data": {

    "callId": "call_xyz789",

    "agentId": "agent_123abc",

    "duration": 125,

    "status": "completed"

  }

}
```

### Webhook Events

- `call.started` - When a call begins
- `call.completed` - When a call ends
- `call.failed` - When a call fails to connect
- `sms.sent` - When an SMS is sent
- `sms.delivered` - When an SMS is delivered
- `agent.created` - When a new agent is created
- `agent.updated` - When an agent is updated
- `flow.created` - When a new flow is created
- `flow.updated` - When a flow is updated

### Webhook Security

Verify webhook signatures using the signature in the `X-Trillet-Signature` header:

```
# Your webhook secret from the dashboard

WEBHOOK_SECRET=whsec_xxxxxxxxxxxxx

# Verify the signature before processing webhooks
```

The API uses conventional HTTP response codes:
- `200` - Success
- `400` - Bad request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not found
- `429` - Too many requests
- `500` - Server error
Error responses include a message and error code:

```
{

  "error": {

    "code": "invalid_number",

    "message": "The provided phone number is invalid"

  }

}
```

## Need Help?

## API Status \[Coming Soon!\]

Check our API status and uptime

Support

Get technical support

[View original](https://docs.trillet.ai/v1/api-reference/)

[Authentication](https://docs.trillet.ai/v1/api-reference/authentication)