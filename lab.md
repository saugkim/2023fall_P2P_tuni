## step by step

Environment 1: Ubuntu 22.04 (Oracle VM VirtualBox)  

```
sudo apt update
sudo apt upgrade
sudo apt install python3-pip

git clone https://github.com/adilmoujahid/blockchain-python-tutorial
mv blockchain-python-tutorial bc

pip install ed25519 Crypto pycryptodome sortedcontainers flask flask-cors

sudo add-apt-repository ppa:wireshark-dev/stable
sudo apt-get update
sudo apt-get install wireshark

sudo wireshark
sudo dpkg-reconfigure wireshark-common
sudo adduser $USER wireshark
```

**Node 1**
```
T1>> cd blockchain_client
T1>> python3 blockchain_client.py -p 8080

GUI1 (http://127.0.0.1:8080/, client): Wallet Generator -> Generate wallet
public key: 30819f300d06092a864886f70d010101050003818d0030818902818100b24401de29a282a5bc164931d1f108de29b5a804f3b175a30ab80c1aac490628da236d2bb56396771ad074619dc6bd24493c31dac9631d31533aa29a5cca9ced9aa83aa8a5e06185562b2a4b1136d16da052cdf980e68ea378aa8ec4889fe165b00e81e0d26c1f6265f9b3dd02617bd9a61da66aafc4667fa48056fb1588922d0203010001

private key:
3082025c02010002818100b24401de29a282a5bc164931d1f108de29b5a804f3b175a30ab80c1aac490628da236d2bb56396771ad074619dc6bd24493c31dac9631d31533aa29a5cca9ced9aa83aa8a5e06185562b2a4b1136d16da052cdf980e68ea378aa8ec4889fe165b00e81e0d26c1f6265f9b3dd02617bd9a61da66aafc4667fa48056fb1588922d02030100010281801c74c1ad928cd7f917d0a0e77c8152ee8fcee91ebd3dd72eeb0f9d1306ec7338c33583804628bb049139b4523ecad237801f45400d04aeccc861e441eacd07069bb71037b2cabc7147acc1b0420d997dd9f3572d4679fb518a6ee3949d5314ff4688238fba7ec7212c004bc51493aed39593cf0655e783c6b78195498d7d972b024100b7389934664ec3ca7e4df5b82d45e14efae50cf4039eeeef9b7b1946bb786742b45e542a34dca99824ed75c72e2349124a6b9340f8202f79886fcff7b4d25e5b024100f913800eb4fe32f39fe2f27423175b182ff6fb80e74aeeb18237a4e0f89bfc81f72384d1e93f7fc67b7f2fd8ab19ef67888a6e0b2499cf7b9621131ac0b1c8170240033aa1209648ff145b837e381fbc228b64ca929ede4d77c28b47f11b1904b7352abe9ad71f955ffbc972d1e78fbd99751410af48aed6ca5f66f329842110b00f02402370a7deefd7df8e14a8e910a751926f9d9b89ebac7d57fb3fe904f7d1c7f824d1f266daab5292aebe31b9b01da062151c337e36edad48fd6fbe2306c276495f024100b46e3661f0b97b854459e8cb6fba5ade05f7467b92d1fa4a713ab0a0ffcb06c1b98fee3e79e5d2af0aa2f6193900cb7ee8b8f44b0a46d20d90ca21a28e39d368

GUI1 (http://127.0.0.1:8080/view/transactions):
  View Transactions -> Enter a blockchain Node URL http://127.0.0.1:5000

T2>> cd blockchain 
T2>> python3 blockchain.py -p 5000

GUI2 (http://127.0.0.1:5000/)
  Mine -> Mine -> Mine -> Mine -> Mine (5 times mined by Node 1)   
GUI2 (http://127.0.0.1:5000/configure)
  Add blockchain nodes -> Node URLs  http://127.0.0.1:5001  -> Add Node

do Valid transaction
GUI1 (http://127.0.0.1:8080/make/transaction):
  Make Transactions ->
  sender   Node 1
  receiver Node 2
  amount   2
  result   success

do invalid transaction
GUI1 (http://127.0.0.1:8080/make/transaction):
  Make Transactions ->
  sender   Node 1
  receiver Node 2
  amount   6
  result   ?
```

**Node 2**
```
T3>> cd blockchain_client
T3>> python3 blockchain_client.py -p 8081

GUI3 (http://127.0.0.1:8081/, client) : Generate wallet
public key:
30819f300d06092a864886f70d010101050003818d0030818902818100bb3ccd33e681409e8d7a3a7d35635af3e9e4358c084f391c71b1b9f473d955301ecaf5a2057b9f3f49301513e755a909bbe5a1baf7eaafe9d84963fb934e865195ba1e033a5b06a0f9b4622793934d6cfad3ecd284618c8fc806d1ba2af0c63834a1e12b97bc9f117fb162b2032e1163fbbce513fc094276242bd1fd515d53170203010001

private key:
3082025b02010002818100bb3ccd33e681409e8d7a3a7d35635af3e9e4358c084f391c71b1b9f473d955301ecaf5a2057b9f3f49301513e755a909bbe5a1baf7eaafe9d84963fb934e865195ba1e033a5b06a0f9b4622793934d6cfad3ecd284618c8fc806d1ba2af0c63834a1e12b97bc9f117fb162b2032e1163fbbce513fc094276242bd1fd515d5317020301000102818044b62eee0d78c0708f25dc62079e230a20fad525c304e3c60af9386f3bb6759b37a9aed3db243f5017b933fafe69c2a36657826f1d3cfc7a9a1b70bc29966716d77a19f05b7cf57c8134b9fb6e51d74c3a10a71d64363b51d4943ca05ce8d1abe1eba9a8c5c292cb02ce1e2cc7f106af82e798b151bf23c34f5028e6c2340e69024100cbb0baad39974a0497316fd1ac9dd54cdb57483f8091e2b0b0c8b22c30860630bbbfbc7b2267c0218c7500b186ae6a1331da9bc32e5e06328d6a13382dcdbd0f024100eb52689af51442cc59e5d8899922be4ec89ab4a8449cb841ab1f6f0354b47f81bdf005c8cabf83e55e6291c0cfa1e7cdb15d1c0d4168e7d1788b1b1acacf9979024055c807d60bfafae1140b6ddc0fa628be45616cbbd1999eae6ac51ac4216b50101601998f01de4fbbd13b351f8e68c5a36fcb70edb20946f2e33b58fcbfcd75610240256598481ff09359046459902c6cf00f7723d6d7f2e77104c69c1d394b49d0059f58b8a29b4dea391651d5d5ed694e7c4ad68031bf165bd8d72e4c256adba90902405146451ab16d425a81f78cbe25820226ed57f0756289b4233115ab8a939b6ffb0db516d6b488ec87a2471ca30b8162aab88b150de2f8a9d157fd3d45ad929c0e

GUI3 (http://127.0.0.1:8081/):
  View Transactions -> Enter a blockchain Node URL http://127.0.0.1:5001

T4>> cd blockchain 
T4>> python3 blockchain.py -p 5001 

GUI4 (http://127.0.0.1:5001/)
  Transactions on the Blockchain -> refresh
  Mine -> Mine -> Mine -> Mine -> Mine (mined 5 times also)
GUI4 (http://127.0.0.1:5001/configure)
  Add blockchain nodes -> Node URLs  http://127.0.0.1:5000  -> Add Node

```


## Preparation

In order to complete this lab, you need Wireshark, Python (at least 3.6) and some additional
Python modules installed. Missing modules can be installed using pip from the command line:
```
>> pip install ed25519 Crypto pycryptodome sortedcontainers flask flask-cors .
```

Open a terminal, navigate to the folder where the blockchain_client.py script is located and launch it
with the command,  
```
>> python3 blockchain_client.py -p 8080 
```

  - The web GUI of the client is now accessible on port 8080. 
  - Open a browser and connect to localhost:8080. 
  - Create a wallet, and store the public and private keys in a text file.


Open a second terminal and navigate the the folder where blockchain.py is located.  
Start up the miner:
```
>> python3 blockchain.py -p 5000  
```
Open up the web GUI of the miner, which is now accessible on localhost:5000.

For the purposes of this exercise, the combination of this client and miner you just set up will be called
the first node. 

Next, you should set up the second node: either repeat the procedure with a second PC in your local
network, or open up another two terminals and repeat the commands with different port numbers, e.g.,
8081 and 5001.


## Joining the blockchain

In this section, your task is to join the existing blockchain and examine the past transactions of the
blockchain.  

Launch Wireshark and start capturing on the loopback interface. If you are using two PCs, also capture
traffic on the interface used for the local network at the same time. 

In the Configure tab of the miner web GUI, add the IP address and port of the other node, for example: 10.0.0.2:5000 or localhost:5001. Remember to repeat this for the other node.


**Answers:**    
--> joining existing blockchain? NO   
Start with node 1 creating genesis block, and node 2 join to the blockchain, which is created by node 1.    

--> done 


## Mining

As your wallet does not contain any currency at the moment, your task is to "mine" some currency. Go
back to the Mining tab in the miner web GUI (top right corner) and click the mine button. Observe the
terminal outputs, Wireshark output and the source code to find out what happens behind the scenes and
then answer the following questions.

```
1. What mining actually is, i.e. what happens when a block is being mined?

--> mining is procedure of finding proof (nonce) == performing proof-of-work and
                           adding mined new block to the existing blockchain when proof was found.


2. What is the function of nonce?

--> nonce is random number to produce a unique hash value from the combination(string concatenation) of current transactions + previous-block-hash + nonce, in a way that the hash value should meet required condition.  
In this remote exercise, the hash value should start with certain number of zeros('00...') and number of leading zero means mining difficuty.

  
3. When a block is considered to be valid and mined?

--> when transactions are verified ...


4. What do the other nodes do when they receive a new mined block from you?

--> the other node(node-2) sees the updated blockchain, can see the newly mined block from node-1

```

## Transactions

In this section, your task is to perform various transactions and observe in Wireshark and the source code
what happens behind the scenes. 

Go to the Make transaction tab in the client web GUI. Fill in the requested information. Address means public key in this context. 

Try to make an invalid transaction and a valid transaction, which you then mine to the blockchain. 
It is enough to do this on one node.

```
1. How does the blockchain network know that it was really this person that sent out the
transaction?

--> using public key and private key related to the public key,



2. How does the blockchain network know whether you have enough currency to perform
the transaction?

--> blockchain holds all information, and blockchain is availabe to public, the balance is simply the result of looking at all the transactions for an address and determining which payment assignments made to that address remain unspent.


3. Can you somehow find out how much currency anyone else has?

--> I as a miner, i should know at least anyone who wants to make transactions (in the queue), has enough currency to make those transactions,

--> I as a just client, and i somehow get someone's public key, then enough to bother to spend some time to look at all the trasactions then I can...

```

Go back to the Mining tab and refresh the transactions in the blockchain by clicking the small blue
button next to the Transactions on the Blockchain header.

In Wireshark, find and examine the blockchain data, and answer the following questions.

```
4. What kind of information is stored in the blockchain? (Hint: http://localhost:5000/chain)
--> block number
--> nonce
--> previous_has
--> timestamp
--> transactions including reward (address of recipient and sender and amount) 


5. How many blocks are now in the blockchain?
--> currently 3


6. What transactions were made in the latest block which included transactions?
--> One transaction that client 1 sending 1000 to client 2


7. Could you edit a past transaction and then pass off the chain as a newer valid one? Why
or why not?

--> No, each block has previous block's hash value, it does not pass chain validation process
```

##  Double spending

In this section, you will perform double spending. On one of the nodes, make two transactions which
both use all of your available currency. Submit one of them to the other node (Blockchain Node URL
in the confirmation dialog) and the other one to the node itself.

Check that the transactions are going to be added to the next block in the miner web GUI on each node
by clicking the small blue button next to the Transactions to be added to the next block header. Mine the
blocks on both of your nodes at the same time (mine -> switch to other node -> mine is okay). Examine
the resulting blockchains on your nodes.

```
1. What happened? What is this situation generally called?

--> conflict in the blockchain, is a situation where two or more nodes try to add different blocks to the same branch of the blockchain, creating a temporary inconsistency

2. How will this situation be resolved? What will happen to the other chain at that point?

--> When one of node has longer chain than other node, blockchain holded by the other node(which has shorter blockchain) is updated with longer blockchain, longer chain wins
--> nothing happens until one of node mines and update its blockchain


3. What should be done to avoid negative consequences from situations like this?

--> A conflict can be resolved by the consensus mechanism of the network-blockchain, which determines which block is valid and which is discarded
--> the transactions in the discarded block should return to the transaction pool again to be mined 

```
