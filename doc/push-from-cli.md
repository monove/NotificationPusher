# NotificationPusher - Documentation

## Push from CLI

For some reasons (tests or others), you could be happened to use pushing from CLI.

To do this, use `np` script (available at root directory) this way:

```
./np push <adapter> <token-or-registration-id> "Your message" --option1=value1 --option2=value2 ...
```

Each options matches with adapters required and optional ones.

Here is a concrete APNS adapter example:

```
./np push apns <token> "It's an example!" --certificate=/path/to/the/certificate.pem
```

Here is a concrete GCM adapter example:

```
./np push gcm <token> "It's an example!" --api-key=XXXXXXXXXX
```

## Documentation index

* [Installation](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/installation.md)
* [Getting started](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/getting-started.md)
* [APNS adapter](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/apns-adapter.md)
* [GCM adapter](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/gcm-adapter.md)
* [Create an adapter](https://github.com/monove/NotificationPusher/tree/multiple_response/doc/create-an-adapter.md)
* Push from CLI
