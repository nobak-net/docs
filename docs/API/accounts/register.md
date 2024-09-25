# `/v1/accounts/register`

## Purpose
The `/v1/accounts/register` endpoint is used to create a new user account within the Recovery Hub system. This endpoint allows developers to programmatically register new users by providing the required information, such as email and password.

## HTTP Method
**POST**

## URL
`/v1/accounts/register`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **email**: Required. The email address for the new account.
- **password**: Required. The password for the new account. Ensure that this password is strong and meets security requirements.
- **confirm_password**: Required. Confirmation of the password to ensure it was entered correctly.

### Example Request Body

```
{
  "email": "newuser@example.com",
  "password": "StrongPassword123!",
  "confirm_password": "StrongPassword123!"
}
```

## Example Request

To register a new user account:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/register \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "email": "newuser@example.com",
  "password": "StrongPassword123!",
  "confirm_password": "StrongPassword123!"
}'
```

## Response Structure
The response will be a JSON object confirming the successful registration of the new account or providing details about any errors encountered.

### Response Fields

- **id**: The unique identifier of the newly created account.
- **email**: The email address associated with the account.
- **status**: The status of the account, typically `pending` until email verification is completed.
- **created_at**: The timestamp when the account was created.
- **message**: A success message confirming account registration, or an error message if the registration failed.

### Example Response

```
{
  "id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "email": "newuser@example.com",
  "status": "pending",
  "created_at": "2024-08-10T08:45:21Z",
  "message": "Account registered successfully. Please verify your email."
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/register \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "email": "newuser@example.com",
  "password": "StrongPassword123!",
  "confirm_password": "StrongPassword123!"
}'
```

This request will create a new user account within the Recovery Hub system. The response will include the account ID and other relevant details.

## Best Practices
- Ensure that the email address provided is valid and accessible to the user, as email verification is typically required.
- Use a strong and unique password for each account to enhance security.
- Handle error responses gracefully, such as cases where the email is already in use or the passwords do not match.
- Store the account ID securely if needed for future reference in your application.