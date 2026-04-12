# Observer Design Pattern

The main intent of the pattern is to create an event notification mechanism between objects.

1. The main intent of the pattern is to create an event notification mechanism between objects.
2. Think of the relationship between a publisher and subscriber:
   a. A Subscriber subscribes to a Publisher of events
   b. When an event happens, the Publisher notifies all the Subscribers in its list that the event has happened.

The Observer Pattern is a behavioural design pattern in which an object usually referred to as the Subject(eg. the Publisher in our examples) maintains a list of its dependents, called Observers (eg. Subscribers in our examples) and notifies them automatically of any state changes.

This pattern perfectly suits any process where data arrives from some input that is not available at a predefined moment, but instead arrieves "at random" (for example HTTP requests, user input from peripherals, distributed databases and blockchains, ent.)

The Observer Pattern is also a key part in the well known and utilized Model-View-Controller (MVC) architectural pattern.

When to use:

1. Use the observer pattern when changes to the state of one object need to be 'known' by other objects. Especially when the actual set of the other objects is either unknown initially or changes dynamically throughout the lifecycle of the application.

2. Use it when an object or a set of objects need to 'observe' changes in other objects and need to be notified in real-time about those changes.


When not to use:

1. Because the order of notifications is potentially random, be carful about your requirements if order of notifications is important.

Pros: 
1. You can introduce new subscriber implementation without having to change the publisher's code. This is compatible with the Open/Closed Principle (OCP)
2. It supports the Principle of Loose Coupling between objects that interacts with each other.
3. You can establish relationships between objects dynamically at runtime.
4. If you think about it, the Observer pattern is the key to reactive behaviour.

Cons:

1. The order in which observers/ subscribers are notifies is potentially random.
2. Debugging notofications can be difficult given the random nature of natifications.

Design Considerations:

1. Look for elements in your business logic that need to be aware of state data changes.
   Break it down into two parts:
   a. The controller/reciever of the events. This will be your Publisher
   b. The components that need to be aware of those changes. These will be Subscribers.

2. Declare the Publisher interface and define the contract for adding removing subscribers.
3. Declare the Publisher interface and define the contract for adding and removing subscribers.
4. Create an abstract Publisher implementation with a mechanism for subscriber management and notification.
5. Identify the state data that will need to be 'observed' and create a concrete Publisher implementation for that state. Define a way for subscribers to get that access to that state.
6. Create a specific implementation of subscribers that you need.


## Code

Step 1: Observer Interface

```java
§public interface Observer {
    void update(String message);
}
```

## Step 2: Observable (Subject)

```java
import java.util.ArrayList;
import java.util.List;

public class NewsAgency {

    private List<Observer> observers = new ArrayList<>();
    private String news;

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void setNews(String news) {
        this.news = news;
        notifyObservers();
    }

    private void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(news);
        }
    }
}
```

## Step 3: Concrete Observers
Email Subscriber

```java
public class EmailSubscriber implements Observer {

    private String email;

    public EmailSubscriber(String email) {
        this.email = email;
    }

    @Override
    public void update(String message) {
        System.out.println("Email to " + email + ": " + message);
    }
}
```

SMS subscriber

```java
public class SmsSubscriber implements Observer {

    private String phone;

    public SmsSubscriber(String phone) {
        this.phone = phone;
    }

    @Override
    public void update(String message) {
        System.out.println("SMS to " + phone + ": " + message);
    }
}

```

## Usage:


```java
public class Main {
    public static void main(String[] args) {

        NewsAgency agency = new NewsAgency();

        Observer email1 = new EmailSubscriber("john@mail.com");
        Observer sms1 = new SmsSubscriber("+359888123456");

        agency.addObserver(email1);
        agency.addObserver(sms1);

        agency.setNews("Breaking News: Observer Pattern in Java!");
        agency.setNews("Second update: Java is still powerful!");
    }
}

```

