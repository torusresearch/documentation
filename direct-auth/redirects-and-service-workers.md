# Redirects & Service Workers

### OAuth Redirect

Redirect URLs are a critical part of the OAuth flow. After a user successfully authorizes an application, the authorization server will redirect the user back to the application with either access/ id token in the URL. Because the redirect URL will contain sensitive information, it is critical that the developer only whitelists authorized URLs with the OAuth provider.

In torus direct auth, we require the query and hash params present in the redirect url to retrieve the user data.

### Web

In [torus-direct-web-sdk](https://github.com/torusresearch/torus-direct-web-sdk), there are two ways to serve the redirect url 

#### using service workers

A service worker is a script that your browser runs in the background, separate from a web page. We can use service workers to capture the redirected url and serve a html page. The code present in the html communicates the query and hash params to the underlying torus sdk which finishes the login process.

To use service workers, you need to serve the sw.js \(present in `torus-direct-web-sdk` npm package\) from the baseUrl of your website \(eg: if `https://example.com/serviceworker/redirect` is your redirect uri, baseUrl would be `https://example.com/serviceworker`\)

To know more about service workers, click [here](https://developers.google.com/web/fundamentals/primers/service-workers)

#### using hosted `redirect.html`

[Some browsers](https://caniuse.com/serviceworkers) don't support service workers. For those browsers, you need to serve redirect.html \(present in `torus-direct-web-sdk` npm package\) from the baseUrl as defined above.

If you're facing problems with redirect being stuck, please refer to [FAQ section](faq.md#my-redirect-page-is-stuck-in-ios-chrome)

### Android \(and react-native android\)

In [torus-direct-android-sdk](https://github.com/torusresearch/torus-direct-android-sdk), please add mainfestPlaceholders in your build.gradle with the following properties

```groovy
android.defaultConfig.manifestPlaceholders = [
        'torusRedirectScheme': 'YOUR_APP_SCHEME', // (torusapp)
        'torusRedirectHost': 'YOUR_APP_HOST', // (org.torusresearch.torusdirectandroid)
        'torusRedirectPathPrefix': 'YOUR_REDIRECT_PATH' // (/redirect)
]
```

 At verifier's interface \(where you obtain client id\), please use `browserRedirectUri` in DirectSdkArgs \(default: '[https://scripts.toruswallet.io/redirect.html](https://scripts.toruswallet.io/redirect.html)'\) as the redirect uri. If you specify a custom `browserRedirectUri`, pls host [redirect.html](https://github.com/torusresearch/torus-direct-android-sdk/blob/master/torusdirect/src/main/java/org/torusresearch/torusdirect/activity/redirect.html) \(present in the package\) at that url.

