# `/v1/servers/verify`

## Purpose
The `/v1/servers/verify` endpoint is used to verify the authentication process initiated with a recovery server. This endpoint validates the signed challenge returned by the client to ensure that the client has successfully authenticated with the recovery server.

## HTTP Method
**POST**

## URL
`/v1/servers/verify`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Body Parameters
- **server_id**: Required. The unique identifier of the recovery server with which the authentication is being verified.
- **account_id**: Required. The ID of the account that is being authenticated.
- **signed_xdr**: Required. The signed cryptographic challenge that was issued by the recovery server.

### Example Request

To verify the authentication with a recovery server:

```
{
  "signed_xdr": "AAAAAgAAAACZ0VZQAAAAFcmKl1dRb9C1H3XK5bbF4vqRHZK+2JS0+T0AAABkAAAAAAmL7fQAAAAFAAAAAQA..."
}
```

## Example cURL Request

```
curl -X POST https://api.recoveryhub.com/v1/servers/verify \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "signed_xdr": "AAAAAgAAAACZ0VZQAAAAFcmKl1dRb9C1H3XK5bbF4vqRHZK+2JS0+T0AAABkAAAAAAmL7fQAAAAFAAAAAQA..."
}'
```

## Response Structure
The response will confirm whether the verification was successful and may include additional data such as a JWT token for future interactions with the recovery server.

### Response Fields

- **verified**: A boolean indicating whether the verification was successful.
- **jwt_token**: (Optional) A JSON Web Token (JWT) that can be used for subsequent authenticated requests with the recovery server.
- **expires_at**: The timestamp indicating when the JWT token will expire.

### Example Response

```
{
  "verified": true,
  "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
  "token_expires_at": "2024-08-05T12:30:00Z"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/servers/verify \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "signed_challenge": "AAAAAgAAAACZ0VZQAAAAFcmKl1dRb9C1H3XK5bbF4vqRHZK+2JS0+T0AAABkAAAAAAmL7fQAAAAFAAAAAQA..."
}'
```

This request verifies the signed challenge with the recovery server and, upon successful verification, provides a JWT token for further authenticated requests.

## Best Practices
- Ensure that your API key and JWT token are kept secure and not exposed in client-side code.
- Handle the JWT token carefully and renew it before it expires to avoid disruptions in your service.
- Validate the response to ensure that the verification process was successful before proceeding with any further actions.
