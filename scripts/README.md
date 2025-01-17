## Compiling
Run `./compile.sh` to compile Root.sol, XRT.sol, Lighthouse.sol, SimpleWallet.sol and MultiValidatorExample.sol.


## Configure
All the interaction scripts read config parameters (e.g. which network to use) from config.js file. See it for more info.
### Giver config
Deploying new contracts requires transfering some balance first. It is done requesting a giver to transfer this value -- see giverConfig.js, which exports one function get_tokens_from_giver. The present giver config contains default TON OS SE giver params -- when deploying in other network, you may want to deploy your own giver first or to use another logic in get_tokens_from_giver.


## Installations bedore deploy
For deploying in local node you must have docker, nodejs and npm installed.
Install packages by
```console
npm i
```
And everdev globally
```console
npm i -g everdev
```
After that start local node by
```console
everdev se start
```
Note: make sure that docker engine started.


## (Re-)Deploying
After compiling contracts, run `node newKeys.js` for for generating new keys (they also serve as nonce for contract addresses, so the new project version won't conflict with older versions which has been already deployed).

Then run `node deployContracts.js`.

## Simple wallets
For testing purposes you can create a few simple wallets with `node createSimpleWallets.js`. They can be used for sending designated internal messages to other contracts. Also if the network type specified in config is 'test', deployContracts.js mints some XRTs to the simple wallets.

# Interaction scripts
tests folder contains some rather manual tests (nevertheless they have some asserts), you can use them to interact with the contracts by created simple wallets.

Note that presently scripts parametrs are defined in their code, not read from command line arguments.

## Creating lighthouse
First of all, create a lighthouse with `node createLighthouse.js` script. You can set lighthouse parametrs and give another name, by which lighthouse is identified.
Also this script lists all the existing lighthouses and checks that expected addresses are equal to actual ones.

## Working with balance
You can `node refillBalance.js` and `node withdrawBalance.js` transfering some XRTs owned by a simple wallet to lighthouse contract (by default one with name 'Lighthouse' is used). You can choice the simple wallet to use changing the nonce field in its constructor params.

This and other script listen to events emited by the contracts and display them.

## Registering a provider
After balance refilled, you can register one or several providers with `node registerProvider.js` (also using simple wallets).

## Using a provider
Registered a provider, you can consume one quota with `node no_liabilities.js`, refill or withdraw stake, create and then finalize liability with the corresponding scripts. Also you may wait for the timeout and check charging fines mechanism with `node checkTimeout.js`, or test on-chain validator finalization (you have to edit createLiability script for this).


# Demo
You can use [demo](https://www.youtube.com/watch?v=ZvAqjMXXaHY) as a reference.
