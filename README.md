# Nobak Documentation

## [App Discovery](https://github.com/nobak-net/metadata)

Nobak's app discovery feature works by utilizing a community-driven approach where anyone can contribute to a repository named [metadata](https://github.com/nobak-net/metadata). Contributors can add their decentralized application (dApp) to this repository. Once added, these apps become discoverable within the Nobak mobile app.

This open-source collaboration enables a diverse range of dApps to be easily accessible to Nobak users, fostering an inclusive and expansive digital ecosystem on the Stellar network. This approach encourages community engagement and ensures that Nobak's app offerings are continually updated and varied.

## [Nobak UI Design System](https://github.com/nobak-net/nobak-native-design-system)

Nobak utilizes a modular design system, allowing for diverse user interface (UI) experiences within its mobile app. This system supports different UI components tailored to varying levels of user blockchain experience.

### Basic UI

- **Target Audience**: Non-tech savvy users or beginners in blockchain.
- **Features**: Simplified interface with essential functionalities, making it easier for new users to navigate.
- **Limitations**: Advanced features are hidden to avoid overwhelming new users.

### Pro UI

- **Target Audience**: Experienced users familiar with blockchain technology.
- **Features**: Offers full access to all of Nobak's functionalities, including advanced settings and tools.
- **Customization**: Users can tweak settings and preferences for a personalized experience.

### Switching Between UIs

- **Flexibility**: Users can switch between Basic and Pro UIs as per their comfort level and expertise.
- **Adaptive Design**: The app dynamically adjusts the UI complexity based on the selected mode.

This design approach ensures Nobak is accessible to all users, from blockchain novices to experts.

## Recovery Hub

The Recovery Hub is a service designed to manage recovery servers for Stellar accounts, simplifying the process of adding, updating, and removing recovery options.

### Monitor Health

Health and status of each of the recovery servers at the stellar ecosystem.

### Features

- **Add Recovery Server**: Add a new recovery server to an account.
- **Remove Recovery Server**: Remove an existing server from an account.
- **List Recovery Servers**: View all available recovery servers.
- **Retrieve Account Recovery Servers**: Get recovery servers linked to a specific account.

### Usage

```shell
POST /auth/{dev_key}
```

#### Adding a Recovery Server

```shell
POST /add-recovery-server

Request:

{
  "accountId": "uuid",
  "serverId": "uuid"
}

Response: 

{
  "xdr": "###"
}
```

#### Remove a Recovery Server

```shell
POST /remove-recovery-server

Request:

{
  "accountId": "uuid",
  "serverId": "uuid"
}

Response: 

{
  "xdr": "###"
}
```

#### List servers

```shell
GET /servers/list

Response: 

{
  "servers":
  [
    "uuid": 
    {

    }
  ]
}
```

#### Account

```shell
GET /accounts/{account_id}

Response: 

{
  "account":
  {
    "id": "uuid",
    "min_threshold": "3",
    "max_threshold": "5",
    servers:
    [
      "uuid", "uuid"
    ]
  }
}

```
