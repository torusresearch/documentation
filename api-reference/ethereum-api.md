# Ethereum API

## web3

The associated web3 object. Please refer to web3 [documentation](https://github.com/ethereum/wiki/wiki/JavaScript-API) for more information

## Ethereum

The associated ethereum object. Please refer to Metamask documentation [here](https://github.com/MetaMask/metamask-inpage-provider)

**Examples**

```javascript
await torus.ethereum.enable(); // does the same thing as `await torus.login();`
```

## Provider

The associated provider object

**Reference**

```typescript
declare class Provider {
  send(payload: JsonRPCRequest, callback: Callback<JsonRPCResponse>): any;
}

interface JsonRPCResponse {
  jsonrpc: string;
  id: number;
  result?: any;
  error?: string;
}

interface JsonRPCRequest {
  jsonrpc: string;
  method: string;
  params: any[];
  id: number;
}

interface Callback<ResultType> {
  (error: Error): void;
  (error: null, val: ResultType): void;
}
```

**Examples**

```javascript
const web3 = new Web3(torus.provider);
```

