# Linking Accounts

DirectAuth supports the linking of user accounts from various identity providers. This allows a user to authenticate from any of their accounts and still be recognized by your app and associated with the same public/private key.

It is possible to link accounts via two methods; user initiated links between accounts after login or via a common unique identifier across logins used.

### User Initiated Linking

This process of linking accounts merges two existing user profiles into a single one. When linking accounts, a **primary login** and a **secondary login** must be specified.

The way this works behind the scenes is we store the difference `nonce` between the primary login key A and secondary key B on a self-hosted/public storage layer \(e.g. IPFS with a cached server\) for future retrieval.

When next time when the user logs into his/her secondary login he/she reconstructs `privKeyA` through the sum of `nonce` and `privKeyB`

```typescript
// Connecting Login A with Login B
privKeyA - privKeyB = nonce

// We store nonce on storage layer
// Next time a user logs in with Login B
privKeyA = privKeyB + nonce

```

### Common Unique Identifier

Several logins in DirectAuth have common datafields for users. For example, Google and traditional email logins share that they use email accounts to identify a user. Take a look at [Supported Verifiers/Logins](supported-authenticators-verifiers.md) for more details here.

We can automatically join accounts here via Aggregate Logins. There are some nuances here when considering how to join users, and mostly joins other than email are not recommended.

