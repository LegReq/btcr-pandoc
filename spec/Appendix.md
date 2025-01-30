## Appendix

### Bech32 Encoding and Decoding

**did:btc1** uses the Bech32 algorithm to encode and decode several data values. The Bech32 algorithm is documented in [BIP-0173]. Additionally, **did:btc1** uses an updated Bech32 algorithm known as "bech32m" that is documented in [BIP-0350]. For this specification we define two functions: `bech32-encode` and `bech32-decode`.

#### bech32-encode

This algorithm takes two required inputs: a string, `hrp` which is the human readable part of the encoding and a array of bytes to be encoded called the `dataPart`.

1. Initialize `result` to the output of Bech32 encoding the `hrp` and the `dataPart` as described in [BIP-0173].
2. Return `result`.

#### bech32-decode

This algorithm takes one required input: a string `bech32Str` representing a Bech32 encoding data value.

1. Initialize `hrp` and `dataPart` to the result of Bech32 decoding the `bech32Str` as described in [BIP-0173].
2. Return a tuple (`hrp`, `dataPart`)

#### Bech32 encoding a secp256k1 public key

A macro or convenience function can be used to encode a `keyBytes` representing a compressed SEC encoded secp256k1 public key. The algorithm takes one required input, `keyBytes`.

1. Initialize `hrp` to `"k"`.
2. Initialize `dataPart` to `keyBytes`.
3. Return the result of the [`bech32-encode`](#911-bech32-encode) algorithm, passing `hrp` and `dataPart`.

#### Bech32 encoding a hash-value

A macro or convenience function can be used to encode a `hashBytes` representing the sha256 hash of an initiating DID document. The algorithm takes one required input, `hashBytes`.

1. Initialize `hrp` to `"x"`.
2. Initialize `dataPart` to `hashBytes`.
3. Return the result of the [`bech32-encode`](#911-bech32-encode) algorithm, passing `hrp` and `dataPart`.


### JSON Canonicalization

A macro function that takes in a json document, `document`, and canonicalizes it following the [JSON Canonicalization Scheme](https://www.rfc-editor.org/rfc/rfc8785). The function returns the `canonicalizedBytes`.

1. Set `canonicalBytes` to the result of applying the JSON Canonicalziation Scheme to the `document`.
2. Return `canonicalBytes`.
