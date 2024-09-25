# `/v1/contracts/add_servers_signers`

## Purpose
The `/v1/contracts/add_servers_signers` endpoint is used to add one or more recovery servers as signers to a Stellar account. This is a crucial step in enabling account recovery functionality, allowing designated servers to participate in the recovery process by signing transactions that manage account signers or keys.

## HTTP Method
**POST**

## URL
`/v1/contracts/add_servers_signers`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **user_public_key**: Required. The Stellar public key of the user's account to which the recovery servers will be added as signers.
- **server_public_keys**: Required. An array of Stellar public keys of the recovery servers to be added as signers.
- **network_passphrase**: Required. The network passphrase for the Stellar network being used (e.g., `Public Global Stellar Network ; September 2015` for the public network, or the test network passphrase).
- **timeout**: Optional. The timeout value in seconds for the transaction.
- **state**: Optional. A state value that may be used to track the progress or status of the operation.
- **contracts_id**: Optional. A unique identifier for the contract or agreement under which the servers are being added.

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
  "state": "init",
  "contracts_id": "123456789abcdef"
}
```

## Example Request

To add recovery servers as signers to a Stellar account:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/add_servers_signers \
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
  "state": "init",
  "contracts_id": "123456789abcdef"
}'
```

## Response Structure
The response will be a JSON object containing the details of the transaction created to add the server signers.

### Response Fields

- **transaction_xdr**: The base64-encoded XDR of the unsigned Stellar transaction.
- **signers_added**: An array of server public keys that were successfully added as signers.
- **status**: The status of the operation (e.g., `success` or `failed`).

### Example Response

```
{
  "transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR
  "signers_added": [
    "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
    "GDVG24QL3HNNQ4SFF5JTB2WIBX5WDMMZ35BXU3US7VSG2SUCIKKJWFZA"
  ],
  "status": "success"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/add_servers_signers \
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
  "state": "init",
  "contracts_id": "123456789abcdef"
}'
```

This request will generate a Stellar transaction to add the specified recovery servers as signers to the user's account, making them part of the account recovery process.

## Best Practices
- Ensure that the `server_public_keys` array contains only valid and trusted server keys.
- Regularly review the list of signers on the account to ensure that only authorized servers have signing capabilities.
- Use the `state` and `contracts_id` fields to track and manage multiple recovery operations effectively.