# test-mantle-2

> This chain is a testnet

## Hardware Requirements

* **Minimal**
  * 4 GB RAM
  * 200 GB SSD
  * x2 CPU
* **Recommended**
  * 8+ GB RAM
  * 500+ GB SSD
  * x4+ CPU

> NOTE: low endurance(tbw) ssd are not recommended for long term node operation

## Operating System

* Linux/Windows/MacOS(x86)
* **Recommended**
  * Linux(x86_64)

## Installation Steps

>Prerequisite: go version ~1.18 required. [ref](https://golang.org/doc/install)
>Prerequisite: git. [ref](https://github.com/git/git)
>Optional requirement: GNU make. [ref](https://www.gnu.org/software/make/manual/html_node/index.html)

* Clone git repository, install node and verify version

```shell
git clone -b v0.4.0 https://github.com/assetmantle/node.git
make install
mantleNode version
```

> The version shoule be `v0.4.0`

### Generate keys

`mantleNode keys add <KEY_NAME>`

or

`mantleNode keys add <KEY_NAME> --recover` to regenerate keys with your [BIP39](https://github.com/bitcoin/bips/tree/master/bip-0039) mnemonic

## Validator setup

### Post genesis

* [Install](#installation-steps) assetMantle application
* Initialize node

```shell
mantleNode init <NODE_NAME> --chain-id test-mantle-2
```

* Replace the contents of your `${HOME}/.mantleNode/Node/config/genesis.json` with that of `test-mantle-2/genesis.json` from the `master` branch of [repository](https://github.com/persistenceOne/genesisTransactions).
* Verify checksum `sha265sum genesis.json` matches `bc22ab3891b5dedc6fe2e0cdc8231f72daea7fbdb87d472271c5c79c4e5eea42`
* Inside file `${HOME}/.mantleNode/Node/config/config.toml`,
  * set `seeds` to

  ```log
  ad545a30dd5c1d85900eda315f5e57c11b3d654c@88.99.31.9:46656,3829b465ff4447472d0db64420ccab936097311a@65.108.65.229:46656,a58bae5c70c7d56fcb3346d831c124f0eb2dd75e@65.109.39.118:46656,069e8fd2dafd6f6fe787f26f77c82fe74d5e8c04@65.108.1.21:46656
  ```

* Set `minimum-gas-prices` in `${HOME}/.mantleNode/Node/config/app.toml` with the minimum price you want (example `0.005umntl`) for the security of the network.

* Start node

```shell
mantleNode start
```

* Acquire $MNTL tokens to self delegate to your validator node.
* Send a create-validator transaction

```shell
mantleNode tx staking create-validator \
--from <KEY_NAME> \
--amount XXXXXXXXumntl \
--pubkey "$(mantleNode tendermint show-validator)" \
--chain-id test-mantle-2 \
--moniker="<VALIDATOR_NAME>" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.1 \
--min-self-delegation="1" \
--details="XXXXXXXX" \
--security-contact="XXXXXXXX" \
--website="XXXXXXXX"
```

## Facuet

[https://facuet.testnet.assetmantle.one/faucet/<ADDRESS\>](https://facuet.testnet.assetmantle.one/faucet/ADDRESS)

## Explorer

[here](https://explorer.testnet.assetmantle.one)

## Wallet

[here](https://staging.wallet.assetmantle.one)
