---
layout: post
title: "Web Audio Context API"
description: ""
category: 
tags: ['code', 'javascript', 'html5']
---
{% include JB/setup %}

The Web Audio Context API surprised me in how fully featured it is. Most of the docs and tutorials I found on it are from 
late 2011 so it shows that I'm late getting to the party. Despite the time passing it appears to only have great support 
in Chrome (This life best viewed in Chrome :p ).

The following constructor creates a shiny new AudioContext Object:

`var audioContext = new webkitAudioContext();`

## Small rant

I've said it before but I find it inconvenient that javascript is prototypal yet the DOM APIs are exposed through a `new` 
constructor. The problem is that the `new` constructor masks the prototypal nature of javascript. In prototypal systems objects inherit directly from other objects. There is no class which you make an instance of. 

`Object.create()` makes more sense but these DOM APIs aren't exposed in that way AFAIK. That's why I've been wrapping so many DOM Objects in AudioFile Objects so that I can just set the DOM object as a property of my AF Object via a `new` constructor but when I want to get an 'instance' of the object I just clone the AF object via `Object.create()`.

I wonder how that's all gonna change with ECMAScript 6 classes?

## Back to the Web Audio Context()

### Properties

The following are the out of the box properties of the AudioContext Object:

1. activeSourceCount: 0
2. currentTime: 1.4164172335600906
3. destination: AudioDestinationNode
4. listener: AudioListener
5. oncomplete: null
6. sampleRate: 44100

### Methods

The following are the out of the box methods of the AudioContext Object:

1. createAnalyser(){}
2. createBiquadFilter(){}
3. createBuffer(){}
4. createBufferSource(){}
5. createChannelMerger(){}
6. createChannelSplitter(){}
7. createConvolver(){}
8. createDelay(){}
9. createDelayNode(){}
10. createDynamicsCompressor(){}
11. createGain(){}
12. createGainNode(){}
13. createJavaScriptNode(){}
14. createMediaElementSource(){}
15. createMediaStreamDestination(){}
16. createMediaStreamSource(){}
17. createOscillator(){}
18. createPanner(){}
19. createScriptProcessor(){}
20. createWaveShaper(){}
21. createWaveTable(){}
22. decodeAudioData(){}
23. startRendering(){}


As you can see there's a lot going on here. I'm going to play around with this a bit and see what I can come up with. I'll check back in later.