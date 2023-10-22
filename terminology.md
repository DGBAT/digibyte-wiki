---
title: Terminology
description: 
published: true
date: 2023-10-22T10:19:41.696Z
tags: 
editor: markdown
dateCreated: 2023-10-22T10:19:41.696Z
---

# Purpose

Every day we participate in a society where acronyms, abbreviations and slang expressions are used widely to describe certain objects or subjects.

These terminologies can be frightening for the uninitiated, and makes participating in conversations a lot harder than it needs to be.

In this article we break it down for you, to help you get a grasp of some of the commonly used terminology in the DigiByte ecosystem.

# Technology

*WRITE SOME GOOD DESCRIPTION HERE..*

## Blockchain

A blockchain is a type of database that distributes and shares data between nodes on a network.

On a traditional database, data are usually stored in tables as separate entries for each data point. On a blockchain the data is grouped together as a collection in what we call blocks.

On a cryptocurrency blockchain, each data entry is a transaction. For a transaction to be broadcasted to the network, it first must go to what is called a mempool

Each block has a specific storage capacity written into the code base. On the DigiByte Protocol the storage capacity of each block is 1 MB (or one million bytes).  
When a block has reached its storage capacity, transactions will have to keep queuing in the [**mempool**](#mempool).

When a block is generated and broadcasted to the network, a [**hash**](#hash) is generated. When it's time for a new block to be generated, it uses the hash from the previous block combined with the new data in the current block to create a new unique hash, the process is the same for all new blocks.

This data structure is what creates a irreversible timeline with inherently immutable data. If you attempted to go back to a previous block and change the data, subsequently the hash would also change, and all blocks after that would have to be re-validated. The difficulty to perform such an action increases with every given block.

The notion of data being comprised as blocks and continuously broadcasted is what gives blockchain its name, a chain of blocks.

## Mempool

The memory pool, or _mempool,_ is a sort of temporary database, and is the first stop for a new transaction, where they sit in queue awaiting a miner to verify it.

Once a transaction is verified, otherwise known as “mined”, the transaction leaves the mempool and gets broadcasted onto the network in the currently comprising block.

On average, the DigiByte [**Blockchain**](#blockchain) verifies a block every 15 seconds. That means that when a block has reached its storage capacity, transactions must sit and wait in the _mempool_ for the next available block.

It should be noted that there are no guarantees that a transaction will make it into the next block, regardless of how long it's been waiting in queue in the mempool.
This is because transactions with the highest fee is prioritized and therefore processed first, as this is of benefit to the miner in terms of rewards received for the computational power they provide. This is the reason for why you may some times see increases in transaction fee on the network, because miners prioritize the highest reward.

In addition, there is a minimum transaction fee on the network, and transaction below this requirement might, in theory, never make it into a block and as a result not get broadcasted on the network.

## Hash

Hashing is a mathematical function that converts input of any length into an encrypted output of a fixed length, producing the _Hash_.
Hash functions are one-way, so once a hash is generated it can not be used to reverse-engineer the data it was generated from. Regardless of how many times you put the data through a hashing function, the resulting hash will always stay the same, this makes for the perfect way to verify sensitive data without the risk of exposing the content of it.

Knowing the hash for a set of data means you can quickly and easily compare data sets to verify that nothing has been altered or corrupted.

## UTXO

An _unspent transaction output_ (**UTXO**) is the technical terminology for the amount of cryptocurrency, in this specific case, DigiByte, remains after a transaction has taken place.

Each time you perform a transaction, a check is made to see how much of a currency is left unspent.  
You can view the UTXO as the change that is returned to you after you have paid for something with a larger bill than the price.

Each transaction requires both what is known as an [**Input**](#transaction-input) and the [**Output**](#transaction-output). This is what is commonly known as double-entry accounting. Don't worry if this term confused you, we explain it below.

### Transaction Input

The input needs to be (at least) enough to cover the charge (cost) entered by the user, this can be comprised of 1 or several UTXO's, depending on their balance and the cost.

This is a method called non-exact, meaning the input is not the exact same amount as the required output.

A transaction input is always the entirety of one or several UTXO's.

### Transaction Output

The transaction output is the selected amount of DigiBytes that is transacted.

The transaction output is exact.

This means an output is the exact required amount of DigiBytes that is going to be sent with the outgoing transaction and will not require the total funds available from the comprised UTXO's.

### **Example**

> This example assumes that Bill's wallet only contains funds from a total of two transactions, i.e UTXO's.
{.is-info}



Let's say that Bill wants to buy some Falafel, and he has 1000 DigiBytes in his account wallet, divided equally from two separate incoming transactions (500 DigiBytes each).

After Bill has selected all of his toppings and his favorite sauce, the Falafel will cost him 800 DigiBytes.

Bill opens up his mobile wallet, scans the vendor's DigiByte payment address, and enters 800 DGB as the amount to send.

Now the wallet will start comprising UTXO's as inputs for the transaction, in this case it will use both of the aforementioned UTXO's á 500 DGB each, so now the total input is exactly 1000 DGB.

But that's too much for the 800 DGB Falafel Bill wants to purchase.

This is where the Output comes in. An output of the required funds is created, corresponding to the 800 DigiBytes Bill entered into their transaction.

Now as the transaction goes out to the Falafel merchant, it will have an output of 800 DigiBytes, and the 200 remaining DigiBytes is send back to Bill as an _unspent transaction output._

Now the next time Bill wants to perform a transaction, there will be one UTXO with a balance of 200 DigiBytes ready to be used as an input for a new transaction.



### Key Points

-   A UTXO is the remaining amount of DigiBytes (cryptocurrency) remaining after a completed transaction
-   UTXO's are processes as part of both the beginning and end of a transaction.
-   After completion of a transaction, any unspent transaction outputs are recorded as available inputs for new transactions.

## PoW

_Proof of Work_ (PoW) is best described as a system where significant amount of effort is required in order to deter malicious use of computing power. Such as denial of service attacks, spam attacks, or otherwise of the sort.

It is a decentralized consensus model, and is today used to, among other things, to secure cryptocurrency transactions, including DigiByte.

With a chain such as DigiByte, the _proof of work_ is also generally referred to as “mining”. When miners work on a [**blockchain**](#blockchain) they compete to be the first miner to generate a valid hash for the data contained within a block. The hash, consisting of a string of numbers and letters, will always stay the same length given the data that is hashed (the [block header](#block-header)), but the hash string itself can differ.

For any computer to generate a valid hash would be very simple, this is why to provide proof of work, the chain applies a [**difficulty adjustment**](#difficulty-adjustment), resulting in a [**target hash**](#target-hash).

The lower the target hash, the fewer possible valid hashes, and the harder to generate one.

## Difficulty Adjustment

Within the code base of DigiByte, there is a fixed value of 15, representing the expected block time, the interval of which blocks are generated and broadcasted on the network. In reality we can never know how much time it takes for a miner to validate, also known as to “solve”, a block. This is where the difficulty adjustment comes in.

DigiByte is rather unique in this aspect, as it applies a real-time _difficulty adjustment_ with the use of the DigiByte developers' own technology known as [DigiShield](#digishield), meaning that it adjusts the difficulty for each block, on every algorithm.

In essence, the point of the difficulty adjustment is to ensure that the actual block time meets the expected block time, in this case 15 seconds.

The equation is pretty simple: 

`new_*difficulty = old_difficulty * (15 seconds) / (the time in seconds to mine the previous block)*`

***_#The above equation is an assumption, and should be fact-checked._***

## Target Hash

The _target hash_, in terms of DigiByte mining, is a numeric value that the hashed [**block header**](#block-header) must be either less than or equal to in order for the block to be considered valid and result in a reward for the miner.

## Block Header

The _block header_ contains three sets of block metadata. It is a 80 byte long string, and is comprised of:

-   4 byte long version number
-   32 byte long previous block [**hash**](#hash)
-   32 byte long [**Merkle root**](#merkle-root)
-   4 byte long block timestamp
-   4 byte long difficulty target
-   4 byte long [**nonce**](#nonce)

The _block header_ is used to identify a specific block on the [**blockchain**](#blockchain)**.** Essentially, it's a cryptographic hash of the data contained within the block, and is created by hashing the metadata mentioned above, twice.

## Merkle Root

The Merkle root is a [**hash**](#hash) of all the transaction hashes contained within a block. It is used to quickly verify the data, to ensure that it is complete and has not been altered or corrupted in any way.

## Nonce

The _Nonce,_ or “number used only once”, is a four-bit number added to the hashed block that when rehashed, meets the [**difficulty**](#difficulty-adjustment) restriction. The nonce is used to attempt to create a [**hash**](#hash) that is less or equal to the [**block header**](#block-header) hash of the block they are validating.

## Hash Power

TO BE WRITTEN

## ASIC Mining

TO BE WRITTEN

# Protocol Implementations

*WRITE SOME GOOD DESCRIPTION HERE..*

## **DigiShield**

_DigiShield_ is the name of a hard fork, activated in February 2014, to protect the DigiByte Blockchain against a multi-pool vulnerability, which in essence means pools were able to mine large amount of DigiBytes at a low difficulty. They way it achieves this is by applying a [Difficulty Adjustment](#difficulty-adjustment) between every block rather than every 2016 blocks, which it was originally.

Not only does this implementation protect against an unfair amount of DigiByte being mined at a low difficulty, but it also makes for a fair mining distribution for the remaining miners once a big amount of [hash power](#hash-power) leaves the network.

The dangers imposed when a big amount of hash power leaves a network is best described as a potential temporary freeze of the chain, a result of the difficulty being too high in relation to the remaining hash power provided. In simple terms, miners are far less likely to be able to validate a block and this can result in transactions not being able to be broadcasted on the network until the difficulty comes back down to viable levels.

During the time of the implementation of this solution, multi-pool “attacks” was common on many [Proof-of-Work](#pow) chains, which was the reason for the rapid development and deployment of the _DigiShield_ implementation. Once implemented, a reported decrease of unfairly mined coins was in the range of 50-80% less than prior to its implementation.

At the time of implementation, DigiByte was using only one algorithm. Since then, 4 more algorithms has been added, and as such, the _DigiShield_ code has been further developed and advanced to provide the same protection on all algorithms. The advanced implementation of _DigiShield_ is now called [MultiShield](#multishield), to better reflect the multi-algo protection.

## MultiAlgo

_MultiAlgo_ is the common term for a hard fork, used to describe the DigiByte Core Protocol's utilization of different [PoW](#pow) mining methods to accommodate mining through more hardware types.

Originally, DigiByte launched to the public with one mining algorithm, called Scrypt, which could be used to mine using computer's Central Processing Units, commonly known as CPU's. With the implementation of _MultiAlgo_, the doors were opened to facilitate mining with Graphical Processing Units, commonly known as GPU's, as well as the more recent [ASIC miners](#asic-mining). To facilitate this, 4 more mining algorithms were introduced to the DigiByte Core protocol, SHA-256D, Qubit, Skein & Groestl.

To this day, DigiByte still uses a 5-mining-algorithm approach, although on July 2, 2019, the algorithm known as Groestl was replaced with [OdoCrypt](#odocrypt), in a attempt to combat ASIC miner dominance and centralization.