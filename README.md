# Nobak: Recovery Hub

## Overview
The Recovery Hub is a service designed to manage recovery servers for Stellar accounts, simplifying the process of adding, updating, and removing recovery options.

## Features
- **Add Recovery Server**: Add a new recovery server to an account.
- **Remove Recovery Server**: Remove an existing server from an account.
- **List Recovery Servers**: View all available recovery servers.
- **Retrieve Account Recovery Servers**: Get recovery servers linked to a specific account.

## Usage

### Adding a Recovery Server

```shell
POST /add-recovery-server
{
  "accountId": "example_account_id",
  "serverId": "example_server_id"
}

POST /remove-recovery-server
{
  "accountId": "example_account_id",
  "serverId": "example_server_id"
}

GET /list-recovery-servers

GET /get-recovery-servers/{account_id}
```