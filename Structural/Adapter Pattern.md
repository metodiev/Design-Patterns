
## Adapter Pattern

 Adapter is a structural design pattern which is used to convert the interface contract of one class to be compatible with another.

 This 'conversion' can take two different elements into account
 1. Adapter can convert source data into formats that the client can understand.
 2. Adapter can also help objects with different (or incompatible) interfaces collaborate
  example:
    Legacy Rectangle has (x, y, w, h)       Interface adapter accept the legacy variables and call the new Rectangle interface -> (x, y, w, h -> )Interface -> x1, y1, x2, y2  finally the interface call the Rectangle Interface -> Rectangle (x1, y1, x2, y2)


## When to use:
1. Use the Adapter pattern when you have an existing class or contract that you would to reuse , but its interface isn't compatible with the rest of your code.

## When not to use:

1. When your system is very time-sensitive since 'waping' the Adaptee creates a but of an overhead as it creates an extra call layer,

Pros: 
1. You can separate data conversion code from the main business logic of your application. This follows the Single Responsibility Principle.
2. You can introduce Adapters into your code without breaking any existing client code. This follows the open/Closed Principle.

Cons:
1. The Adapter pattern can increase the overall complexity of your code since you introduce a set of new interfaces and classes


## Code

## Step 1 Target Interface
```java
public interface PaymentProcessor {
    void pay(double amount);
}
```

## Step 2 Legacy Class
```java
public class LegacyPaymentService {

    public void makePayment(double value) {
        System.out.println("Paid " + value + " using legacy system");
    }
}
```


### Step 3 Adapter

```java
public class PaymentAdapter implements PaymentProcessor {

    private final LegacyPaymentService legacyService;

    public PaymentAdapter(LegacyPaymentService legacyService) {
        this.legacyService = legacyService;
    }

    @Override
    public void pay(double amount) {
        // adapt method call
        legacyService.makePayment(amount);
    }
}

```

### Step 4 Usage, with Main Method:

```java
public class Main {
    public static void main(String[] args) {

        LegacyPaymentService legacyService = new LegacyPaymentService();

        PaymentProcessor processor = new PaymentAdapter(legacyService);

        processor.pay(100.0);
    }
}
```



## Real Senior-Level Use Cases

You’ll see this pattern in:

1. External APIs
  Wrapping third-party SDKs (Stripe, PayPal, etc.)
    Keeping your domain clean
2. Microservices Integration
   Adapting different service contracts
   Version migrations (v1 → v2)
3. Data Layer
   Adapting JDBC → your domain model
   Or different DB drivers
