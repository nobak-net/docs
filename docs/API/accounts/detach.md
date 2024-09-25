# `/v1/accounts/detach`

## Purpose
The `/v1/accounts/detach` endpoint is used to detach or unlink an external account (such as an email or phone number) from a user's existing account within the Recovery Hub system. This is useful when a user no longer wants to associate a particular authentication method or contact method with their primary account.

## HTTP Method
**POST**

## URL
`/v1/accounts/detach`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **account_id**: Required. The ID of the account from which the external account is being detached.
- **auth_method_type**: Required. The type of authentication method being detached (e.g., `email`, `phone`, etc.).
- **auth_method_value**: Required. The value of the authentication method (e.g., the actual email address or phone number).

### Example Request Body

```
{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com"
}
```

## Example Request

To detach an email address from a user's account:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/detach \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com"
}'
```

## Response Structure
The response will be a JSON object indicating the success or failure of the account detachment process.

### Response Fields

- **status**: The status of the detachment request (e.g., `success` or `failed`).
- **message**: A success message confirming the account was detached, or an error message detailing the failure.
- **detached**: A boolean value indicating whether the account has been successfully detached.

### Example Response (Successful Detachment)

```
{
  "status": "success",
  "message": "Account detached successfully.",
  "detached": true
}
```

### Example Response (Failed Detachment)

```
{
  "status": "failed",
  "message": "Failed to detach the account. The email may not be linked to the provided account.",
  "detached": false
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/detach \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "auth_method_type": "email",
  "auth_method_value": "user@example.com"
}'
```

This request will detach the specified email address from the user's account, ensuring that the user can no longer use that email address for authentication or communication purposes.

## Best Practices
- Ensure that the external account (e.g., email, phone number) is correctly verified before detaching it from the user's account to avoid accidental detachment.
- Handle potential errors gracefully, such as attempting to detach an account that is not associated with the user's account.
- Consider implementing additional security measures, such as requiring the user to confirm the detachment action via email or SMS.
