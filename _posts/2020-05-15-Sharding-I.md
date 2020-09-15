---
layout: post
title:  "Sacling Money I"
author: tiaan
categories: [Bitcoin, Cryptocurrency, Money, Fractional Reserve Banking, Scaling, Fiat]
tags: [Bitcoin, Cryptocurrency, Money, Fractional Reserve Banking, Scaling, Fiat]
image: assets/images/ScalingMoneyI.png
description: "We look at the Ethereum blockchain, sharding, and how sharding will allow blockchains to scale."
featured: false
hidden: false
rating: 
---

In this two-part explainer, we look at the Ethereum blockchain, sharding, and how sharding will allow blockchains to scale.

Ethereum is the blockchain most synonymous with the concept of sharding, and to understand why the Ethereum developer community wants to implement sharding, it’s important to understand what it is, and why it's an attractive solution.

According to ETH Gas Station, it takes around 1.78 minutes for a transaction to be added to the Ethereum blockchain, with new blocks being produced every 32 seconds with an average of 15–20 transactions being processed a second. This ecosystem creates an environment that favors miners over users, where if a user wants to prioritize their transaction, they have to increase their gas prices.

Low throughput in conjunction with high latency and prices limit the network, and as a result, the network is less suitable for services and applications that need to scale as they are adopted. The primary reason for Ethereum’s low throughput is due to the requirement for every node on the network to process every transaction.

#### What is Sharding?
Simply put, sharding is a way of partitioning to spread out computational and storage workloads across a P2P network so that each node isn’t responsible for processing the entire network’s transactional load but rather only maintains information related to its partition (or shard).

To further explain sharding we can use the very simplest example of sharding. Vitalik Buterin, the founder of Ethereum refers to this as “scaling by 1000 altcoins”

In this instance, instead of running a single blockchain, we run multiple blockchains and instead of referring to each as a blockchain, we call each chain a shard. Each shard, in turn, has its own network of validators or nodes which either mine blocks using a PoW algorithm, or by staking or voting.

#### The Challenges to Sharding
The first issue we find when attempting to use sharding is that because each shard has its own set of nodes, each shard is less secure than having a single chain like Ethereum. So if Ethereum with the 𝑥 amount of nodes decided to hard fork and split into a sharded chain, and distributed the network over 10 shards, each shard would have 1% of the original chains’ security. This means that each shard could be compromised or corrupted by controlling 5.1% of the nodes of the original chain as opposed to 51% of it.

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

The second problem we run into is: “how do we / who chooses which node validates which shard?” For a bad actor, controlling 5.1% of the network’s nodes is only a problem if they are all validating in the same shard. Allowing nodes to choose which shard they validate within could cause frequent network attacks, so the best way to minimize the risk of attack is to not allow nodes to choose which shard they validate for.

Virtually all sharding architecture relies on randomness to assign nodes to a shard. Assigning nodes to a shard requires calculations that aren’t shard specific and almost all of these designs make use of a separate chain that handles the maintenance of the entire network of shards and nodes.

This chain, referred to as a beacon chain in Ethereum, is responsible for generating random numbers, assigning nodes to shards, taking snapshots of individual shards, processing stakes and various other functions.

Beacon chains have a few of their shortcomings. They are responsible for the record keeping computations mentioned before, so the more shards that a network makes use of, the more work the beacon chain has to do, resulting in the same problem that a network without sharding might encounter — Low throughput in conjunction with high latency, so the scalability of a sharded network has a natural limitation.

A sharded network does, however, have multiplicative properties, so if there are improvements to the efficiency of the network that result in the nodes in the network processing transactions four times faster, the beacon chain would be able to handle four times the amount of shards, improving the network speed by 16.

#### How can Data be Split into Shards?
Let’s start by looking at what functions nodes typically perform on a blockchain:

1. They process/validate transactions
2. They relay these transactions as well as the blocks they mine to other nodes on the network
3. They store the history of all transactions

As a network grows, nodes need to be able to keep up with the requirements of the network, so as the network grows;

1. Increasing the number of transactions being processed required each node to add more computing power
2. More transactions being relayed requires more bandwidth from the node
3. Storing all the data on the blockchain also gradually requires the node to add more storage

Looking at these three parameters you’ll notice that data storage will grow whether the number of transactions per second or number of transactions that are relayed increases or not.

At the time of writing, the sharding of storage but not transactions have been proposed, and some projects have implemented the sharding of transaction processing but not the storage, however, the most common type of sharding being worked on is called “State Sharding” and this consists of the nodes in each shard building their own blockchain that contains transactions that only affect their part of the entire global network, which means that nodes only need to store their shards’ transaction history, process transactions that affect their shard and relay those transactions within their shard.

In our next part, we’ll look at cross-shard transactions, invalid transactions and malicious behavior.

_This post is intended for informational purposes only. The views expressed in this post are not, and should not be construed as investment advice or recommendations. This article is not an offer, nor the solicitation of an offer, to buy or sell any of the assets or securities mentioned herein. All opinions in this post are my own._