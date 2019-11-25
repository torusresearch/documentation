## getPublicAddress

This resolves an email address to an Ethereum public Address. Returns an account if it already exists on torus network. Creates, if otherwise

```javascript
const publicAddress = await torus.getPublicAddress(params);
```

**Parameters**

- `params` - `VerifierArgs` : The parameters passed to the method
  - `verifier` - `enum` : The verifier to use. Supported enums are `google`, `reddit`, `discord`
  - `verifierId` - `string` : The unique identifier for that verifier. \(Say email for google, username for reddit and id for discord\)

**Returns**

- `Promise<string>` : Returns a promise which resolves to the Ethereum address associated with the email

**Reference**

```typescript
interface VerifierArgs {
  verifier: "google" | "reddit" | "discord";
  verifierId: string;
}
```

**Examples**

```javascript
const publicAddress = await torus.getPublicAddress({
  verifier: "google",
  verifierId: "random@gmail.com"
});
```

## setProvider

This changes the network provider to a specified provider. Opens a popup for user's consent

```javascript
await torus.setProvider(params);
```

**Parameters**

- `params` - `NetworkInterface` : The network options. Used to specify a network provider
  - `host` - `string` : The hostname or the `HTTPS` `JSON-RPC` endpoint. Supported options for hostname are `mainnet` `rinkeby` `ropsten` `kovan` `goerli` `localhost` `matic`
  - `chainId` - `number` \(optional\) : ChainId of the network
  - `networkName` - `string` \(optional\) : Name of the network

**Returns**

- `Promise<void>` : Returns a promise which resolves to void

**Reference**

```typescript
interface NetworkInterface {
  host:
    | "mainnet"
    | "rinkeby"
    | "ropsten"
    | "kovan"
    | "goerli"
    | "localhost"
    | "matic"
    | string;
  chainId?: number;
  networkName?: string;
}
```

**Examples**

```javascript
await torus.setProvider({
  host: "rinkeby" // default : 'mainnet'
});
```

```javascript
await torus.setProvider({
  host: "https://ethboston1.skalenodes.com:10062", // mandatory
  chainId: 1, // optional
  networkName: "Skale Network" // optional
});
```

## login

Prompts the user to login. Opens the login popup

```javascript
await torus.login(params);
```

**Parameters**

- `params` - `LoginParams` \(optional\) : The login options. Used to specify a type of login
  - `verifier` - `enum` : The OAuth verifier name. Supported options for verifier are `google` `facebook` `twitch` `reddit` `discord`

**Returns**

- `Promise<string[]>` : Returns a promise which resolves to the Ethereum Addresses associated with the user

**Reference**

```typescript
interface LoginParams {
  verifier?: "google" | "facebook" | "twitch" | "reddit" | "discord";
}
```

**Examples**

```javascript
await torus.login();
```

## getUserInfo

Returns the logged-in user's google info including name, email, and imageUrl. Please make sure the user is logged in before calling this method. In every `session`, only the first call opens the popup for the user's consent. All subsequent requests don't open the popup

```javascript
const userInfo = await torus.getUserInfo();
```

**Returns**

- `Promise<UserInfo>` : Returns a promise which resolves to `UserInfo` object

**Reference**

```typescript
interface UserInfo {
  email: string;
  name: string;
  profileImage: string;
  verifier: string;
  verifierId: string;
}
```

**Examples**

```javascript
const userInfo = await torus.getUserInfo();
```

## logout

Logs the user out of torus. Requires that a user is logged in already

```javascript
await torus.logout();
```

**Returns**

- `Promise<void>` : Returns a promise which resolves to void

**Examples**

```javascript
await torus.logout();
```

## cleanUp

This cleans up the iframe and buttons created by torus package. If the user is logged in, it logs him out first and then cleans up

```javascript
await torus.cleanUp();
```

**Returns**

- `Promise<void>` : Returns a promise which resolves to void

**Examples**

```javascript
await torus.cleanUp();
```
