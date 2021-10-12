<img src="https://user-images.githubusercontent.com/211411/34776833-6f1ef4da-f618-11e7-8b13-f0697901d6a8.png" height="100" />

[Github](https://github.com/LedgerHQ/ledgerjs/),
[Ledger Devs Slack](https://ledger-dev.slack.com/)

## @ledgerhq/hw-app-solana

Ledger Hardware Wallet Solana JavaScript bindings.

## Notes

To run `speculos-smoke` test make sure [Speculos](https://github.com/LedgerHQ/speculos) running (apdu port 9999 and api rest endpoint <http://0.0.0.0:5000>) with [Solana app](https://github.com/LedgerHQ/app-solana) installed on it. Then run the command from root workspace:

```bash
$ yarn run ts-node packages/hw-app-solana/tests/speculos-smoke.ts
```

## Troubleshooting

If ledger returns error `6808` - enable blind signature in settings (not needed for unit testing).

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [Solana](#solana)
    -   [Parameters](#parameters)
    -   [Examples](#examples)
    -   [getAddress](#getaddress)
        -   [Parameters](#parameters-1)
        -   [Examples](#examples-1)
    -   [signTransaction](#signtransaction)
        -   [Parameters](#parameters-2)
        -   [Examples](#examples-2)
    -   [getAppConfiguration](#getappconfiguration)
        -   [Examples](#examples-3)

### Solana

Solana API

#### Parameters

-   `transport` **Transport** a transport for sending commands to a device
-   `scrambleKey` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a scramble key (optional, default `"solana_default_scramble_key"`)

#### Examples

```javascript
import Solana from "@ledgerhq/hw-app-solana";
const solana = new Solana(transport);
```

#### getAddress

Get Solana address (public key) for a BIP32 path.

Because Solana uses Ed25519 keypairs, as per SLIP-0010
all derivation-path indexes will be promoted to hardened indexes.

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a BIP32 path
-   `display` **[boolean](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** flag to show display (optional, default `false`)

##### Examples

```javascript
solana.getAddress("44'/501'/0'").then(r => r.address)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{address: [Buffer](https://nodejs.org/api/buffer.html)}>** an object with the address field

#### signTransaction

Sign a Solana transaction.

##### Parameters

-   `path` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** a BIP32 path
-   `txBuffer` **[Buffer](https://nodejs.org/api/buffer.html)** serialized transaction

##### Examples

```javascript
solana.signTransaction("44'/501'/0'", txBuffer).then(r => r.signature)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;{signature: [Buffer](https://nodejs.org/api/buffer.html)}>** an object with the signature field

#### getAppConfiguration

Get application configuration.

##### Examples

```javascript
solana.getAppConfiguration().then(r => r.version)
```

Returns **[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;AppConfig>** application config object