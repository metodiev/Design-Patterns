# Strategy Pattern

1. State design pattern can be considered as an extension of Strategy. Both patterns utilize composition at their core: they allow the modification of their process by delegating work to helper objects. Strategy makes these objects completely independent and unaware of each other. However, State allows the objects to alter their behaviour when internal state changes.

2. Command and Strategy seem similar, but have different motivations"
  a. Command allows for conversion of any operation into an object
   b. Strategy allows for objects to achieve the same thing but in different ways.

When to use:
  1. Use this pattern to abstract the business logic of a class from its implementation details so that it can be 'plugged in'.
  2. Use it when your class has a potential conditional statement that switches between different variants of the same algorithm,
  3. Use Strategy Pattern when you want to use different variants/version of an algorithm within an object and need to have the ability to switch from one algorithm to another during runtime.


When not to use: 
1. If you only have a few algorithms and they rarely change, it might be unnecessary to overcomplicate your code with new classes and interfaces

Pros: 

In the strategy pattern, the behavior of a class should not be inherited, but instead the behavior should be abstracted and encapsulated using interfaces.
This is compatible with the Open/Closed Principle (OCP), which proposes that classes should be open for extension but closed for modification.

2. You can introduce new Strategies into the context without breaking any client code. This follows the Open/Closed Principle.

Cons:
1. Clients must be aware of the differences between strategies to be able to select a proper one.

## Design Considerations:

1. Identify the algorithm that can vary depending on the circumstances of the context.
2. Declare the client interface, which will be the strategy contract for all the variants of the processing algorithm.
3. Implement each interface for the specific algorithms you have indetified.
4. Add a private field to the Context class to store a reference to the Strategy object. Also, provide a way to initialize the specific strategy in the context.
5. NOTE: if the Strategy needs access to some context data then provide a way for the strategy to access such data.
6. Clients of the context must be able to properly initialize the context with the correct strategy for a given circumstance.


## Code
Real Scenario 

You’re building a payment system and want different payment strategies:

1. Credit Card
2. PayPal
3. Crypto

### Step 1: Strategy Interface
```java
public interface PaymentStrategy {
    void pay(double amount);
}
```

### Step 2: Concrete Strategies
Credit Card


```java
public class CreditCardPayment implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}
```

PayPal

```java
public class PayPalPayment implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using PayPal");
    }
}
```


Crypto

```java
public class CryptoPayment implements PaymentStrategy {

    @Override
    public void pay(double amount) {
        System.out.println("Paid " + amount + " using Crypto");
    }
}
```


### Step 3: Context Class

```java
public class PaymentContext {

    private PaymentStrategy strategy;

    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void processPayment(double amount) {
        if (strategy == null) {
            throw new IllegalStateException("Strategy not set");
        }
        strategy.pay(amount);
    }
}
```

### Step 4: Usage

```java
public class Main {
    public static void main(String[] args) {

        PaymentContext context = new PaymentContext();

        // Use Credit Card
        context.setStrategy(new CreditCardPayment());
        context.processPayment(100);

        // Switch to PayPal
        context.setStrategy(new PayPalPayment());
        context.processPayment(200);

        // Switch to Crypto
        context.setStrategy(new CryptoPayment());
        context.processPayment(300);
    }
}
```
