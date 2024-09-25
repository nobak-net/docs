# Authentication

To securely interact with the Recovery Hub API, all requests must be authenticated using API keys. This ensures that only authorized clients can access and perform actions on the API.

## Obtaining an API Key

To obtain an API key, you must first create an account on the Recovery Hub platform. Once your account is set up, you can generate an API key from the developer dashboard. This key is used to authenticate your API requests.

### Steps to Obtain an API Key

1. **Sign Up/Login**  
   Visit the Recovery Hub platform and sign up for an account or log in if you already have one.

2. **Generate API Key**  
   Navigate to the developer section of your dashboard.  
   Click on "Generate API Key."  
   Copy the generated API key and store it securely. Do not share this key, as it provides access to your API functionalities.

## Using the API Key

Once you have your API key, you must include it in the `Authorization` header of every API request. The API key should be prefixed with the word `Bearer`, followed by a space, and then the key itself.

## Example with cURL

Here’s an example of how to make an authenticated request to the Recovery Hub API using cURL:

```bash
curl -X GET https://api.recoveryhub.com/v1/servers/status \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json"
```

### Breakdown of the Example

- **`-X GET`**: Specifies the HTTP method. In this case, it’s a GET request.
- **`https://api.recoveryhub.com/v1/servers/status`**: The endpoint you’re accessing.
- **`-H "Authorization: Bearer YOUR_API_KEY"`**: The header where you pass your API key. Replace `YOUR_API_KEY` with the actual API key you obtained from the platform.
- **`-H "Content-Type: application/json"`: Specifies that the request body (if any) is in JSON format.

### Handling Authentication Errors

If your API key is missing, invalid, or expired, the API will return a `401 Unauthorized` error. Ensure your API key is correct and included in all requests to avoid this error.
