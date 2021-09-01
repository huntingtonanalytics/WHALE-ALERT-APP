# Whale Alerts | Moralis

## About

Purpose: Allow user to track wallet addresses, cross-chain (ETH/BSC/MATIC/…) and recieve alerts when specific transaction conditions are met.

This tutorial video is a great video introduction: [Link to Moralis YouTube Video](https://youtu.be/-M1GR45GykQ).

Built on [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html) a ReactJS front-end with a Moralis backend.

## ⚙️ Quick start

Via terminal, navigate to root directory:

```sh
npm install

```

Also install Moralis admin client:

```sh
npm install -g moralis-admin-cli

```

This will allow you to sync Moralis Cloud Functions in [src/Cloud/CloudFile.js](CloudFile.js):

```sh
moralis-admin-cli watch-cloud-file --moralisApiKey xxx --moralisApiSecret xxx --moralisSubdomain xxx.moralisweb3.com --autoSave 1 --moralisCloudfolder /xxx/moralis-whale-alerts/src/Cloud

```

Finally provide your path to the CloudFile.js and sync with Moralis server instance:

```sh
/xxx/moralis-whale-alerts/src/Cloud/CloudFile.js

```

Once installed and synced with your Moralis server instance, in the project directory run:

```sh
npm start

```

## Dependencies:

`moralis`: [Docs](https://docs.moralis.io/)
`@chakra-ui/react`: [Docs](https://chakra-ui.com/docs/getting-started)
`react-final-form`: [Docs](https://final-form.org/docs/final-form/getting-started)

`react`, `react-dom` `react-moralis` should be installed automatically ([package.json](./package.json)).

## Adapt Alert Conditons

Cloud function `run` on `watchEthAddress` adds `address` to your list of addresses to track transactions on.

```javascript
//
// sync all txs in realtime to WatchedEthAddress class
Moralis.Cloud.run("watchEthAddress", {
  address,
  sync_historical: false,
});
```

Function `afterSave` on `EthTransactions` then is where you create conditons against those transactions to intiate alerts.

```javascript
 Moralis.Cloud.afterSave("EthTransactions", async function (request) {
    …
 }
```

## Todos

- Dispatch alerts via Telegram/Twitter/
- Threshold conditions against tx e.g. only txs > $1,000,000.
- Enable cross-chain compatibility.
- Much more TBA.

---