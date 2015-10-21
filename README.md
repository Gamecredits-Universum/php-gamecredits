node-gamecredits
===============

![Gamecredits](http://i.imgur.com/fJrOs5U.png)![Gamecredits](http://i.imgur.com/Nfb8DQx.png)

A simple class for making calls to Gamecredits's API using PHP.

Getting Started
---------------
1. Include gamecredits.php into your PHP script:

	`require_once('gamecredits.php');`
2. Initialize Gamecredits connection/object:

	`$gamecredits = new Gamecredits('username','password');`

	Optionally, you can specify a host, port. Default is HTTP on localhost port 40001.

	`$gamecredits = new Gamecredits('username','password','localhost','40001');`

	If you wish to make an SSL connection you can set an optional CA certificate or leave blank
	`$Gamecredits->setSSL('/full/path/to/mycertificate.cert');`

3. Make calls to Gamecreditsd as methods for your object. Examples:

	`$gamecredits->getinfo();`
	`$gamecredits->getrawtransaction('0e3e2357e806b6cdb1f70b54c3a3a17b6714ee1f0e68bebb44a74b1efd512098',1);`
	`$gamecredits->getblock('000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f');`

Additional Info
---------------
* When a call fails for any reason, it will return false and put the error message in $gamecredits->error

* The HTTP status code can be found in $gamecredits->status and will either be a valid HTTP status code or will be 0 if cURL was unable to connect.

* The full response (not usually needed) is stored in $gamecredits->response while the raw JSON is stored in $gamecredits->raw_response


API CALL LIST :
---------------

## Commands

<table>
<tr>
<th> Command </th>
<th> Parameters </th>
<th> Description </th>
<th> Requires unlocked wallet?
</th></tr>
<tr>
<td> addmultisigaddress </td>
<td> [nrequired] ["key","key"] [account] </td>
<td> <b>Currently only available on testnet</b> Add a nrequired-to-sign multisignature address to the wallet. Each key is a GameCredits address or hex-encoded public key. If [account] is specified, assign address to [account]. </td>
<td> N
</td></tr>
<tr>
<td> backupwallet </td>
<td> [destination] </td>
<td> Safely copies wallet.dat to destination, which can be a directory or a path with filename. </td>
<td> N
</td></tr>
<tr>
<td> dumpprivkey </td>
<td> [GameCreditsaddress] </td>
<td> Reveals the private key corresponding to <GameCreditsaddress< </td>
<td> Y
</td></tr>
<tr>
<td> encryptwallet </td>
<td> [passphrase] </td>
<td> Encrypts the wallet with <passphrase<. </td>
<td> N
</td></tr>
<tr>
<td> getaccount </td>
<td> [GameCreditsaddress] </td>
<td> Returns the account associated with the given address. </td>
<td> N
</td></tr>
<tr>
<td> getaccountaddress </td>
<td> [account] </td>
<td> Returns the current GameCredits address for receiving payments to this account. </td>
<td> N
</td></tr>
<tr>
<td> getaddressesbyaccount </td>
<td> [account] </td>
<td> Returns the list of addresses for the given account. </td>
<td> N
</td></tr>
<tr>
<td> getbalance </td>
<td> [account] [minconf=1] </td>
<td> If [account] is not specified, returns the server's total available balance.<br />If [account] is specified, returns the balance in the account. </td>
<td> N
</td></tr>
<tr>
<td> getblock </td>
<td> [hash] </td>
<td> Returns information about the given block hash. </td>
<td> N
</td></tr>
<tr>
<td> getblockcount </td>
<td> </td>
<td> Returns the number of blocks in the longest block chain. </td>
<td> N
</td></tr>
<tr>
<td> getblockhash </td>
<td> [index] </td>
<td> Returns hash of block in best-block-chain at <index< </td>
<td> N
</td></tr>
<tr>
<td> getblocknumber </td>
<td> </td>
<td> <b>Deprecated</b>. Use getblockcount. </td>
<td> N
</td></tr>
<tr>
<td> getconnectioncount </td>
<td> </td>
<td> Returns the number of connections to other nodes. </td>
<td> N
</td></tr>
<tr>
<td> getdifficulty </td>
<td> </td>
<td> Returns the proof-of-work difficulty as a multiple of the minimum difficulty. </td>
<td> N
</td></tr>
<tr>
<td> getgenerate </td>
<td> </td>
<td> Returns true or false whether GameCreditsd is currently generating hashes </td>
<td> N
</td></tr>
<tr>
<td> gethashespersec </td>
<td> </td>
<td> Returns a recent hashes per second performance measurement while generating. </td>
<td> N
</td></tr>
<tr>
<td> getinfo </td>
<td> </td>
<td> Returns an object containing various state info. </td>
<td> N
</td></tr>
<tr>
<td> getmemorypool </td>
<td> [data] </td>
<td> If [data] is not specified, returns data needed to construct a block to work on:
<ul><li> "version": block version
</li><li> "previousblockhash": hash of current highest block
</li><li> "transactions": contents of non-coinbase transactions that should be included in the next block
</li><li> "coinbasevalue": maximum allowable input to coinbase transaction, including the generation award and transaction fees
</li><li> "time": timestamp appropriate for next block
</li><li> "bits": compressed target of next block
</li></ul>
<p>If [data] is specified, tries to solve the block and returns true if it was successful.
</p>
</td>
<td> N
</td></tr>
<tr>
<td> getmininginfo </td>
<td> </td>
<td> Returns an object containing mining-related information:
<ul><li> blocks
</li><li> currentblocksize
</li><li> currentblocktx
</li><li> difficulty
</li><li> errors
</li><li> generate
</li><li> genproclimit
</li><li> hashespersec
</li><li> pooledtx
</li><li> testnet
</li></ul>
</td>
<td> N
</td></tr>
<tr>
<td> getnewaddress </td>
<td> [account] </td>
<td> Returns a new GameCredits address for receiving payments.  If [account] is specified (recommended), it is added to the address book so payments received with the address will be credited to [account]. </td>
<td> N
</td></tr>
<tr>
<td> getreceivedbyaccount </td>
<td> [account] [minconf=1] </td>
<td> Returns the total amount received by addresses with [account] in transactions with at least [minconf] confirmations. If [account] not provided return will include all transactions to all accounts. (version 0.3.24-beta) </td>
<td> N
</td></tr>
<tr>
<td> getreceivedbyaddress </td>
<td> [GameCreditsaddress] [minconf=1] </td>
<td> Returns the total amount received by <GameCreditsaddress< in transactions with at least [minconf] confirmations. While some might consider this obvious, value reported by this only considers *receiving* transactions. It does not check payments that have been made *from* this address. In other words, this is not "getaddressbalance". Works only for addresses in the local wallet, external addresses will always show 0. </td>
<td> N
</td></tr>
<tr>
<td> gettransaction </td>
<td> [txid] </td>
<td> Returns an object about the given transaction containing:
<ul><li> "amount": total amount of the transaction
</li><li> "confirmations":  number of confirmations of the transaction
</li><li> "txid": the transaction ID
</li><li> "time": time the transaction occurred
</li><li> "details" - An array of objects containing:
<ul><li> "account"
</li><li> "address"
</li><li> "category"
</li><li> "amount"
</li></ul>
</li></ul>
</td>
<td> N
</td></tr>
<tr>
<td> getwork </td>
<td> [data] </td>
<td> If [data] is not specified, returns formatted hash data to work on:
<ul><li> "midstate": precomputed hash state after hashing the first half of the data
</li><li> "data": block data
</li><li> "hash1": formatted hash buffer for second hash
</li><li> "target": little endian hash target
</li></ul>
<p>If [data] is specified, tries to solve the block and returns true if it was successful. 
</p>
</td>
<td> N
</td></tr>
<tr>
<td> help </td>
<td> [command] </td>
<td> List commands, or get help for a command. </td>
<td> N
</td></tr>
<tr>
<td> importprivkey </td>
<td> [GameCreditsprivkey] [label] </td>
<td> Adds a private key (as returned by dumpprivkey) to your wallet. </td>
<td> Y
</td></tr>
<tr>
<td> keypoolrefill </td>
<td> </td>
<td> Fills the keypool, requires wallet passphrase to be set. </td>
<td> Y
</td></tr>
<tr>
<td> listaccounts </td>
<td> [minconf=1] </td>
<td> Returns Object that has account names as keys, account balances as values. </td>
<td> N
</td></tr>
<tr>
<td> listreceivedbyaccount </td>
<td> [minconf=1] [includeempty=false] </td>
<td> Returns an array of objects containing:
<ul><li> "account": the account of the receiving addresses
</li><li> "amount": total amount received by addresses with this account
</li><li> "confirmations": number of confirmations of the most recent transaction included
</li></ul>
</td>
<td> N
</td></tr>
<tr>
<td> listreceivedbyaddress </td>
<td> [minconf=1] [includeempty=false] </td>
<td> Returns an array of objects containing:
<ul><li> "address": receiving address
</li><li> "account": the account of the receiving address
</li><li> "amount": total amount received by the address
</li><li> "confirmations": number of confirmations of the most recent transaction included
</li></ul>
<p>To get a list of accounts on the system, execute GameCreditsd listreceivedbyaddress 0 true
</p>
</td>
<td> N
</td></tr>
<tr>
<td> listsinceblock</td>
<td> [blockhash] [target-confirmations] </td>
<td> Get all transactions in blocks since block [blockhash], or all transactions if omitted. </td>
<td> N
</td></tr>
<tr>
<td> listtransactions </td>
<td> [account] [count=10] [from=0] </td>
<td> Returns up to [count] most recent transactions skipping the first [from] transactions for account [account]. If [account] not provided will return recent transaction from all accounts.
</td>
<td> N
</td></tr>
<tr>
<td> move </td>
<td> [fromaccount] [toaccount] [amount] [minconf=1] [comment] </td>
<td> Move from one account in your wallet to another </td>
<td> N
</td></tr>
<tr>
<td> sendfrom </td>
<td> [fromaccount] [toGameCreditsaddress] [amount] [minconf=1] [comment] [comment-to] </td>
<td> <amount< is a real and is rounded to 8 decimal places. Will send the given amount to the given address, ensuring the account has a valid balance using [minconf] confirmations. Returns the transaction ID if successful (not in JSON object). </td>
<td> Y
</td></tr>
<tr>
<td> sendmany </td>
<td> [fromaccount] [address:amount,...] [minconf=1] [comment] </td>
<td> amounts are double-precision floating point numbers </td>
<td> Y
</td></tr>
<tr>
<td> sendtoaddress </td>
<td> [GameCreditsaddress] [amount] [comment] [comment-to] </td>
<td> <amount< is a real and is rounded to 8 decimal places. Returns the transaction ID <txid< if successful. </td>
<td> Y
</td></tr>
<tr>
<td> setaccount </td>
<td> [GameCreditsaddress] [account] </td>
<td> Sets the account associated with the given address. Assigning address that is already assigned to the same account will create a new address associated with that account. </td>
<td> N
</td></tr>
<tr>
<td> setgenerate </td>
<td> [generate] [genproclimit] </td>
<td> [generate] is true or false to turn generation on or off.

Generation is limited to [genproclimit] processors, -1 is unlimited. </td>
<td> N
</td></tr>
<tr>
<td> signmessage </td>
<td> [GameCreditsaddress] [message] </td>
<td> Sign a message with the private key of an address. </td>
<td> Y
</td></tr>
<tr>
<td> settxfee </td>
<td> [amount] </td>
<td> [amount] is a real and is rounded to the nearest 0.00000001 </td>
<td> N
</td></tr>
<tr>
<td> stop </td>
<td> </td>
<td> Stop GameCredits server. </td>
<td> N
</td></tr>
<tr>
<td> validateaddress </td>
<td> [GameCreditsaddress] </td>
<td> Return information about [GameCreditsaddress]. </td>
<td> N
</td></tr>
<tr>
<td> verifymessage </td>
<td> [GameCreditsaddress] [signature] [message] </td>
<td> Verify a signed message. </td>
<td> N
</td></tr>
<tr>
<td> walletlock </td>
<td>  </td>
<td> Removes the wallet encryption key from memory, locking the wallet. After calling this method,  you will need to call walletpassphrase again before being able to call any methods which require the wallet to be unlocked. </td>
<td> N
</td></tr>
<tr>
<td> walletpassphrase </td>
<td> [passphrase] [timeout] </td>
<td> Stores the wallet decryption key in memory for <timeout< seconds. </td>
<td> N
</td></tr>
<tr>
<td> walletpassphrasechange </td>
<td> [oldpassphrase] [newpassphrase] </td>
<td> Changes the wallet passphrase from <oldpassphrase< to <newpassphrase<. </td>
<td> N
</td></tr></table>
