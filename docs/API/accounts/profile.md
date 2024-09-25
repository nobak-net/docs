# `/v1/accounts/profile`

## Purpose
The `/v1/accounts/profile` endpoint is used to retrieve the profile information of the authenticated user's account. This information includes key details such as the account's unique identifier, associated email, and other relevant data.

## HTTP Method
**GET**

## URL
`/v1/accounts/profile`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
This endpoint does not accept any parameters.

## Example Request

To retrieve the profile information of the authenticated account:

```
curl -X GET https://api.recoveryhub.com/v1/accounts/profile \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

## Response Structure
The response will be a JSON object containing the profile details of the authenticated user's account.

### Response Fields

- **id**: The unique identifier of the account.
- **email**: The email address associated with the account.
- **created_at**: The timestamp when the account was created.
- **updated_at**: The timestamp when the account profile was last updated.
- **status**: The current status of the account, such as `active` or `suspended`.

### Example Response

```
{
  "id": "6073d93f-ae98-4098-b717-6023ffc6eb22",
  "email": "user@example.com",
  "created_at": "2024-08-01T12:34:56Z",
  "updated_at": "2024-08-10T08:45:21Z",
  "status": "active"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X GET https://api.recoveryhub.com/v1/accounts/profile \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

This request will return the profile information associated with the authenticated user's account.

## Best Practices
- Ensure that your API key is securely stored and not exposed in client-side code.
- Use this endpoint to regularly verify the status of your account and update your profile information as needed.
- Handle potential errors gracefully, such as when the account is suspended or the API key is invalid.