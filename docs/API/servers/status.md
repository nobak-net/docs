# `/v1/servers/status`

## Purpose
The `/v1/servers/status` endpoint is used to retrieve the status of all available servers within the Recovery Hub system. This endpoint provides information on the operational state of each server, which can be useful for monitoring and ensuring system reliability.

## HTTP Method
**GET**

## URL
`/v1/servers/status`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
This endpoint does not accept any parameters.

## Example Request

To retrieve the status of all servers:

```
curl -X GET https://api.recoveryhub.com/v1/servers/status \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

## Response Structure
The response will be a JSON object containing an array of server status objects. Each object provides the status details of an individual server.

### Response Fields

- **id**: The unique identifier of the server.
- **name**: The name of the server.
- **status**: The current status of the server, such as `online` or `offline`.
- **uptime_percentage**: The percentage of time the server has been operational.
- **last_checked**: The timestamp of the last status check.

### Example Response

```
{
  "servers": [
    {
      "name": "Server 1",
      "status": "online",
      "uptime_percentage": 99.9,
      "last_checked": "2024-08-05T12:00:00Z"
    },
    {
      "name": "Server 2",
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
curl -X GET https://api.recoveryhub.com/v1/servers/status \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

This request will return the status of all servers within the system. Use this information to monitor server availability and ensure that your operations are not disrupted by server downtime.

## Best Practices
- Ensure that your API key is kept secure and not exposed in client-side code.
- Regularly check server statuses, especially if your application depends on the availability of certain servers.
- Handle potential errors or downtime gracefully in your application to maintain a good user experience.
