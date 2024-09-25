# `/v1/servers/auth`

## Purpose
The `/v1/servers/auth` endpoint is used to initiate the authentication process with a recovery server. This endpoint allows you to start the process of proving ownership of an account by generating a challenge that must be signed and verified by the recovery server.

## HTTP Method
**POST**

## URL
`/v1/servers/auth`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Body Parameters
- **server_id**: Required. The unique identifier of the recovery server with which you want to initiate the authentication process.
- **account_id**: Required. The ID of the account that you want to authenticate.

### Example Request

To initiate authentication with a recovery server:

```
{
  "server_id": "6ffdd8cd-8b80-4cbc-bc5e-1b1638aaf71e",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}
```

## Example cURL Request

```
curl -X POST https://api.recoveryhub.com/v1/servers/auth \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "server_id": "6ffdd8cd-8b80-4cbc-bc5e-1b1638aaf71e",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}'
```

## Response Structure
The response will contain a challenge that must be signed and returned to the server for verification.

### Response Fields

- **challenge**: A cryptographic challenge that needs to be signed by the client's private key.
- **expires_at**: The timestamp indicating when the challenge will expire.
- **server_public_key**: The public key of the server that issued the challenge.

### Example Response

```
{
  "challenge": "AAAAAgAAAACZ0VZQAAAAFcmKl1dRb9C1H3XK5bbF4vqRHZK+2JS0+T0AAABkAAAAAAmL7fQAAAAFAAAAAQA...",
  "expires_at": "2024-08-05T12:10:00Z",
  "server_public_key": "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/servers/auth \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "server_id": "6ffdd8cd-8b80-4cbc-bc5e-1b1638aaf71e",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}'
```

This request initiates the authentication process with the specified recovery server. You will receive a challenge that must be signed and returned to complete the authentication.

## Best Practices
- Ensure that your API key is kept secure and not exposed in client-side code.
- Handle the challenge promptly, as it will expire after a set period.
- Verify the server's public key to ensure that you are communicating with the correct recovery server.
