# API Reference

## Constructor

Construct your Torus Direct SDK

```typescript
const torus = new TorusDirectSdk(options);
```

#### Arguments

`options` is an object with the following parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>baseUrl</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>Redirect Uri for OAuth is <code>baseUrl+redirectPathName</code>
        </p>
        <p>Torus Direct SDK installs a service worker to capture the auth redirect.
          Usually, your app may have it&apos;s own service worker at the root. So,
          please use <code>`${location.origin}/auth`</code>as <code>baseUrl </code>instead
          and use <code>`${location.origin}/auth/${redirectPathName}`</code>as redirect
          Uri at the OAuth registration page</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>network?</code>
      </td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>Torus Network to target</p>
        <p><code>options: &quot;mainnet&quot; | &quot;testnet&quot;</code>
        </p>
        <p><code>default: &quot;mainnet&quot;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>proxyContractAddress?</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>The contract address of torus network</p>
        <p><code>mainnet: &quot;0x638646503746d5456209e33a2ff5e3226d698bea&quot;</code>
        </p>
        <p><code>testnet: &quot;0x4023d2a0D330bF11426B12C6144Cfb96B7fa6183&quot;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>enableLogging?</code>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>Whether to enable logging</p>
        <p><code>default: false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>redirectPathName?</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>The path from which redirect.html is being served</p>
        <p><code>default: &quot;redirect&quot;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>redirectToOpener?</code>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">
        <p>For chrome extensions, the general methods for capturing auth redirects
          don&apos;t work. So, we redirect to the window which opens the auth window.</p>
        <p><code>default: false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>apiKey?</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">API Key for torus to enable higher access limits</td>
    </tr>
  </tbody>
</table>

#### Returns

An instance of Torus Direct SDK

#### Examples

{% tabs %}
{% tab title="Mainnet" %}
```typescript
// Say location.origin is example.com

// Targets mainnet
// Final redirect url is 'https://example.com/auth/redirect'
const torusdirectsdk = new TorusDirectSdk({
    baseUrl: `${location.origin}/auth`,
});

/* 
  Register the final redirect url with OAuth client
  Don't forget to serve sw.js and redirect.html from baseUrl
  which means 'https://example.com/auth/sw.js' and 
  'https://example.com/auth/redirect' 
  should serve redirect.html present in the repo
 */
```
{% endtab %}

{% tab title="Testnet" %}
```typescript
// Say location.origin is example.com

// Targets testnet + custom path name
// Final redirect url is 'https://example.com/auth/redirect.html'
const torusdirectsdk = new TorusDirectSdk({
    baseUrl: `${location.origin}/auth`,
    enableLogging: true,
    redirectPathName: "redirect.html",
    // details for test net
    proxyContractAddress: "0x4023d2a0D330bF11426B12C6144Cfb96B7fa6183",
    network: "testnet",
});


/* 
  Register the final redirect url with OAuth client
  Don't forget to serve sw.js and redirect.html from baseUrl
  which means 'https://example.com/auth/sw.js' and 
  'https://example.com/auth/redirect.html' 
  should serve redirect.html present in the repo
 */
```
{% endtab %}

{% tab title="Chrome Extension" %}
```typescript
// Say location.origin is example.com

// testnet + chrome extension
// Final redirect url is 'https://example.com/auth/redirect'
const torusdirectsdk = new TorusDirectSdk({
    baseUrl: `${location.origin}/auth`,
    enableLogging: true,
    redirectToOpener: true,
    // details for test net
    proxyContractAddress: "0x4023d2a0D330bF11426B12C6144Cfb96B7fa6183",
    network: "testnet", // details for test net
});

/* 
  Register the final redirect url with OAuth client
  Don't forget to serve sw.js and redirect.html from baseUrl
  which means 'https://example.com/auth/sw.js' and 
  'https://example.com/auth/redirect' 
  should serve redirect.html present in the repo
 */
```
{% endtab %}
{% endtabs %}

## `init`

Initializes the torus direct sdk and checks for the existence of service worker and redirect.html.  
Please make sure to serve both `sw.js` and `redirect.html` present in the sdk from `baseUrl`

```typescript
await torusdirectsdk.init(options);
```

#### Arguments

`options` is an object with the following parameters

| Parameter | Type | Definition |
| :--- | :--- | :--- |
| `skipSw?` | boolean | Does not require the service worker from operation |

#### Returns

A promise with void

#### Examples

{% tabs %}
{% tab title="Check" %}
```typescript
await torusdirectsdk.init();
```
{% endtab %}

{% tab title="Skip" %}
```typescript
await torusdirectsdk.init({ skipSw: true });
```
{% endtab %}
{% endtabs %}

## `triggerLogin`

`triggerLogin` performs the following actions

Opens the login window of the auth provider as a popup  
Listens on the redirected url  
Returns the `verifier` scoped public private key pair + user info  
  
If your `verifier` is of normal type, use this method.

If you wish to have account linking / multiple verifiers returning same keys \(e.g.: `passwordless` and `google` logins returning the same key\), use `triggerAggregateLogin` instead. 

```typescript
await torusdirectsdk.triggerLogin(options);
```

#### Arguments

`options` is an object of type `SubVerifierDetails` with the following parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>typeOfLogin</code>
      </td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">
        <p>Login Types</p>
        <p><code>&quot;google&quot; | &quot;facebook&quot; | &quot;reddit&quot; | &quot;discord&quot; | &quot;twitch&quot; | &quot;apple&quot; | &quot;github&quot; | &quot;linkedin&quot; | &quot;twitter&quot; | &quot;weibo&quot; | &quot;line&quot;  | &quot;email_password&quot; | &quot;jwt&quot;</code>
        </p>
        <p>For <code>passwordless</code> and other types of custom logins use &quot;<code>jwt</code>&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>verifier</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>A verifier is a unique identifier for your OAuth registration on the torus
          network. The public/private keys generated for a user are scoped to a verifier.</p>
        <p>Register your app <a href="http://register.directauth.io">here</a> to get
          your verifier today</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>clientId</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>clientid obtained from OAuth registration</p>
        <p>For native logins, please use the one from OAuth registration.</p>
        <p>For proxy logins, please use the client id obtained from proxy provider</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>jwtParams?</code>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">Details below</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>hash?</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The location hash returned from OAuth login</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>queryParameters?</code>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">Key value pairs of query parameters returned from OAuth login</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
In some cases \(electron apps, chrome extensions, redirect flow\), your app will be redirected to the redirect url with hash and query params from OAuth provider.

To get torus key in such cases, please pass along those parameters into the sdk. Passing these will skip the login and return the torus result directly.
{% endhint %}

```typescript
// jwt params
// we support all proxy auth providers which use JWT standard
// e.g: Auth0, Okta, Cognito, Firebase, authing etc.
interface jwtParams {
  /**
   * Your proxy provider account domain such as `'example.auth0.com'`,
   * `'example.eu.auth0.com'` or , `'example.mycompany.com'`
   */
  domain: string;
  /**
   * The Client ID found on your proxy provider's page
   * This will override the clientId specified above
   */
  client_id?: string;
  /**
   * The default URL where your browser is redirected to with
   * the authentication result. It must be whitelisted in
   * the "Allowed Callback URLs" field in your Proxy provider application's
   * settings. If not provided here, it should be provided in the other
   * methods that provide authentication.
   * Note: This will override the redirectUrl generated using baseUrl
   */
  redirect_uri?: string;
  /**
   * The value in seconds used to account for clock skew in JWT expirations.
   * Typically, this value is no more than a minute or two at maximum.
   * Defaults to 60s.
   */
  leeway?: number;

  /**
   * The field in jwt token which maps to verifier id
   */
  verifierIdField?: string;

  /**
   * Whether the verifier id field is case sensitive
   * @default true
   */
  isVerifierIdCaseSensitive?: boolean;
   /**
   * - `'page'`: displays the UI with a full page view
   * - `'popup'`: displays the UI with a popup window
   * - `'touch'`: displays the UI in a way that leverages a touch interface
   * - `'wap'`: displays the UI with a "feature phone" type interface
   */
  display?: "page" | "popup" | "touch" | "wap" | string;
  /**
   * - `'none'`: do not prompt user for login or consent on reauthentication
   * - `'login'`: prompt user for reauthentication
   * - `'consent'`: prompt user for consent before processing request
   * - `'select_account'`: prompt user to select an account
   */
  prompt?: "none" | "login" | "consent" | "select_account" | string;
  /**
   * Maximum allowable elasped time (in seconds) since authentication.
   * If the last time the user authenticated is greater than this value,
   * the user must be reauthenticated.
   */
  max_age?: string | number;
  /**
   * The space-separated list of language tags, ordered by preference.
   * For example: `'fr-CA fr en'`.
   */
  ui_locales?: string;
  /**
   * Previously issued ID Token.
   */
  id_token_hint?: string;
  /**
   * The user's email address or other identifier. When your app knows
   * which user is trying to authenticate, you can provide this parameter
   * to pre-fill the email box or select the right session for sign-in.
   *
   * This currently only affects the classic Lock experience.
   */
  login_hint?: string;
  acr_values?: string;
  /**
   * The default scope to be used on authentication requests.
   * The defaultScope defined in the Auth0Client is included
   * along with this scope
   */
  scope?: string;
  /**
   * The default audience to be used for requesting API access.
   */
  audience?: string;
  /**
   * The name of the connection configured for your application.
   * If null, it will redirect to the Auth0 Login Page and show
   * the Login Widget.
   */
  connection?: string;

  /**
   * If you need to send custom parameters to the Authorization Server,
   * make sure to use the original parameter name.
   */
  [key: string]: unknown;
}
```

#### Returns

A promise with `TorusLoginResponse`

```typescript
type TorusLoginResponse = TorusSingleVerifierResponse & TorusKey;

interface TorusSingleVerifierResponse {
  userInfo: TorusVerifierResponse & LoginWindowResponse;
}

interface TorusKey {
  publicAddress: string;
  privateKey: string;
}

interface TorusVerifierResponse {
  email: string;
  name: string;
  profileImage: string;
  verifier: string;
  verifierId: string;
  typeOfLogin: LOGIN_TYPE;
}

interface LoginWindowResponse {
  accessToken: string;
  idToken?: string;
}

type LOGIN_TYPE = "google" | "facebook" | "reddit" | "discord" 
| "twitch" | "apple" | "github" | "linkedin" | "twitter" | "weibo" 
| "line"  | "email_password" | "jwt";
```

#### Examples

{% tabs %}
{% tab title="Native" %}
```typescript
/*
 Native logins use this approach
 The following are native logins
 - google
 - facebook
 - reddit
 - discord
 - twitch
 All others are proxy logins
*/

const loginDetails = await torusdirectsdk.triggerLogin({
    typeOfLogin: "google",
    verifier: "YOUR_VERIFIER_HERE", // get your verifier deployed today
    clientId: "YOUR_GOOGLE_CLIENT_ID",
});

const loginDetails = await torusdirectsdk.triggerLogin({
    typeOfLogin: "facebook",
    verifier: "YOUR_VERIFIER_HERE", // get your verifier deployed today
    clientId: "YOUR_FACEBOOK_APP_ID",
});
```
{% endtab %}

{% tab title="Proxy" %}
```typescript
/*
  All logins done via a proxy auth provider use this method
  domain is a mandatory param
*/


const jwtParams = {
    domain: "YOUR_PROXY_VERIFIER_DOMAIN" // eg: "https://torus-test.auth0.com"
}

// twitter
const loginDetails = await torusdirectsdk.triggerLogin({
    typeOfLogin: "twitter",
    verifier: "YOUR_TWITTER_VERIFIER",
    // this is obtained at the proxy website (e.g.: auth0 application client id)
    clientId: "YOUR_PROXY_TWITTER_CLIENT_ID", 
    jwtParams,
});

// passwordless
const loginDetails = await torusdirectsdk.triggerLogin({
    typeOfLogin: "jwt",
    verifier: "YOUR_PASSWORDLESS_VERIFIER",
    // this is obtained at the proxy website (e.g.: auth0 application client id)
    clientId: "YOUR_PROXY_PASSWORDLESS_CLIENT_ID", 
    jwtParams: { 
        ...jwtParams, 
        // this corresponds to the field inside jwt which must be used to uniquely
        // identify the user
        verifierIdField: "name",
        isVerifierIdCaseSensitive: false,
    },
});

```
{% endtab %}

{% tab title="Rehydrate" %}
```typescript
/*
  In some platforms (electron etc.) or in cases where you wish to perform 
  authentication in a different manner other than opening a popup (redirect flow),
  you can pass in hash and queryParameters of redirected url into the method
  to bypass opening of popup window and return the result
*/

var url = new URL(location.href);
const hash = url.hash.substr(1);
const queryParameters = {};
for (let key of url.searchParams.keys()) {
  queryParameters[key] = url.searchParams.get(key);
}

const loginDetails = await torusdirectsdk.triggerLogin({
    typeOfLogin: "google",
    verifier: "YOUR_GOOGLE_VERIFIER",
    clientId: "YOUR_GOOGLE_CLIENT_ID",
    jwtParams: {},
    hash,
    queryParameters,
});

```
{% endtab %}
{% endtabs %}

## `triggerAggregateLogin`

`triggerAggregateLogin` performs the following actions

Opens the login window of the auth provider as a popup  
Listens on the redirected url  
Returns the `verifier` scoped public private key pair + user info  
  
Use this if you wish to have account linking / multiple verifiers returning same keys \(e.g.: `passwordless` and `google` logins returning the same key or google iOS,  web, android clients to return the same key\)

Currently, only `single_id_verifier`is supported as aggregate verifier type

```typescript
await torusdirectsdk.triggerAggregateLogin(options);
```

#### Arguments

`options` is an object of type `AggregateLoginParams` with the following parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>aggregateVerifierType</code>
      </td>
      <td style="text-align:left">enum</td>
      <td style="text-align:left">Currently only <code>single_id_verifier</code> is supported</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>verifierIdentifier</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>A <code>verifierIndentifier</code> is a unique identifier for your OAuth
          registration on the torus network. The public/private keys generated for
          a user are scoped to a <code>verifierIdentifier</code> for aggregate login.</p>
        <p>Register your app <a href="http://register.directauth.io">here</a> to get
          your <code>verifierIdentifier</code> today</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>subVerifierDetailsArray</code>
      </td>
      <td style="text-align:left"><code>SubVerifierDetails[]</code>
      </td>
      <td style="text-align:left"><code>SubVerifierDetails</code> is the options parameter for <code>triggerLogin</code>
      </td>
    </tr>
  </tbody>
</table>

#### Returns

A promise with `TorusAggregateLoginResponse`

```typescript
type TorusAggregateLoginResponse = TorusAggregateVerifierResponse & TorusKey;

interface TorusAggregateVerifierResponse {
  userInfo: (TorusVerifierResponse & LoginWindowResponse)[];
}
// Additional types are present in the triggerLogin documentation
```

#### Examples

{% tabs %}
{% tab title="Native" %}
```typescript
/*
 If you want google and facebook logins to have the same user account,
 do the following 
*/

const subVerifierDetailsGoogle = {
    typeOfLogin: "google",
    verifier: "ANY_UNIQUE_STRING",
    clientId: "YOUR_GOOGLE_CLIENT_ID",
}

const subVerifierDetailsFacebook = {
    typeOfLogin: "facebook",
    verifier: "ANY_UNIQUE_STRING",
    clientId: "YOUR_FACEBOOK_APP_ID",
}

// The deployed verifier identifier links both google and facebook
const commonVerifierIdentifier = "YOUR_VERIFIER_IDENTIFIER_HERE";

// when user clicks google button, use this
const loginDetails = await torusdirectsdk.triggerAggregateLogin({
    aggregateVerifierType: "single_id_verifier",
    // get your verifier identifier deployed today
    verifierIdentifier: commonVerifierIdentifier,
    subVerifierDetailsArray: [subVerifierDetailsGoogle],
});

// when user clicks facebook button, use this
const loginDetails = await torusdirectsdk.triggerAggregateLogin({
    aggregateVerifierType: "single_id_verifier",
    // get your verifier identifier deployed today
    verifierIdentifier: commonVerifierIdentifier,
    subVerifierDetailsArray: [subVerifierDetailsFacebook],
});
```
{% endtab %}

{% tab title="Proxy" %}
```typescript
/*
 If you want google and passwordless logins to have the same user account,
 do the following 
*/

const jwtParams = {
    domain: "YOUR_PROXY_VERIFIER_DOMAIN" // eg: "https://torus-test.auth0.com"
}

const subVerifierDetailsGoogle = {
    typeOfLogin: "google",
    verifier: "ANY_UNIQUE_STRING",
    clientId: "YOUR_GOOGLE_CLIENT_ID",
}

const subVerifierDetailsPasswordless = {
    typeOfLogin: "jwt",
    verifier: "ANY_UNIQUE_STRING",
    // this is obtained at the proxy website (e.g.: auth0 application client id)
    clientId: "YOUR_PROXY_PASSWORDLESS_CLIENT_ID", 
    jwtParams: { 
        ...jwtParams, 
        // this corresponds to the field inside jwt which must be used to uniquely
        // identify the user. This is mapped b/w google and passwordless logins
        verifierIdField: "name",
        isVerifierIdCaseSensitive: false,
    },
}

// The deployed verifier identifier links both google and passwordless
const commonVerifierIdentifier = "YOUR_VERIFIER_IDENTIFIER_HERE";

// when user clicks google button, use this
const loginDetails = await torusdirectsdk.triggerAggregateLogin({
    aggregateVerifierType: "single_id_verifier",
    // get your verifier identifier deployed today
    verifierIdentifier: commonVerifierIdentifier,
    subVerifierDetailsArray: [subVerifierDetailsGoogle],
});

// when user clicks passwordless button, use this
const loginDetails = await torusdirectsdk.triggerAggregateLogin({
    aggregateVerifierType: "single_id_verifier",
    // get your verifier identifier deployed today
    verifierIdentifier: commonVerifierIdentifier,
    subVerifierDetailsArray: [subVerifierDetailsPasswordless],
});
```
{% endtab %}

{% tab title="Rehydrate" %}
```typescript
/*
  In some platforms (electron etc.) or in cases where you wish to perform 
  authentication in a different manner other than opening a popup (redirect flow),
  you can pass in hash and queryParameters of redirected url into the method
  to bypass opening of popup window and return the result
*/

var url = new URL(location.href);
const hash = url.hash.substr(1);
const queryParameters = {};
for (let key of url.searchParams.keys()) {
  queryParameters[key] = url.searchParams.get(key);
}

const subVerifierDetailsGoogle = {
    typeOfLogin: "google",
    verifier: "ANY_UNIQUE_STRING",
    clientId: "YOUR_GOOGLE_CLIENT_ID",
    jwtParams: {},
    hash,
    queryParameters,
}

// The deployed verifier identifier links both google and other login type
const commonVerifierIdentifier = "YOUR_VERIFIER_IDENTIFIER_HERE";

// when user clicks passwordless button, use this
const loginDetails = await torusdirectsdk.triggerAggregateLogin({
    aggregateVerifierType: "single_id_verifier",
    // get your verifier identifier deployed today
    verifierIdentifier: commonVerifierIdentifier,
    subVerifierDetailsArray: [subVerifierDetailsGoogle],
});
```
{% endtab %}
{% endtabs %}

## `getTorusKey`

`getTorusKey` is a helper method which by passes the login flow and communicates directly with the torus nodes to return you the user's key.

Use this if you have a custom login flow and wish to get just the user's key

```typescript
await torusdirectsdk.getTorusKey(verifier: string,
    verifierId: string,
    verifierParams: { verifier_id: string },
    idToken: string,
    additionalParams?: extraParams);
```

#### Arguments

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Definition</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>verifier</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>A <code>verifier</code> is a unique identifier for your OAuth registration
          on the torus network. The public/private keys generated for a user are
          scoped to a verifier.</p>
        <p>Register your app <a href="http://register.directauth.io">here</a> to get
          your <code>verifier</code> today</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>verifierId</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p><code>verifierId </code>is the unique identifier to publicly represent
          a user on a verifier.</p>
        <p>e.g: email, sub etc. other fields can be classified as <code>verifierId</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>verifierParams</code>
      </td>
      <td style="text-align:left"><code>Object</code>
      </td>
      <td style="text-align:left">
        <p>As stated in the signature.</p>
        <p>Can contain other fields which can be useful for aggregate logins</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>idToken</code>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><code>idToken</code> or <code>accessToken</code> received from the OAuth
        provider</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>additionalParams?</code>
      </td>
      <td style="text-align:left"><code>extraParams</code>
      </td>
      <td style="text-align:left">
        <p>Any additional parameters you wish to send to the torus nodes.</p>
        <p>useful for WebAuthn logins</p>
      </td>
    </tr>
  </tbody>
</table>

#### Returns

A promise with `TorusKey`

```typescript
interface TorusKey {
  publicAddress: string;
  privateKey: string;
}

interface extraParams {
  [key: string]: unknown;
}
```

#### Examples

{% tabs %}
{% tab title="Native" %}
```typescript

// google
const torusKey = await torusdirectsdk.getTorusKey("YOUR_GOOGLE_VERIFIER", 
    "USER_EMAIL",
    { verifier_id: "USER_EMAIL" },
    "USER_GOOGLE_ID_TOKEN")
    
```
{% endtab %}
{% endtabs %}

