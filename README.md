# Encoder

FORK IN PROGRESS, NOT READY FOR PRIME TIME.

A lighweight, simple to use Library for common Arduino Rotary Encoders with pushbutton. With "one more thing" ~~added~~ to be added by alto777

Please read all the documetation from where this was forked. John-Lluch has nailed this down good and explains it.

# Motivation

I forked this to play with it. So far in my searches and researches, it is the only one to take the approach of hanging all work on a regular timer generated interrupt. I didn't see the button enjoying the same treatment and challenge myself here to add it.

# How it works

Again, totally John-Lluch's example, only this one ~~compiles~~ will be fixed to compile and fully demonstrate the original and my added feature, at the expense of involving Serial.begin &c.

```
// define the input pins
#define pinA 19
#define pinB 20
#define pinP 21

// create an encoder object initialized with their pins
Encoder encoder( pinA, pinB, pinP );

// setup code
void setup() 
{
  // start the encoder time interrupts
  EncoderInterrupt.begin( &encoder );
}

// loop code
void loop()
{
  // read the debounced value of the encoder button
  bool pb = encoder.button();

  // get the encoder variation since our last check, it can be positive or negative, or zero if the encoder didn't move
  // only call this once per loop cicle, or at any time you want to know any incremental change
  int delta = encoder.delta();

  // add the delta value to the variable you are controlling
  myEncoderControlledVariable += delta;

  // do stuff with the updated value

  // that's it
}
```

# More

This is worth studying both for the high level approach taken and the low level dets of messing with timers across AVR architectures.

I think it is worth noting there is an alternate that just uses the build-in millis timer; I have not yet experimented with that but I am at this point sure that my modifcations will go along for the ride happily.
