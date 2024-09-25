# `/v1/contracts/sign`

## Purpose
The `/v1/contracts/sign` endpoint is used to request a signature from a recovery server on a pre-constructed Stellar transaction. This is typically part of the recovery process where multiple servers need to sign a transaction to reset or recover account access.

## HTTP Method
**POST**

## URL
`/v1/contracts/sign`

## Headers
- `Authorization`: Required. The API key must be included in the header to authenticate the request. Example: `Bearer YOUR_API_KEY`.
- `Content-Type`: Required. Set to `application/json`.

## Parameters
The following parameters should be included in the JSON body of the request:

- **user_public_key**: Required. The Stellar public key of the user's account that the transaction pertains to.
- **transaction_xdr**: Required. The base64-encoded XDR of the Stellar transaction that needs to be signed.
- **server_public_key**: Required. The Stellar public key of the recovery server that is being requested to sign the transaction.
- **network_passphrase**: Required. The network passphrase for the Stellar network being used (e.g., `Public Global Stellar Network ; September 2015` for the public network, or the test network passphrase).

### Example Request Body

```
{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR
  "server_public_key": "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
  "network_passphrase": "Test SDF Network ; September 2015"
}
```

## Example Request

To request a signature on a Stellar transaction:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/sign \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR
  "server_public_key": "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
  "network_passphrase": "Test SDF Network ; September 2015"
}'
```

## Response Structure
The response will be a JSON object containing the signed transaction XDR and confirmation details.

### Response Fields

- **signed_transaction_xdr**: The base64-encoded XDR of the Stellar transaction with the server's signature applied.
- **status**: The status of the operation (e.g., `success` or `failed`).

### Example Response

```
{
  "signed_transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR with signature
  "status": "success"
}
```

## Example Usage

Here's an example of how to call this endpoint using `curl`:

```
curl -X POST https://api.recoveryhub.com/v1/contracts/sign \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "user_public_key": "GDBPRWMGNQ34ZZTGZQ25EAPAMANIF3WARWOMX5OXCPHMXC53DVMA6TGQ",
  "transaction_xdr": "AAAAAgAAAAA....", // Truncated XDR
  "server_public_key": "GCS5RZY7UVP445FUFDKBGPWUG3LFVBJKA2UKATG2QSCY23434E5R4UFC",
  "network_passphrase": "Test SDF Network ; September 2015"
}'
```

This request will return the signed transaction XDR, which can then be submitted to the Stellar network for processing.

## Best Practices
- Ensure that the `transaction_xdr` is correctly constructed before sending it for signing to avoid invalid transactions.
- Verify the signatures on the transaction after receiving the signed XDR to ensure that the correct server has signed it.
- Handle any errors or failed signatures gracefully in your application to avoid disruption in the recovery process.
