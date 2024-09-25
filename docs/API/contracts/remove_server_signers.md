# `/v1/contracts/remove_servers_signers`

## Purpose
The `/v1/contracts/remove_servers_signers` endpoint is used to remove one or more recovery servers as signers from a Stellar account. This operation is typically performed when a server is no longer trusted or required as part of the account recovery process.

## HTTP Method
**POST**

## URL
`/v1/contracts/remove_servers_signers`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **user_public_key**: Required. The Stellar public key of the user's account from which the recovery servers will be removed as signers.
- **server_public_keys**: Required. An array of Stellar public keys of the recovery servers to be removed as signers.
- **network_passphrase**: Required. The network passphrase for the Stellar network being used (e.g., `Public Global Stellar Network ; September 2015` for the public network, or the test network passphrase).
- **timeout**: Optional. The timeout value in seconds for the transaction.
- **state**: Optional. A state value that may be used to track the progress or status of the operation.
- **contracts_id**: Optional. A unique identifier for the contract or agreement under which the servers are being removed.

### Example Request Body

```
{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "server_public_keys": [
    "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
    "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA"
  ],
  "network_passphrase": "Test SDF Network ; September 2015",
  "timeout": 300,
  "state": "remove",
  "contracts_id": "123456789abcdef"
}
```

## Example Request

To remove recovery servers as signers from a Stellar account:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/remove_servers_signers \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "server_public_keys": [
    "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
    "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA"
  ],
  "network_passphrase": "Test SDF Network ; September 2015",
  "timeout": 300,
  "state": "remove",
}'
```

## Response Structure
The response will be a JSON object containing the details of the transaction created to remove the server signers.

### Response Fields

- **transaction_xdr**: The base64-encoded XDR of the unsigned Stellar transaction.
- **signers_removed**: An array of server public keys that were successfully removed as signers.
- **status**: The status of the operation (e.g., `success` or `failed`).

### Example Response

```
{
  "transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR
  "signers_removed": [
    "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
    "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA"
  ],
  "status": "success"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/remove_servers_signers \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "server_public_keys": [
    "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
    "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA"
  ],
  "network_passphrase": "Test SDF Network ; September 2015",
  "timeout": 300,
  "state": "remove",
}'
```

This request will generate a Stellar transaction to remove the specified recovery servers as signers from the user's account.

## Best Practices
- Ensure that the `server_public_keys` array contains only the keys of servers that are no longer needed or trusted.
- Regularly review the list of signers on the account to maintain security and ensure that only authorized servers have signing capabilities.
- Use the `state` and `contracts_id` fields to track and manage multiple recovery operations effectively.
