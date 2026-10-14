# API Reference: End User Schema API

> **About this sample**
>
> - **Type:** REST API reference
> - **Audience:** Developers integrating their user data with GuideFlow
> - **My role:** Documented the API while building and testing customer integrations with Postman
>
> This sample is based on documentation I wrote for a digital adoption platform. Product names, URLs, identifiers, and example data have been replaced with a fictional product, *GuideFlow*, to protect client and employer confidentiality. Example requests and responses are illustrative.

Use the End User Schema API to manage the custom fields that describe your users, such as their role, department, or start date. GuideFlow uses these fields to decide which users see which content.

With this API, you can:

- Get every field in your account's end user schema.
- Add custom fields or update existing ones.
- Get the details of a single field by name.

## Table of contents

- [Before you begin](#before-you-begin)
- [Authentication](#authentication)
- [Data types](#data-types)
- [Status codes](#status-codes)
- [Errors](#errors)
- [Get the end user schema](#get-the-end-user-schema)
- [Add or update custom fields](#add-or-update-custom-fields)
- [Get a field by name](#get-a-field-by-name)

## Before you begin

- **Base URL:** All requests in this reference use `https://api.example.com`.
- **Account ID:** Each endpoint needs your account ID, called `entId`. You can find it on the GuideFlow dashboard under **Settings** > **Account**.
- **Format:** Requests and responses use JSON. For requests with a body, set the `Content-Type` header to `application/json`.

## Authentication

Every request needs two headers:

| Header | Value |
| --- | --- |
| `x-guideflow-integration-key` | Your API integration key. To create one, see "Generate an API integration key" in the GuideFlow Help Center. |
| `x-guideflow-user` | The email address of the GuideFlow user making the request. |

If either header is missing or invalid, the API returns `401 Unauthorized`.

> **Important:** Treat your integration key like a password. Don't commit it to source control or include it in client-side code.

## Data types

Each custom field has one of the following types:

| Type | Description | Example value |
| --- | --- | --- |
| `boolean` | True or false. | `true` |
| `double` | A number, with or without decimals. | `20.78` |
| `string` | Text. | `"manager"` |
| `timestamp` | A date and time in ISO 8601 format. | `"2001-07-04T12:08:56.235-0700"` |
| `encrypted_string` | Text that GuideFlow stores encrypted. Use this type for sensitive values. | `"john.doe@example.com"` |

## Status codes

| Code | Meaning |
| --- | --- |
| `200 OK` | The request succeeded, and the response body contains the result. |
| `400 Bad Request` | The request body or parameters aren't valid. The response explains what to fix. |
| `401 Unauthorized` | The integration key or user header is missing or not valid. |
| `403 Forbidden` | The integration key doesn't have permission for this account or action. |
| `404 Not Found` | The account or field doesn't exist. |
| `429 Too Many Requests` | You sent too many requests in a short time. Wait, and then retry. |
| `500`, `502`, `503`, `504` | A server error occurred. These requests often succeed if you retry after a short wait. |

## Errors

When a request fails, the response body includes an error code and a message that explains what went wrong:

```json
{
  "error": {
    "code": "FIELD_LIMIT_EXCEEDED",
    "message": "An account can have up to 50 custom fields. This request would bring the total to 52."
  }
}
```

Use `code` to handle errors in your integration, and show or log `message` to help with troubleshooting. Messages can change over time, so don't build logic that depends on their exact wording.

## Get the end user schema

Returns every field in your account's end user schema, including the default fields that GuideFlow provides and any custom fields you've added.

```text
GET /v1/accounts/{entId}/endUserSchema
```

### Path parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `entId` | string | Yes | Your account ID. |

### Example request

```bash
curl https://api.example.com/v1/accounts/acme-123/endUserSchema \
  -H "x-guideflow-integration-key: YOUR_INTEGRATION_KEY" \
  -H "x-guideflow-user: admin@example.com"
```

### Example response

`200 OK`

```json
{
  "defaultFields": [
    {
      "name": "user_id",
      "type": "string",
      "description": "Unique ID for the user."
    },
    {
      "name": "first_seen",
      "type": "timestamp",
      "description": "When GuideFlow first saw the user."
    }
  ],
  "customFields": [
    {
      "name": "employee_role",
      "type": "string",
      "description": "Job role of the user."
    },
    {
      "name": "is_new_hire",
      "type": "boolean",
      "description": "Whether the user started in the last 30 days."
    }
  ]
}
```

## Add or update custom fields

Adds one or more custom fields to the end user schema. If a field with the same name already exists, GuideFlow updates it instead, so you can use this endpoint for both tasks.

An account can have up to 50 custom fields.

```text
PUT /v1/accounts/{entId}/endUserSchema
```

### Path parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `entId` | string | Yes | Your account ID. |

### Request body

An array of field objects:

| Property | Type | Required | Description |
| --- | --- | --- | --- |
| `name` | string | Yes | The field name. Must be unique in the account. Use lowercase letters, numbers, and underscores. |
| `type` | string | Yes | One of the [data types](#data-types). |
| `description` | string | No | What the field is for. |

### Example request

```bash
curl -X PUT https://api.example.com/v1/accounts/acme-123/endUserSchema \
  -H "x-guideflow-integration-key: YOUR_INTEGRATION_KEY" \
  -H "x-guideflow-user: admin@example.com" \
  -H "Content-Type: application/json" \
  -d '[
    {
      "name": "department",
      "type": "string",
      "description": "Department the user works in."
    },
    {
      "name": "start_date",
      "type": "timestamp",
      "description": "First day of work."
    }
  ]'
```

### Example response

`200 OK`

```json
{
  "updated": [
    {
      "name": "department",
      "type": "string",
      "description": "Department the user works in."
    },
    {
      "name": "start_date",
      "type": "timestamp",
      "description": "First day of work."
    }
  ],
  "customFieldCount": 4
}
```

### Example error

`400 Bad Request`, returned when a field uses a type that isn't supported:

```json
{
  "error": {
    "code": "INVALID_FIELD_TYPE",
    "message": "Field 'start_date' has type 'date'. Use one of: boolean, double, string, timestamp, encrypted_string."
  }
}
```

## Get a field by name

Returns the details of one field in the end user schema.

```text
GET /v1/accounts/{entId}/endUserSchema/{fieldName}
```

### Path parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `entId` | string | Yes | Your account ID. |
| `fieldName` | string | Yes | The name of the field to get. |

### Example request

```bash
curl https://api.example.com/v1/accounts/acme-123/endUserSchema/department \
  -H "x-guideflow-integration-key: YOUR_INTEGRATION_KEY" \
  -H "x-guideflow-user: admin@example.com"
```

### Example response

`200 OK`

```json
{
  "name": "department",
  "type": "string",
  "description": "Department the user works in.",
  "isDefault": false
}
```

### Example error

`404 Not Found`, returned when the field doesn't exist:

```json
{
  "error": {
    "code": "FIELD_NOT_FOUND",
    "message": "No field named 'departmnet' exists in this account's end user schema."
  }
}
```
