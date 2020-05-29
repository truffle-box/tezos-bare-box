Tezos Bare Box
=================

**Note: Experimental. Currently designed for demo purposes only.**

This box contains the default project structure for a Tezos project, used in the Tezos version of Truffle (see installation instructions below).


## Prerequisites

- [Docker](https://docs.docker.com/v17.12/install/)
  - Used for LIGO compilations and running a local sandbox Tezos node.
- [NodeJS](https://nodejs.org/en/)
  -  v8.9.4 to v12.2.0


## Installation

1. Install Truffle globally. Make sure you install `truffle@tezos`.
  ```shell
  npm install -g truffle@tezos
  ```

2. Download the box. This also takes care of installing the necessary dependencies.
  ```shell
  truffle init
  ```


## Usage

- Compiling the example smart contracts

  ```shell
  truffle compile
  ```

- Starting the local sandbox Tezos node
  ```shell
  npm run start-sandbox
  ```

- Migrating contracts
  ```shell
  truffle migrate
  ```

- Running contract tests
  ```shell
  truffle test
  ```


## Sandbox Management

An archive mode sandbox Tezos node is provided in this box with RPC exposed at port `8732` and two accounts generously funded.


#### Commands

```shell
npm run start-sandbox
npm run kill-sandbox
npm run restart-sandbox
```


#### Available Accounts

|alias  |pkh  |pk  |sk   |
|---|---|---|---|
|alice   |tz1VSUr8wwNhLAzempoch5d6hLRiTh8Cjcjb   |edpkvGfYw3LyB1UcCahKQk4rF2tvbMUk8GFiTuMjL75uGXrpvKXhjn   |edsk3QoqBuvdamxouPhin7swCvkQNgq4jP5KZPbwWNnwdZpSpJiEbq   |
|bob   |tz1aSkwEot3L2kmUvcoxzjMomb9mvBNuzFK6   |edpkurPsQ8eUApnLUJ9ZPDvu98E8VNj4KtJa1aZr16Cr5ow5VHKnz4   |edsk3RFfvaFaxbHx8BMtEW1rKQcPtDML3LXjNqMNLCzC3wLC1bWbAt   |


## Interacting with Live Networks

- A test faucet key can be obtained from https://faucet.tzalpha.net/. Once saved, it can be imported inside `truffle-config.js`:

  ```javascript

  const { mnemonic, secret, password, email } = require("./faucet.json");

  module.exports = {
    networks: {
      carthagenet: {
        host: "https://carthagenet.smartpy.io",
        port: 443,
        network_id: "*",
        secret,
        mnemonic,
        password,
        email,
        type: "tezos"
      }
    }
  };

  ```

- `truffle@tezos` also supports importing an activated account's secret key:

  ```javascript

  module.exports = {
    networks: {
      carthagenet: {
        host: "https://carthagenet.smartpy.io",
        port: 443,
        network_id: "*",
        secretKey: "edsk...", // private key
        type: "tezos"
      }
    }
  };
  ```

  ```shell
  truffle migrate --network carthagenet
  truffle test --network carthagenet
  ```
