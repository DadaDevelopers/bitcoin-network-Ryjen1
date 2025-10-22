Bitcoin Network – Regtest Exploration

 Objective  
Exploring and interacting with a Bitcoin network in *regtest* mode using Bitcoin Core.  
*Regtest* (short for “Regression Test”) allows developers to create a private Bitcoin blockchain for testing — without needing the mainnet or testnet.

---

 Lab 1 — Setting Up a Regtest Node

 Steps Taken

1. *Started Bitcoin Core in regtest mode*:
  
   bitcoind -regtest -daemon
   
   *Output*:  
   Bitcoin Core starting

2. *Verified blockchain info*:
  
   bitcoin-cli -regtest getblockchaininfo
   
   *Example Output*:
  
   {
     "chain": "regtest",
     "blocks": 104,
     "headers": 104,
     "difficulty": 4.6565e-10,
     "initialblockdownload": true,
     "pruned": true
   }
   
3. *Created a wallet*:
  
   bitcoin-cli -regtest createwallet "testwallet"
   
   *Result*:
  
   error code: -4
   error message:
   Wallet file verification failed. Failed to create database path. Database already exists.
   
    *Wallet already existed — no duplicates allowed.*

4. *Checked wallet storage*:
   Wallets are stored in:
   `bash`
~/.bitcoin/regtest/wallets/
  

---

 Lab 2 — Setting Up a Second Node

 Steps Taken

1. *Created a new data directory*:
   
bash
   mkdir -p ~/bitcoin-node2
  

2. *Started a second node with custom ports*:
   
bash
   bitcoind -regtest -datadir=HOME/bitcoin-node2 -port=18445 -rpcport=18446 -daemon
   “

   *Output*:  
   Bitcoin Core starting

3. *Tried checking blockchain info*:
   “bash
   bitcoin-cli -datadir=HOME/bitcoin-node2 -regtest getblockchaininfo
  

   *Error*:
   
   Authorization failed: Incorrect rpcuser or rpcpassword
  

    *This is due to missing RPC credentials.*

4. *Fix*: Add the following to `$HOME/bitcoin-node2/bitcoin.conf`:
   
ini
   rpcuser=user
   rpcpassword=pass
  

---

Key Takeaways

- Regtest provides a safe and private environment for Bitcoin development.
- `bitcoind` runs the node; `bitcoin-cli` is used for interaction.
- Multiple nodes can be configured using separate data directories and ports.
- Wallet creation errors often mean the wallet already exists

