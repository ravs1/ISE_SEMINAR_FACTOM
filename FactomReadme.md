# TU BERLIN ISE SEMINAR-FACTOM

# SYNOPSIS
This is a general study of the Factom blockchain technology which include setting up of factom node and to send the data to FACTOM's opensource blockchain. The whole credit for the information provided here goes to [Factom](https://www.factom.com/) and the list of the resources from where the information is taken are listed below titled as SOURCES. 
# 
# 
# FACTOM - BLOCKCHAIN TECHNOLOGY
[Factom](https://www.factom.com/) is a company that builds blockchain software. It secures the data either from private or public organizations by publiching the data into the Factom's opensource blockchain , thus getting the cryptographic finger print of the data.Often it is described as a publishing and auditing engine. It allows users to write data to its ledger for a small fee.  Once information has entered into the Factom Blockchain it can’t be removed. 
# 
# 
#
# FACTOM COMPONENTS
Factom Architecture consist of following main components -
* ENTRIES - Contains applicaton raw data or hash of the private data.
* CHAINS - Grouping of entries specific to the Application
* ENTRY BLOCK LAYER - Consist of hashes of all the relevant entries.There is one                       Entry Block for each updated CHAIN.
* DIRECTORY BLOCK LAYER - The Directory layer is the first level of hierarchy in the Factom system. It defines which Entry ChainIDs have been updated during the time period covered by a Directory Block. It mainly consists of a list pairing a ChainID and the Merkle root of the Entry Block containing data for that ChainID.
#
#
#
# FACTOM DATA ANCHORING 
Process of adding the merkel root into the blockchain is known as ANCHORING. 
ANCHORING done by the FACTOM in the following ways - 
* Entries are hashed and group according to the prescribed classification rule into different chains and chain IDs are assigned to them .
* These Chains are further hashed and stored into the ENTRY BLOCK.Which consist of unique ENTRY HEADER for each chain.
* Entry headers references of all the ENTRY BLOCKS are stored in the DIRECTORY BLOCK.
* And finally the DIRECTORY BLOCKS are pushed into the blockchain.

The following Diagram explains the ANCHORING PROCESS--
#### image page 15 [WHITE PAPER](https://github.com/FactomProject/FactomDocs/raw/master/Factom_Whitepaper.pdf)
![Factom Architecture](ISE_SEMINAR_FACTOM/factom_images/Factom.png?raw=true)







# FACTOM AND BITCOIN 
* Entering data into the Bitcoin blockchain is prohibitively expensive at volume. In addition, the Bitcoin blockchain cannot handle high transactional volumes. The Factom blockchain is orders of magnitude less expensive and has orders of magnitude more capacity for transaction volume. 
* Factom also has built-in layers of redundant security that other blockchain do not offer. The Factom Blockchain anchors itself into the Bitcoin blockchain, among others, to take advantage of the security of Bitcoin’s hashrate. The layering effect of security, ensures the immutability of its blocks.
* Another feature that the Factom blockchain offers, that helps those wishing to do large volumes of transaction, is it also has a theme tracking capability. What this enables is the ability to chain together data you care about and forget the rest of the data set. Unlike the Bitcoin Blockchain that requires you have all of the data to prove any of the data, Factom allows you to prove your data set without need all the data in Factom.

Details can be found here [FACTOM FAQs](https://www.factom.com/about/faqs).
#
#
#
# FACTOM EXAMPLE
This is example is supported by the newly launched [FACTOM FEDERTION TESTNET](https://www.factom.com/blog/factom-launches-federated-testnet)(It is still rolling out , there are chances of system down ).

##  INSTALLATION
It needs GoLang environment and the details to set up for setting up the environment both for Linux and Mac is [here](https://github.com/FactomProject/FactomDocs/blob/master/communityTesterDirectionsM2.md).

After installing the environment for the testnet , we need to do the below steps.

For running of the Factom , we need to run three components - 
1. factomd it is a server that download the blockchain . 
2. factom-walletd its a wallet where we can see the tansactions of factoids.
3. factom-cli its the main command line tool where all the commands are given.

STEP1- Install factomd,factom-walletd and factom.cli
commands 
```sh
$ go get -v github.com/FactomProject/factomd
$ go get -v github.com/FactomProject/factom-cli
$ go get -v github.com/FactomProject/factom-walletd
$ go get -v github.com/FactomProject/netki-go-partner-client 
go get -v github.com/FactomProject/go-bip44
```
In a terminal navigate to $GOPATH/src/github.com/FactomProject/factomd run the all.sh script
```sh
$ cd GOPATH/src/github.com/FactomProject/factomd
$ ./all.sh m2-rc1
````
at the end of the installation you should see this 
```sh
Compiling: factomd
Compiling: factom-cli
Compiling: factom-walletd
````
No come out of the GOPATH and there will be a go folder 
Type these commands to run factomd
```sh
$ cd go
$ cd bin
$ ./factomd 
````
### image factomd
we can check whether our node is running or not by pasting http://localhost:8090 in browser. It will display the GUI displaying the running node and transactions taking place. Wait for the node to get 100% sync and then start factom-walletd.
### image guinode

Now follow these steps to run factom-walletd in a new terminal 
```sh
$ cd go
$ cd bin
$ ./factom-walletd
```
### image factom-walletd

Now in the Third terminal open the factom-cli import address Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj. 
This is the address which has FACTOIDS loaded. Its only for the test purpose. 
commands 
```sh
$ cd go
$ cd bin
$ ./factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj 
````
It should import address-
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC.

To create local factoid address - 
command 
```sh
$ ./factom-cli newfctaddress
```
it will create the new factoid address starting with letter FA... 
eg FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S
this address will be different for different user.

TO find the list of the address 
command 
```sh
$ ./factom-cli listaddresses
```
it will list all the address you have 
eg. 
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC 3.1249 FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 0 

The first address is the one that you imported and it has 3.1249 Factoids for the testnet and the second address is the one that we have just created . So it does not have any factoids. 

So now we have to transfer the factoid credits from the address we imported to our new address . 
command 
```sh
$ ./factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.2340
```
this command transfers 1.234 factoids from first address which we have imported to our new factoid address. 

To check the balance and status of all the address 
command 
```sh
$ ./factom-cli listaddresses
```
it will display like this - 
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC 1.8909 FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.2340

now our new Factoid address has 1.2340 factoids. 

In order to make new entries into the blockchain ,we first create the Entry credit address 
command 
```sh 
$ ./factom-cli newecaddress
```
It will generate new entry credit address starting with initials EC .. 
eg . EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 

In order to make new entries we need some entry credits 
command
```sh
$ ./factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 1.0000
```
here we have transfered credits from our Factoid Address to the Entry Credit address. 
Now crating the chain in which we have to make the entries 
here we are entering string  "first testnet chain " into the chain . 
command 
```sh
$ echo "first testnet chain" | factom-cli addchain -e chainName EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 
```
we must get the following output
Commiting Chain Transaction ID: c1a2861d14b788c13d6c48f1e5603f5c53afc599d07d338deeb4c3d5012e24da 
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 Entryhash: 232d1e54ecdfc369cc66e35dda73ce4beb7dffd3e75af94192034e79beaf6c8f 
thus we get our ChainID and Entryhash of the string that we wanted to anchor in the blockchain .
Entering another string but to the same chain ID 
command 
```sh
$ ./ echo "second entry in the first chain" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 
```
here the chain ID and EC address are same. 

These entries are anchored into the blockchain by Factom 
in order to know the no. of enteries made 
command t the chain ID
```sh
$ factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 
```
It will display the entries. 

# ERRORS
While implimenting the above example which is provided by [FACTOM](https://www.factom.com/blog/factom-launches-federated-testnet) it was not possible to transfer the Factoid credits to the newly created Factoid Address to perform the follow up operations. 
### POSSIBLE REASON 
Since Factom is still in the process of transfering to the new testnet which is soetimes also refered to M2, so there is a system down and services are not working as expected. 
Reasonig collected from 
[REDDIT](https://www.reddit.com/r/factom/).
[FACTOM SLACK GROUP](https://factomfoundation.slack.com/).
# OTHER EXAMPLES - FACTOM TAX DOCUMENTATION
Other available examples to test FACTOM were the one provided by the official github of FACTOM , [here](https://github.com/FactomProject/FactomDocs/tree/master/examples/tax). Its the Factom Tax Documentation example where demonstration of sending document to the factom blockchain is shown but its very old documentation and not updated and failed as the PUBLIC key is expired . Attempts were made to extend the expiry of the public key using PGP for mac but it further requires a secret key and unfortunately not working . 

# DIFFERENT INSTALLATION METHODS TRIED 
In order to access testnet properly other methods were also tried where creation of SANDBOX Server was mentioned . 
SOURCES ...
[FACTOM PROJECT](https://github.com/FactomProject/FactomDocs/blob/master/developerSandboxSetup.md)
[FACTOM PROJECT TEST](https://github.com/FactomProject/Testing/blob/master/examples/python/writeToFactom.md)
[FACTOM COMMUNITY INSTALLER](https://github.com/FactomProject/FactomDocs/blob/master/communityTesterDirections.md)
But similar issues regarding PUBLIC KEY are arising. 

# SOURCES
All the information mentioned here is taken from the mentioned sources and [FACTOM](https://www.factom.com/) has all the rights. 
SOURCES - 
* [FACTOM](https://www.factom.com/) 
* [FACTOM PROJECT](https://github.com/FactomProject/FactomDocs/blob/master/developerSandboxSetup.md)
* [FACTOM DOCS ](https://github.com/FactomProject/FactomDocs/tree/master/examples/tax)
* [REDDIT FACTOM ](https://www.reddit.com/r/factom/)
* [FACTOM SLACK GROUP](https://factomfoundation.slack.com/)
* [FACTOM FAQs](https://www.factom.com/about/faqs)
* [FACTOM TESTNET](https://www.factom.com/blog/factom-launches-federated-testnet)
* [FACTOM WHITE PAPER](https://github.com/FactomProject/FactomDocs/raw/master/Factom_Whitepaper.pdf)

























