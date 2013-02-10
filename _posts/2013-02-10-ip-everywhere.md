---
layout: post
title: "IP everywhere"
description: ""
category: 
tags: ['network', 'code']
---
{% include JB/setup %}

(This relates to IPV4. I'll cover IPV6 later)

IP addressing is at the core of networked computing. Everyone has heard "Go to
this IP address" but what does that actually mean? Let's dig in a bit.

## First things first What is an IP address? 

An [IP Address](http://en.wikipedia.org/wiki/IP_address)
is an **Internet Protocol Address**. Similar to the address on your house an IP
Address is used to route packets to a host computer on some network.

More specifically an IP Address is a 32 bit number which is usually split up
into 4 8 bit 'octets' seperated by a `.`.

An example is `192.168.10.1`

## Network(s) and Host(s)

Keep in mind that the Internet/Web is a 'Network of networks.' That just means
that within the large Network there are many smaller `networks`. Examples are your
house, job, etc.

Within each one of those networks there are at least one potentially many
computers--otherwise known as `hosts`. An IP Address tells us which network and which individual computer to route the
packet to. It does this with a `network ID` and a `host ID`.

You can think of a `network ID` as analogous to the street that you live on and
the `host ID` is like your house number. Using both your street and house number
a person could send you a package from anywhere in the world (in theory). Using
a `network ID` and `host ID` a packet can get routed to any computer on the
network.

The `network ID` and the `host ID` are of course both in the IP Address so the
question is how do you tell which part is which? That is done with a `subnet
mask`.

## subnet mask

A `subnet mask` is another 32 bit number broken up into 4 8 bit octets. As a
complete over simplification (because this stuff isn't simple) you can imagine
that if an octet has all the bits set to 1 then that octet in the IP Address is
part of the `network ID`. If the `subnet mask` octet has all the bits set to 0
then that octet of the IP Address is part of the `host ID`.

Let's take a look at an example. Imagine that we have the following IP Address
and `subnet mask`

    IP Address: 192.168.10.1
    Subnet mask: 255.255.255.0

Based on the `subnet mask` the IP Address would be broken down:

    Network ID: 192.168.10
    Host ID: 1

An important thing to notice is that as the potential count of the networks goes
up the potential number of hosts on a network goes down. Conversely as the
potential count of the networks goes down the potential number of hosts on a
network goes up.

## Total potential Host IDs

First a quick rule. A `host ID` can't be all 0s or all 1s. 

A `host ID` of all 0s is a `network ID` and a `host ID` of all 1s is a
`broadcast ID`. More on that later.

In the beginning (again a simplification) there were 3 classes of IP
Addresses--A, B, and C. They had the following `subnet masks`:

    Class A 1-126 255.0.0.0
    Class B 128-191 255.255.0.0
    Class C 192-223 255.255.255.0

Let's do some calculations to figure out how many potential `host IDs` would be
available in this scenario.

### Class A

    126 networks, 16,777,214 hosts

### Class B

    16,384 networks, 65,534 hosts

### Class C

    2,097,152 networks, 254 hosts 

### Total
    3,720,314,268 total potential Host IDs

So initially there were just shy of 4 billion potential `host IDs` on the
network. At the time in the 70's this was considered to be enough. That proved
not to be the case though which is what IPV6 (to be covered at another time) is
all about.

## More info:

* [Networking 101 - IP Address, Router, Default Gateway](http://www.opto22.com/community/showthread.php?t=269&page=1)

