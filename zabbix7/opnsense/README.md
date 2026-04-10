# Features

## Wireguard monitoring

API endpoint: `/api/wireguard/service/show`

`type: interface` describes the local interface. probably won't need this  
`type: peer` can be either an outgoing peer (we connect every x seconds) or an incoming peer (peer connects every x seconds)  
We probably need some way to differentiate and only list those peers we can connect to outgoing. Can be done using `/api/wireguard/client/get` for example and looking for clients with `serveraddress` filled
`latest-handshake-age` is when the last handshake occurred in seconds

```json
{
  "total": 2,
  "rowCount": 2,
  "current": 1,
  "rows": [
    {
      "if": "wg1",
      "type": "interface",
      "public-key": "wg public key redacted",
      "listen-port": "48326",
      "fwmark": "off",
      "endpoint": "48326",
      "status": "up",
      "name": "vpn name redacted",
      "latest-handshake-age": null,
      "latest-handshake-epoch": null,
      "peer-status": "offline",
      "ifname": "local if name redacted"
    },
    {
      "if": "wg1",
      "type": "peer",
      "public-key": "wg public key redacted",
      "endpoint": "peer public ip",
      "allowed-ips": "allowed ip routes redacted",
      "latest-handshake": 1775822830,
      "transfer-rx": 20319184,
      "transfer-tx": 12397340,
      "persistent-keepalive": "20",
      "name": "peer name redacted",
      "latest-handshake-age": 28,
      "latest-handshake-epoch": "2026-04-10 12:07:10",
      "peer-status": "online",
      "ifname": "vpn name redacted"
    }
  ]
}
```

`/api/wireguard/client/get`

```json
{
  "client": {
    "clients": {
      "client": {
        "da5c1bbb-b882-4203-8649-5947a86ddf49": {
          "enabled": "1",
          "name": "peer name redacted",
          "pubkey": "wg public key redacted",
          "psk": "",
          "tunneladdress": {
            "192.168.24.0\/24": { "value": "192.168.24.0\/24", "selected": 1 }
          },
          "serveraddress": "peer public ip redacted",
          "serverport": "51820",
          "endpoint": "",
          "keepalive": "20",
          "servers": {
            "8bf47746-2fb5-4c2f-86bb-1418feafa43b": {
              "value": "vpn name redacted",
              "selected": 1
            }
          }
        }
      }
    }
  }
}
```
