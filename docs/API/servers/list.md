# `/v1/servers/list`

## Purpose
The `/v1/servers/list` endpoint is used to retrieve a list of all servers within the Recovery Hub system. This endpoint provides detailed information about each server, which can be useful for understanding the available infrastructure.

## HTTP Method
**GET**

## URL
`/v1/servers/list`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
This endpoint does not accept any parameters.

## Example Request

To retrieve the list of all servers:

```
curl -X GET https://api.recoveryhub.com/v1/servers/list \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

## Response Structure
The response will be a JSON object containing an array of server objects. Each object provides detailed information about an individual server.

### Response Fields

- **id**: The unique identifier of the server.
- **name**: The name of the server.
- **description**: A brief description of the server's purpose or function.
- **domain**: The domain where the server is hosted.
- **public_key**: The public key associated with the server.
- **status**: The current status of the server, such as `online` or `offline`.
- **uptime_percentage**: The percentage of time the server has been operational.
- **last_checked**: The timestamp of the last status check.

### Example Response

```
{
  "servers": [
    {
      "name": "Server 1",
      "description": "Primary recovery server",
      "public_key": "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
      "status": "online",
      "uptime_percentage": 99.9,
      "last_checked": "2024-08-05T12:00:00Z"
    },
    {
      "name": "Server 2",
      "description": "Backup recovery server",
      "public_key": "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA",
      "status": "offline",
      "uptime_percentage": 95.4,
      "last_checked": "2024-08-05T12:00:00Z"
    }
  ]
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X GET https://api.recoveryhub.com/v1/servers/list \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

This request will return a list of all servers within the system, including detailed information about each server's status and configuration.

## Best Practices
- Ensure that your API key is kept secure and not exposed in client-side code.
- Regularly check the server list to stay updated on the available infrastructure.
- Handle potential errors or downtime gracefully in your application to maintain a good user experience.

