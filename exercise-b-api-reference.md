# Exercise B — API Reference Entry

## Create a Task

**Method:** `POST`

**Endpoint:** `/api/v1/projects/{projectId}/tasks`

### Description

Creates a new task inside the specified project for the authenticated user. The caller supplies a title, optional description, assignee user ID, due date, and priority. On success, the API returns the newly created task, including its server-generated ID and timestamps.

## Authentication

The endpoint requires a valid bearer access token.

### Required Request Headers

| Header | Type | Required | Description |
|---|---|---:|---|
| `Authorization` | string | Yes | Bearer access token in the format `Bearer <token>`. |
| `Content-Type` | string | Yes | Must be `application/json`. |
| `Accept` | string | Yes | Should be `application/json` to request a JSON response. |

## Path Parameters

| Parameter | Type | Required | Description |
|---|---|---:|---|
| `projectId` | string | Yes | Unique identifier of the project in which the task will be created. |

## Query Parameters

This endpoint has no query parameters.

## Request Body

The request body must be a JSON object.

| Field | Type | Required | Description |
|---|---|---:|---|
| `title` | string | Yes | Short name of the task. Must contain at least 1 non-whitespace character and be no longer than 200 characters. |
| `description` | string | No | Longer explanation of the task. If omitted, the description is empty. |
| `assigneeId` | string | Yes | Unique identifier of the user assigned to the task. The user must have access to the project. |
| `dueDate` | string (date) | Yes | Task deadline in ISO 8601 calendar-date format: `YYYY-MM-DD`. |
| `priority` | string (enum) | Yes | Task priority. Allowed values are `low`, `medium`, and `high`. |

### Example Request

```http
POST /api/v1/projects/proj_8f31a2/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkXVCJ9.example
Content-Type: application/json
Accept: application/json

{
  "title": "Prepare database schema",
  "description": "Create the initial schema and document the main relationships.",
  "assigneeId": "usr_10482",
  "dueDate": "2026-10-15",
  "priority": "high"
}
```

## Response

### Success Response

**Status:** `201 Created`

The server returns the created task as a JSON object.

### Example Successful Response

```json
{
  "id": "task_7c92e1",
  "projectId": "proj_8f31a2",
  "title": "Prepare database schema",
  "description": "Create the initial schema and document the main relationships.",
  "assigneeId": "usr_10482",
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "todo",
  "createdAt": "2026-10-05T08:13:42Z",
  "updatedAt": "2026-10-05T08:13:42Z"
}
```

## HTTP Response Codes

| Code | Meaning | When it occurs |
|---|---|---|
| `201 Created` | Task created | The request is valid and the new task has been created successfully. |
| `400 Bad Request` | Invalid request | The JSON body is malformed, a required field is missing, a field has an invalid type, or a value such as `priority` is outside the allowed values. |
| `401 Unauthorized` | Authentication required or invalid | The `Authorization` header is missing, the token is invalid, or the token has expired. |
| `403 Forbidden` | Access denied | The authenticated user is not allowed to create tasks in the specified project or cannot assign tasks to the selected user. |
| `404 Not Found` | Resource not found | The specified project or assignee does not exist, or the authenticated user cannot access the referenced resource. |
| `409 Conflict` | Request conflicts with current state | Creating the task would violate a project rule or another uniqueness/business constraint. |
| `422 Unprocessable Entity` | Validation failed | The JSON is syntactically valid but one or more values fail business validation, such as an invalid date or a user who cannot be assigned to the project. |
| `429 Too Many Requests` | Rate limit exceeded | The client has sent more requests than the API currently permits. |
| `500 Internal Server Error` | Server error | An unexpected error occurs while processing the request. |
| `503 Service Unavailable` | Service temporarily unavailable | The API or a required backend service is temporarily unavailable. |

## Validation Rules

- `title` is required and must be 1–200 characters after trimming whitespace.
- `description` is optional.
- `assigneeId` is required and must identify a user who can access the project.
- `dueDate` is required and must use `YYYY-MM-DD`.
- `priority` is required and must be exactly one of `low`, `medium`, or `high`.
- The authenticated user must have permission to create tasks in the selected project.
