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
