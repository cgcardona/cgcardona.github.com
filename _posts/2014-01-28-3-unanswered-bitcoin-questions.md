---
layout: post
title: "3 unanswered Bitcoin questions"
description: "3 remaining unanswered Bitcoin related questions"
category: 
tags: ['bitcoin']
---
{% include JB/setup %}

## 1. Bitcoin days destroyed on Coinbase

On initially thinking it through you would think that the growth of the Bitcoin network could be judged by looking at the number of transactions per day. The problem however is that someone could just send a single satoshi back and forth between 2 wallets an increasing number of times each day and it would artificially make the network appear that the number of transactions per day was increasing.

To handle this situation more accurately Bitcoin has the metric [Bitcoin Days Destroyed](https://en.bitcoin.it/wiki/Bitcoin_Days_Destroyed)

> Bitcoin days destroyed for any given transaction is calculated by taking the number of Bitcoins in a transaction and multiplying it by the number of days it has been since those coins were last spent.

So an appropriate pseudo-algorithm would be:

```ruby
bitcoin_days_destroyed = number_of_bitcoins_in_transaction * number_of_days_since_those_coins_were_spent
```

### Example

So a simple example is a user who has 10 bitcoins. This user leaves the bitcoin
in their wallet for a complete week and then spend them all buying a brand new
DW drum set.

According to our algorithm above how many Bitcoin Days were destroyed?

```ruby
number_of_bitcoins_in_transaction = 10 
number_of_days_since_those_coins_were_spent = 7
bitcoin_days_destroyed = number_of_bitcoins_in_transaction * number_of_days_since_those_coins_were_spent
# 7 Bitcoin Days Destroyed
```

### Regarding Coinbase off-blockchain transactions

[Coinbase recently announced](http://blog.coinbase.com/post/57483182558/you-can-now-send-micro-transactions-with-zero-fees) that you can send micro-transactions between Coinbase wallets that have 0 fees and are confirmed instantly.

This makes micro-transactions **truly** feasible by overcoming the [bitcoin dust](https://code.google.com/p/bitcoin-wallet/wiki/DustTransactions) problem

My question is how do Bitcoin Days destroyed work with regards to off-blockchain transactions? 

If Coinbase (and other off-blockchain transaction vendors) doesn't accurately reflect the number of bitcoin days destroyed in off-blockchain transactions then as a community are we getting an accurate view of how quickly the Bitcoin economy and transactions are growing?

* * *
## 2. Harder or easier to launch an alt-coins in the future

Each day we hear about a new [alt coin](http://www.urbandictionary.com/define.php?term=altcoin) being created. This is the combination of
a couple of factors. The first is that it's getting easier and easier to create an alt-coin. Many have now paved the way and there are even pay services which let you just pay some cash, plug in some values, and it creates the alt coin for you.
 
Now with the emergence of the so called 'bitcoin 2.0' and projects like [mastercoin](http://www.mastercoin.org/) and [colored coins](http://coloredcoins.org/) we are going to see even more alt coins built on top of the blockchain.

The second reason that we're seeing so many alt coins is that as the difficulty level to mine a bitcoin block becomes ever more difficult all of the outdated mining hardware begins mining a different coin.

My question is will it be easier to launch an alt coin in the future due to the proliferation of tools and open source code or will it be harder because of the chance that your alt coin's blockchain could be [51%ed](https://en.bitcoin.it/wiki/Weaknesses#Attacker_has_a_lot_of_computing_power) by all of the mining power sitting out on the web.

* * *
## 3. Do off blockchain zero fee transactions ultimately hurt the network in any way.

The Bitcoin Coinbase is the number of coins that get released to the wallet of
the computer which mines the latest block about each 10 minutes. Every 4 years
the value of the coinbase gets cut in half. 

It started at 50 coins every block then it got cut to 25 coins per block and in
the future it will continue to get cut in half until the year 2140 when all
(nearly) 21,000,000 bitcoins will have been mined.

The way that the miners continue to pay for mining gear as the coinbase drops
to zero is that they are rewarded all of the transaction fees that accrue since
the mining of the last block.

However in off-blockchain zero fee transactions there are literally zero fees
accrued for the miners to benefit from.

My question is as the number of transactions that are happening in
off-blockchain zero fee transactions services increases does it somehow hurt the
network because it's not generating the fees which the miners are going to come
to rely on as the coinbase drops.
