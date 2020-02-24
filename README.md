# cups

## API

### Authorization

Cups uses Basic Auth

- The username is always `me`.
- The password is defined in `./start9/config.yaml`

### Send Message

#### Request

`POST` with body `0x00 <Tracking ID (UUID BE)> <ED25519 PubKey of Recipient (32 bytes)> <UTF-8 Encoded Message>`

### Name User

#### Request

`POST` with body `0x01 <ED25519 PubKey of User> <UTF-8 Encoded Name>`

### Get Contact Book

#### Request

`GET` with query `?type=users`

#### Response

`<User Info>*` where `<User Info>` = `<ED25519 PubKey of User> <Unreads Count (u64 BE)> <Length of Name (1 byte)> <UTF-8 Encoded Name>`

### Get Messages

#### Request

`GET` with query `?type=messages&pubkey=<RFC4648 Base32 encoded ED25519 PubKey of User>&limit=<Maximum number of messages to return>`

#### Response

`<Message>*` in reverse chronological order where `<Message>` = `<0x00 for Inbound / 0x01 for Outbound> <ID (i64 BE)> <Tracking ID (UUID BE)> <Unix Epoch (i64 BE)> <Length of Message (u64 BE)> <UTF-8 Encoded Message>`

### Get Version

#### Request

Unauthenticated `GET` with no query

#### Response

`<Major Version (u64 BE)> <Minor Version (u64 BE)> <Patch Version (u64 BE)>` 