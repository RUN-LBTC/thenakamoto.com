---
layout: post
title:  "Sharding II"
author: tiaan
categories: [Bitcoin, Cryptocurrency, Money, Fractional Reserve Banking, Scaling, Fiat]
tags: [Bitcoin, Cryptocurrency, Money, Fractional Reserve Banking, Scaling, Fiat]
image: assets/images/ShardingII.png
description: "We look at the Ethereum blockchain, sharding, and how sharding will allow blockchains to scale."
featured: false
hidden: false
rating: 
---

_In our last update, we discussed what sharding is, the problems it aims to solve and some of the hurdles we need to overcome to effectively implement it. Today we’ll look at cross-shard transactions, invalid transactions, and malicious behavior._

The basic type of shard we described in our last article isn’t a very useful or practical method of sharding, because they can’t communicate with each other, which makes them as useful as one individual blockchain.

Let’s take the example of making a simple payment. If user A and user B were on the same shard, the validators within the shard would be able to process the transaction without issue, but what happens when they have accounts on different shards?

User A is on shard #1 and user B is on shard #2. The validators on the individual shards would not be able to debit or credit the users’ accounts because they would have no authority on each others’ respective shards.

There are however solutions to this problem, so let’s take a look at some of them in a little more detail:

#### Synchronous (same-time) cross-shard transactions
In this case, when user A on shard #1 needs to send funds to user B on shard #2, the blocks in each shard that contains state transition that’s related to the transaction itself are produced simultaneously, and the validators on each shard work collaboratively to confirm the transaction. Vitalik Buterin proposed merge blocks with this solution back in early 2018.

#### Asynchronous cross-shard transactions
This is a slightly easier operation to complete, and far simpler to coordinate so it is more popular than synchronous transactions.

Again, we’ll use the example of user A on shard #1 wanting to send money to user B on shard #2.

In this scenario, the shard in charge of crediting user B’s account will only validate its part of the transaction once it has enough proof that the shard in charge of debiting user A’s account has been done.
This approach is not perfect though, there is a non-zero chance that one of the blocks of one of the shards gets orphaned. A non-zero chance, however unlikely is still a vulnerability that can’t be ignored.

Taking the figure below into consideration we’ll look at why:

![Asynchronous Cross-Shard Transactions](https://github.com/The-Nakamoto/thenakamoto.com/blob/gh-pages/assets/posts/ShardingII-1.jpg?raw=true "Asynchronous Cross-Shard Transactions")

This blockchain has two shards, and by pure coincidence, they both fork at the exact point that the transaction is incorporated into block A in shard #1 and block X’ in shard #2.

When a fork like this happens, the shard has to orphan one of the chains and accept the other. In this case, if chain A, B, etc. becomes the accepted chain in shard #1 and chain W’, X’, etc. becomes the accepted chain in shard #2, then the transaction gets finalized and everyone is happy.

If the A’, B’ etc. chan in shard #1 is accepted and chain W, X etc. in shard #2 is accepted, then the entire transaction fails, which is also an acceptable outcome, because the transaction can be resent.

What happens if chain A, B, etc. is accepted in shard #1 and chain W, X, etc. is accepted in shard #2? One part of the transaction is finalized (A, B, etc.) and the other part of the transaction is abandoned (W, X, etc.)

#### Is that it?
Now that you have a better understanding of sharding and how it works, you might be satisfied, or have more questions, there is however at least one more thing to consider: bad actors.

#### Malicious nodes
It’s quite common (in any scenario) that when there is the potential for a large payday, there will be people out there thinking of ways to beat the system, whatever that system might be.

#### Approving invalid blocks
Bad actor nodes might decide that they want to attack the network by creating blocks that attempt to alter the network. Using user #1 and #2, let’s hypothesize that User #1 has 10 coins and user #2 has 0 tokens. Malicious nodes on the network could attempt to create a block when user #1 sends those 10 coins to user #2, which ends up with user #1 having 0 coins and user #2 has 1000 coins.

![Approving invalid blocks](https://github.com/The-Nakamoto/thenakamoto.com/blob/gh-pages/assets/posts/ShardingII-2.jpeg?raw=true "Approving invalid blocks")

In a regular blockchain that isn’t sharded, this type of attack is impossible, since every node validates every block, and if an invalid block is discovered, all the nodes (whether they are miners or not) reject that block.

With classic blockchains, it doesn’t matter how many blocks malicious nodes create, or how fast they create them, the honest actors of the network will always ignore those blocks and continue building the honest chain.

Consider a chain that splits into two because bad nodes want to build invalid blocks to fill their accounts with a bunch of coins. The malicious nodes might even outnumber the honest nodes as is this case. The shorter chain is the honest chain, and the longer one is invalid. In a regular non-sharded blockchain, every participant is responsible for validating all the blocks they receive and confirming the state, therefore anyone who has a vested interest in the blockchain (and by extension its integrity) would immediately recognize the invalid chain and disregard it for the (in this case) shorter chain.

![Approving invalid blocks](https://github.com/The-Nakamoto/thenakamoto.com/blob/gh-pages/assets/posts/ShardingII-3.jpg?raw=true "Approving invalid blocks")

A sharded chain is a little more complex because participants can’t validate every transaction on each shard, so we have to figure out how to confirm that there are no invalid blocks within the entire history of the shard.

Since the beacon chain (discussed in our last post) doesn’t normally have the capacity to validate every block in every shard, we need another solution to ensure the integrity of each chain.

Assuming that the network, and by association, each shard has a Byzantine Fault Tolerance mechanism, and the malicious nodes within a shard control less than 66.667% you could build a mechanism that alerts the system if there are any attempts to generate invalid blocks, wherein one or more honest nodes could attest to valid or invalid blocks. If more than 66.667% of the shard is controlled by malicious nodes, then they could theoretically finalize blocks, however as long as one node within the shard is honest, a mechanism can be built to allow honest nodes to contest malicious ones.

_This post is intended for informational purposes only. The views expressed in this post are not, and should not be construed as investment advice or recommendations. This article is not an offer, nor the solicitation of an offer, to buy or sell any of the assets or securities mentioned herein. All opinions in this post are my own._