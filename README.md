#  Foundry Starter Kit

<br/>
<p align="center">
<a href="https://chain.link" target="_blank">
<img src="./img/chainlink-foundry.png" width="225" alt="Chainlink Foundry logo">
</a>
</p>
<br/>

# THIS REPO IS NOT FINISHED!!!
# Still in draft mode

- [Foundry Starter Kit](#foundry-starter-kit)
- [THIS REPO IS NOT FINISHED!!!](#this-repo-is-not-finished)
- [Still in draft mode](#still-in-draft-mode)
  - [This is a working draft based on dapptools-template](#this-is-a-working-draft-based-on-dapptools-template)
- [Installation](#installation)
  - [Requirements](#requirements)
  - [Getting Started](#getting-started)
  - [Testing](#testing)
- [Deploying](#deploying)
  - [Setup your Account/ethsign](#setup-your-accountethsign)
  - [Setup your .env file](#setup-your-env-file)
  - [Testnet & Mainnet Deployment](#testnet--mainnet-deployment)
    - [Local Testnet](#local-testnet)
    - [Verifying on Etherscan](#verifying-on-etherscan)
- [Resources](#resources)
- [TODO](#todo)

## This is a working draft based on [dapptools-template](https://github.com/gakonst/dapptools-template)
See the [#TODO](#todo) list at the bottom for a list of things to complete. 

Implementation of the following 3 Chainlink features using the [foundry](https://github.com/gakonst/foundry) development environment:
 - [Chainlink Price Feeds](https://docs.chain.link/docs/using-chainlink-reference-contracts)
 - [Chainlink VRF](https://docs.chain.link/docs/chainlink-vrf/)
 - [Chainlink Keepers](https://docs.chain.link/docs/chainlink-keepers/introduction/)

# Installation

## Requirements
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Rust and Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html)
- [Foundry](https://github.com/gakonst/foundry)

## Getting Started 

```sh
git clone git clone --single-branch --branch foundry https://github.com/smartcontractkit/dapptools-starter-kit
cd dapptools-starter-kit
make # This installs the project's dependencies.
make test
```

## Testing 

```
make test 
```
or 

```
forge test
```

All the commands from [forge](https://github.com/gakonst/foundry/tree/master/forge) work with this repo, like `forge build`, `ethsign`, and `forge test`. 

# Deploying

To deploy, you first need to setup your `ethsign` and your `.env` file. 

## Setup your Account/ethsign

To get your private keys into dapptools, you can either use a keystore or `ethsign`. `ethsign` comes with the install of `dapptools`. For `ethsign`, run the following:
```bash
ethsign import 
```
And you'll be prompted for your private key, and a password. You can get a private key from a wallet like [Metamask](https://metamask.io/). Once successful, add the address of the private key to your `.env` file under an `ETH_FROM` variable. See the `.env.example` file for an example. 

See the [`Makefile`](./Makefile#25) for more context on how this works under the hood

## Setup your .env file

You can see in the `.env.example` an example of what your `.env` should look like (to deploy to a live network).
1. `ALCHEMY_API_KEY`: You can find this from getting an [Alchemy](https://www.alchemy.com/) account. 
2. `ETH_FROM`: The address of your wallet you want to send transactions from. You must have the private key of the address you want to use loaded into your `ethsign`, see above for this. 
3. (Optional)`ETHERSCAN_API_KEY`: For verifying contracts on etherscan. 
4. (Optional)`ETH_RPC_URL`: For having a default deployment network when using `make deploy`. This 

## Testnet & Mainnet Deployment

Set your `ETH_RPC_URL` or `ALCHEMY_API_KEY` in your `.env` file, then run one of the following:

Counters (Keeper Compatible Contract):
```bash
make deploy CONTRACT=Counter
```

Price Feed:
```bash
make deploy CONTRACT=PriceFeedConsumer
```

Chainlink VRF Consumer:
```bash
make deploy CONTRACT=VRFConsumer
```

You can change their deployment parameters in their respective `deploy` file in the `scripts` folder. All the constructor arguments are created in the `./src/helper-config.sh` folder. This is where you can assign different constructor arguments across networks. 


### Local Testnet

```
# on one terminal
dapp testnet
```

Change your `ETH_RPC_URL` to `http://127.0.0.1:8545`

Then run your deploy script. 

### Verifying on Etherscan

After deploying your contract you can verify it on Etherscan using:

```
ETHERSCAN_API_KEY=<api-key> dapp verify-contract <contract_directory>/<contract>:<contract_name> <contract_address>
```

For example:

```
ETHERSCAN_API_KEY=123456765 dapp verify-contract ./src/Counter.sol:Counter 0x23456534212536435424
```


Check out the [dapp documentation](https://github.com/dapphub/dapptools/tree/master/src/dapp#dapp-verify-contract) to see how
verifying contracts work with DappTools.


# Resources

* [DappTools](https://dapp.tools)
    * [Hevm Docs](https://github.com/dapphub/dapptools/blob/master/src/hevm/README.md)
    * [Dapp Docs](https://github.com/dapphub/dapptools/tree/master/src/dapp/README.md)
    * [Seth Docs](https://github.com/dapphub/dapptools/tree/master/src/seth/README.md)
* [DappTools Overview](https://www.youtube.com/watch?v=lPinWgaNceM)
* [Chainlink](https://docs.chain.link)
* [Awesome-DappTools](https://github.com/rajivpo/awesome-dapptools)


# TODO 
[x] Enable network & contract choice from the command line
    ie: make deploy-rinkeby contract=counter 

[ ] Add mockOracle for any API calls 

[ ] Add scripts that interact with deployed contracts 

[x] Fix Chainlink VRF deploy script 

[x] Add config for parametatizing variables across networks and contracts 
