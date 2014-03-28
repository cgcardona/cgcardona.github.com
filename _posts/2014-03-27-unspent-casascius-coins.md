---
layout: post
title: "Unspent Casascius Coins"
description: ""
category: 
tags: ['bitcoin']
---
{% include JB/setup %}

## Intro

Lately I've been researching bitcoin cold storage and have become increasingly
more interested in [Casascius Coins](https://www.casascius.com/). Unfortunately
[Mike Caldwell](https://www.twitter.com/casascius) had to suspend selling the coins preloaded w/ btc so now you
have to buy them blank and load them w/ the btc yourself.

While exploring the site I found a [full list of all Casascius coins ever
minted](https://www.casascius.com/fulllist.txt). This was so interesting that of
course I started picking out addresses at random and looking them up on the
blockchain to check their balance.

I noticed that many of the addresses that I checked either had 0
transactions/balance, which leads me to believe that at least some and perhaps
many of the coins in the list never actually had any btc loaded onto them, or
had already been 'spent.'

This got me wondering exactly how many of the listed coins had not been spent.
So I decided to write a short script to query the block chain and figure it out
(yay transparency!).

First I started with [blockr.io's `Address Balance` API](http://btc.blockr.io/api/v1/address/balance/1AgzXorQHKmWTYWbtJnzBaJYQVMJi6CDhD,1AgzxTcbTpgEiHYhVUdfzc4R1rzF3ttGW2) because it accepts multiple input values. After experimenting it appeared to be able to return the balance of up 20 wallets at a time without falling over. 

So I wrote a ruby script which pulls the values out of the fulllist.txt file into an array. It then loops over the array and checks the blockchain 20 addresses at a time for the balance.  If any address has a balance it sets it aside.

```ruby
require 'httparty'

tmp_arr = []
addresses_still_with_coins = []
casascius_coin_addresses = []

File.open('fulllist.txt').each do |line|
  casascius_coin_addresses << line
end

casascius_coin_addresses.each_with_index do |address, index|
  tmp_arr << address.gsub("\n","").gsub("\r","")
  if tmp_arr.count == 20
    coin_string = tmp_arr.join(",")
    success = HTTParty.get("http://btc.blockr.io/api/v1/address/balance/#{coin_string}")
    success['data'].each do |balance|
      if balance['balance'] > 0
        addresses_still_with_coins << balance['address']
      end
      tmp_arr = []
    end
  end
end

File.open("unspent_casascius_coins.txt", "w+") do |f|
  addresses_still_with_coins.each { |element| f.puts(element) }
end
```

You might have noticed that this code leaves 19 addresses at the end that haven't been checked. Yea I just plugged those in by hand.

The results can be seen in [this gist 'Unspent Casascius Coins'](https://gist.github.com/cgcardona/9826685). There were 25101 coins which
had a positive balance which would lead me to believe that they had never been
spent. 

Please let me know if you see any fault in my logic here or if you have a
coin(s) on the fulllist that you've not spent which isn't on my final list of
'Unspent Casascius Coins.'

Thanks!
