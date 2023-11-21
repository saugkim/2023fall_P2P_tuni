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
public key:
...
private key:
...

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
...

private key:
...

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
the idea of a chain should be apparent—each new block contains within itself, the hash of the previous Block. This is crucial because it’s what gives blockchains immutability: If an attacker corrupted an earlier Block in the chain then all subsequent blocks will contain incorrect hashes.
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
