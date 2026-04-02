# Interface Segregation Principle (ISP)

Clients should not be forced to depend upon interfaces that they do not use

```java
public interface Worker {
  void eat();
  void work();
}

public class HumanWorker implements Worker {


}

public class RobotWorker implements Worker {


}
```

The correct way is to separate the interfaces methods into
two separate interfaces like the one below 

```java
public interface Workable {

}

public interface Eatable {
  void eat();
}

public class HumanWorker implements Eatable {}
public class RobotWorker implements Workable {}
``` 
