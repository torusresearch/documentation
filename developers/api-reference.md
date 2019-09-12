# API Reference

#### `init`

Called at the start of an import of torus to initialise the setup 

* Args
  * `buildEnv? : string` - 'production' \| 'development' \| 'staging' \| 'testing'
  * `enableLogging? : boolean` - false by default

#### `getPublicAddress`

Name resolver for email addresses to Ethereum Addresses

* Args
  * `email: string` Google account of user e.g. "hello@tor.us"
* Returns
  * `Promise<string>` associated Ethereum address of account

#### `setProvider`

Changes the network provider to specified provider

* Args

  * `network : string | {networkUrl: string, chainId: number, networkName: string}`  

          Options for network: `mainnet | rinkeby | ropsten | goerli | kovan`  
          If network is of type `"rpc"`, network should be passed as an object with `{ networkUrl, chainid, networkName}` params

  * `type?` - type of endpoint e.g. "rpc"

#### `showWallet(calledFromEmbed: boolean)`

Pops up the Torus Wallet app for the user

* Args
  * `calledFromEmbed` default to true

#### `showTorusButton()` 

Shows the Torus Button to the user

#### `hideTorusButton()`

Hides the Torus default button from the user 

#### `getUserInfo()`

Returns the loggedin user's google info including name, email and imageUrl

* Returns
  * `Promise<UserInfo>` 
* `interface UserInfo { email: string; name: string; profileImage: string; }`

#### `login()`

Prompts the user to login

* Returns
  * `Promise<string[]>`of Ethereum Addresses associated with the user login

#### `logout()`

Logs the user out

* Returns
  * `Promise<void>`

#### `web3`

The associated web3 object

#### `ethereum`

The associated ethereum object

#### `provider`

The associated provider object

