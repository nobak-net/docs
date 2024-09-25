# `/v1/accounts/verify`

## Purpose
The `/v1/accounts/verify` endpoint is used to verify a user's account. This endpoint is typically called after the user has received a verification code (e.g., via email or SMS). Verifying the account confirms the user's identity and enables access to services within the Recovery Hub system.

## HTTP Method
**POST**

## URL
`/v1/accounts/verify`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **verification_code**: Required. The verification code sent to the user via email or SMS.
- **account_id**: Required. The ID of the account being verified.

### Example Request Body

```
{
  "verification_code": "123456",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}
```

## Example Request

To verify a user's account:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/verify \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "verification_code": "123456",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}'
```

## Response Structure
The response will be a JSON object indicating the success or failure of the account verification process.

### Response Fields

- **status**: The status of the verification request (e.g., `success` or `failed`).
- **message**: A success message confirming account verification or an error message detailing the failure.
- **verified**: A boolean value indicating whether the account is now verified.

### Example Response (Successful Verification)

```
{
  "status": "success",
  "message": "Account verified successfully.",
  "verified": true
}
```

### Example Response (Failed Verification)

```
{
  "status": "failed",
  "message": "Invalid verification code.",
  "verified": false
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/accounts/verify \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "verification_code": "123456",
  "account_id": "6073d93f-ae98-4098-b717-6023ffc6eb22"
}'
```

This request will verify the user's account using the provided verification code. A successful response will confirm that the account has been verified and can now be used for further actions within the system.

## Best Practices
- Ensure the verification code is sent to the user securely (e.g., via a trusted email or SMS provider).
- Handle error responses such as incorrect or expired verification codes gracefully in your application.
- Keep track of the verification status of user accounts to enable or restrict access to certain features.