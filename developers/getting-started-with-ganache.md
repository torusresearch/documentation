---
description: Install Ganache to run a local blockchain test-net on your machine.
---

# Developing with Ganache

Torus website runs on https. The browser security model does not allow an insecure connection to a http endpoint over https. Install the following NPM package to proxy your http traffic from Ganache through a https endpoint. The NPM package redirects the traffic present on your Ganache port through https://localhost:8545.

### 1. Install and run ganache-http-proxy

```bash
npm install -g ganache-http-proxy
ganache-http-proxy
```

### 2. Run Ganache on port 8546

8546 is the port where Ganache is running locally.

```bash
ganache-cli -p 8546
```

### 3. Connect to the Ganache localhost instance in Torus

![Select localhost:8545 from in the Network selector under the Settings tab within the Torus wallet](../.gitbook/assets/torus-ganache-localhost.png)

### 4. Accept localhost certificates in your browser

Chrome: Paste the following URL into the address bar.

```text
chrome://flags/#allow-insecure-localhost
```

