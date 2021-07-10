# Bitcoin Core V21.1 : Signet 


What is Bitcoin?
----------------

Bitcoin is an experimental digital currency that enables instant payments to
anyone, anywhere in the world. Bitcoin uses peer-to-peer technology to operate
with no central authority: managing transactions and issuing money are carried
out collectively by the network. Bitcoin Core is the name of open source
software which enables the use of this currency.

For more information read the original Bitcoin whitepaper.


Full Node Setup!
----------------
Demonstration to deploy full node on Bitcoin Signet Network (Windows)

Good sources for learning:
* Grokking Bitcoin
* https://bitcoin.org/en/full-node
* Googling
* Bitcoin wiki https://en.bitcoin.it/wiki


Bitcoin Core Realease V21.1 :
-----------------------------

Download [bitcoin-0.21.1-win64.zip](https://bitcoincore.org/bin/bitcoin-core-0.21.1/bitcoin-0.21.1-win64.zip) <br>

Download the signature of the bitcoin to verify <br>
[SHA256SUMS.asc](https://bitcoincore.org/bin/bitcoin-core-0.21.1/SHA256SUMS.asc)       

Verify Sig
--------------------------------------------------------------------------------------------
`$ certutil -hashfile C:/Users/Acer/Downloads/bitcoin-0.21.1-win64.zip SHA256` <br>
<br>
--> Above cmd will give you hash of the file, compare it with SHA256SUMS.asc <br>
<br>
`$ type SHA256SUMS.asc` <br> 

Lookup the fingerprint of Bitcoin Core's release key <br>
It should be [01EA5486DE18A882D4C2684590C8019E36C2E964](https://bitcoincore.org/en/download/)<br>

### Check fingerprint is authentic with multiple sources :
* Grokking Bitcoin
* Ask on forums
* Ask someone you trust
* Check bitcoincore.org
`$ gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 01EA5486DE18A882D4C2684590C8019E36C2E964`

When you're sure that you have the correct key, verify the signature in the signature file <br>
`$ gpg --verify SHA256SUMS.asc` <br>
Look for "Good signature from..." and verify that the fingerprint matches what you expect <br>


Startup using CLI  :
---------------
* Unzip Bitcoin Core -> Go to the bin dir<br>
`$ cd bitcoin-0.21.1/bin`

* Start Bitcoin Core on a test network, called signet <br>
`$ \bitcoind -signet`

* Have a look at data from the blockchain<br>
`$ \bitcoin-cli -signet getblockchaininfo` <br><br>
Look for "initialblockdownload". True means it's sill syncing

* Stop Bitcoin Core<br>
`$ \bitcoin-cli -signet stop`<br><br>

* Make it always run signet<br>
`$ echo "chain=signet" >> `~[Path to Bitcoin config](https://en.bitcoin.it/wiki/Running_Bitcoin)<br><br>

* Enable transaction index<br>
`$ echo "txindex=1" >> `~[Path to Bitcoin config](https://en.bitcoin.it/wiki/Running_Bitcoin)<br><br>

* Now you can start bitcoind<br> 
`$ .\bitcoind `<br><br>

* You can check again whether sync is finished<br>
`$ .\bitcoin-cli getblockchaininfo`<br><br>

Create, encrypt and backup wallet :
----------------------------------

* Use the help. It's very often needed<br>
`$ .\bitcoin-cli help`<br><br>

* Get help on a specific command<br>
`$ \bitcoin-cli help createwallet`<br><br>

* Create a wallet<br>
`$ \bitcoin-cli - createwallet grok false false <password> false false true`<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ \bitcoin-cli getwalletinfo`<br><br>

* Bitcoin core uses a simple copy of the wallet file for backups. For real Bitcoin you would store this and your wallet passphrase in a safe place.<br>
`$ .\bitcoin-cli backupwallet ~\walletbackup.dat`<br><br>

Receive and send some bitcoin :
-----------------------------
* Get a fresh address<br>
`$ .\bitcoin-cli getnewaddress`<br><br>

* Get the confirmed balance<br>
`$ .\bitcoin-cli getbalance`<br><br>

* Get unconfirmed and confimed balances<br>
`$ .\bitcoin-cli getbalances`<br><br>
 See if you can figure out the three types of balances in the output. Use the help command.

* Get all transactions concerning your wallet<br>
`$ .\bitcoin-cli listtransactions`<br><br>

* To use your private keys, you must decrypt them. The following will decrypt and clean memory after 300 seconds.<br>
`$ .\bitcoin-cli <walletpassphrase> 300` <br><br>

* To get some Test coin, you can use [Signet Faucet](https://signet.bc-2.jp/)<br>


* Send some coins to a address <br>
`$ .\bitcoin-cli -named sendtoaddress address=<address> amount=0.001`<br><br>

* Lock the wallet again. The 300 seconds is just a safeguard in case you forget to lock.<br>
`$ .\bitcoin-cli walletlock`<br><br>




