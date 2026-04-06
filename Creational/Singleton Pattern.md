# Singleton Pattern 

1. Classic GoF Singleton in Java
   a. This will give us most simple and generic version
   b. We will control constructor access
   c. Instantiation will be through a static method

2. Eager and Lazy versions of the Gof Singleton
   a. We will explore the different ways that we could control the instantiation of the Singleton instance.

3. Thread-Safe version of the GoF Singleton
     a. We will look at how to make the implementation of thread-safe
     b. We will also explore and analyze the performance cost of such this implementation.


## Lazy Instantiation Singleton in Java

```java
class SingletonGof {
  private static SingletonGoF instance = null;

  privta SingletonGof(){
    //private constructor instantiation  
  }
  public static SingletonGof getInstance() {
    if(instance == null) {
      instance = new SingletonGof();
   }
    return instance;
  }
}
```

## Eager Loading Singleton in Java

```java
class EagerSingletonGof {
    private static final EagerSingletonGoF instance = new EagerSingletonGoF();

    private EagerSingletonGof() {
      //private constructor to prevent instantiation
    }

    public static EagerSingletonGof getInstance() {
        return instance;
    }
}
```

## Thread-safe Singleton Implementation 

```java
public class SingletonThreadSafeImplementation {
  private static final SingletonThreadSafeImplementation instance = null ;

  private SingletonThreadSafeImplementation() {
    //private constructor
  }

  public static synchronized SingletonThreadSafeImplementation getInstance() {
    if(instance === null){
        instance = new SingletonThreadSafeImplementation();
    }
     return instance;
  }

}
```

## Singleton Pattern Basic Logger implementation

```java
class BasicLogger {
   private PrintWriter writer;

   public BasicLogger(String fileName) throws IOException {
      //Open the given file in append mode.
      writer = new PrintWriter(new FileWriter(fileName, true));
   
   }

   public void log(String message){
      //Decorate and write the message
      String decorateMessage = decorate(message);
      writer.println(decorate(message));
      writer.println(decorateMessage);
      writer.flush(); //Ensure the message is written immediately
      }

      private String decorate(String message) {
         //TODO
   }
}
```

let's define the decorate class first 

```java
private String decorate(String message) {
   try{
      //Decorate the message with the computer name. current time, and the original
     String computerName = InetAddress.getLocalHost.getHostName();
     LocalDateTime now = LocalDateTime.now();
     return String.format("[%s] [%s] %s", computerName, now, message);
      } catch (IOEception e) {
      //Fallback if hostname can't be resolved
      LocalDateTime now = LocalDateTime.now();
      return String.format("[Unknown Host] [%s]", now, message);
   }
}
```
