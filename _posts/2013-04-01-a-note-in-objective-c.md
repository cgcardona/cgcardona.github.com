---
layout: post
title: "An AFNote in Objective-C"
description: ""
category: 
tags: ['audiofile', 'objectivec']
---
{% include JB/setup %}

## Intro

I'm porting an Audiofile project to Objective-C and I've created an `AFNote`
class. The idea is that `AFNote` objects will be the primitive building block with
which developers can create `AFInterval`, `AFChord`, and `AFScale` objects.

## The files

First let's start with the files and then an explanation. For now this is just one class so there is an AFNote.h and an AFNote.m file.

### AFNote.h

```objectivec
#import <Foundation/Foundation.h>

@interface AFNote : NSObject

@property NSNumber *pitch;
@property NSNumber *octave;
@property NSNumber *noteType;
@property NSNumber *key;
@property NSNumber *beatsPerMinute;

// make the following properties readonly
@property NSNumber *frequency;
@property NSArray *frequencies;
@property NSNumber *duration;

- (id) initWithPitch:(NSNumber *) pitch andOctave:(NSNumber *) octave andAFNoteType:(NSNumber *) noteType andKey:(NSNumber *) key andBeatsPerMinute:(NSNumber *) beatsPerMinute;

@end
```

### AFNote.m

```objectivec
#import "AFNote.h"

@implementation AFNote

-(id) initWithPitch:(NSNumber *)pitch andOctave:(NSNumber *)octave andAFNoteType:(NSNumber *)noteType andKey:(NSNumber *)key andBeatsPerMinute:(NSNumber *)beatsPerMinute
{
  if (self = [super init])
  {
    [self setPitch:pitch];
    [self setOctave:octave];
    [self setNoteType:noteType];
    [self setKey:key];
    [self setBeatsPerMinute:beatsPerMinute];
    [self setFrequencies:[NSArray arrayWithObjects:@"27.5", @"29.1352", @"30.8677", @"32.7032", @"34.6478", @"36.7081", @"38.8909", @"41.2034", @"43.6535", @"46.2493", @"48.9994", @"51.9131", @"55", @"58.2705", @"61.7354", @"65.4064", @"69.2957", @"73.4162", @"77.7817", @"82.4069", @"87.3071", @"92.4986", @"97.9989", @"103.826", @"110", @"116.541", @"123.471", @"130.813", @"138.591", @"146.832", @"155.563", @"164.814", @"174.614", @"184.997", @"195.998", @"207.652", @"220.000", @"233.082", @"246.942", @"261.626", @"277.183", @"293.665", @"311.127", @"329.628", @"349.228", @"369.994", @"391.995", @"415.305", @"440", @"466.164", @"493.883", @"523.251", @"554.365", @"587.330", @"622.254", @"659.255", @"698.456", @"739.989", @"783.991", @"830.609", @"880", @"932.328", @"987.767", @"1046.50", @"1108.73", @"1174.66", @"1244.51", @"1318.51", @"1396.91", @"1479.98", @"1567.98", @"1661.22", @"1760", @"1864.66", @"1975.53", @"2093", @"2217.46", @"2349.32", @"2489.02", @"2637.02", @"2793.83", @"2959.96", @"3135.96", @"3322.44", @"3520", @"3729.31", @"3951.07", @"4186.01", nil]
    ];

    [self setFrequency:[NSNumber numberWithFloat:[[[self frequencies] objectAtIndex:[[self octave] intValue] * 12 + [[self pitch] intValue]] floatValue]]];
    [self setDuration:[NSNumber numberWithFloat:60 / [[self beatsPerMinute] floatValue]]];

  }
  return self;
}

@end
```

## Custom `init` method

I created a custom `init` method which sets up the `AFNote` with the values that we need:

```objectivec
- (id) initWithPitch:(NSNumber *) pitch andOctave:(NSNumber *) octave andAFNoteType:(NSNumber *) noteType andKey:(NSNumber *) key andBeatsPerMinute:(NSNumber *) beatsPerMinute;
```

### Sidenote

I have been finding Objective-C a challening syntax to grasp. It's beginning to sink in but it took a while to be able to wade through the nested square
brackets. But this method name shows what I think is an extremely cool feature
of the language once your brain can casually read it. And that feature is how
the method name is self documenting with regards to parameters.

You can perhaps imagine something like this in Javascript:

```javascript
function AFNote(pitch, octave, noteType, key, beatsPerMinute);
``` 

The problem is that when a developer creates an instance of an `AFNote` Object she
needs to be aware of the `AFNote` constructor method's signature.

Objective-C solves this problem by including part of the name for each argument.
So in my custom `init` method you can see that it requires a price, octave,
noteType, key, and beatsPerMinute.

Now back to our regularly scheduled program...

## The Properties

An `AFNote` object has several properties:

### `key`

To set the `key` for an `AFNote` pass an `NSNumber` between -7 and 7 into the settings object. The entire [circle of fifths](http://en.wikipedia.org/wiki/Circle_of_fifths). 0 = C, -7 = C flat, and 7 = C sharp. 

### `octave`

There are 8 octaves on the keyboard.

To set an `AFNote`'s `octave` pass an `NSNumber` with a value between 0&ndash;8. 

### `pitch`

Each octave is 12 notes. For example 1 octave in the key of C is: C, C#, D, D#, E, F, F#, G, G#, A, A#, B. Between one
note and the next is called a half-step. Therefore to both set an `AFNote`'s `pitch` pass an `NSNumber` with a value between 0&ndash;11. 

Remember that all counting is zero indexed and starts with 0. So in the key of C—C would be 0 and the B nearly one octave higher would be 11.

### `noteType`

Different types of notes. `1` for whole note, `2` for half note, `4` for
quarter note, and `8` for eighth notes etc.

### `beatsPerMinute`

The number of beats per minute which is used to calculate the duration of each note.

### `frequency`

The `frequency` of an `AFNote` is a combination of it’s `octave` property which tells which octave the note is in (0–8) as well as the `pitch` property which tells the note’s location within the octave.  

### `frequencies`

This is an `NSArray` of `NSString` objects which are the frequencies of the 88
keys on a keyboard.

### `duration`

The length a note should sound. This is calculated by dividing 60 seconds by the
number of beats per minute.

## Create an AFNote Object

```objectivec
AFNote *myAFNote = [[AFNote alloc] initWithPitch:[NSNumber numberWithInt:3] andOctave:[NSNumber numberWithInt:0] andNoteType:[NSNumber numberWithInt:8] andKey:[NSNumber numberWithInt:0] andBeatsPerMinute:[NSNumber numberWithInt:120]];
```

## Thoughts

I realize that `frequencies` shouldn't be a public property which can be set
with `[AFNote setFrequencies]`. This is obviously a fail because someone could
destroy the `NSArray` of frequencies.

There are actually a few properties which I'd like to make `readonly` but I'm
not sure the exact sytax so I'm going with this for now.

Those properties are:

```objectivec
@property NSNumber *frequency;
@property NSArray *frequencies;
@property NSNumber *duration;
```
