
# Builder Pattern

It hides the process of building complex objects. A builder is an object able to construct other objects. It constructs and assembles different object parts to build the result objects.
The builder pattern is not just about encapsulation and hiding of the creation process; it is also designed for reusability and flexibility.

When to use the builder pattern: 
1. When you have a complex class with many constructors
2. When you have to build complex composite tree objects.
3. When you want to build different representations of your complex objects, but still use the same general steps.

Pros:
1. Provides clear separation between the construction and representation of an object.
2. Provides finer control over the steps of the construction process.
3. It supports changing the internal representation of objects.

Cons:
1. A distinct Concrete Builder must be created for each type of object.
2. Builder classes must be mutable
3. May hamper/complicate dependency injection.


Design Consideration:

1. Encapsulate creating and assembling the parts of a complex object in a separate Buidelr object,
2. Create a specific class (a Director) which will delegate object creation to a Builder object instead of creating the objects directly,
3. Look for synergy in the family of the object you are modelling. You should be able to use the same construction process by delegating to different Builder objects to create diffrent representations of a complex object. 
