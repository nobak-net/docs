# `/v1/accounts/link`

## Purpose
The `/v1/accounts/link` endpoint is used to link an external account (such as an email or phone number) to a user's existing account within the Recovery Hub system. This allows users to associate additional methods of authentication or contact with their primary account.

## HTTP Method
**POST**

## URL
`/v1/accounts/link`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **account_id**: Required. The ID of the account to which the external account is being linked.
- **auth_method_type**: Required. The type of authentication method being linked (e.g., `email`, `phone`, etc.).
- **auth_method_value**: Required. The value of the authentication method (e.g., the actual email address or phone number).
- **state**: Optional. A state parameter that might be used for verification purposes.

### Example Request Body

```
{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com",
  "state": "optionalStateValue"
}
```

## Example Request

To link an email address to a user's account:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/link \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com",
  "state": "optionalStateValue"
}'
```

## Response Structure
The response will be a JSON object indicating the success or failure of the account linking process.

### Response Fields

- **status**: The status of the linking request (e.g., `success` or `failed`).
- **message**: A success message confirming the account was linked, or an error message detailing the failure.
- **linked**: A boolean value indicating whether the account has been successfully linked.

### Example Response (Successful Linking)

```
{
  "status": "success",
  "message": "Account linked successfully.",
  "linked": true
}
```

### Example Response (Failed Linking)

```
{
  "status": "failed",
  "message": "Failed to link the account. The email may already be linked to another account.",
  "linked": false
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/link \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com",
  "state": "optionalStateValue"
}'
```

This request will link the specified email address to the user's account, allowing them to use that email address for authentication or communication purposes.

## Best Practices
- Ensure that the external account (e.g., email, phone number) is verified before linking it to the user's account.
- Handle potential errors gracefully, such as attempting to link an account that is already associated with another user.
- Consider implementing additional security measures, such as requiring the user to confirm the linking action via email or SMS.
