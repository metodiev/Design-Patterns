# Observer Design Pattern

The main intent of the pattern is to create an event notification mechanism between objects.

1. The main intent of the pattern is to create an event notification mechanism between objects.
2. Think of the relationship between a publisher and subscriber:
   a. A Subscriber subscribes to a Publisher of events
   b. When an event happens, the Publisher notifies all the Subscribers in its list that the event has happened.

The Observer Pattern is a behavioural design pattern in which an object usually referred to as the Subject(eg. the Publisher in our examples) maintains a list of its dependents, called Observers (eg. Subscribers in our examples) and notifies them automatically of any state changes.

This pattern perfectly suits any process where data arrives from some input that is not available at a predefined moment, but instead arrieves "at random" (for example HTTP requests, user input from peripherals, distributed databases and blockchains, ent.)

The Observer Pattern is also a key part in the well known and utilized Model-View-Controller (MVC) architectural pattern.
