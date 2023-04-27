# Solana Wallet Names

[![Build status](https://github.com/portalpayments/solana-wallet-names/actions/workflows/tests.yaml/badge.svg)](https://github.com/portalpayments/solana-wallet-names/actions)


<img src="docs/logo.png" alt="A human wearing a badge that says Hello my name is Solana Wallet Names" />

This package resolves **wallet names** (like `mikemaccana.sol`) to **wallet addresses** (like `5FHwkrdxntdK24hgQU8qgBjn35Y1zwhz1GZwCkP2UJnM`) (and the reverse - wallet addresses to names) across the entire Solana ecosystem, including **✨8✨ different name services** and **✨5✨ different profile picture (PFP) services**.

Supported **wallet names** are:

 - **.abc** (using Solana PFP standard for profile pictures)
 - **.backpack** (using Backpack for profile pictures)
 - **.bonk** (using Solana PFP standard for profile pictures)
 - **.glow** (using Glow for profile pictures)
 - **.ottr** (using Ottr for profile pictures)
 - **.poor** (using Solana PFP standard for profile pictures)
 - **.sol** (using Solana PFP standard for profile pictures)
 - **@twitter** (using Twitter standard for profile pictures)

## Note: wallet names do not assert identity

Wallet names are a convenient alternative for wallet addresses. However **wallet names do not assert real world identity**. Most of services used in this library do not check the real-world identity of people registering wallet names.
 - Many wallet names that sounds like real world people and organisations are not those organisation - `barclays.sol` isn't Barclays, `cashapp.sol` isn't cashapp, `joemccann.sol` isn't the well known Solana investor. This isn't just Solana, all blockchain name services and DNS itself operate this way. Having a particular name registered simply means the holder was the first person to register that name.
 - Wallet name services that include given and family names do not check that the person has identification matching the given and family names.
 - Profile picture services do not check that the person depicted matches the owner of the wallet

Ensure users are aware of this:

> **Warning**
> There is no guarantee that (walletName) represents a particular individual or organisation.

We'll be releasing some other tech 🔜 to assert individual or organisation identity and get profile pictures that are proven match the identity of the wallet holder. 

# Installation

```
npm i "@portal-payments/solana-wallet-names"
```

# Setup

All you need is a Solana `Connection` object. Optionally, you can also get a [Twitter bearer token](https://developer.twitter.com/en/docs/authentication/oauth-2-0/bearer-tokens) - not including `twitterBearerToken` will simply disable Twitter results.

## 🧑🏻‍🦱➡️🔡🖼️ Wallet name to wallet address (and profile picture)

If you have a wallet name, like `mikemaccana.abc`, and you want to get an address and profile picture:

```typescript
import { walletNameToAddressAndProfilePicture } from "@portal-payments/solana-wallet-names";

const walletAddressAndProfilePicture = await walletNameToAddressAndProfilePicture(
  // A Solana connection
  connection,
  // One of: .abc .backpack .bonk .glow .poor .sol or @twitter
  "mikemaccana.abc"
);
```

`walletAddressAndProfilePicture` will look like:

```
{
  walletAddress: "5FHwkrdxntdK24hgQU8qgBjn35Y1zwhz1GZwCkP2UJnM",
  profilePicture: https://some.url/filename.ext,
}
```

If either (or both) aren't found, they will be `null`. We only error for actual errors (and don't throw error when there are no results):

```
{
  walletAddress: null,
  profilePicture: null,
}
```

## 🔡➡️🧑🏻‍🦱🖼️ Wallet address to wallet name (and profile picture)

If you have a wallet address, like `5FHwkrdxntdK24hgQU8qgBjn35Y1zwhz1GZwCkP2UJnM`, and you want to get an address and profile picture:

```typescript
import { walletAddressToNameAndProfilePicture } from "@portal-payments/solana-wallet-names";

const walletNameAndProfilePicture = await walletAddressToNameAndProfilePicture(
  // A Solana connection
  connection,
  // A Solana wallet address
  walletAddress
);
```

`walletNameAndProfilePicture` will look like:

```
{
  walletName: "mikemaccana.sol",
  profilePicture: https://some.url/filename.ext,
}
```

## Was this useful?

I'm a poor startup founder. Send me some tokens! `mikemaccana.sol`.

## Limits

- In cases where addresses can have multiple account names, only the first or 'main' account name is returned.
- Twitter to address lookup is handled through Bonfida `.sol` domains. Very few people with `.sol` domains have set up Twitter handle to `.sol` domain handling. If you do own a `.sol` domain it [setting up Twitter to .sol mapping](https://docs.bonfida.org/collection/solana-name-service-twitter) takes less than five minutes.
- Solana PFP Standard uses the Netscape 'broken image' icon for missing images. This is ugly, so instead we return `null`.
- Backpack and Ottr do not currently have wallet address to name mappings available.

# Contributing 

This library is designed to support all Solana naming services - as new services are added over time, we'd love you to contribute them here.

Please see [Portal Wallet Coding Guidelines](https://github.com/portalpayments/portalwallet/blob/main/CODING_GUIDELINES.md) when writing your PRs.

File issues in the **Issues** tab in GitHub 

# Changelog

See [CHANGELOG](./CHANGELOG.md).
