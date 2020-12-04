# FAQ

## What is a verifier?

A verifier is a unique identifier for your OAuth registration on the torus network. The Public/private keys generated for a user are scoped to a verifier. 

Please contact us to get a verifier deployed for you.

## What is a verifierId?

VerifierId is the unique identifier to publicly represent a user on a verifier. 

e.g: email, sub etc. other fields can be classified as VerifierId

## What is a network?

Torus has two environments where the verifiers reside - `mainnet` and `testnet`.

 `testnet` is a sandbox environment for developers to experiment. People usually test and finish their integration here. 

`mainnet` is prod environment.

## My Redirect page is stuck in iOS Chrome

iOS Chrome doesn't support service workers. So, you need to serve a fallback html page `redirect.html` Please check if redirect.html is being served correctly by navigating to `baseUrl/redirect#a=123`. It should show a loader

For nginx, here is a simple server configuration

```text
    location ~* (/serviceworker/redirect) {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header Content-Security-Policy "default-src https:; script-src https: 'unsafe-inline' 'unsafe-eval'; style-src https: 'unsafe-inline';";
            add_header X-Content-Type-Options nosniff;
            add_header X-XSS-Protection "1; mode=block";
            add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";
            default_type "text/html";
            alias PATH_TO_REDIRECT_HTML_FILE;
            autoindex off;
    }
```

Alternatively, you can configure your redirect url to include redirect.html by passing in an option `redirectPathName: 'redirect.html'` while instantiating the sdk. Please remember to change the oauth redirect url to reflect this change

## Discord Login only works once in 30 min

Torus Login requires a new token for every login attempt. Discord returns the same access token for 30 min unless it's revoked. Unfortunately, it needs to be revoked from the backend since it needs a client secret. Here's some sample code which does it

```javascript
const axios = require("axios").default;
const FormData = require("form-data");

const { DISCORD_CLIENT_SECRET, DISCORD_CLIENT_ID } = process.env;
const { token } = req.body;
const formData = new FormData();
formData.append("token", token);
await axios.post("https://discordapp.com/api/oauth2/token/revoke", formData, {
  headers: {
    ...formData.getHeaders(),
    Authorization: `Basic ${Buffer.from(`${DISCORD_CLIENT_ID}:${DISCORD_CLIENT_SECRET}`, "binary").toString("base64")}`,
  },
});
```

## How to initialise web3 with private key \(returned after login\) ?

One can use privateKeyToAccount method to initialise web3 with a privatekey. If you are supplying a hexadecimal number, it must have 0x prefix in order to be in line with other Ethereum libraries.

```javascript
web3.eth.accounts.privateKeyToAccount(PRIVATE_KEY);
```



