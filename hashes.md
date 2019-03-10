# Hashes

Groestlcoin's network relies on hash algorithms that differ from Bitcoin. There are three hash algorithms that are necessary to work with Groestlcoin data:

- **sha256d**: Two rounds of SHA256. This is the algorithm used by Bitcoin. It is also used in some Groestlcoin contexts.
- **sha256**: A single round of SHA256.
- **groestlHash**: Two rounds of Groestl-512, truncated to 32 bytes. Throughout this document, the term "groestlHash" is used. The more specific term "groestl512d" is used in some Groestlcoin projects.

Converting a hash-related Bitcoin implementation to Groestlcoin largely involves replacing a use of sha256d with one of the other two algorithms.

## Overview

The differences in hash algorithms between Bitcoin and Groestlcoin are summarized in this table. The specific cases are detailed below.

|Data|Bitcoin|Groestlcoin|
|----|-------|-----------|
|Block headers|sha256d|groestlHash|
|Transactions|sha256d|sha256|
|Base58 Checksums|sha256d|groestlHash|
|Messages signed by user|sha256d|sha256|
|P2P network messages|sha256d|groestlHash|

## Details

### Blocks

Block hashes are groestlHash digests of the block header instead of sha256d digests.

### Transactions

Transaction hashes are sha256 digests in Groestlcoin instead of sha256d digests as in Bitcoin. This change applies to all hashes involving a raw transaction: Transaction IDs and witness transaction IDs both use sha256. Likewise, in generating signatures for segwit transactions, sha256 is used instead of sha256d where it appears in the [BIP 143 specification](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki#specification). This means that when serializing a segwit input for signing, the *hashPrevouts*, *hashSequence*, and *hashOutputs* items from the BIP 143 specification are sha256 digests instead of sha256d.

##### Transaction Scripts

The OP_HASH256 opcode applies groestlHash to its input instead of sha256d.

### Addresses, xpub, WIF

Base58 encoding uses groestlHash for the four-byte checksum instead of sha256d. The RIPEMD-160 hash that precedes the checksum is the same as it is in Bitcoin (see "Unchanged Hashes" below).

### Messages signed by user (with private key of an address)

Message signing/verification uses sha256 in Groestlcoin instead of sha256d.

### P2P network messages

Checksum of messages which Groestlcoin servers use to talk to each other uses groestlHash instead of sha256d.

## Unchanged Hashes

Some uses of algorithms in Bitcoin are also used in Groestlcoin without changes.

RIPEMD-160, wherever used in Bitcoin, is also used in Groestlcoin. This includes base58 encoding for addresses.

Merkle roots in block headers are sha256d digests in Groestlcoin as well as in Bitcoin.

## Algorithm Implementations

sha256 is widely implemented and should work for Groestlcoin hashing without any changes.

groestlHash can be found in GitHub repositories under the [Groestlcoin organization](https://github.com/Groestlcoin/). Notably:

- The Python package that includes a C implementation as an extension is on [GitHub](https://github.com/Groestlcoin/groestlcoin-hash-python) and can be installed with [pip](https://pypi.org/project/groestlcoin_hash/).
- The JavaScript package is on [GitHub](https://github.com/Groestlcoin/groestl-hash-js) and can be installed with [npm](https://www.npmjs.com/package/groestl-hash-js).
- The Go package is on [GitHub](https://github.com/Groestlcoin/go-groestl-hash)
