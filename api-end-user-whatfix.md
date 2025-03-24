# API Documentation

## End User Schema API

The End User Schema API allows you to manage custom fields in the end user schema for your account. This API enables you to fetch, update, or add custom fields to the end user schema, which defines the data associated with users interacting with your platform.

### Table of Contents
- [Overview](#overview)
- [Authentication](#authentication)
- [Status Codes](#status-codes)
- [Pagination](#pagination)
- [End User Schema](#end-user-schema)
  - [Get End User Schema](#get-end-user-schema)
  - [Update/Add Custom Fields](#updateadd-custom-fields)
  - [Get End User Schema by Field Name](#get-end-user-schema-by-field-name)
  - [Get All End Users (Paginated)](#get-all-end-users-paginated)
- [Data Types](#data-types)

<p>&nbsp;</p>




## Overview

The End User Schema API allows you to:
- Fetch the schema of the end user resource.
- Add or update custom fields in the schema.
- Retrieve information about specific fields by name.
- Get a list of all end users associated with your account.


---
<p>&nbsp;</p>

## Authentication

To get authenticated you will need to create a user API token from the Whatfix dashboard and pass as header **x-whatfix-integration-key**. To know more, see [Generating the API Integration Key](link). Pass the email address of the user as the **x-whatfix-user** header.


## Status Codes
The following status codes are possible in Whatfix API Responses:
- 2xx: Success
- 4xx: Request error
- 5xx: Server-side error

| **Status Code**               | **Description**                                                                                   |
|-------------------------------|---------------------------------------------------------------------------------------------------|
| **200 - OK**                   | Returned for GET and PUT requests when the request is processed successfully and a payload is returned. |
| **201 - Created**              | Returned for POST and PUT requests when a new object is created.                                 |
| **204 - No Content**           | Returned for DELETE requests when a resource is deleted.                                         |
| **207 - Multistatus**          | Returned for partial success during POST/PUT/DELETE requests.                                     |
| **400 - Bad Request**          | Returned if the API format is incorrect or if query parameters are invalid.                      |
| **401 - Unauthorized**         | Returned if the Whatfix integration key is not valid.                                             |
| **403 - Forbidden**            | Returned if the Whatfix integration key does not have permission for the requested resource.      |
| **404 - Not Found**            | Returned for GET and DELETE requests when no content is found for the requested resource ID.      |
| **429 - Too Many Requests**    | Returned if the rate limit is exceeded.                                                          |
| **500, 502, 503, 504 - Server Errors** | Returned for server-side errors. Requests may succeed on retry.                                    |

## Pagination
Pagination is performed by the use of 2 filters: cursor and limit
- **cursor**: Pointer to a specific row of data.
- **limit**: Specifies the maximum number of records to return in the result.

<p>&nbsp;</p>

---

## End User Schema

APIs for managing end user schema allow you to define fields for users in your platform. The following data types are allowed:
- **boolean**: Boolean values (e.g., `true`, `false`)
- **double**: Numeric values (e.g., `10`, `20.78`)
- **string**: Any string value (e.g., `employee_role`)
- **timestamp**: Timestamp in ISO-8601 format (e.g., `2001-07-04T12:08:56.235-0700`)
- **encrypted_string**: Any string value stored in an encrypted format for security purposes (e.g., `john.doe@whatfix.com`)

<p>&nbsp;</p>
## Get End User Schema

The Get End User Schema API fetches the schema for the end users resource for your account. It returns both Whatfix-provided default fields and custom fields defined by the account user.

### PATH PARAMETERS
- **entId** (required): string, account ID
- **fieldName** (required): string, field name

### Example API Call
**GET** ```/v1/accounts/{entId}/endUserSchema```

### Responses
```200 OK: Returns the schema information for the end users resource.```


## Data Integrations
Updates or adds one or more custom fields in the end user schema. Field names are unique and are used to identify the fields that are required to be updated. A maximum of 50 custom fields can be added to the user schema for each account. Called from integrations UI on the dashboard.

### PATH PARAMETERS
- **entId** (required): string, account ID

### Request Body Schema
- **description**: string, explanation of the field's purpose.
- **name**: string, name of the field.
- **type**: string, data type of the field.

### Example API Call
**PUT** ```/v1/accounts/{entId}/endUserSchema```

### Request samples
Content type: application/json
```json
[
  {
    "description": "string",
    "name": "string",
    "type": "string"
  }
]
```
<p>&nbsp;</p>

### Responses
```200 OK: Returns the schema information for the end users resource.```


## Get an end user schema by field name
Get an end user schema by field name. This is called from integrations dashboard.

### PATH PARAMETERS
- **entId** (required): string, account ID
- **fieldName** (required): string, field name

### Example API Call
**GET** ```/v1/accounts/{entId}/endUserSchema/{fieldName}```

### Responses
```200 OK: Returns the schema information for the end users resource.```

<p>&nbsp;</p>
---

## Conclusion
This API documentation provides you with the necessary endpoints to manage and interact with the end user schema for your Whatfix account. By using the provided API calls, you can easily add, update, and retrieve user schema data as needed.
