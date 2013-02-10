---
layout: post
title: "Ping me maybe"
description: ""
category: 
tags: ['network']
---
{% include JB/setup %}

[ping](http://linux.die.net/man/8/ping) is a command that tests a source
computer's connection with a destination machine.

    ping localhost
    ping 127.0.0.1
    ping example.com

## It's all about the flags

Like any good Unix command `ping` has a host of flags. Let's explore some.

### `-A` `audible`

Sound audible beep when a packet is received before the packet what was sent
before it.

    ping -A localhost

### `-a` `audible`

    ping -a localhost

Sound audible beep when a packet is received

### `-c` `count`

Stop after sending and receiving `count` packets. 

    ping -c localhost

### `-i` `wait`

Wait `wait` seconds between sending packets. You can only increase/decrease in
1/10 second increments.

    ping -i localhost

### `-f` `flood`

Output packets as fast as they come back or 100 times per second whichever is
faster. `WARNING:` This is basically a Denial of Service (DoS) attack and it can be illegal
to do against a computer that you don't own. I highly suggest only doing this on
your own machine or a machine that you own.

Only a SuperUser can use this command.

    ping -f localhost

It's worth noting that when I just `ping` my `localhost` I have 0% packet loss.
However when I `ping -f` my `localhost` I have usually around a 20% packet loss.

### `-l` `preload`

Send `preload` numer of packets as fast as possible before falling into normal
mode of behavior.

Only a SuperUser can use this command.

    ping -l localhost

### `-n` 

Numeric output only.

    ping -n localhost

### `-o` 

Exit successfully after receiving only 1 packet.

    ping -o localhost

### `-q` 

Quiet output. Only show summary at startup time and when finished.

    ping -q localhost

### `-Q` 

Somewhat quiet output. 

    ping -Q localhost
