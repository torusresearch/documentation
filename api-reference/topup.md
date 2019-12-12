# Topup

## initiateTopup

Initiates a topup tx with the specified provider right from the dapp. Please refer below for supported values of params and providers

```javascript
const paymentStatus = await torus.initiateTopup(provider, params);
```

**Parameters**

* `provider` - `enum` \(required\) : The specified payment partner. Supported options for provider are `moonpay` `wyre` `coindirect`
* `params` - `PaymentParams` \(optional\) : The topup tx params. used to autofill the form for that specific provider
  * `selectedCurrency` - `string` \(optional\) : The fiat currency supported. e.g.: "USD". In case an unsupported currency is specified, it throws
  * `fiatValue` - `Number` \(optional\) : The fiat value. It must be between the max and min value supported by that provider
  * `selectedCryptoCurrency` - `string` \(optional\) : The crypto currency supported. e.g.: "ETH". In case an unsupported crypto currency is specified, it throws

**Returns**

* `Promise<boolean>` : Returns a promise which resolves to a `boolean` indicating whether user has successfully completed the flow

**Reference**

```javascript
const paymentProviders = {
  simplex: {
    minOrderValue: 50,
    maxOrderValue: 20000,
    validCurrencies: ['USD', 'EUR'],
    validCryptoCurrencies: ['ETH']
  },
  moonpay: {
    minOrderValue: 24.99,
    maxOrderValue: 2000,
    validCurrencies: ['USD', 'EUR', 'GBP'],
    validCryptoCurrencies: ['ETH', 'DAI', 'TUSD', 'USDC', 'USDT']
  },
  wyre: {
    minOrderValue: 20,
    maxOrderValue: 250,
    validCurrencies: ['USD'],
    validCryptoCurrencies: ['ETH', 'DAI', 'USDC']
  },
  coindirect: {
    minOrderValue: 20,
    maxOrderValue: 1000,
    validCurrencies: ['EUR'],
    validCryptoCurrencies: ['ETH']
  }
}
```

```typescript
interface PaymentParams {
  selectedCurrency?: string;
  fiatValue?: Number;
  selectedCryptoCurrency?: string;  
}
```

**Examples**

```javascript
const paymentStatus = await torus.initiateTopup('wyre');
```

```javascript
const paymentStatus = await torus.initiateTopup('moonpay', {
  selectedCurrency: "USD",
  fiatValue: 50,
  selectedCryptoCurrency: "ETH"
});
```

```javascript
const paymentStatus = await torus.initiateTopup('simplex', {
  selectedCurrency: "USD"
});
```

