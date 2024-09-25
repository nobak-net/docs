# `/v1/servers/available`

## Purpose
The `/v1/servers/available` endpoint is used to retrieve a list of recovery servers that are available for use by an authenticated user. This endpoint helps users identify which recovery servers they can interact with for account recovery purposes.

## HTTP Method
**GET**

## URL
`/v1/servers/available`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
This endpoint does not accept any parameters.

## Example Request

To retrieve a list of available recovery servers:

```
curl -X GET https://api.recoveryhub.com/v1/servers/available \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

## Response Structure
The response will be a JSON object containing an array of available server objects. Each object provides details about an individual recovery server.

### Response Fields

- **id**: The unique identifier of the recovery server.
- **name**: The name of the recovery server.
- **description**: A brief description of the recovery server.
- **domain**: The domain where the recovery server is hosted.
- **status**: The current status of the recovery server, such as `online` or `offline`.

### Example Response

```
{
  "servers": [
    {
      "id": "6ffdd8cd-8b80-4cbc-bc5e-1b1638aaf71e",
      "name": "Server 1",
      "description": "Primary recovery server",
      "status": "online"
    },
    {
      "id": "370e0be1-0030-470c-91f7-c24d1d030d30",
      "name": "Server 2",
      "description": "Backup recovery server",
      "status": "offline"
    }
  ]
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X GET https://api.recoveryhub.com/v1/servers/available \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

This request will return a list of recovery servers that are currently available for use by the authenticated user. The user can then interact with these servers for account recovery purposes.

## Best Practices
- Regularly check the availability of recovery servers to ensure they are operational before initiating any recovery processes.
- Use the information from this endpoint to choose the most reliable servers for critical operations.
- Ensure that your API key is kept secure and not exposed in client-side code.