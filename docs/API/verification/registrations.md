# `/v1/registrations`

## Purpose
The `/v1/registrations` endpoint is used to register a new account within the Recovery Hub system. This is the first step for a user or developer to create an account and start interacting with the platform. The registration process typically involves providing essential details such as an email address or phone number and possibly other identifying information.

## HTTP Method
**POST**

## URL
`/v1/registrations`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **email**: Required. The email address of the user registering the account.
- **phone_number**: Optional. The phone number of the user registering the account.
- **password**: Required. The password for the account being created.
- **organization_name**: Optional. The name of the organization that the user is creating or associating with the account.

### Example Request Body

```
{
  "value": "user@example.com",
  "type": "email"
}
```

## Example Request

To register a new account:

```
curl -X POST https://api.recoveryhub.com/v1/registrations \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "value": "user@example.com",
  "type": "email"
}'
```

## Response Structure
The response will be a JSON object indicating the success or failure of the registration process.

### Response Fields

- **status**: The status of the registration request (e.g., `success` or `failed`).
- **message**: A message providing additional details about the status of the request.
- **user_id**: The unique identifier for the newly created account (only present if the request was successful).
- **organization_id**: The unique identifier for the associated organization (if applicable).

### Example Response (Successful Registration)

```
{
  "status": "success",
  "message": "Registration completed successfully.",
}
```

### Example Response (Failed Registration)

```
{
  "status": "failed",
  "message": "Registration failed. The email address may already be in use or the provided data is invalid."
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/registrations \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "value": "user@example.com",
  "type": "email"
}'
```

This request will create a new account and optionally associate it with an organization, allowing the user to start interacting with the Recovery Hub system.

## Best Practices
- Use strong, unique passwords for account registration to enhance security.
- Ensure that the email address provided is valid, as it will be used for account verification and recovery.
- Consider implementing email confirmation for new registrations to verify the user's ownership of the provided email address.